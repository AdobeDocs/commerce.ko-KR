---
title: Commerce 서비스 커넥터
description: 프로덕션 및 샌드박스 API 키를 사용하여 Adobe Commerce 또는 Magento Open Source 인스턴스를 서비스에 통합하는 방법을 알아봅니다.
feature: Services, Saas
role: Admin, User
exl-id: 1aa6ba8b-be39-496e-b83d-a4a7db9f5dd8
badgePaas: label="PaaS만" type="Informative" url="https://experienceleague.adobe.com/ko/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce 온 클라우드 프로젝트(Adobe 관리 PaaS 인프라) 및 온프레미스 프로젝트에만 적용됩니다."
source-git-commit: d7cf4898d5f44ab73017eb0a16b10856f0c4fc75
workflow-type: tm+mt
source-wordcount: '1486'
ht-degree: 0%

---

# [!DNL Commerce Services Connector]

일부 Adobe Commerce 및 Magento Open Source 기능은 [!DNL Commerce Services]에서 제공되며 SaaS(Software as a Service)로 배포됩니다. 이러한 서비스를 사용하려면 프로덕션 및 샌드박스 API 키를 사용하여 [!DNL Commerce] 인스턴스를 연결하고 [구성](#saas-configuration)에서 데이터 공간을 지정해야 합니다. 각 인스턴스에 대해 연결을 한 번만 구성하면 됩니다.

## 사용 가능한 서비스 {#availableservices}

다음은 [!DNL Commerce]을(를) 통해 액세스할 수 있는 [!DNL Commerce Services Connector] 기능을 나열합니다.

| 서비스 | 가용성 |
| ---|--- |
| Adobe Sensei 제공 [[!DNL Product Recommendations]](/help/product-recommendations/overview.md) | Adobe Commerce |
| Adobe Sensei 제공 [[!DNL Live Search]](/help/live-search/overview.md) | Adobe Commerce |
| [[!DNL Payment Services]](/help/payment-services/guide-overview.md) | Adobe Commerce 및 Magento Open Source |
| [[!DNL Catalog Service]](/help/catalog-service/overview.md) | Adobe Commerce |
| [[!DNL Data Connection]](/help/data-connection/overview.md) | Adobe Commerce |

## 아키텍처

높은 수준에서 [!DNL Commerce Services Connector]은(는) 다음 핵심 요소로 구성됩니다.

![Commerce 서비스 커넥터 아키텍처](assets/saas-config-sync-workflow.png)

다음 섹션에서는 이러한 각 요소에 대해 자세히 설명합니다.

## 자격 증명 {#apikey}

프로덕션 및 샌드박스 API 키는 [!DNL Commerce]라이선스 소유자[의 &#x200B;](https://experienceleague.adobe.com/ko/docs/commerce-cloud-service/start/onboarding) 계정에서 생성됩니다. Commerce 계정은 고유한 [!DNL Commerce] ID(MageID)로 식별됩니다. 판매자 조직의 라이선스 소유자는 계정이 양호한 경우 제품 추천 또는 라이브 검색과 같은 서비스에 대한 API 키를 생성할 수 있습니다.

라이선스 소유자를 대신하여 프로젝트 및 환경을 관리하는 시스템 통합자 또는 개발 팀과 &quot;필요한 정보&quot;에 따라 키를 공유할 수 있습니다. 라이선스 소유자가 [!DNL Shared Access]을(를) 부여한 개발자는 해당 계정의 [!DNL Switch Accounts] 드롭다운에 판매자의 조직이 있더라도 해당 사용자를 대신하여 키를 생성할 수 없습니다.

또한 솔루션 통합자는 [!DNL Commerce Services]을(를) 사용할 수 있습니다. 솔루션 통합자인 경우 [!DNL Commerce] 파트너 계약의 서명자가 API 키를 생성해야 합니다.

>[!NOTE]
>키 식별자 *Production* 및 *Sandbox*&#x200B;이(가) 환경을 참조하지 않습니다. 로컬, 개발, 스테이징 또는 프로덕션 환경과 같은 각 환경에 대해 동일한 API 키 세트를에 사용합니다.
>
>라이선스 소유자는 일반적으로 Adobe Commerce 계정의 기본 담당자이며 항상 Adobe Commerce on cloud infrastructure 프로젝트의 프로젝트 소유자와 동일하지 않습니다.

### 프로덕션 및 샌드박스 API 키 생성 {#genapikey}

1. [!DNL Commerce]https://account.magento.com[에서 &#x200B;](https://account.magento.com/customer/account/login){:target="_blank"} 계정에 로그인합니다.

1. **Magento** 탭에서 사이드바의 **API 포털**&#x200B;을 선택합니다.

1. _환경_ 메뉴에서 **프로덕션** 또는 **샌드박스**&#x200B;를 선택합니다.

   >[!NOTE]
   >
   >*프로덕션* 및 *샌드박스*&#x200B;는 Adobe SaaS 백엔드 시스템에 데이터가 저장되는 데이터 공간 환경을 나타냅니다. 키를 사용할 상거래 환경은 참조되지 않습니다.

1. _API 키_ 섹션에 이름을 입력하고 **새로 추가**&#x200B;를 클릭하여 대화 상자를 열어 새 키를 다운로드합니다.

   ![개인 키 다운로드](assets/download-api-private-key.png)

   >[!WARNING]
   >
   > 이 대화 상자는 키를 복사하거나 다운로드할 수 있는 유일한 기회를 제공합니다.

1. **다운로드**&#x200B;를 클릭한 다음 **취소**&#x200B;를 클릭합니다.

1. 각 환경(프로덕션 및 샌드박스)에 대해 위의 단계를 반복합니다.

   이제 **API 키** 섹션에 API(공개) 키가 표시됩니다. 라이선스와 연결된 환경 또는 설치에서 [SaaS 프로젝트를 선택 또는 생성](#createsaasenv)할 때 4개의 키(프로덕션 및 샌드박스 키, 공용+개인)가 모두 필요합니다.

## SaaS 구성 {#saasenv}

[!DNL Commerce]에서 올바른 위치에 데이터를 보낼 수 있도록 [!DNL Commerce Services]개의 인스턴스를 SaaS 프로젝트 및 SaaS 데이터 공간으로 구성해야 합니다. SaaS 프로젝트는 모든 SaaS 데이터 공간을 그룹화합니다. SaaS 데이터 공간은 [!DNL Commerce Services]이(가) 작동하도록 하는 데이터를 수집하고 저장하는 데 사용됩니다. 이 데이터 중 일부는 [!DNL Commerce] 인스턴스에서 내보낼 수 있으며 일부는 상점 앞의 쇼핑객 활동에서 수집할 수 있습니다. 그런 다음 해당 데이터는 보안 클라우드 스토리지로 유지됩니다.

[!DNL Product Recommendations]의 경우 SaaS 데이터 공간에 카탈로그 및 동작 데이터가 포함되어 있습니다. [!DNL Commerce] 구성에서 [선택하여](https://experienceleague.adobe.com/ko/docs/commerce-admin/config/services/saas) SaaS 데이터 공간으로 [!DNL Commerce] 인스턴스를 지정할 수 있습니다.

>[!WARNING]
>
> 데이터 충돌을 방지하려면 프로덕션 **설치에서만**&#x200B;프로덕션 SaaS 데이터 공간[!DNL Commerce]을 사용하십시오. 그렇지 않으면 테스트 데이터로 프로덕션 사이트 데이터를 오염시켜 배포가 지연될 위험이 있습니다. 예를 들어 스테이징 URL과 같은 스테이징 데이터에서 프로덕션 제품 데이터를 실수로 덮어쓸 수 있습니다.
> &#x200B;> 이 경우 데이터 정리를 요청하려면 [지원 요청을 제출](https://experienceleague.adobe.com/ko/docs/commerce-knowledge-base/kb/overview)하십시오.

관리 패널에서 LiveSearch 구성 필드를 찾을 수 없는 경우 올바른 SaaS API 키를 입력했는지 확인하십시오.  프로덕션 데이터 공간을 구성할 때 프로덕션 SaaS 키를 추가했는지 확인하고 스테이징 데이터 공간을 구성할 때 스테이징 키를 추가했는지 확인합니다. 잘못된 키를 구성하면 Adobe Commerce 환경에서 LiveSearch와 같은 SaaS 서비스를 사용할 수 없습니다.

### SaaS 데이터 공간 프로비저닝

모든 Adobe Commerce 판매자는 SaaS 프로젝트당 하나의 프로덕션 데이터 공간과 두 개의 테스트 데이터 공간에 액세스할 수 있습니다.

여러 환경에서 동일한 데이터 공간을 동시에 사용하지 않는 한 비프로덕션 환경에서 테스트 데이터 공간을 사용할 수 있습니다. 다른 환경에서 테스트 데이터 공간을 사용하려면 해당 환경에서 데이터 공간을 선택하고 구성하기 전에 데이터 정리를 수행하십시오.

여러 스테이징 환경이 있는 Adobe Commerce Cloud Pro 프로젝트의 경우 [지원 요청을 제출](https://experienceleague.adobe.com/home?lang=ko&support-tab=home#support)하여 각 스테이징 환경에 대한 추가 테스트 데이터 공간을 요청할 수 있습니다. 그러나 스테이징 환경이 한 개만 있고 추가 테스트 데이터 공간이 필요한 경우 다음 옵션을 사용할 수 있습니다.

- 추가 스테이징 환경을 요청하려면 고객 성공 팀 또는 귀사의 지정된 고객 성공 관리자에게 문의하십시오.

- 추가 테스트 데이터 공간을 요청하고 추가 데이터 공간에 대한 비즈니스 타당성을 나타내려면 [지원 요청을 제출](https://experienceleague.adobe.com/home?lang=ko&support-tab=home#support)하십시오. 이 요청은 승인 대상이 됩니다.

Adobe 결제 서비스를 사용하는 Magento Open Source 고객도 추가 데이터 공간을 요청할 수 있습니다. 테스트 데이터 공간을 요청하기 위해 [지원 요청](https://experienceleague.adobe.com/home?lang=ko&support-tab=home#support)을 제출하기 전에 결제 팀에 연락하여 추가 데이터 공간의 사전 승인을 받으십시오.

여러 클라우드 프로젝트 또는 온-프레미스(라이브/프로덕션) 설치를 보유한 고객은 [지원 요청을 제출](https://experienceleague.adobe.com/home?lang=ko&support-tab=home#support)하여 각 프로젝트 또는 인스턴스에 대한 추가 프로덕션 및 테스트 데이터 공간을 요청할 수도 있습니다.

### SaaS 프로젝트 선택 또는 만들기 {#createsaasenv}

SaaS 프로젝트를 선택하거나 만들려면 스토어의 [!DNL Commerce] 라이선스 소유자에게 [!DNL Commerce] API 키를 요청하십시오.

>[!NOTE]
>
> **[!UICONTROL Commerce Services Connector]** 구성에 [!DNL Commerce] 섹션이 표시되지 않으면 원하는 [!DNL Commerce]서비스[[!DNL Commerce] 에 대한 &#x200B;](#availableservices) 모듈을 설치해야 합니다.

1. _관리자_ 사이드바에서 **시스템** > 서비스 > **Commerce 서비스 커넥터**(으)로 이동합니다.

   **[!UICONTROL Commerce Services Connector]** 구성에 [!DNL Commerce] 섹션이 표시되지 않으면 원하는 [!DNL Commerce]서비스[[!DNL Commerce] 에 대한 &#x200B;](#availableservices) 모듈을 설치하십시오. 또한 `magento/module-services-id` 패키지가 설치되어 있는지 확인하십시오.

1. _[!UICONTROL Sandbox API Keys]_&#x200B;및&#x200B;_[!UICONTROL Production API Keys]_ 섹션에 키 값을 붙여 넣습니다.

   - 비공개 키에는 키 시작 부분의 `----BEGIN PRIVATE KEY---` 및 키 끝 부분의 `----END PRIVATE KEY----`이(가) 포함되어야 합니다.
   - 실제 키의 사본이 없는 경우 계정 소유자에게 요청한 다음 값을 구성에 연결합니다.

   >[!WARNING]
   >
   > 데이터베이스 백업이나 스냅샷을 쿼리하고 값을 구성에 붙여 넣어 키 값을 추가하면 추가 암호화 계층이 적용되고 키가 작동하지 않습니다.

1. **저장**&#x200B;을 클릭합니다.

키와 연결된 모든 SaaS 프로젝트가 **SaaS 식별자** 섹션의 **프로젝트** 필드에 나타납니다.

1. SaaS 프로젝트가 없는 경우 **프로젝트 만들기**&#x200B;를 클릭하십시오. 그런 다음 **프로젝트** 필드에 SaaS 프로젝트의 이름을 입력합니다.

>[!NOTE]
>
>혼동을 방지하기 위해 특정 Commerce 서비스를 프로젝트 이름으로 사용하지 마십시오(예: *라이브 검색*, *제품 추천* 또는 *데이터 연결*).  여러 SaaS 프로젝트에 대해 라이선스가 프로비저닝되지 않은 경우 여러 서비스에 대해 동일한 SaaS 프로젝트를 사용할 수 있습니다.

1. **저장소의 현재 구성에 사용할**&#x200B;데이터 공간[!DNL Commerce]을(를) 선택하십시오.

>[!NOTE]
>
>Commerce 서비스와 통합할 인스턴스가 따로 있는 경우 [지원 티켓을 제출](https://experienceleague.adobe.com/ko/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket)하여 각 추가 인스턴스에 대해 새 SaaS 프로젝트를 요청하세요. 지원이 SaaS 프로젝트를 만든 후 동일한 API 키를 사용하여 인스턴스에 대한 Commerce Services 통합을 구성하고 데이터 공간에 대한 새 SaaS 프로젝트를 선택합니다.

>[!WARNING]
>
> 내 계정의 API 포털 섹션에서 새 키를 생성하는 경우 관리 구성에서 API 키를 즉시 업데이트합니다. 새 키를 생성하고 관리에서 업데이트하지 않으면 SaaS 확장이 더 이상 작동하지 않고 중요한 데이터를 잃게 됩니다.

SaaS 프로젝트 또는 데이터 공간의 이름을 변경하려면 둘 중 하나 옆에 있는 **이름 바꾸기**&#x200B;를 클릭합니다. 이름은 프로젝트와 데이터 공간을 식별하고 구분하는 데 도움이 되는 레이블일 뿐이므로 이름을 변경해도 서비스에 영향을 주지 않습니다.

## IMS 조직(선택 사항) {#organizationid}

Adobe Commerce 인스턴스를 Adobe Experience Platform에 연결하려면 Adobe ID을 사용하여 Adobe 계정에 로그인합니다. 로그인하면 Adobe 계정과 연결된 IMS 조직이 이 섹션에 표시됩니다.

## SaaS 데이터 내보내기

[!DNL Commerce] 인스턴스가 [!DNL Commerce Services]에 연결되면 SaaS 데이터 내보내기 프로세스는 연결된 Commerce 서비스와 동기화할 수 있도록 [!DNL Commerce] 서버의 Commerce 데이터를 [!DNL Commerce SaaS Services]&#x200B;(으)로 내보냅니다. 관리에서 [데이터 관리 대시보드](https://experienceleague.adobe.com/ko/docs/commerce-admin/systems/data-transfer/data-dashboard)를 사용하여 동기화 상태를 확인할 수 있습니다. 자세한 내용은 [SaaS 데이터 내보내기 안내서](../data-export/overview.md)를 참조하십시오.
