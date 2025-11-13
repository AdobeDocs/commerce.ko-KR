---
title: Adobe Commerce Optimizer 커넥터
description: Commerce 클라우드 또는 온프레미스 프로젝트에서 Adobe Commerce Optimizer으로 데이터를 연결하는 방법에 대해 알아봅니다
feature: Personalization, Integration, Configuration
badgePaas: label="PaaS만" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce 온 클라우드 프로젝트(Adobe 관리 PaaS 인프라) 및 온프레미스 프로젝트에만 적용됩니다."
hidefromtoc: true
hide: true
source-git-commit: 1654aede42cf53b2dffe2965680f122d7c247234
workflow-type: tm+mt
source-wordcount: '1529'
ht-degree: 0%

---


# Commerce용 Adobe Commerce Optimizer 커넥터

Adobe Commerce 커넥터는 기존 Adobe Commerce Cloud on Cloud 또는 온프레미스 배포와 Adobe Commerce Optimizer 구성 가능한 카탈로그 데이터 모델 간에 카탈로그 및 가격 데이터를 동기화하는 통합 브리지입니다. 이를 통해 동적 AI 검색, 권장 사항, Edge Delivery Services의 Adobe Commerce 상점 등 빠른 로드 헤드리스 상점 및 실시간 성능 분석과 같은 기능을 사용할 수 있습니다.

>[!NOTE]
>
>이 설명서는 초기 액세스 개발 상태의 제품에 대해 설명하고 일반 가용성을 위한 모든 기능을 반영하지는 않습니다.

## 아키텍처 및 경험

Adobe Commerce 커넥터는 Commerce의 `website/store/storeview` 카탈로그 계층 구조를 Adobe Commerce Optimizer `channel/policy/source` 데이터 모델에 매핑하여 작동합니다.

Commerce 관리자로부터 Commerce 서비스(라이브 검색 및 제품 권장 사항)를 구성하고 관리하는 대신 [Adobe Commerce Optimizer 머천다이징 도구](../optimizer/merchandising/overview.md)를 사용하여 제품 검색(라이브 검색) 및 권장 사항(제품 권장 사항) 규칙 구성을 관리합니다.  Adobe Commerce 인스턴스가 카탈로그 및 가격 데이터의 데이터 원본이 됩니다. Commerce에서 데이터가 업데이트되면 업데이트가 Adobe Commerce Optimizer 인스턴스에 동기화됩니다.

## 워크플로

커넥터를 사용하면 다음과 같은 몇 가지 주요 워크플로를 사용할 수 있습니다.

* **Commerce 카탈로그 데이터를 Adobe Commerce Optimizer으로 내보내기** - 가격 및 가격 장부 데이터를 `website` 수준에서 내보냅니다. 제품 및 제품 특성 데이터를 `store view` 수준에서 내보냅니다. 기본적으로 모든 Commerce 범위(웹 사이트 및 스토어 보기)에 대해 카탈로그 데이터 동기화가 활성화됩니다.

  이 워크플로를 사용하려면 작성기를 사용하여 `adobe-commerce/commerce-data-export-aco-adapter` PHP 확장을 설치한 다음 IMS 자격 증명을 제공하여 Commerce 프로젝트 간의 연결을 인증합니다.

* **Commerce `website/store/storeview` 데이터를 매핑하여 Adobe Commerce Optimizer으로 내보내기**

  관리자(**[!UICONTROL Stores]** -> [!UICONTROL Settings] -> **[!UICONTROL All Stores]**)의 저장소 그리드에서 내보내기 구성을 업데이트하여 특정 범위에 대한 데이터만 내보내도록 Adobe Commerce Optimizer 내보내기 설정을 사용자 지정할 수 있습니다.

* **머천다이징 규칙 구성 및 관리**

  커넥터를 사용하면 Commerce 관리자의 [!UICONTROL Live Search] 및 [!UICONTROL Product Recommendations] 페이지가 아닌 Adobe Commerce Optimizer UI에서 제품 검색 및 권장 사항에 대한 머천다이징 규칙을 정의하고 관리할 수 있습니다.

* **Edge Delivery Services에서 Commerce 상점 배포**

  Adobe Commerce Optimizer과의 통합을 설정한 후 Commerce Storefront를 Edge Delivery 서비스에 설정 및 배포하여 Adobe Commerce Optimizer에서 사용할 수 있는 구성 가능한 API 기반 아키텍처 및 모듈식 구성 요소를 사용하여 초고속 성능, 확장성, 원활한 콘텐츠 작성, 통합 개인화 및 운영 비용 절감을 제공할 수 있습니다.

## 통합 사용 요구 사항

* Adobe Commerce 2.4.7+

   * PHP 8.2, 8.3 또는 8.4
   * Composer 2.x

* 프로비저닝된 샌드박스 인스턴스가 있는 Adobe Commerce Optimizer 라이센스.

* 작성기를 사용하여 Commerce Connector 메타패키지를 다운로드하려면 [repo.magento.com](https://repo.magento.com)에 액세스하십시오.

* [Adobe Commerce Optimizer 샌드박스 인스턴스](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-commerce-optimizer/create-first-instance)에 대한 관리자 액세스 권한.

통합을 구성하는 Adobe Commerce 사용자에게는 다음이 있어야 합니다.

* Adobe Commerce 관리자에 대한 관리자 액세스 권한.

* [Adobe Commerce 응용 프로그램 서버에 대한 명령줄 액세스](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/project/user-access).

* Adobe Commerce Optimizer 프로젝트가 프로비저닝된 [IMS 조직](https://experienceleague.adobe.com/en/docs/core-services/interface/administration/organizations?)에 대한 개발자 액세스 권한.

## 시작

1. **통합 설정**

   1. [Commerce 커넥터 패키지 설치](#install-the-commerce-connector-package).

   1. [Commerce Optimizer 연결 구성에 필요한 값 가져오기](#get-required-values-for-configuring-the-commerce-optimizer-connection)

   1. [Adobe Commerce Optimizer 통합을 사용하도록 설정](#enable-the-adobe-commerce-optimizer-integration).

   1. [데이터 동기화가 작동하는지 확인](#verify-that-the-data-sync-is-working).

   1. [데이터 내보내기 구성을 사용자 지정](#customize-commerce-data-export-configuration)(선택 사항).

1. **[Adobe Commerce Optimizer 스토어 구성](#configure-adobe-commerce-optimizer-stores)**

1. **[Edge Delivery Services에서 Commerce 상점 설정](#set-up-a-commerce-storefront-on-edge-delivery-services)**

## Commerce 커넥터 패키지 설치

Adobe Commerce Connector Composer 메타패키지는 Adobe Commerce Optimizer에 대한 활성 라이선스를 가진 모든 Commerce 판매자가 사용할 수 있습니다.

### 설치 단계

1. 작성기를 사용하여 `adobe-commerce/commerce-data-export-aco-adapter` 모듈 추가:

```shell
 composer require adobe-commerce/commerce-data-export-aco-adapter
```

1. Adobe Commerce 스테이징 환경에 변경 사항을 배포합니다.

변경 사항이 배포되면 Commerce 관리 메뉴에서 Commerce Optimizer Optimizer 옵션을 사용할 수 있습니다.

>[!NOTE]
>
>자세한 확장 설치 지침은 다음 안내서를 참조하십시오.
>
>[클라우드 인프라에서 Adobe Commerce에 확장 설치](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/configure-store/extensions)
>
>[확장 Adobe Commerce 온-프레미스 설치](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/extensions)

## Commerce Optimizer 연결 구성에 필요한 값 가져오기

### API 자격 증명 가져오기

>[!NOTE]
>
>Commerce Optimizer 인스턴스가 배포된 IMS 조직의 데이터 수집 API로 개발자 프로젝트를 이미 구성한 경우 해당 프로젝트의 OAUTH-서버 간 자격 증명에서 필요한 API 자격 증명과 조직 ID를 가져올 수 있습니다.

Adobe Developer 콘솔에서 새 개발자 프로젝트를 만들어 Adobe Commerce Optimizer 수집 API 자격 증명을 가져와 Commerce 인스턴스와 Commerce Optimizer 인스턴스 간의 통합을 구성합니다. 자세한 내용은 [머천다이징 개발자 안내서](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/authentication/#obtain-ims-credentials)에서 *IMS 자격 증명 가져오기*&#x200B;를 참조하십시오.

프로젝트를 만든 후 [OAUTH 서버 간 자격 증명] 페이지에서 다음 값을 저장합니다.

* **조직 ID**(`org_id`)

* **IMS `client_id` 및`client_secret`**

### Adobe Commerce Optimizer 인스턴스 세부 사항 가져오기

Adobe Commerce Optimizer 인스턴스 세부 사항에서 다음 값을 저장합니다.

* **인스턴스 ID - **Adobe Commerce Optimizer 인스턴스의 고유 식별자입니다. 테넌트 ID라고도 합니다.

  Adobe Commerce Optimizer 인스턴스에 액세스하려면 URL에서 인스턴스 ID를 가져옵니다. 예를 들어 URL `https://na1-sandbox.admin.commerce.adobe.com/1234567890abcdef`에서 인스턴스 ID는 `1234567890abcdef`입니다.

* **지역—**Adobe Commerce Optimizer 샌드박스 인스턴스가 호스팅되는 지역입니다.

  Adobe Commerce Optimizer URL에서 지역을 가져옵니다. 예를 들어 URL `https://na1-sandbox.admin.commerce.adobe.com/1234567890abcdef`에서 영역은 `na1`입니다.

## Adobe Commerce Optimizer 통합 활성화

>[!IMPORTANT]
>
>구성 명령을 실행하면 데이터 동기화 처리가 시작됩니다. 기본적으로 모든 Commerce 범위(웹 사이트 및 스토어 보기)에 대해 카탈로그 데이터 동기화가 활성화됩니다. 카탈로그 크기에 따라 데이터 동기화 프로세스는 많은 시간이 걸릴 수 있습니다.

이제 이전 단계에서 수집한 API 자격 증명과 인스턴스 세부 사항을 사용하여 Commerce과 Adobe Commerce Optimizer 인스턴스 간의 통합을 구성할 수 있습니다.

1. Commerce 관리자에서 **[!UICONTROL Adobe Commerce Optimizer]**&#x200B;을(를) 선택하여 지침이 포함된 구성 페이지를 표시합니다.

   ![Adobe Commerce Optimizer 구성 페이지](../assets/aco-connector-config-page.png)

1. 명령줄에서 [SSH를 사용](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/secure-connections)하여 Commerce 스테이징 환경에 연결합니다.

1. 다음 Commerce CLI 명령을 실행하여 통합을 구성하고 자리 표시자 값을 Commerce Optimizer 프로젝트에 대한 값으로 바꿉니다.

```terminal
bin/magento aco:config:init --org_id=<<your_org_id>> --tenant_id=<<your_tenant_id>> --client_id=<<your_client_id>> --client_secret=<<your_client_secret>> --region=<<na1>> --type=sandbox
```

1. Commerce 관리자로 돌아가 [!UICONTROL Adobe Commerce Optimizer] 옵션을 선택하여 연결을 확인합니다.

   옵션을 클릭하면 새 탭에서 Adobe Commerce Optimizer UI가 열립니다.

## 데이터 동기화가 작동하는지 확인

Commerce 관리 및 Commerce Optimizer 모두에서 데이터 동기화를 확인할 수 있습니다.

* **[데이터 피드 동기화 상태 페이지](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status.md)**&#x200B;에는 Commerce에서 Adobe Commerce Optimizer으로의 카탈로그 데이터 동기화 진행 상황이 표시됩니다.

* Adobe Commerce Optimizer의 **[[!UICONTROL Data Sync]페이지](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/data-sync)**&#x200B;은(는) Commerce 인스턴스에서 전송된 카탈로그 데이터를 표시합니다.

1. 카탈로그 데이터가 Commerce에서 Commerce Optimizer으로 흐르고 있는지 확인합니다.

   Commerce 관리자에서 [!UICONTROL Data Feed Sync Status]** > [!UICONTROL System] > [!UICONTROL Data Transfer]을(를) 선택하여 **[!UICONTROL Data Feed Sync Status]** 페이지를 엽니다.

   ![피드 항목 상태를 보고하는 데이터 피드 동기화 상태 페이지](./assets/data-feed-sync-status.png)

   데이터 동기화가 시작되면 피드 데이터에 성공적으로 전송된 레코드가 표시됩니다. 각 피드에 대한 세부 사항을 보고 동기화 문제를 보고 해결할 수도 있습니다.

1. Adobe Commerce Optimizer이 카탈로그 데이터를 수신하는지 확인합니다.

   Commerce Optimizer 메뉴에서 **[!UICONTROL Data Sync]**&#x200B;을(를) 선택하여 데이터 동기화 페이지를 엽니다.

   ![데이터 동기화](./assets/data-sync.png)

### 문제 해결

데이터 동기화가 시작되지 않은 경우 카탈로그 인덱스가 유효한지 확인하십시오. 색인이 유효하지 않은 경우 Commerce CLI에서 다음 명령을 실행하여 카탈로그 데이터를 다시 색인화합니다.

```terminal
bin/magento indexer:reindex" catalog indexer re-index CLI command to start PaaS to ACO catalog data synchronization.
```

## Commerce 데이터 내보내기 구성 사용자 지정

관리자(**[!UICONTROL Stores]** -> [!UICONTROL Settings] -> **[!UICONTROL All Stores]**)의 저장소 그리드에서 내보내기 구성을 업데이트하여 특정 범위에 대한 데이터만 내보내도록 Adobe Commerce Optimizer 내보내기 설정을 사용자 지정할 수 있습니다.

* `website` 수준에서 내보내기 설정을 사용하지 않도록 설정하면 가격 및 가격 장부 데이터의 Adobe Commerce Optimizer 내보내기가 중지됩니다.

* `storeview` 수준에서 내보내기 설정을 사용하지 않도록 설정하면 제품 및 제품 특성을 Adobe Commerce Optimizer으로 내보내기가 중지됩니다.

구성이 변경되면 해당 인덱스가 무효화되어 영향을 받는 엔티티의 재내보내기가 트리거됩니다.

## Adobe Commerce Optimizer 스토어 구성

카탈로그 보기 및 정책을 만들어 Adobe Commerce Optimizer 스토어를 구성합니다&#x200B;. Adobe Commerce Optimizer 안내서에서 [카탈로그 보기 만들기](../optimizer/setup/catalog-view.md)를 참조하십시오.

가격 장부는 Adobe Commerce 고객 그룹에서 자동으로 생성됩니다.

## Edge Delivery Services에서 Commerce 상점 설정

이 섹션에서는 Commerce 상점 설정에 필요한 단계에 대한 높은 수준의 개요를 제공합니다. 자세한 내용은 [Adobe Commerce 상점]&#x200B;(https://experienceleague.adobe.com/developer/commerce/storefront/) 설명서 사이트에서 확인할 수 있습니다.

1. [사이트 작성자 도구](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator)를 사용하여 Adobe Commerce Storefront 보일러플레이트를 복제하고 EDS에 배포합니다.

1. [로컬 개발 환경을 설정합니다](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/#set-up-local-environment).

1. [GraphQL Storefront 호환성 패키지 설치](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/storefront-compatibility/install/)&#x200B;.

1. [클라우드 환경에서 Commerce 인스턴스에 대한 CORS 헤더를 구성합니다](#configure-cors-headers-for-commerce-instance).

1. [Commerce 데이터 원본에 상점 연결](#connect-the-storefront-to-commerce-data-sources).

### Commerce 인스턴스에 대한 CORS 헤더 구성

GraphQL 요청이 EDS(Edge Delivery Services) 상점 첫 화면에서 Adobe Commerce 온 클라우드 또는 온프레미스 환경으로 오도록 하려면 특정 CORS(원본 간 리소스 공유) 헤더를 Adobe Commerce GraphQL 끝점에 추가합니다&#x200B;. 지침은 [Adobe Commerce 상점](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/cors-setup/) 설명서의 *CORS 설정*&#x200B;을 참조하십시오.

### Storefront를 Commerce 데이터 소스에 연결

Storefront 보일러플레이트 코드에 대한 GitHub 저장소에서 다음 매개 변수로 storefront 구성 파일 `config.json`을(를) 업데이트합니다.

* `"commerce-core-endpoint": "Commerce cloud instance GraphQL endpoint"`(예: `https://{{your store}}/graphql`).

* `"commerce-endpoint": "Commerce Optimizer instance GraphQL endpoint"`(예: `https://na1-sandbox.api.commerce.adobe.com/{{instanceId}}/v1/catalog&#x200B;`).

* `"AC-Environment-Id": "Customer organization ID"` - [Commerce 클라우드 프로젝트](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/project/overview#project-overview)에서 이 값을 가져옵니다.

* `"AC-View-ID": "Catalog view ID in Commerce Optimizer Admin"` - Adobe Commerce Optimizer의 [카탈로그 보기 세부 정보](../optimizer/setup/catalog-view.md#view-details)에서 이 값을 가져옵니다.

* `"AC-Price-Book-ID": "base::b6589fc6ab0dc82cf12099d1c2d40ab994e8410c"` — Adobe Commerce Optimizer의 [카탈로그 보기 세부 정보](../optimizer/setup/catalog-view.md#view-details)에 있는 할당된 가격 장부 목록에서 이 값을 가져옵니다.

* `"AC-Source-Locale": "catalogSource"`— Commerce 상점 전망과 연결된 원본을 지정하여 상점 전망에 연결합니다. Adobe Commerce Optimizer의 [데이터 동기화](../optimizer/setup/data-sync.md) 페이지에서 사용 가능한 소스를 볼 수 있습니다.

자세한 내용은 [Adobe Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/) 설명서의 *Storefront 구성*&#x200B;을 참조하십시오.


