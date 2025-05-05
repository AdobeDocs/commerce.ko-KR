---
title: ' [!DNL Adobe Commerce as a Cloud Service] 시작'
description: ' [!DNL Adobe Commerce as a Cloud Service]을(를) 시작하는 방법에 대해 알아봅니다.'
role: Admin, Developer, User
exl-id: 58d98b9e-b41d-44db-9666-c924a5b005b3
source-git-commit: 9b90e6f79a394ec0941c9e48aee3859f0bcdedd5
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 0%

---

# 시작

{{accs-early-access}}

[!DNL Adobe Commerce as a Cloud Service]에서는 대부분의 구성을 즉시 제공합니다. 몇 가지 기본 설정 프로세스를 완료하면 스토어가 즉시 작동되고 실행됩니다. 이 안내서에서는 인스턴스를 만들고 작업하는 방법을 안내합니다.

다음 사용자 유형에 대한 높은 수준의 워크플로 개요를 보려면 아래 탭을 클릭하십시오.

* 관리자
* 판매자
* 개발자

>[!BEGINTABS]

>[!TAB 관리자 및 판매자 워크플로]

이 다이어그램은 관리자 및 판매자가 [!DNL Adobe Commerce as a Cloud Service]개의 인스턴스에 액세스하고 관리하는 방법에 대한 높은 수준의 개요를 제공합니다. 관리자 워크플로에 대한 자세한 내용은 [Adobe Admin Console 안내서](https://helpx.adobe.com/kr/enterprise/admin-guide.html)를 참조하십시오.

![[!DNL Adobe Commerce as a Cloud Service] 판매자 흐름 다이어그램](./assets/merchant-flow.svg){zoomable="yes"}

>[!TAB 개발자 워크플로]

이 다이어그램은 개발자가 App Builder을 사용하여 [!DNL Adobe Commerce as a Cloud Service]에 대한 통합을 만드는 방법에 대한 높은 수준의 개요를 제공합니다. 자세한 내용은 [API 설명서](https://developer.adobe.com/commerce/services/cloud/)를 참조하세요.

![[!DNL Adobe Commerce as a Cloud Service] 개발자 흐름 다이어그램](./assets/developer-flow.svg){zoomable="yes"}

>[!ENDTABS]

## 인스턴스 만들기

>[!NOTE]
>
>인스턴스를 만들려면 먼저 조직의 제품 관리자 또는 시스템 관리자가 사용자를 [!DNL Adobe Commerce as a Cloud Service] 제품의 사용자로 추가해야 합니다. 자세한 내용은 [사용자 및 관리자 추가](./user-management.md#add-users-and-admins)를 참조하십시오.

[!DNL Adobe Commerce as a Cloud Service]개의 인스턴스가 신용 기반 시스템을 사용합니다. 여러 인스턴스를 만들 수 있지만 각 인스턴스에는 상대적 크레딧이 필요합니다. 처음에 보유하고 있는 크레딧의 양은 구독에 따라 다릅니다.

1. [Adobe Experience Cloud](https://experience.adobe.com/) 계정에 로그인합니다.

1. [!UICONTROL Quick access]에서 [!UICONTROL **Commerce**]&#x200B;을(를) 클릭하여 [!UICONTROL Commerce Cloud Manager]을(를) 엽니다.

   [!UICONTROL Commerce Cloud Manager]에는 Adobe IMS 조직에서 사용할 수 있는 [!DNL Adobe Commerce as a Cloud Service] 인스턴스 목록이 표시됩니다.

1. 화면 오른쪽 상단에서 [!UICONTROL **인스턴스 추가**]&#x200B;를 클릭합니다.

   ![인스턴스 만들기](./assets/create-instance.png){width="50%" align="center" zoomable="yes"}

1. [!UICONTROL **Commerce as a Cloud Service**]&#x200B;을(를) 선택합니다.

1. 인스턴스의 **이름** 및 **설명**&#x200B;을 입력하십시오.

1. 인스턴스를 호스팅할 지역을 선택합니다.

   >[!NOTE]
   >
   >인스턴스를 생성하면 영역을 수정할 수 없습니다.

1. 인스턴스의 [!UICONTROL **환경 유형**]&#x200B;을(를) 선택하십시오. 다음 옵션 중에서 선택할 수 있습니다.

   * [!UICONTROL **샌드박스**] - 디자인 및 테스트 목적에 적합. 샌드박스 환경을 사용하여 [!DNL Adobe Commerce as a Cloud Service] 여정을 시작해야 합니다.
   * [!UICONTROL **프로덕션**] - 라이브 스토어 및 고객 응대 사이트용.

   >[!NOTE]
   >
   >샌드박스 인스턴스는 현재 북미 지역으로 제한됩니다.

1. _(선택 사항)_ 테스트 및 학습 목적으로 샘플 제품 데이터를 포함하려면 [!UICONTROL **테스트 데이터**] 드롭다운에서 [!UICONTROL **Adobe 스토어**]&#x200B;를 선택합니다.

   이 옵션을 건너뛸 수 있지만 건너뛰면 상점 앞에 제품이 없습니다. 전체 상점 경험을 보려면 [카탈로그를 가져와야](#import-your-catalog)합니다.

1. [!UICONTROL **인스턴스 추가**]&#x200B;를 클릭합니다.

## 인스턴스 액세스

인스턴스를 만든 후에는 [!UICONTROL Commerce Cloud Manager]에서 액세스할 수 있습니다.

1. [Adobe Experience Cloud](https://experience.adobe.com/) 계정에 로그인합니다.

1. [!UICONTROL Quick access]에서 [!UICONTROL **Commerce**]&#x200B;을(를) 클릭하여 [!UICONTROL Commerce Cloud Manager]을(를) 엽니다.

   [!UICONTROL Commerce Cloud Manager]에는 Adobe IMS 조직에서 사용할 수 있는 인스턴스 목록이 표시됩니다.

1. 인스턴스에 대한 [!UICONTROL Commerce Admin]을(를) 열려면 인스턴스 이름을 클릭합니다.

>[!TIP]
>
>REST 및 GraphQL 엔드포인트와 관리 URL을 포함하여 인스턴스에 대한 정보를 보려면 인스턴스 이름 옆에 있는 정보 아이콘을 클릭합니다.

## 카탈로그 가져오기

기본적으로 [!DNL Adobe Commerce as a Cloud Service] 인스턴스에는 제품 데이터가 포함되지 않습니다. 자체 카탈로그를 가져오기 전에 테스트 및 학습 목적으로 인스턴스를 만들 때 샘플 제품 데이터를 포함할 수 있는 옵션이 있습니다.

카탈로그를 [!DNL Adobe Commerce as a Cloud Service]&#x200B;(으)로 가져오는 방법에는 두 가지가 있습니다.

* [**Commerce 관리자**](https://experienceleague.adobe.com/ko/docs/commerce-admin/systems/data-transfer/import/data-import) - 몇 번의 클릭만으로 카탈로그 데이터를 가져올 수 있는 사용자 친화적인 인터페이스입니다.
* [**JSON API 가져오기**](https://developer.adobe.com/commerce/webapi/rest/modules/import/#import-json-api) - 카탈로그 데이터를 프로그래밍 방식으로 가져올 수 있는 REST API입니다.

<!-- TODO

- Add guidance about how to choose which method to use
- Add guidance for new vs existing customers (cross-reference OR and _include file for migration content)

-->

## 상점 배치

인스턴스를 만들었으므로 이제 Edge Delivery Services에서 제공하는 Commerce Storefront를 [설정](storefront.md)할 준비가 되었습니다.
