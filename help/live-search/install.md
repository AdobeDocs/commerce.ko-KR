---
title: ' [!DNL Live Search] 시작'
description: Adobe Commerce에서  [!DNL Live Search] 의 시스템 요구 사항 및 설치 단계에 대해 알아봅니다.
role: Admin, Developer
exl-id: 45b985f1-9afb-4a07-93e8-f2fe231c5400
badgePaas: label="PaaS만" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce 온 클라우드 프로젝트(Adobe 관리 PaaS 인프라) 및 온프레미스 프로젝트에만 적용됩니다."
source-git-commit: 1548b7e11249febc2cd8682581616619f80c052f
workflow-type: tm+mt
source-wordcount: '3151'
ht-degree: 0%

---

# [!DNL Live Search]&#x200B;(으)로 성공을 위한 설정

Adobe Commerce [!DNL Live Search]과(와) [[!DNL Catalog Service]](../catalog-service/guide-overview.md)이(가) 함께 작동하여 성능이 뛰어나고 관련성이 있으며 직관적인 검색 솔루션을 제공하므로 고객이 필요한 것을 빠르게 찾을 수 있습니다. 특히 [!DNL Catalog Service]은(는) 사용할 [!DNL Live Search]과(와) 같은 SaaS 서비스를 위한 카탈로그 데이터를 표시합니다.

이 문서에서는 [!DNL Live Search]을(를) 사용하여 [!DNL Catalog Service]을(를) 구현하기 위한 단계별 지침을 제공합니다.

## 대상자

이 문서는 Adobe Commerce 인스턴스 설치 및 구성을 담당하는 개발자나 시스템 통합자를 대상으로 합니다.

## 요구 사항

- [Adobe Commerce](https://business.adobe.com/products/magento/magento-commerce.html) 2.4.4+
- PHP 8.1, 8.2 또는 8.3
- [!DNL Composer]
- Cron 작업 및 색인 실행

>[!IMPORTANT]
>
>[!DNL Live Search]을(를) 구현하기 전에 [경계 및 제한](boundaries-limits.md) 섹션을 참조하여 [!DNL Live Search]이(가) 비즈니스 요구 사항에 맞는지 확인하십시오.

## 중요 업데이트

- [!DNL Live Search] 3.0.2부터 [!DNL Catalog Service] 확장이 설치와 함께 번들로 제공됩니다.

- 2023년 8월에 Elasticsearch 7의 지원 종료 발표로 인해 Adobe은 모든 Adobe Commerce 고객을 OpenSearch 2.x 검색 엔진으로 마이그레이션하는 것을 권장합니다. 제품을 업그레이드하는 동안 검색 엔진을 마이그레이션하는 방법에 대한 자세한 내용은 [업그레이드 안내서](https://experienceleague.adobe.com/en/docs/commerce-operations/upgrade-guide/prepare/opensearch-migration)에서 _OpenSearch로 마이그레이션_&#x200B;을 참조하십시오.

## 지원되는 플랫폼

- ECE(Adobe Commerce on Cloud) : 2.4.4+
- Adobe Commerce 온-프레미스 (EE) : 2.4.4+

## 워크플로우 개요

높은 수준에서 [!DNL Live Search]을(를) 온보딩하려면 다음을 수행해야 합니다.

1. [ 확장을 ](#1-install-the-live-search-extension)설치[!DNL Live Search]
1. API 키 [구성](#2-configure-api-keys)
1. 카탈로그 데이터 [동기화](#3-sync-your-catalog-data)
1. 카탈로그 데이터를 내보냈는지 [확인](#4-verify-that-the-data-was-exported)
1. 데이터를 [구성](#5-configure-the-data)
1. 연결을 [테스트](#6-test-the-connection)
1. 이벤트가 데이터를 캡처하고 있는지 [확인](#7-validate-events-are-capturing-data)
1. 상점 [사용자 지정](#8-customize-for-your-storefront)

## &#x200B;1. [!DNL Live Search] 확장 설치

[!DNL Live Search]이(가) [Adobe 마켓플레이스](https://commercemarketplace.adobe.com/magento-live-search.html)부터 [작성기](https://getcomposer.org/)까지 확장으로 설치되었습니다. [!DNL Live Search]을(를) 설치하고 구성한 후 Adobe [!DNL Commerce]에서 SaaS 서비스와 검색 및 카탈로그 데이터를 공유하기 시작합니다. 이 시점에서 *관리자* 사용자는 검색 패싯, 동의어 및 머천다이징 규칙을 설정하고, 사용자 지정하고, 관리할 수 있습니다.

>[!BEGINTABS]

>[!TAB 새 Commerce 인스턴스]

새 Commerce 인스턴스에 [!DNL Live Search]을(를) 설치하는 경우 다음 지침을 따르십시오.

1. [cron jobs](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs) 및 [인덱서](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management)가 실행 중인지 확인하십시오.

1. 작성기를 사용하여 라이브 검색 모듈을 프로젝트에 추가합니다.

   ```bash
   composer require magento/live-search --no-update
   ```

1. 종속성을 업데이트하고 확장을 설치합니다.

   ```bash
   composer update magento/live-search --with-dependencies
   ```

1. [!DNL OpenSearch] 및 관련 모듈을 일시적으로 사용하지 않도록 설정하고 [!DNL Live Search]을(를) 설치하십시오.

   ```bash
   bin/magento module:disable Magento_ Magento_Elasticsearch8 Magento_Elasticsearch7 Magento_OpenSearch Magento_ElasticsearchCatalogPermissions Magento_InventoryElasticsearch Magento_ElasticsearchCatalogPermissionsGraphQl
   ```

   [!DNL Elasticsearch] 서비스가 백그라운드에서 카탈로그 데이터를 동기화하고 제품을 인덱싱하는 동안 [!DNL Live Search]은(는) 상점 첫 화면의 검색 요청을 계속 관리합니다.

1. 업데이트를 설치합니다.

   ```bash
   bin/magento setup:upgrade
   ```

1. 다음 [인덱서](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management)가 &quot;일정별 업데이트&quot;로 설정되어 있는지 확인하십시오.

   - 제품 피드
   - 제품 변형 피드
   - 카탈로그 속성 피드
   - 제품 가격 피드
   - 범위 웹 사이트 데이터 피드
   - Scopes 고객 그룹 데이터 피드
   - 카테고리 피드
   - 범주 권한 피드

인덱서를 확인한 후 [API 키를 구성](#2-configure-api-keys)합니다.

>[!TAB 기존 Commerce 인스턴스]

기존 Commerce 인스턴스에 [!DNL Live Search]을(를) 설치하는 경우 다음 지침을 따르십시오.

1. [cron jobs](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs) 및 [인덱서](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management)가 실행 중인지 확인하십시오.

1. 작성기를 사용하여 라이브 검색 모듈을 프로젝트에 추가합니다.

   ```bash
   composer require magento/live-search --no-update
   ```

1. 종속성을 업데이트하고 확장을 설치합니다.

   ```bash
   composer update magento/live-search --with-dependencies
   ```

1. Storefront 검색 결과를 제공하는 [!DNL Live Search] 모듈을 비활성화합니다.

   ```bash
   bin/magento module:disable Magento_LiveSearchAdapter Magento_LiveSearchStorefrontPopover Magento_LiveSearchProductListing
   ```

   [!DNL Elasticsearch] 서비스가 백그라운드에서 카탈로그 데이터를 동기화하고 제품을 인덱싱하는 동안 [!DNL Live Search]은(는) 상점 첫 화면의 검색 요청을 계속 관리합니다.

1. 업데이트를 설치합니다.

   ```bash
   bin/magento setup:upgrade
   ```

1. 다음 [인덱서](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management)가 &quot;일정별 업데이트&quot;로 설정되어 있는지 확인하십시오.

   - 제품 피드
   - 제품 변형 피드
   - 카탈로그 속성 피드
   - 제품 가격 피드
   - 범위 웹 사이트 데이터 피드
   - Scopes 고객 그룹 데이터 피드
   - 카테고리 피드
   - 범주 권한 피드

1. [!DNL Live Search] 확장을 사용하도록 설정하고 [!DNL OpenSearch]&#x200B;(Magento Elasticsearch 및 OpenSearch 모듈)을 사용하지 않도록 설정합니다.

   ```bash
   bin/magento module:enable Magento_LiveSearchAdapter Magento_LiveSearchStorefrontPopover  Magento_LiveSearchProductListing
   ```

   ```
   bin/magento module:disable Magento_Elasticsearch Magento_Elasticsearch6 Magento_Elasticsearch7 Magento_Elasticsearch8 Magento_OpenSearch Magento_ElasticsearchCatalogPermissions Magento_InventoryElasticsearch Magento_ElasticsearchCatalogPermissionsGraphQl
   ```

   >[!NOTE]
   >
   >disable 명령에는 OpenSearch를 지원하는 Commerce 모듈 목록이 포함되어 있습니다. Commerce 인스턴스에 모듈이 설치되어 있지 않으면 `module does not exist` 오류가 표시됩니다.

1. 업데이트를 설치합니다.

   ```bash
   bin/magento setup:upgrade
   ```

인덱서를 확인한 후 [API 키를 구성](#2-configure-api-keys)합니다.

>[!ENDTABS]

### [!DNL Live Search] 베타 설치

>[!IMPORTANT]
>
>다음 기능은 Beta 버전입니다. Beta에 참여하려면 [commerce-storefront-services](mailto:commerce-storefront-services@adobe.com)에 전자 메일 요청을 보내십시오.

이 베타는 [`productSearch` 쿼리](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/)에서 세 가지 새로운 기능을 지원합니다.

- **계층화된 검색** - 다른 검색 컨텍스트에서 검색 - 이 기능을 사용하면 검색 쿼리에 대해 최대 두 개의 계층을 검색할 수 있습니다. For example:

   - **계층 1 검색** - &quot;product_attribute_1&quot;에서 &quot;motor&quot;를 검색합니다.
   - **계층 2 검색** - &quot;product_attribute_2&quot;에서 &quot;부품 번호 123&quot;을 검색합니다. 이 예제에서는 결과 내에서 &quot;motor&quot;에 대해 &quot;part number 123&quot;을 검색합니다.

  아래에 설명된 대로 `startsWith` 검색 인덱싱과 `contains` 검색 인덱싱에 모두 계층화된 검색을 사용할 수 있습니다.

- **검색 인덱싱으로 시작** - `startsWith` 인덱싱을 사용하여 검색 이 새로운 기능을 통해 다음과 같은 작업을 수행할 수 있습니다.

   - 속성 값이 특정 문자열로 시작하는 제품을 검색합니다.
   - 구매자가 속성 값이 특정 문자열로 끝나는 제품을 검색할 수 있도록 &quot;다음으로 끝남&quot; 검색을 구성합니다. &quot;다음으로 끝남&quot; 검색을 활성화하려면 제품 특성을 반대로 수집해야 하며 API 호출도 반전된 문자열이어야 합니다.

- **검색 인덱싱을 포함** -포함 인덱싱을 사용하여 특성을 검색합니다. 이 새로운 기능을 통해 다음과 같은 작업을 수행할 수 있습니다.

   - 더 큰 문자열 내에서 쿼리를 검색하고 있습니다. 예를 들어 구매자가 문자열 &quot;HAPE-123&quot;에서 제품 번호 &quot;PE-123&quot;을 검색하는 경우,

     >[!NOTE]
     >
     >이 검색 유형은 자동 완성 검색을 수행하는 기존 [구 검색](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#phrase)과(와) 다릅니다. 예를 들어 제품 속성 값이 &quot;outdoor pants&quot;인 경우 구문 검색은 &quot;out pan&quot;에 대한 응답을 반환하지만 &quot;or ants&quot;에 대한 응답은 반환하지 않습니다. 그러나 에는 검색이 포함되어 있으며 &quot;or ants&quot;에 대한 응답을 반환합니다.

이러한 새 조건은 검색 결과를 구체화하기 위한 검색 쿼리 필터링 메커니즘을 향상시킵니다. 이러한 새 조건은 기본 검색 쿼리에 영향을 주지 않습니다.

검색 결과 페이지에서 이러한 새 조건을 구현할 수 있습니다. 예를 들어, 쇼핑객이 검색 결과를 더 구체화할 수 있는 페이지에 새 섹션을 추가할 수 있습니다. 구매자가 &quot;제조업체&quot;, &quot;부품 번호&quot; 및 &quot;설명&quot;과 같은 특정 제품 속성을 선택할 수 있도록 할 수 있습니다. 여기에서 `contains` 또는 `startsWith` 조건을 사용하여 해당 특성 내에서 검색합니다. 검색 가능한 [특성](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/attributes-input-types) 목록은 관리 안내서를 참조하십시오.

1. Beta를 설치하려면 프로젝트에 다음 종속성을 추가하십시오.

   ```bash
   composer require magento/module-live-search-search-types:"^1.0.0-beta1"
   ```

1. `composer.json` 및 `composer.lock` 파일에 대한 변경 내용을 커밋하고 클라우드 프로젝트에 푸시합니다. [자세히 알아보기](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure-store/extensions#upgrade-an-extension)

   이 베타는 관리자의 **[!UICONTROL Search types]**, **[!UICONTROL Autocomplete]** 및 **[!UICONTROL Contains]**&#x200B;에 대한 **[!UICONTROL Starts with]**&#x200B;개의 확인란을 추가합니다. 또한 이러한 새로운 검색 기능을 포함하도록 [`productSearch`](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#filtering-using-search-capability) GraphQL API를 업데이트합니다.

1. 관리에서 [제품 특성을 검색 가능하게 설정](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/product-attributes-add#step-5-describe-the-storefront-properties)하고 해당 특성에 대한 검색 기능을 지정하십시오(예: **포함**(기본값) 또는 **다음으로 시작**). **포함**&#x200B;에 대해 최대 6개의 특성을 사용할 수 있도록 지정하고 **다음으로 시작**&#x200B;에 대해 최대 6개의 특성을 사용할 수 있도록 지정할 수 있습니다. Beta의 경우 관리자가 이 제한을 적용하지 않지만 API 검색에 적용된다는 점에 유의하십시오.

   ![검색 기능 지정](./assets/search-filters-admin.png)

1. 새로운 [ 및 ](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#filtering-using-search-capability) 검색 기능을 사용하여 [!DNL Live Search] API 호출을 업데이트하는 방법에 대해 알아보려면 `contains`개발자 설명서`startsWith`를 참조하십시오.

### 필드 설명

| 필드 | 설명 |
|--- |--- |
| `Autocomplete` | 기본적으로 활성화되고 수정할 수 없습니다. `Autocomplete`에서는 `contains`검색 필터[에서 ](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#filtering)을(를) 사용할 수 있습니다. `contains`의 검색 쿼리가 자동 완성 형식 검색 응답을 반환합니다. Adobe에서는 일반적으로 50자를 초과하는 설명 필드에 대해 이 유형의 검색을 사용하는 것이 좋습니다. |
| `Contains` | 자동 완성 검색 대신 &quot;문자열에 포함된 텍스트&quot; 검색을 true로 설정합니다. `contains`검색 필터[에서 ](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#filtering-using-search-capability)을(를) 사용합니다. 자세한 내용은 [제한](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#limitations)을 참조하세요. |
| `Starts with` | 특정 값으로 시작하는 쿼리 문자열입니다. `startsWith`검색 필터[에서 ](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#filtering-using-search-capability)을(를) 사용합니다. |

## &#x200B;2. API 키 구성

Adobe Commerce API 키와 연결된 개인 키가 있어야 Adobe Commerce 설치에 [!DNL Live Search]을(를) 연결할 수 있습니다. API 키는 개발자 또는 시스템 통합자와 공유할 수 있는 [!DNL Commerce] 라이선스 소유자의 계정에서 생성 및 관리됩니다. 그런 다음 개발자는 라이선스 소유자를 대신하여 SaaS Data Spaces를 만들고 관리할 수 있습니다. 이미 API 키 세트가 있는 경우 재생성할 필요가 없습니다.

[Commerce 서비스 커넥터](../landing/saas.md) 문서에서 API 키를 구성하는 방법을 알아봅니다.

## &#x200B;3. 카탈로그 데이터 동기화

[!DNL Live Search]이(가) 카탈로그 데이터를 Adobe의 SaaS 인프라로 이동합니다. 데이터가 색인화되고 검색 결과가 이 색인에서 상점 앞으로 직접 전달됩니다. 크기와 복잡성에 따라 색인화는 30분에서 2시간 정도 소요될 수 있습니다.

카탈로그 데이터를 SaaS 서비스에 초기 동기화하려면 다음 명령을 순서대로 실행합니다.

```bash
bin/magento saas:resync --feed productattributes
bin/magento saas:resync --feed products
bin/magento saas:resync --feed scopesCustomerGroup
bin/magento saas:resync --feed scopesWebsite
bin/magento saas:resync --feed prices
bin/magento saas:resync --feed productoverrides
bin/magento saas:resync --feed variants
bin/magento saas:resync --feed categories
bin/magento saas:resync --feed categoryPermissions
```

이 명령을 실행하면 카탈로그 데이터가 SaaS 서비스에 처음 동기화됩니다.

>[!WARNING]
>
>동기화 중에는 검색 및 범주 찾아보기 작업을 사용할 수 없습니다. 이 프로세스는 카탈로그 크기에 따라 1시간 이상 걸릴 수 있습니다.

### 동기화 진행 상황 모니터링

동기화 진행률을 모니터링하려면 [데이터 관리 대시보드](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard)를 사용하십시오. 이 대시보드는 상점 첫 화면에서 제품 데이터의 가용성에 대한 중요한 통찰력을 제공하여 고객에게 즉시 표시되도록 합니다.

![데이터 관리 대시보드](assets/data-management-dashboard.png)

[Commerce CLI](../data-export/data-export-cli-commands.md#troubleshooting) 및 데이터 내보내기 확장 로그를 사용하여 동기화 명령을 실행하고 동기화 프로세스 문제를 해결할 수도 있습니다.

#### 향후 제품 업데이트

초기 동기화 후 점포 검색에서 증분 제품 업데이트를 사용할 수 있는 데 최대 15분이 걸릴 수 있습니다. 자세한 내용은 색인화 설명서에서 [제품 업데이트 스트리밍](indexing.md)을 참조하세요.

## &#x200B;4. 데이터를 내보냈는지 확인합니다

카탈로그 데이터를 Adobe Commerce에서 내보내고 [!DNL Live Search]과(와) 동기화했는지 확인하려면 다음 몇 가지 옵션을 사용하십시오.

- 다음 표에서 항목을 찾습니다.

   - `cde_products_feed`
   - `cde_product_attributes_feed`

  >[!NOTE]
  >
  >`table does not exist` 오류가 발생하면 `catalog_data_exporter_products` 및 `catalog_data_exporter_product_attributes` 테이블에서 항목을 찾습니다. 이 테이블 이름은 [!DNL Live Search] 버전 4.2.1 이전 버전에서 사용됩니다.

- 기본 쿼리와 함께 [GraphQL 플레이그라운드](https://experienceleague.adobe.com/en/docs/commerce/live-search/live-search-admin/graphql)를 사용하여(자세한 내용은 [GraphQL 참조](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/) 참조) 다음을 확인하십시오.

   - 반환된 제품 수는 스토어 보기에 예상되는 값과 비슷합니다.
   - Facet이 반환됩니다.

추가 도움말은 지원 기술 자료에서 [[!DNL Live Search] 동기화되지 않은 카탈로그](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/live-search-catalog-data-sync)를 참조하십시오.

## &#x200B;5. 데이터 구성

제품 데이터를 올바르게 구성하면 고객에게 좋은 검색 결과를 얻을 수 있습니다. 이 섹션에서는 제품 목록 위젯을 활성화하고 카테고리를 할당합니다.

### 제품 목록 위젯 활성화

[!DNL Live Search] 4.0.0+를 설치하면 기본적으로 제품 목록 위젯이 활성화됩니다. 위젯이 활성화되면 검색 결과와 카테고리 검색 제품 목록 페이지에 대해 다른 UI 구성 요소가 사용됩니다. 이 UI 구성 요소는 [카탈로그 서비스 API](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/)를 직접 호출하여 응답 시간이 빨라집니다.

[!DNL Live Search] 버전이 4.0.0+보다 오래된 경우 제품 목록 위젯을 수동으로 활성화해야 합니다.

1. *관리자*&#x200B;에서 **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**(으)로 이동합니다.
1. **[!UICONTROL Live Search]**&#x200B;에서 **[!UICONTROL Storefront Features]**&#x200B;을(를) 선택합니다.
1. **[!UICONTROL Enable Product Listing Widgets]**&#x200B;을(를) `Yes`(으)로 설정합니다.

   ![제품 목록 위젯 사용](assets/ls-admin-enable-widget.png)

이 구성을 변경하면 `Page cache is invalidated` 메시지가 나타납니다. 변경 사항을 저장하려면 Magento 캐시를 플러시해야 합니다.

1. 다음 중 하나를 수행하여 [캐시 관리](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/cache-management) 페이지에 액세스합니다.

   - 작업 영역 위의 메시지에서 **[!UICONTROL Cache Management]** 링크를 클릭합니다.
   - _관리자_ 사이드바에서 **[!UICONTROL System]** > _[!UICONTROL Tools]_>**[!UICONTROL Cache Management]**(으)로 이동합니다.

1. **구성** [!UICONTROL Cache Type]을(를) 선택하고 **[!UICONTROL Flush Magento Cache]**&#x200B;을(를) 클릭합니다.

   Storefront에 대한 변경 사항은 캐시를 플러시한 직후 입니다.

### 범주 할당

[!DNL Live Search]에서 반환된 제품은 [category](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/categories/categories)에 할당되어야 합니다. 예를 들어 Luma에서 제품은 &quot;남성&quot;, &quot;여성&quot; 및 &quot;톱니바퀴&quot;와 같은 범주에 배치됩니다. 또한 하위 카테고리는 &quot;Tops&quot;, &quot;Bottom&quot; 및 &quot;Watches&quot;에 대해 설정됩니다. 이러한 범주 할당은 필터링 시 세부기간을 개선합니다.

## &#x200B;6. 연결 테스트

이제 SaaS에서 카탈로그 데이터를 사용하여 다음 시나리오에서 제품 데이터가 반환되는지 테스트하십시오.

- [!UICONTROL Search] 상자는 결과를 올바르게 반환합니다.
- 범주 찾아보기가 결과를 올바르게 반환합니다.
- 패싯은 검색 결과 페이지에서 필터로 사용할 수 있습니다

모든 기능이 올바르게 작동하면 [!DNL Live Search]이(가) 설치 및 연결되어 사용할 준비가 되었습니다.

상점 앞에서 문제가 발생하면 `var/log/system.log` 파일에서 서비스 측에서 API 통신 오류 또는 오류를 확인하십시오.

방화벽을 통해 [!DNL Live Search]을(를) 허용하려면 `commerce.adobe.io`을(를) 허용 목록에 추가하십시오.

## &#x200B;7. 이벤트가 데이터를 캡처하고 있는지 확인합니다

사이트에 배포된 Storefront 이벤트가 작동하는지 확인합니다. 이 검사는 Headless 구현에 특히 중요합니다.

- [에 필요한 ](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#live-search)이벤트[!DNL Live Search]을(를) 검토하십시오.
- [실시간 검색 대시보드](performance.md)에 비프로덕션 환경의 데이터가 표시되는지 확인하십시오.
- [이벤트 컬렉션 확인](../product-recommendations/verify.md). 이 페이지가 [!DNL Product Recommendations] 안내서에 있는 동안 확인 단계는 [!DNL Live Search]에도 적용됩니다.

## &#x200B;8. 상점용 사용자 지정

[!DNL Live Search] 확장을 설치하고, 동기화하고, 검증하고, 데이터를 구성했습니다. 다음 단계는 [!DNL Live Search] 위젯이 스토어의 모양과 느낌을 준수하도록 하는 것입니다.

필요에 따라 사용자 정의 CSS 규칙을 정의하여 팝오버 및 PLP 위젯의 스타일을 지정할 수 있습니다. [스타일 팝오버 요소](storefront-popover.md#styling-popover-example) 및 [제품 목록 페이지 위젯](plp-styling.md#styling-example)을 참조하세요.

위젯의 기능을 확장하려는 경우 각각의 소스 코드를 공용 리포지토리에서 사용할 수 있습니다.
이 시나리오에서는 사용자 자신의 요구 사항에 맞게 JavaScript을 사용자 지정한 다음 CDN에서 사용자 지정 코드를 호스팅할 수 있습니다. 이 사용자 지정 스크립트는 [!DNL Live Search] 서비스와 통신하며 일반적인 결과를 반환하므로 사용자가 위젯의 기능을 제어할 수 있습니다.

- [PLP 위젯 리포지토리](https://github.com/adobe/storefront-product-listing-page)
- [검색 창 리포지토리](https://github.com/adobe/storefront-search-as-you-type)

## [!DNL Live Search] 업데이트 중

[!DNL Live Search]을(를) 업데이트하기 전에 작성기를 사용하여 설치된 [!DNL Live Search]의 버전을 확인하세요.

```bash
composer show magento/module-live-search | grep version
```

[!DNL Live Search]을(를) 업데이트하려면 명령줄에서 다음을 실행하십시오.

```bash
composer update magento/live-search --with-dependencies
```

3.1.1에서 4.0.0으로 등 주요 버전으로 업데이트하려면 다음과 같이 프로젝트의 루트 [!DNL Composer] `.json` 파일을 편집하십시오.

1. 현재 설치된 `magento/live-search` 버전이 `3.1.1` 이하이고 `4.0.0` 버전 이상으로 업그레이드하는 경우 업그레이드하기 전에 다음 명령을 실행하십시오.

   ```bash
   bin/magento module:enable Magento_AdvancedSearch
   ```

   현재 설치된 `magento/live-search` 버전에 대한 자세한 내용을 보려면 다음 명령을 실행하십시오.

   ```bash
   composer show magento/live-search
   ```

1. 루트 `composer.json` 파일을 열고 `magento/live-search`을(를) 검색합니다.

1. `require` 섹션에서 버전 번호를 다음과 같이 업데이트합니다.

   ```json
   "require": {
      ...
      "magento/live-search": "^4.0",
      ...
    }
   ```

1. `composer.json`을(를) 저장합니다. 그런 다음 명령줄에서 다음을 실행합니다.

   ```bash
   composer update magento/live-search --with-dependencies
   ```

## [!DNL Live Search]을(를) 제거하는 중

[!DNL Live Search]을(를) 제거하려면 [모듈 제거](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/uninstall-modules)를 참조하세요.

## 패키지 [!DNL Live Search]개

[!DNL Live Search] 확장은 다음 패키지로 구성됩니다.

| 패키지 | 설명 |
|--- |--- |
| `module-live-search` | 상인이 페이스팅, 동의어, 쿼리 규칙 등에 대한 검색 설정을 구성할 수 있도록 하고 읽기 전용 GraphQL 플레이그라운드에 액세스하여 *관리자*&#x200B;의 쿼리를 테스트할 수 있도록 합니다. |
| `module-live-search-adapter` | Storefront에서 [!DNL Live Search] 서비스로 검색 요청을 라우팅하고 Storefront에서 결과를 렌더링합니다. <br />- 범주 찾아보기 - 상점 [위쪽 탐색](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/navigation/navigation-top)에서 검색 서비스로 요청을 라우팅합니다.<br />- 전역 검색 - [빠른 검색](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search) 필드에서 [!DNL Live Search] 서비스로 요청을 라우팅합니다. 빠른 검색 필드는 상점 첫 페이지의 오른쪽 상단에 있습니다. |
| `module-live-search-storefront-popover` | &quot;입력할 때 검색&quot; 팝오버는 표준 빠른 검색을 대체하며 상위 검색 결과의 데이터 및 썸네일을 반환합니다. |

## [!DNL Live Search]개의 종속성

[!DNL Composer] 확장을 설치하기 위한 [!DNL Live Search] 메타패키지에 다음 모듈 종속성이 포함되어 있습니다.

- `magento/module-saas-catalog`
- `magento/module-saas-category`
- `magento/module-saas-category-permissions`
- `magento/module-saas-product-override`
- `magento/module-saas-product-variant`
- `magento/module-saas-price`
- `magento/module-saas-scopes`
- `magento/module-bundle-product-data-exporter`
- `magento/module-catalog-inventory-data-exporter`
- `magento/module-catalog-url-rewrite-data-exporter`
- `magento/module-configurable-product-data-exporter`
- `magento/module-parent-product-data-exporter`
- `magento/module-gift-card-product-data-exporter`
- `magento/module-bundle-product-override-data-exporter`
- `data-services`
- `services-id`

## 고급 개념

다음 단원에서는 [!DNL Live Search] 및 [!DNL Catalog Service]을(를) 사용할 때 더 많은 고급 항목을 제공합니다.

### 엔드포인트

[!DNL Live Search]은(는) `https://catalog-service.adobe.io/graphql`의 끝점을 통해 통신합니다.

[!DNL Live Search]이(가) 전체 제품 데이터베이스에 액세스할 수 없으므로 [!DNL Live Search] GraphQL 및 Commerce 코어 GraphQL API에 전체 패리티가 없습니다.

Adobe에서는 SaaS API(특히 카탈로그 서비스 엔드포인트)를 직접 호출하는 것이 좋습니다.

- Commerce 데이터베이스/Graphql 프로세스를 건너뛰어 성능 향상 및 프로세서 로드 감소
- [!DNL Catalog Service] 페더레이션을 사용하여 단일 끝점에서 [!DNL Live Search], [!DNL Catalog Service] 및 [!DNL Product Recommendations]을(를) 호출합니다.

일부 사용 사례의 경우 [!DNL Catalog Service]에 전화를 걸어 제품 세부 정보 및 유사한 사례를 확인하는 것이 좋습니다. 자세한 내용은 [refineProduct](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/refine-product/)을(를) 참조하십시오.

사용자 지정 Headless 구현이 있는 경우 [!DNL Live Search] 참조 구현을 확인하십시오.

- [PLP 위젯](https://github.com/adobe/storefront-product-listing-page)
- [[!DNL Live Search] 필드](https://github.com/adobe/storefront-search-as-you-type)

검색 어댑터, Luma 위젯 또는 AEM CIF 위젯과 같은 표준 구성 요소를 사용하지 않는 경우 사용자 상호 작용 데이터의 자동 수집이 기본적으로 작동하지 않습니다. Adobe Sensei은 수집된 이 데이터를 지능형 머천다이징 및 성능 추적에 사용합니다. 이 문제를 해결하려면 headless 방식으로 이 데이터 수집을 구현할 수 있는 맞춤형 솔루션을 개발해야 합니다.

[!DNL Live Search]의 최신 버전은 이미 [!DNL Catalog Service]을(를) 사용하고 있습니다.

### 언어 지원

[!DNL Live Search] 위젯은 다음 언어를 지원합니다.

|  |  |  |  |
|--- |--- |--- |--- |
| 언어 | 지역 | 언어 코드 | Magento 로케일 |
| 불가리아어 | 불가리아 | bg_BG | bg_BG |
| 카탈로니아어 | 스페인 | ca_ES | ca_ES |
| 체코어 | 체코 | cs_CZ | cs_CZ |
| 덴마크어 | 덴마크 | da_DK | da_DK |
| 독일어 | 독일 | de_DE | de_DE |
| 그리스어 | 그리스 | el_GR | el_GR |
| 영어 | 영국 | en_GB | en_GB |
| 영어 | 미국 | en_US | en_US |
| 스페인어 | 스페인 | es_ES | es_ES |
| 에스토니아어 | 에스토니아 | et_EE | et_EE |
| 바스크어 | 스페인 | eu_ES | eu_ES |
| 페르시아어 | 이란 | fa_IR | fa_IR |
| 핀란드어 | 핀란드 | fi_FI | fi_FI |
| 프랑스어 | 프랑스 | fr_FR | fr_FR |
| 갈리시아어 | 스페인 | gl_ES | gl_ES |
| 힌디어 | 인도 | hi_IN | hi_IN |
| 헝가리어 | 헝가리 | hu_HU | hu_HU |
| 인도네시아어 | 인도네시아 | id_ID | id_ID |
| 이탈리아어 | 이탈리아 | it_IT | it_IT |
| 한국어 | 대한민국 | ko_KR | ko_KR |
| 리투아니아어 | 리투아니아 | lt_LT | lt_LT |
| 라트비아어 | 라트비아 | lv_LV | lv_LV |
| 노르웨이어 | 노르웨이 복말 | nb_NO | nb_NO |
| 네덜란드어 | 네덜란드 | nl_NL | nl_NL |
| 폴란드어 | 폴란드 | pl_PL | pl_PL |
| 포르투갈어 | 브라질 | pt_BR | pt_BR |
| 포르투갈어 | 포르투갈 | pt_PT | pt_PT |
| 루마니아어 | 루마니아 | ro_RO | ro_RO |
| 러시아어 | 러시아 | ru_RU | ru_RU |
| 스웨덴어 | 스웨덴 | sv_SE | sv_SE |
| 태국인 | 태국 | th_TH | th_TH |
| 터키어 | 터키 | tr_TR | tr_TR |
| 중국어 | 중국 | zh_CN | zh_Hans_CN |
| 중국어 | 대만 | zh_TW | zh_Hant_TW |

위젯이 Commerce 관리 언어 설정이 지원되는 언어와 일치함을 감지하면 기본적으로 해당 언어로 설정됩니다. 그렇지 않은 경우 위젯은 기본적으로 영어로 설정됩니다. 관리자의 경우 _[!UICONTROL Stores]_> [!UICONTROL Settings] >_[!UICONTROL Configuration]_ > _[!UICONTROL General]_> [!UICONTROL Country Options]&#x200B;(으)로 이동하여 언어 설정을 구성합니다.

관리자는 [검색 인덱스](settings.md#language)의 언어를 설정하여 더 나은 검색 결과를 얻을 수 있습니다.

### 위젯 코드 저장소

제품 목록 페이지 위젯 및 [!DNL Live Search] 필드 위젯에 대한 코드는 GitHub에서 다운로드할 수 있습니다.

코드에 액세스할 수 있는 개발자는 코드의 작동 방식과 모양을 완전히 사용자 지정할 수 있습니다. 자체 서버에서 코드를 호스팅하지만 여전히 [!DNL Live Search] 서비스를 사용합니다.

- [PLP 위젯](https://github.com/adobe/storefront-product-listing-page)
- [검색 창](https://github.com/adobe/storefront-search-as-you-type)

### 데이터 내보내기 확장

[!DNL Live Search]이(가) 활성화되면 데이터 내보내기 확장은 Commerce 응용 프로그램과 [!DNL Live Search] 간에 Commerce 데이터를 동기화합니다. 이 프로세스를 통해 상점에서 최신 Commerce 데이터를 사용할 수 있습니다. 관리에서 데이터 관리 대시보드를 사용하여 동기화 상태를 확인할 수 있습니다. Commerce CLI 및 로그를 사용하여 데이터 내보내기 프로세스를 관리하고 문제를 해결할 수 있습니다. 자세한 내용은 [데이터 내보내기 안내서](../data-export/overview.md)를 참조하세요.

### Inventory management

[!DNL Live Search]은(는) Commerce(이전에는 Multi-Source Inventory 또는 MSI로 알려짐)에서 [Inventory management](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/introduction) 기능을 지원합니다. 전체 지원을 활성화하려면 종속성 모듈 [을(를) 버전 102.2.0+로 ](install.md#updating-live-search)업데이트`commerce-data-export`해야 합니다.

[!DNL Live Search]은(는) Inventory management 내에서 제품을 사용할 수 있는지 여부를 나타내는 부울을 반환하지만, 재고가 있는 소스에 대한 정보는 포함하지 않습니다.

### 가격 인덱서

[!DNL Live Search] 고객은 더 빠른 가격 변경 업데이트 및 동기화 시간을 제공하는 [SaaS 가격 인덱서](../price-index/price-indexing.md)를 사용할 수 있습니다.

### 가격 지원

[!DNL Live Search] 위젯은 대부분의 위젯을 지원하지만 Adobe Commerce에서 지원하는 모든 가격 유형은 지원하지 않습니다.

현재 기본 가격이 지원됩니다. 지원되지 않는 고급 가격은 다음과 같습니다.

- 비용
- 최소 광고 가격

보다 복잡한 가격 계산은 [API Mesh](../catalog-service/mesh.md)를 참조하세요.

가격 형식은 Commerce 인스턴스 내의 로케일 구성 설정을 지원합니다. *스토어* > 설정 > *구성* > 일반 > *일반* > 로컬 옵션 > 로케일.

### 헤드리스 상점 첫 화면 지원

선택적으로, 상점 동작 데이터 수집에 필요한 필드를 포함하도록 응용 프로그램의 기존 GraphQL 범위를 확장하는 `module-data-services-graphql` 모듈을 설치해야 할 수 있습니다.

```bash
composer require magento/module-data-services-graphql
```

이 모듈은 GraphQL 쿼리에 추가 컨텍스트를 추가합니다.

- `dataServicesStorefrontInstanceContext`
- `dataServicesMagentoExtensionContext`
- `dataServicesStoreConfigurationContext`

### B2B 지원

[!DNL Live Search]은(는) 추가 [제한](https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/guide-overview)과 함께 [B2B 기능](boundaries-limits.md#b2b-and-category-permissions)을 지원합니다.

### PWA 지원

[!DNL Live Search]은(는) PWA Studio에서 작동하지만 다른 Commerce 구현과 비교하여 약간의 차이가 있을 수 있습니다. 검색 및 제품 목록 페이지와 같은 기본 기능은 Venia에서 작동하지만 Graphql의 일부 순열이 제대로 작동하지 않을 수 있습니다. 성능 차이도 있을 수 있습니다.

- [!DNL Live Search]의 현재 PWA 구현에서는 기본 Commerce 상점 이름을 사용하는 [!DNL Live Search]보다 검색 결과를 반환하는 데 더 많은 처리 시간이 필요합니다.
- PWA의 [!DNL Live Search]은(는) [이벤트 처리](https://developer.adobe.com/commerce/services/shared-services/storefront-events/sdk/)를 지원하지 않습니다. 따라서 검색 보고 및 지능형 머천다이징은 PWA 상점 첫 화면에서 작동하지 않습니다.
- [PWA Studio](https://developer.adobe.com/commerce/pwa-studio/)을(를) 사용하는 경우 GraphQL에서는 `description`, `name`, `short_description`에서 직접 필터링을 지원하지 않지만, 더 일반적인 필터를 사용하여 이러한 필드를 반환할 수 있습니다.

PWA Studio에서 [!DNL Live Search]을(를) 사용하려면 통합자도 다음을 수행해야 합니다.

1. [livesearch-storefront-utils](https://www.npmjs.com/package/@magento/ds-livesearch-storefront-utils)을(를) 설치합니다.
1. `environmentId` 개체에서 `storeDetails`을(를) 설정합니다.

   ```javascript
   const storeDetails: StoreDetailsProps = {
       environmentId: <Storefront_ID>,
       websiteCode: "base",
       storeCode: "main_website_store",
       storeViewCode: "default",
       searchUnitId: searchUnitId,
       config: {
           minQueryLength: 5,
           pageSize: 8,
           currencySymbol: "$",
           },
       };
   ```

### 쿠키

[!DNL Live Search]은(는) 기본 기능의 일부로 사용자 상호 작용 데이터를 수집하며 쿠키는 이 데이터를 저장하는 데 사용됩니다. 사용자 정보를 수집할 때 사용자는 쿠키를 저장하는 데 동의해야 합니다. [!DNL Live Search] 및 [!DNL Product Recommendations]이(가) 데이터 스트림을 공유하므로 동일한 쿠키 메커니즘이 사용됩니다. 자세한 내용은 [쿠키 제한 처리](https://experienceleague.adobe.com/en/docs/commerce/product-recommendations/developer/setting-cookie)를 참조하세요.
