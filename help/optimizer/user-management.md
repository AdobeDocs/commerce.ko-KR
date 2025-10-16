---
title: 사용자 관리
description: ' [!DNL Adobe Commerce Optimizer]의 사용자를 만들고 관리하고 사용자 역할을 할당하는 방법을 알아봅니다.'
badgeSaas: label="SaaS만" type="Positive" url="https://experienceleague.adobe.com/ko/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."
exl-id: 9ab2118d-b7e3-4e2e-adac-8f3950fe1824
source-git-commit: 36a953d4fb0e1e14c7cb88a80f3b59d6fe8eb49e
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 0%

---

# 사용자 관리

[!DNL Adobe Commerce Optimizer]에 대한 액세스를 활성화하려면 [Adobe Admin Console](https://adminconsole.adobe.com){target="_blank"}에서 사용자를 추가하고 Commerce 제품에 대한 액세스 권한이 있는지 확인하십시오.

다음 역할 중 하나에 사용자를 할당할 수 있습니다.

- **사용자**— 사용자는 [!DNL Adobe Commerce Optimizer] UI에 액세스하여 카탈로그 보기 및 머천다이징 규칙을 보고 관리하며 성능 지표를 추적할 수 있습니다.

- [**개발자**](https://helpx.adobe.com/kr/enterprise/using/manage-developers.html#Adddevelopers){target="_blank"}— 개발자는 Adobe Developer Console에 대한 사용자 권한과 액세스 권한이 있습니다. 즉, App Builder 및 API Mesh와 같은 Adobe 확장성 도구와 함께 [!DNL Adobe Commerce Optimizer] API 및 SDK와 같은 개발자 도구를 사용하도록 프로젝트를 만들고 자격 증명을 구성할 수 있습니다.

- **관리자** - 세 가지 유형의 관리자 역할이 있습니다.
   - [시스템 관리자](https://helpx.adobe.com/kr/enterprise/using/admin-roles.html){target="_blank"} - 시스템 관리자는 Adobe Admin Console을 통해 조직의 모든 제품 및 제품 프로필에 액세스할 수 있습니다.
   - [제품 관리자](#add-a-product-admin) - 제품 관리자는 [에서 &#x200B;](#add-users-and-admins)제품에 대한 사용자, 역할 및 권한을 관리[!DNL Adobe Admin Console]할 수 있습니다.
   - [제품 프로필 관리자](#add-users-developers-and-product-profile-admins) - 제품 프로필 관리자는 [!DNL Adobe Admin Console]의 제품에 대한 사용자를 관리할 수 있습니다.

## 제품 관리자 추가

>[!BEGINTABS]

>[!NOTE]
>
>제품 관리자로 추가하기 전에 제품 관리자에게 [사용자 역할](#add-users)을 할당하십시오. 기본 Commerce 권한에 사용자 역할이 필요합니다.

>[!TAB GA(2025년 10월 13일 이후에 프로비저닝됨)]

1. <https://adminconsole.adobe.com>(으)로 이동하여 Adobe ID으로 로그인합니다.

1. 조직을 선택합니다.

1. [!UICONTROL **사용자**] 탭을 선택합니다.

1. [!UICONTROL **관리자**] 탭을 선택합니다.

1. [!UICONTROL **관리자 추가**]&#x200B;를 클릭합니다.

1. 관리자로 추가할 사용자의 사용자 이름 또는 전자 메일 주소를 입력하고 [!UICONTROL **다음**]&#x200B;을(를) 클릭합니다.

1. [!UICONTROL **제품 프로필 관리자**] 역할을 선택하십시오.

1. 제품을 추가하려면 **+**&#x200B;을(를) 클릭하십시오.

1. 관리자를 추가할 기존 Commerce Optimizer 인스턴스를 선택합니다. Commerce Optimizer 인스턴스는 `Adobe Commerce - <instance-name> - ACO - <environment-type> - <tenant-id>` 형식을 사용합니다.

1. 제품 프로필을 선택합니다.

1. [!UICONTROL **적용**]&#x200B;을 클릭합니다.

1. [!UICONTROL **저장**]&#x200B;을 클릭합니다.

>[!TAB 조기 액세스(2025년 10월 13일 전에 프로비저닝됨)]

1. <https://adminconsole.adobe.com>(으)로 이동하여 Adobe ID으로 로그인합니다.

1. 조직을 선택합니다.

1. [!UICONTROL **제품**] 탭의 [!UICONTROL **제품 및 서비스**]&#x200B;에서 [!UICONTROL **Adobe Commerce - Commerce Cloud 관리자**] 제품을 선택합니다.

   ![제품 선택](/help/cloud-service/assets/backend.png){width="600" zoomable="yes"}

1. [!UICONTROL **관리자**] 탭을 선택합니다.

1. [!UICONTROL **관리자 추가**]&#x200B;를 클릭합니다.

1. 관리자로 추가할 사용자의 사용자 이름 또는 전자 메일 주소를 입력하고 [!UICONTROL **저장**]&#x200B;을 클릭합니다.

>[!ENDTABS]

## 사용자 추가

다음 지침은 [!DNL Commerce Cloud Manager] 및 Commerce Optimizer에 사용자를 추가하는 방법에 대한 정보를 제공합니다. [!DNL Commerce Cloud Manager] 인터페이스를 사용하면 Commerce Optimizer 인스턴스를 만들고 관리할 수 있습니다. 이 프로세스는 개발자 및 관리자를 포함한 모든 사용자에게 필요합니다.

>[!NOTE]
>
>제품 관리자와 시스템 관리자만 Adobe Commerce Optimizer 제품에 사용자 및 개발자를 추가할 수 있습니다.

>[!BEGINTABS]

>[!TAB GA(2025년 10월 13일 이후에 프로비저닝됨)]

1. <https://adminconsole.adobe.com>(으)로 이동하여 Adobe ID으로 로그인합니다.

1. 조직을 선택합니다.

1. [!UICONTROL **제품**] 탭을 선택합니다.

1. [!UICONTROL **Adobe Commerce**] 제품을 선택하십시오.

1. 사용자를 Cloud Manager 인터페이스에 추가하려는 경우 Commerce Cloud Manager 제품을 선택합니다. 여기서 Commerce Optimizer 인스턴스를 생성하고 관리할 수 있으며, 기존 Commerce Optimizer 인스턴스를 선택하여 사용자를 추가할 수도 있습니다. Commerce Optimizer 인스턴스는 `Adobe Commerce - <instance-name> - ACO - <environment-type> - <tenant-id>` 형식을 사용합니다.

1. [!UICONTROL **사용자**] 탭을 선택하고 [!UICONTROL **사용자 추가**]&#x200B;를 클릭합니다.

1. 추가할 사용자의 사용자 이름 또는 전자 메일 주소를 입력하고 [!UICONTROL **저장**]&#x200B;을 클릭합니다.

1. 원하는 제품 프로필을 선택합니다.

1. [!UICONTROL **적용**]&#x200B;을 클릭합니다.

1. [!UICONTROL **저장**]&#x200B;을 클릭합니다.

>[!TAB 조기 액세스(2025년 10월 13일 전에 프로비저닝됨)]

1. <https://adminconsole.adobe.com>(으)로 이동하여 Adobe ID으로 로그인합니다.

1. 조직을 선택합니다.

1. [!UICONTROL **제품**] 탭의 [!UICONTROL **제품 및 서비스**]&#x200B;에서 [!UICONTROL **Adobe Commerce - Commerce Cloud 관리자**] 제품을 선택합니다.

   ![제품 선택](/help/cloud-service//assets/backend.png){width="600" zoomable="yes"}

1. [!UICONTROL **기본 - Cloud Manager**] 제품 프로필을 클릭합니다.

1. [!UICONTROL **사용자**] 탭을 선택하고 [!UICONTROL **사용자 추가**]&#x200B;를 클릭합니다.

   ![탭 선택](/help/cloud-service/assets/tab-select.png){width=600 zoomable="yes"}

1. 추가할 사용자의 사용자 이름 또는 전자 메일 주소를 입력하고 [!UICONTROL **저장**]&#x200B;을 클릭합니다.

>[!ENDTABS]

### 개발자 및 제품 프로필 관리자 추가

개발자 및 제품 프로필 관리자를 추가하려면 [사용자 추가](#add-users) 프로세스를 반복하되, [!UICONTROL **사용자**] 탭 대신 [!UICONTROL **개발자**] 또는 [!UICONTROL **관리자**] 탭을 선택하십시오.

>[!NOTE]
>
>개발자를 개발자로 추가하기 전에 개발자에게 사용자 역할을 할당하십시오. 기본 Commerce 권한에 사용자 역할이 필요합니다.

![탭 선택](/help//cloud-service/assets/tab-select.png){width=600 zoomable="yes"}

## 대량 사용자 관리

다음 방법 중 하나를 사용하여 여러 사용자를 보다 효율적으로 추가할 수 있습니다.

- Adobe Admin Console의 **CSV로 사용자 추가** 기능을 사용하여 [일괄 CSV 업로드](https://helpx.adobe.com/kr/enterprise/using/bulk-upload-users.html){target="_blank"}를 수행합니다.
- [사용자 그룹](https://helpx.adobe.com/kr/enterprise/using/user-groups.html){target="_blank"}을(를) 만들어 역할에 여러 사용자를 추가하십시오. 그런 다음 [!UICONTROL **Adobe Commerce - Commerce Cloud 관리자**] 제품을 사용자 그룹에 추가합니다.

