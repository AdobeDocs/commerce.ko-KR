---
title: ' [!DNL Adobe Commerce Optimizer Connector] 시작'
description: ' [!DNL Adobe Commerce Optimizer Connector]을(를) 설치하고, 범위 내보내기 설정을 구성하고, IMS 인증을 사용하도록 설정하고, 카탈로그 동기화를 확인하는 방법을 알아봅니다.'
feature: Integration, Configuration
badgePaas: label="PaaS만" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce 온 클라우드 프로젝트(Adobe 관리 PaaS 인프라) 및 온프레미스 프로젝트에만 적용됩니다."
autotag-review: '2026-06-09T16:55:50.934Z'
TQID: 'https://experienceleague.adobe.com/AcZ6CNyuIdUlfVHXhyQEYuThfLNd4WWqMMY82tjMMCc'
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: b974b164-8a4e-43b8-a9e2-8e67ec131677id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: c32adafa-ed01-4b31-997e-2413013911b0id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
subfeature_v2: id: e126554b-28f9-4290-b58c-10b888b88174id: a40ebd6b-b542-4432-a730-1803ef74518d
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 1079
ht-degree: 0%

---


# 시작하기

[!DNL Adobe Commerce] 카탈로그 데이터를 [!DNL Adobe Commerce Optimizer]과(와) 동기화하도록 [!DNL Adobe Commerce Optimizer Connector]을(를) 설치하고 구성한 다음 데이터 동기화 상태를 모니터링하여 상점이 최신 상태인지 확인하십시오.

{{aco-integration-environment-alignment}}

## 통합 사용 요구 사항 {#requirements-to-use-the-integration}

* [!DNL Adobe Commerce] 2.4.7+

   * PHP 8.2, 8.3 또는 8.4
   * Composer 2.x

* 프로비저닝된 샌드박스 인스턴스가 있는 [!DNL Commerce Optimizer] 라이선스.

* 작성기를 사용하여 커넥터 메타패키지를 다운로드하려면 [인증 키](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/authentication-keys)를 사용하십시오.

* [[!DNL Commerce Optimizer] 샌드박스 인스턴스](../optimizer/get-started.md)에 대한 관리자 액세스 권한.

통합을 구성하는 [!DNL Adobe Commerce] 사용자에게는 다음이 있어야 합니다.

* Commerce 관리자에 대한 관리자 액세스 권한.

* [명령줄 액세스 [!DNL Adobe Commerce] 응용 프로그램 서버](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/project/user-access).

* [!DNL Commerce Optimizer] 프로젝트가 프로비저닝된 [IMS 조직](https://experienceleague.adobe.com/en/docs/core-services/interface/administration/organizations?)에 대한 개발자 액세스 권한.

>[!BEGINSHADEBOX]

## 충돌하는 확장 제거 {#remove-conflicting-extensions}

다음 확장이 설치되어 있는 경우 [!DNL Adobe Commerce Optimizer Connector]을(를) 설치하기 전에 해당 확장을 제거하십시오.

* [!DNL Adobe Commerce Live Search] (`magento/live-search`)
* [!DNL Adobe Commerce Product Recommendations] (`magento/product-recommendations`)
* [!DNL Adobe Commerce Catalog Service] (`magento/catalog-service`, `magento/catalog-service-installer`)
* **[!UICONTROL Data Management Dashboard]** (`magento-catalog-sync-admin`)

이러한 확장과 연결된 데이터는 여전히 Commerce 데이터베이스에서 사용할 수 있습니다. 그러나 커넥터를 사용하도록 설정한 경우 [!DNL Commerce Optimizer]&#x200B;(으)로 내보내지 않습니다. 커넥터를 사용하도록 설정한 후 이러한 확장에서 제공하는 검색 및 머천다이징 기능을 구현하려면 [[!DNL Commerce Optimizer] 관리 UI](https://experienceleague.adobe.com/en/docs/commerce/optimizer/overview#quick-tour)에서 구성하십시오.

>[!IMPORTANT]
>
>커넥터를 사용하기 전에 이러한 확장을 제거하지 않으면 커넥터와 기존 확장 모두에서 동일한 데이터를 내보냈기 때문에 구성 화면이 손상되고 [!DNL Commerce Optimizer]에 데이터가 중복되며, 확장 및 커넥터가 연결된 서비스를 인증하는 방식의 충돌로 인해 로그에 401 또는 403 오류가 표시될 수 있습니다.

>[!ENDSHADEBOX]

## 구성 단계 {#configuration-steps}

[!DNL Adobe Commerce Optimizer Connector]을(를) 사용하도록 설정하고 [!DNL Adobe Commerce]의 데이터를 [!DNL Commerce Optimizer] 인스턴스로 동기화하려면 다음 단계를 따르십시오.

1. **[작성기를 사용하여  [!DNL Adobe Commerce Optimizer Connector] 패키지](#install-the-adobe-commerce-optimizer-connector-package)**&#x200B;를 설치하여 [!DNL Adobe Commerce] 인스턴스를 [!DNL Commerce Optimizer]에 연결합니다.

1. 관리자의 **[Commerce 범위 내보내기 구성을 사용자 지정](#customize-the-commerce-scopes-export-configuration)**&#x200B;합니다.

1. **[통합을 사용하도록 설정 [!DNL Commerce Optimizer] 통합](#enable-the-adobe-commerce-optimizer-integration)**.

1. **[데이터 동기화가 작동하는지 확인](#verify-that-the-data-sync-is-working)**.

## [!DNL Adobe Commerce Optimizer Connector] 패키지 설치 {#install-the-adobe-commerce-optimizer-connector-package}

[!DNL Adobe Commerce Optimizer Connector]은(는) [!DNL Commerce Optimizer]에 대한 활성 라이선스를 가진 모든 Commerce 판매자가 사용할 수 있는 작성기 메타패키지로 제공됩니다.

### 설치 단계

1. 작성기를 사용하여 `adobe-commerce/commerce-data-export-aco-adapter` 모듈 추가:

   ```shell
   composer require adobe-commerce/commerce-data-export-aco-adapter
   ```

1. [!DNL Adobe Commerce] 스테이징 환경에 변경 내용을 배포합니다.

   배포가 완료되면 Commerce 관리 메뉴에서 [!DNL Commerce Optimizer] 옵션을 사용할 수 있습니다. **[!UICONTROL Commerce Optimizer]**&#x200B;을(를) 선택하여 Commerce 관리자에서 직접 [!DNL Commerce Optimizer] 인스턴스를 엽니다.

>[!NOTE]
>
>자세한 확장 설치 지침은 다음 안내서를 참조하십시오.
>
>[Cloud Infrastructure에서 [!DNL Adobe Commerce] 확장 설치](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/configure-store/extensions)
>
>[확장 설치 [!DNL Adobe Commerce] 온-프레미스](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/extensions)

## Commerce 범위 내보내기 구성 사용자 지정 {#customize-the-commerce-scopes-export-configuration}

기본적으로 모든 Commerce 범위(웹 사이트, 고객 그룹 및 스토어 보기)에 대해 카탈로그 데이터 동기화가 활성화됩니다. 비즈니스 요구 사항에 따라 특정 범위의 데이터만 동기화하도록 내보내기 설정을 사용자 지정할 수 있습니다. 예를 들어 같은 언어를 공유하는 여러 스토어 보기가 있는 경우 스토어 보기 중 하나에 대한 데이터만 내보내도록 선택하고 [!DNL Commerce Optimizer]의 여러 카탈로그 보기에 대해 [카탈로그 소스](../optimizer/setup/catalog-sources.md)(으)로 사용할 수 있습니다.

>[!IMPORTANT]
>
>내보내기 설정을 변경하면 전체 색인 재지정이 트리거되며, 이는 카탈로그 크기에 따라 상당한 시간이 걸릴 수 있습니다. Adobe에서는 통합을 활성화하고 초기 데이터 동기화를 시작하기 전에 [!DNL Commerce Optimizer]과(와) 동기화하도록 Commerce 범위를 구성하는 것이 좋습니다.

다음 표에서는 각 범위 수준에서 내보내는 데이터에 대해 설명합니다.

| 범위 | 데이터 내보냄 | 메모 |
| ----- | ------------- | ----- |
| 웹 사이트 및 고객 그룹 | 가격 및 가격 장부 | 명명 규칙 `&lt;website&gt;::&lt;SHA1 of customer group ID&gt;`을(를) 사용하여 각 가격 집합을 [가격 장부](../optimizer/setup/pricebooks.md)(으)로 내보냅니다. 웹 사이트의 모든 고객 그룹이 포함됩니다. |
| 스토어 보기 | 제품 및 제품 속성 | 각 저장소 보기는 [!DNL Commerce Optimizer]에 별도의 [카탈로그 원본](../optimizer/setup/catalog-sources.md)을 만듭니다. |

![Commerce Optimizer 동기화 설정으로 그리드 저장](./assets/aco-connector-storeviews-list.png){width="600" zoomable="yes"}

### 범위 내보내기 설정을 변경하려면

1. Commerce 관리에서 **[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL All Stores]**(으)로 이동합니다.

1. 구성할 웹 사이트 또는 스토어 보기를 선택합니다.

1. **[!DNL Commerce Optimizer]내보내기 설정**&#x200B;에서 확인란을 사용하여 필요에 따라 데이터 동기화를 활성화하거나 비활성화합니다.

   ![데이터 동기화 구성 업데이트](./assets/aco-connector-storeview-export-settings.png){width="500" zoomable="yes"}

1. 변경 사항을 저장합니다.

### 비헤이비어 활성화 및 비활성화

| 액션 | 결과 |
| -------- | -------- |
| 스토어 보기 비활성화 | **동기화를 사용하지 않도록 설정하면 스토어에서 카탈로그 데이터가 제거됩니다.** 카탈로그 원본이 [!DNL Commerce Optimizer]에 남아 있지만 동기화된 모든 데이터는 다음 cron 실행 시 제거됩니다. |
| 스토어 조회수 비활성화 후 재활성화 | 동일한 카탈로그 소스가 전체 데이터 재동기화로 다시 채워집니다. |

## [!DNL Commerce Optimizer] 통합 사용 {#enable-the-adobe-commerce-optimizer-integration}

`aco:config:init` CLI 명령을 실행하여 통합을 활성화하고 데이터 동기화를 시작합니다. 이 명령은 다음 단계를 완료합니다.

1. 명령줄 인수로 제공된 자격 증명을 사용하여 IMS 액세스 토큰을 얻습니다.
1. 테넌트의 유효성을 검사하고 수집 URL 및 [!DNL Commerce Optimizer] Studio URL을 추출하기 위해 `https://ccm.api.commerce.adobe.com/api/v1/tenants/{tenantId}/owner/{orgId}`에서 Commerce Cloud 관리자(CCM) 서비스를 호출합니다.
1. `core_config_data`에 모든 구성(클라이언트 암호로 암호화됨)을 저장합니다.
1. 모든 [!DNL Commerce Optimizer] 피드 인덱서를 무효화하여 초기 전체 동기화를 예약합니다.

>[!IMPORTANT]
>
>구성을 완료하는 즉시 백그라운드에서 데이터 동기화 처리가 시작됩니다. 카탈로그 크기에 따라 데이터 동기화 프로세스는 몇 분에서 몇 시간 정도 걸릴 수 있습니다.

### 필수 연결 세부 정보 가져오기

[Adobe Developer Console](https://developer.adobe.com/console)에서 [!DNL Commerce Optimizer] 수집 서비스에 대해 활성화된 새 프로젝트를 만들고 OAuth 서버 간 자격 증명을 생성합니다. 자세한 지침은 *머천다이징 개발자 안내서*&#x200B;의 [IMS 자격 증명 가져오기](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/authentication/#obtain-ims-credentials)를 참조하십시오.

자격 증명 페이지에서 다음 값을 저장합니다.

* **조직 ID**(`org_id`)
* **클라이언트 ID**(`client_id`)
* **클라이언트 암호**(`client_secret`)

![Adobe Developer Console 프로젝트 페이지에서 자격 증명 세부 정보 가져오기](./assets/developer-console-project-credentials.png){width="500" zoomable="yes"}

### [!DNL Commerce Optimizer] 인스턴스 세부 정보 가져오기

[!DNL Commerce Optimizer] 인스턴스 [[!DNL Instance details] 페이지](../optimizer/get-started.md#manage-instances)의 _[!DNL Instance Id]_필드 또는 인스턴스에 액세스하는 데 사용된 URL에서_&#x200B;테넌트 ID _을(를) 가져옵니다. 예: `https://experience.adobe.com/#/@&lt;your organization&gt;/in:&lt;tenant ID&gt;/commerce-optimizer-studio/home`.

1. Commerce 관리자에서 **[!UICONTROL Adobe Commerce Optimizer]**&#x200B;을(를) 선택하여 지침이 포함된 구성 페이지를 표시합니다.

   ![[!DNL Commerce Optimizer] 구성 페이지](./assets/aco-connector-admin-installation.png){width="500" zoomable="yes"}

1. 명령줄에서 [SSH를 사용](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/secure-connections)하여 [!DNL Adobe Commerce] 스테이징 환경에 연결합니다.

1. 다음 [!DNL Adobe Commerce] CLI 명령을 실행하여 통합을 구성하고 자리 표시자 값을 [!DNL Commerce Optimizer] 프로젝트의 값으로 바꿉니다.

   ```shell
   bin/magento aco:config:init --org_id=your-org --tenant_id=your-tenant --client_id=your-client-id --client_secret=your-secret
   ```

1. Commerce 관리자로 돌아가 [!UICONTROL Adobe Commerce Optimizer] 옵션을 선택하여 연결을 확인합니다.

   옵션을 선택하면 새 탭에서 [!DNL Commerce Optimizer] UI가 열립니다.

## 데이터 동기화가 작동하는지 확인 {#verify-that-the-data-sync-is-working}

{{$include /help/_includes/aco-connector/verify-optimizer-data-sync.md}}

## 다음 단계

1. **카탈로그 보기 및 정책 [!DNL Commerce Optimizer]개 구성**

   [!DNL Commerce Optimizer] UI에 카탈로그 보기 및 정책을 만듭니다. 가격 장부는 [!DNL Adobe Commerce] 고객 그룹에서 자동으로 만들어집니다. 지침은 *[!DNL Commerce Optimizer]사용 안내서*&#x200B;의 [카탈로그 보기](../optimizer/setup/catalog-view.md) 및 [정책](../optimizer/setup/policies.md) 설명서를 참조하십시오.

1. **[!DNL Edge Delivery Services]**&#x200B;에서 Commerce 상점 설정

   [Storefront 설정 설명서](https://experienceleague.adobe.com/developer/commerce/storefront/setup/){target="_blank"}에 따라 Storefront를 [!DNL Commerce Optimizer] 인스턴스에 연결하고 개인화된 상거래 경험을 제공하기 시작합니다.
