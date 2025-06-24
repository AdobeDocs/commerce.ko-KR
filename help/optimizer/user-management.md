---
title: 사용자 관리
description: ' [!DNL Adobe Commerce Optimizer]에서 사용자를 관리하는 방법을 알아봅니다.'
badgeSaas: label="SaaS만" type="Positive" url="https://experienceleague.adobe.com/ko/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."
source-git-commit: 02758aa5cc14af6d46bfc4bb7865fa37a787d4cb
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---

# 사용자 관리

[!DNL Adobe Commerce Optimizer]에 대한 액세스를 활성화하려면 [Adobe Admin Console](https://adminconsole.adobe.com){target="_blank"}에서 사용자를 추가하고 Commerce 제품에 대한 액세스 권한이 있는지 확인하십시오.

다음 역할 중 하나에 사용자를 할당할 수 있습니다.

- **사용자**— 사용자는 [!DNL Adobe Commerce Optimizer] UI에 액세스하여 카탈로그 보기 및 머천다이징 규칙을 보고 관리하며 성능 지표를 추적할 수 있습니다.

- [**개발자**](https://helpx.adobe.com/kr/enterprise/using/manage-developers.html#Adddevelopers){target="_blank"}— 개발자는 Adobe Developer Console에 대한 사용자 권한과 액세스 권한이 있습니다. 즉, App Builder 및 API Mesh와 같은 Adobe 확장성 도구와 함께 [!DNL Adobe Commerce Optimizer] API 및 SDK와 같은 개발자 도구를 사용하도록 프로젝트를 만들고 자격 증명을 구성할 수 있습니다.

- **관리자** - 세 가지 유형의 관리자 역할이 있습니다.
   - [시스템 관리자](https://helpx.adobe.com/kr/enterprise/using/admin-roles.html){target="_blank"} - 시스템 관리자는 Adobe Admin Console을 통해 조직의 모든 제품 및 제품 프로필에 액세스할 수 있습니다.
   - [제품 관리자](#add-a-product-admin) - 제품 관리자는 [!DNL Adobe Admin Console]에서 [제품에 대한 사용자, 역할 및 권한을 관리](#add-users-and-admins)할 수 있습니다.
   - [제품 프로필 관리자](#add-users-developers-and-product-profile-admins) - 제품 프로필 관리자는 [!DNL Adobe Admin Console]의 제품에 대한 사용자를 관리할 수 있습니다.

## 제품 관리자 추가

1. [Admin Console](https://adminconsole.adobe.com)&#x200B;(으)로 이동하여 Adobe ID으로 로그인합니다.

1. 조직을 선택합니다.

1. [!UICONTROL **제품**] 탭의 [!UICONTROL **제품 및 서비스**]&#x200B;에서 [!UICONTROL **Adobe Commerce as a Cloud Service - 백엔드**] 제품을 선택합니다.

   ![제품 선택](../cloud-service/assets/backend.png){width="600" zoomable="yes"}

1. [!UICONTROL **관리자**] 탭을 선택합니다.

1. [!UICONTROL **관리자 추가**]&#x200B;를 클릭합니다.

1. 관리자로 추가할 사용자의 사용자 이름 또는 전자 메일 주소를 입력하고 [!UICONTROL **저장**]&#x200B;을 클릭합니다.

## 사용자, 개발자 및 제품 프로필 관리자 추가

>[!BEGINSHADEBOX &quot;필수 구성 요소&quot;]
>
>사용자 관리에 다음 프로비저닝이 필요합니다.

- [!DNL Adobe Commerce Optimizer]에 대해 IMS 조직이 프로비저닝됨
- 시스템 또는 제품 관리자 역할이 있는 동일한 IMS 조직의 Adobe Experience Cloud 계정

>[!ENDSHADEBOX]

다음 지침에 따라 사용자와 개발자를 [!DNL Commerce Cloud Manager]에 추가하여 Commerce 인스턴스를 관리합니다.

1. [Adobe Admin Console](https://adminconsole.adobe.com)&#x200B;(으)로 이동하여 Adobe ID으로 로그인합니다.

1. 조직을 선택합니다.

1. [!UICONTROL **제품**] 탭의 [!UICONTROL **제품 및 서비스**]&#x200B;에서 [!UICONTROL **Adobe Commerce as a Cloud Service - 백엔드**] 제품을 선택합니다.

   ![제품 선택](../cloud-service/assets/backend.png){width="600" zoomable="yes"}

1. [!UICONTROL **기본 - Cloud Manager**] 제품 프로필을 클릭합니다.

1. [!UICONTROL **사용자**], [!UICONTROL **개발자**] 또는 [!UICONTROL **관리자**] 탭을 선택하고 [!UICONTROL **사용자 추가**] 또는 [!UICONTROL **개발자 추가**] 또는 [!UICONTROL **관리자 추가**]&#x200B;를 클릭합니다.

   이 화면에서 추가된 관리자는 [제품 프로필 관리자](#understanding-roles) 그룹에 할당됩니다.

   ![탭 선택](../cloud-service/assets/tab-select.png){width=600 zoomable="yes"}

1. 관리자로 추가할 사용자의 사용자 이름 또는 전자 메일 주소를 입력하고 [!UICONTROL **저장**]&#x200B;을 클릭합니다.

## 대량 사용자 관리

다음 방법 중 하나를 사용하여 여러 사용자를 보다 효율적으로 추가할 수 있습니다.

- Adobe Admin Console의 **CSV로 사용자 추가** 기능을 사용하여 [일괄 CSV 업로드](https://helpx.adobe.com/kr/enterprise/using/bulk-upload-users.html){target="_blank"}를 수행합니다.
- [사용자 그룹](https://helpx.adobe.com/kr/enterprise/using/user-groups.html){target="_blank"}을(를) 만들어 역할에 여러 사용자를 추가하십시오. 그런 다음 [!UICONTROL **Adobe Commerce as a Cloud Service - 백엔드**] 제품을 사용자 그룹에 추가합니다.

