---
title: 시작하기
description: ' [!DNL Adobe Commerce Optimizer]을(를) 시작하는 방법에 대해 알아봅니다.'
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="SaaS만" type="Positive" url="https://experienceleague.adobe.com/ko/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."
source-git-commit: f49a86b8793e2d91413acfbc0b922cb94db67362
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 0%

---

# 시작

이 문서에서는 [!DNL Adobe Commerce Optimizer]을(를) 사용하여 최신 정보를 얻는 방법에 대해 설명합니다. 이 안내서는 머천다이저 및 관리자 역할에 중점을 두고 있으며, 개발자가 수행하는 간단한 고급 작업이 포함되어 있습니다. 자세한 개발자별 콘텐츠는 [개발자 설명서](https://developer-stage.adobe.com/commerce/services/composable-catalog/)를 참조하십시오.

## 당신의 역할은 무엇입니까?

[!DNL Adobe Commerce Optimizer]을(를) 성공적으로 설정하려면 일반적으로 다음 팀원이 필요합니다.

- 관리자
- 개발자
- 머천다이저

각 팀원은 다음 표에 설명된 대로 각자의 역할 및 책임 세트를 가집니다.

| 역할 | 작업 |
|---|---|
| 관리자 | Admin Console을 사용하여 관리자, 사용자 그룹, 사용자 및 개발자를 만듭니다&#x200B;. |
|  | Commerce Cloud 관리자에서 새 [!DNL Adobe Commerce Optimizer] 인스턴스를 만듭니다&#x200B;. |
|  | 정책 및 카탈로그 보기를 설정합니다. |
| 개발자 | Developer Console을 사용하여 프로젝트를 만들고, 개발자에게 API 액세스 권한을 부여하고, 필요한 애플리케이션 및 사용자 지정을 설치할 수 있습니다. |
|  | API Mesh 및 App Builder을 사용하여 백오피스 시스템(장바구니, 체크아웃)에 연결합니다&#x200B;. |
|  | 머천다이징 서비스 데이터 수집 API를 사용하여 기존 상거래 솔루션에서 카탈로그 데이터 &#x200B; 수집 |
|  | 상점 설정 |
| 머천다이저 | 제품 검색을 설정합니다&#x200B;. |
|  | 제품 권장 사항을 설정합니다. |

각 역할은 [!DNL Adobe Commerce Optimizer] 환경의 성공적인 온보딩 및 시작에 필수적인 역할을 합니다. 다음 다이어그램은 조직의 각 역할에 대한 높은 수준의 시작 - 종료 워크플로우를 보여 줍니다.

![높은 수준의 워크플로](./assets/high-level-workflow.png){zoomable="yes"}

### 관리자

관리자는 조직의 인스턴스 설정, 사용자, 그룹 및 권한을 관리합니다.

- **[Adobe Admin Console에 액세스](https://helpx.adobe.com/kr/enterprise/admin-guide.html)** - 전체 조직에서 Adobe 권한을 관리합니다. 귀하 또는 조직의 제품 관리자 또는 시스템 관리자가 [!DNL Adobe Commerce Optimizer] 제품에 사용자를 추가하는 방법에 대해 알아보려면 [사용자 관리](./user-management.md)를 참조하세요.

- **인스턴스 만들기** - [!DNL Adobe Commerce Optimizer] 인스턴스가 크레딧 기반 시스템을 사용합니다. 각 인스턴스에 하나의 해당하는 크레딧이 필요한 여러 샌드박스 및 프로덕션 인스턴스를 만들 수 있습니다. 처음에 보유하고 있는 크레딧의 양은 구독에 따라 다릅니다. [자세히 알아보기](#create-an-instance)

- **인스턴스에 액세스** - 인스턴스를 만든 후 [!UICONTROL Commerce Cloud Manager]에서 액세스할 수 있습니다. [자세히 알아보기](#access-an-instance)

- **카탈로그 보기 및 정책을 설정** - [카탈로그 보기 및 정책을 정의하는 방법](./setup/catalog-view.md)을 알아보세요. 카탈로그에는 제품 데이터가 포함될 뿐만 아니라 비즈니스 구조를 정의하는 데도 도움이 됩니다.

### 개발자

개발자는 프로젝트와 자격 증명을 생성하고, 확장을 설치하고, 카탈로그 데이터를 수집하고, 일반적인 플랫폼 아키텍처 작업을 수행합니다. 자세한 개발자별 콘텐츠는 [개발자 설명서](https://developer-stage.adobe.com/commerce/services/composable-catalog/)를 참조하십시오.

- **Developer Console 액세스** - [Developer Console](https://developer.adobe.com/developer-console/docs/guides/getting-started)에 액세스하여 [!DNL Adobe Commerce Optimizer]에 대한 프로젝트를 만들고, 액세스 토큰을 생성하고, 필요한 응용 프로그램과 사용자 지정을 설치합니다.

- **카탈로그 데이터 수집** - [데이터 수집 API](https://developer-stage.adobe.com/commerce/services/composable-catalog/data-ingestion/using-the-api/) 설명서를 참조하여 카탈로그 데이터를 [!DNL Adobe Commerce Optimizer]&#x200B;(으)로 가져오는 방법에 대해 알아보십시오.

  수집된 카탈로그 데이터가 [데이터 동기화](./setup/data-sync.md) 페이지에 표시됩니다.

- **Storefront 설정** - Storefront를 설정하기 전에 먼저 조직의 [관리자](#administrator)가 일반적으로 수행하는 작업인 인스턴스를 만들어야 합니다. 인스턴스를 만들면 Edge Delivery Services에서 제공하는 Commerce Storefront를 [설정](./storefront.md)할 준비가 되었습니다.

### 머천다이저

머천다이저는 쇼퍼 데이터 및 분석을 사용하여 상점에서의 제품 배치, 가격 및 프로모션에 대한 전략적 결정을 내리는 동시에 제품 검색 및 추천을 통해 쇼핑 경험을 최적화합니다.

- **제품 검색 및 권장 사항 설정** - 제품 검색 및 권장 사항을 통해 쇼핑객을 위한 [개인화된 경험을 만들기](./merchandising/overview.md)하는 방법을 알아봅니다.

## 인스턴스 만들기

1. [Adobe Experience Cloud](https://experience.adobe.com/) 계정에 로그인합니다.

1. [!UICONTROL Quick access]에서 [!UICONTROL **Commerce**]&#x200B;을(를) 클릭하여 [!UICONTROL Commerce Cloud Manager]을(를) 엽니다.

   [!UICONTROL Commerce Cloud Manager]은(는) [!DNL Adobe Commerce Optimizer] 및 [!DNL Adobe Commerce as a Cloud Service]에 대해 프로비저닝된 인스턴스를 모두 포함하여 Adobe IMS 조직에서 사용할 수 있는 [!DNL Adobe Commerce] 인스턴스 목록을 표시합니다.

1. 화면 오른쪽 상단에서 [!UICONTROL **인스턴스 추가**]&#x200B;를 클릭합니다.

   ![인스턴스 만들기](./assets/create-aco-instance.png){width="100%" align="center" zoomable="yes"}

1. [!UICONTROL **Commerce Optimizer**]&#x200B;을(를) 선택합니다.

1. 인스턴스의 **이름** 및 **설명**&#x200B;을 입력하십시오.

1. 인스턴스를 호스팅할 지역을 선택합니다.

   >[!NOTE]
   >
   >인스턴스를 생성한 후에는 영역을 변경할 수 없습니다.

1. 인스턴스에 대해 다음 [!UICONTROL **환경 유형**] 중 하나를 선택하십시오.

   - [!UICONTROL **샌드박스**] - 디자인 및 테스트 목적에 적합. 샌드박스 환경을 사용하여 [!DNL Adobe Commerce Optimizer] 여정을 시작해야 합니다.
   - [!UICONTROL **프로덕션**] - 라이브 스토어 및 고객 응대 사이트용.

   >[!NOTE]
   >
   >샌드박스 인스턴스는 현재 북미 지역으로 제한됩니다.

1. [!UICONTROL **인스턴스 추가**]&#x200B;를 클릭합니다.

   이제 Cloud Manager에서 새 인스턴스를 사용할 수 있습니다.

1. GraphQL 및 카탈로그 서비스 끝점, Adobe Commerce Optimizer 애플리케이션에 액세스할 수 있는 URL, 인스턴스 ID(테넌트 ID) 등 인스턴스 세부 사항을 보려면 인스턴스 이름 옆에 있는 정보 아이콘을 클릭합니다.

   ![인스턴스 만들기](./assets/aco-instance-details.png){width="100%" align="center" zoomable="yes"}

## 인스턴스 액세스

1. [Adobe Experience Cloud](https://experience.adobe.com/) 계정에 로그인합니다.

1. [!UICONTROL Quick access]에서 [!UICONTROL **Commerce**]&#x200B;을(를) 클릭하여 [!UICONTROL Commerce Cloud Manager]을(를) 엽니다.

   [!UICONTROL Commerce Cloud Manager]에는 Adobe IMS 조직에서 사용할 수 있는 인스턴스 목록이 표시됩니다.

1. 인스턴스와 연결된 [!UICONTROL Commerce Optimizer] 응용 프로그램을 열려면 인스턴스 이름을 클릭합니다.


