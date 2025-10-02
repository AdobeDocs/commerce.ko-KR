---
title: 사용자 관리
description: ' [!DNL Adobe Commerce as a Cloud Service]에서 사용자를 관리하는 방법을 알아봅니다.'
exl-id: 9bc80fe6-6dfd-4bb3-8dc5-d5efd8a8d90c
badgeSaas: label="SaaS만" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."
role: Admin
source-git-commit: 00d31ca7e4e81ecbc34373ce95b1256a7ae012db
workflow-type: tm+mt
source-wordcount: '1225'
ht-degree: 0%

---

# 사용자 관리

사용자가 [!DNL Adobe Commerce as a Cloud Service]에서 관리자에 액세스하려면 해당 사용자를 조직의 사용자로 추가하고 [Adobe Admin Console](https://adminconsole.adobe.com){target="_blank"}의 Cloud Service 제품에 액세스할 수 있는지 확인해야 합니다.

이 프로세스에는 [!DNL Adobe Commerce as a Cloud Service]에 액세스할 수 있는 IMS 조직이 필요합니다. 조직의 시스템 관리자 또는 제품 관리자만 이러한 프로세스를 수행할 수 있습니다.

>[!TIP]
>
>여러 사용자를 동시에 추가하려면 [일괄 CSV 업로드](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html){target="_blank"}를 수행할 수 있습니다.
> 
> [사용자 그룹](https://helpx.adobe.com/enterprise/using/user-groups.html){target="_blank"}을 만들어 역할에 여러 사용자를 추가할 수도 있습니다. 그런 다음 [!UICONTROL **Adobe Commerce - Commerce Cloud 관리자**] 제품을 사용자 그룹에 추가할 수 있습니다.

## 역할 이해

[!DNL Adobe Commerce as a Cloud Service]에 사용할 수 있는 역할은 다음과 같습니다. 이러한 역할을 보거나 편집하려면 Commerce 관리에서 **시스템** > **권한** > **사용자 역할**(으)로 이동합니다.

* **사용자** - 사용자는 Commerce 관리자에 대한 관리자 액세스 권한이 있지만 Admin Console에서 제품 수준 액세스를 관리할 수 없습니다. [에서 ](./getting-started.md#create-an-instance)인스턴스 만들기[!DNL Commerce Cloud Manager]에 크레딧을 사용할 수도 있습니다.

  >[!NOTE]
  >
  >개발자 및 관리자를 포함한 모든 Commerce 사용자에게도 사용자 역할이 할당되어야 합니다. 기본 Commerce 권한에 필요합니다.

* [**개발자**](https://helpx.adobe.com/enterprise/using/manage-developers.html#Adddevelopers){target="_blank"} 개발자는 사용자 권한이 있으며 Commerce 인스턴스에 개발자 사용자로 추가됩니다. 즉, [관리 UI SDK](https://developer.adobe.com/commerce/extensibility/admin-ui-sdk/){target="_blank"}, [이벤트 구성](https://developer.adobe.com/commerce/extensibility/events/){target="_blank"} 및 [웹후크 만들기](https://developer.adobe.com/commerce/extensibility/webhooks/){target="_blank"}를 사용할 수 있습니다.

* 관리자 - 세 가지 유형의 관리자가 있습니다.
   * [시스템 관리자](https://helpx.adobe.com/enterprise/using/admin-roles.html){target="_blank"} - 시스템 관리자는 Admin Console을 통해 조직의 모든 제품 및 제품 프로필에 액세스할 수 있습니다.
   * [제품 관리자](#add-a-product-admin) - 제품 관리자는 [에서 ](#add-users)제품에 대한 사용자, 역할 및 권한을 관리[!DNL Adobe Admin Console]하고 [Commerce 관리자의 사용자를 관리](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/user-accounts/permissions-users-all#create-a-user){target="_blank"}할 수 있습니다.
   * [제품 프로필 관리자](#add-developers-and-product-profile-admins) - 제품 프로필 관리자는 Adobe Commerce 관리자에 액세스할 수 없지만 [!DNL Adobe Admin Console]에서 제품에 대한 사용자를 관리할 수 있습니다.

Adobe Commerce 내의 각 역할에 부여된 권한에 대한 자세한 내용은 [사용자 권한](#user-permissions)을 참조하세요.

## 제품 관리자 추가

>[!NOTE]
>
>제품 관리자로 추가하기 전에 제품 관리자에게 [사용자 역할](#add-users)을 할당하십시오. 기본 Commerce 권한에 사용자 역할이 필요합니다.

1. https://adminconsole.adobe.com으로 이동한 다음 Adobe ID으로 로그인합니다.

1. 조직을 선택합니다.

1. [!UICONTROL **제품**] 탭의 [!UICONTROL **제품 및 서비스**]&#x200B;에서 [!UICONTROL **Adobe Commerce - Commerce Cloud 관리자**] 제품을 선택합니다.

   ![제품 선택](./assets/backend.png){width="600" zoomable="yes"}

1. [!UICONTROL **관리자**] 탭을 선택합니다.

1. [!UICONTROL **관리자 추가**]&#x200B;를 클릭합니다.

1. 관리자로 추가할 사용자의 사용자 이름 또는 전자 메일 주소를 입력하고 [!UICONTROL **저장**]&#x200B;을 클릭합니다.

## 사용자 추가

다음 지침은 [!DNL Commerce Cloud Manager] 및 Commerce 관리자에 사용자를 추가하는 방법에 대한 정보를 제공합니다. [!DNL Commerce Cloud Manager] 인터페이스를 사용하면 Commerce 인스턴스를 만들고 관리할 수 있습니다. 이 프로세스는 개발자 및 관리자를 포함한 모든 사용자에게 필요합니다.

>[!NOTE]
>
>제품 관리자와 시스템 관리자만 Adobe Commerce as a Cloud Service 제품에 사용자와 개발자를 추가할 수 있습니다.

1. https://adminconsole.adobe.com으로 이동한 다음 Adobe ID으로 로그인합니다.

1. 조직을 선택합니다.

1. [!UICONTROL **제품**] 탭의 [!UICONTROL **제품 및 서비스**]&#x200B;에서 [!UICONTROL **Adobe Commerce - Commerce Cloud 관리자**] 제품을 선택합니다.

   ![제품 선택](./assets/backend.png){width="600" zoomable="yes"}

1. [!UICONTROL **기본 - Cloud Manager**] 제품 프로필을 클릭합니다.

1. [!UICONTROL **사용자**] 탭을 선택하고 [!UICONTROL **사용자 추가**]&#x200B;를 클릭합니다.

   ![탭 선택](./assets/tab-select.png){width=600 zoomable="yes"}

1. 관리자로 추가할 사용자의 사용자 이름 또는 전자 메일 주소를 입력하고 [!UICONTROL **저장**]&#x200B;을 클릭합니다.

### 개발자 및 제품 프로필 관리자 추가

개발자 및 제품 프로필 관리자를 추가하려면 [사용자 추가](#add-users) 프로세스를 반복하되, [!UICONTROL **사용자**] 탭 대신 [!UICONTROL **개발자**] 또는 [!UICONTROL **관리자**] 탭을 선택하십시오.

>[!NOTE]
>
>제품 프로필 관리자는 Commerce 관리자에 액세스할 수 없습니다. 자세한 내용은 [역할 이해](#understanding-roles)를 참조하세요.
>
>개발자를 개발자로 추가하기 전에 개발자에게 사용자 역할을 할당하십시오. 기본 Commerce 권한에 사용자 역할이 필요합니다.

![탭 선택](./assets/tab-select.png){width=600 zoomable="yes"}

## 역할 리소스

다음 목록은 기본 역할이 Adobe Commerce 관리자 내에서 액세스할 수 있는 권한을 갖는 리소스를 설명합니다. 각 역할에 대한 기본 권한을 편집하려면 Commerce 관리자의 **시스템** > **권한** > **사용자 역할**(으)로 이동합니다.

**사용자**

* 카탈로그
   * 인벤토리
      * 제품
         * 제품 가격 읽기

**개발자**

* 카탈로그
   * 인벤토리
      * 제품
         * 제품 가격 읽기
* 시스템
   * 데이터 전송
      * 가져오기 기록
* Adobe IO 이벤트 구성
   * 구성 확인
   * 이벤트 공급자 만들기
   * 구성 업데이트
   * 이벤트 동기화
   * 이벤트 공급자 목록 가져오기
* 이벤트 프레임워크
   * 이벤트 목록
   * 이벤트 연결 테스트
   * 이벤트 구독
   * 이벤트 구독 취소
   * 이벤트 상태
   * 이벤트 구독을 가져오기 위한 API
   * 이벤트 구독 관리 UI 보기
   * 이벤트 구독 관리 UI 만들기
   * 새 이벤트 관리자 UI 요청
* 웹훅
   * Webhooks 디지털 서명
      * Webhooks 디지털 서명 설정
      * Webhooks 디지털 서명 생성 키
   * Webhooks 관리
      * Webhooks 그리드
      * 웹후크 편집
      * 웹후크 테스트
      * Webhook에 대한 API 구독
      * Webhook에서 API 구독 취소
      * Webhooks 목록
      * 새 Webhook 요청
      * 웹후크 로그
      * Webhooks 목록 가져오기

**관리자**

관리자는 모든 권한에 액세스할 수 있습니다.

## AEM Assets 또는 제품 비주얼에 사용자 추가

[!DNL Adobe Experience Manager Assets] 및 [!DNL Product Visuals powered by AEM Assets] 사용자에게는 다음 설정이 필요합니다.

계정에 [Adobe Experience Manager as a Cloud Service](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service)에 대한 액세스 권한이 있고 사용자가 [과(와) 함께 ](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/overview){target="_blank"}AEM Assets[!DNL Adobe Commerce as a Cloud Service]의 고급 기능에 액세스할 수 있도록 허용하려면 다음 프로세스를 사용하십시오.

>[!NOTE]
>
>적절한 자산 권한이 없는 사용자는 [!DNL AEM Assets]AI 이미지 생성[, ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/generative-ai/generative-ai-in-aem){target="_blank"}생성된 변형[ 등과 같은 ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/generative-ai/generate-variations-integrated-editor){target="_blank"}의 고급 기능에 액세스할 수 없습니다.

>[!TIP]
>
>여러 사용자를 동시에 추가하려면 [일괄 CSV 업로드](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html){target="_blank"}를 수행할 수 있습니다.
>
>[사용자 그룹](https://helpx.adobe.com/enterprise/using/user-groups.html){target="_blank"}을 만들어 역할에 여러 사용자를 추가할 수도 있습니다. [!UICONTROL **Adobe Experience Manager as a Cloud Service - Cloud Manager**] 제품을 사용자 그룹에 추가할 수 있습니다.

1. https://adminconsole.adobe.com으로 이동한 다음 Adobe ID으로 로그인합니다.

1. 조직을 선택합니다.

1. [!UICONTROL **제품**] 탭의 [!UICONTROL **제품 및 서비스**]&#x200B;에서 [!UICONTROL **Adobe Experience Manager as a Cloud Service - Cloud Manager**] 제품을 선택합니다.

   ![제품 선택](./assets/backend-aem.png){width="600" zoomable="yes"}

1. [!UICONTROL **사용자**] 탭을 선택합니다.

1. [!UICONTROL **사용자 추가**]&#x200B;를 클릭합니다.

1. 추가하려는 사용자의 사용자 이름 또는 이메일 주소를 입력합니다.

1. [!UICONTROL **제품 추가**]&#x200B;를 클릭합니다.

1. AEM Assets을 Commerce과 통합하는 데 필요한 다음 제품 프로필을 선택하십시오.

   * 비즈니스 소유자 - 프로그램을 만들고 관리하는 데 필요합니다.
   * 배포 관리자 - 저장소에서 AEM으로 코드를 배포하는 데 필요합니다.

   Cloud Manager 또는 Experience Manager 인터페이스에 액세스할 필요가 없는 개발자를 추가하는 경우 대신 개발자 역할을 할당할 수 있습니다.

   >[!NOTE]
   >
   >이러한 권한이 AEM Assets에 대한 액세스에 미치는 영향에 대한 자세한 내용은 [Cloud Manager 제품 프로필](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/concepts/aem-cs-team-product-profiles#cloud-manager-product-profiles){target="_blank"}을 참조하세요.

1. [!UICONTROL **적용**]&#x200B;을 클릭합니다.

1. [!UICONTROL **저장**]&#x200B;을 클릭합니다.

사용자에게 액세스 권한이 있는지 확인하려면 사용자 이름을 클릭하여 해당 프로필 페이지를 엽니다. [!UICONTROL **제품**] 섹션에는 [!UICONTROL **Adobe Experience Manager as a Cloud Service - Cloud Manager**] 제품 아래에 [!UICONTROL **완료**]&#x200B;이 표시됩니다. 사용자를 추가한 후 프로필에서 업데이트된 상태를 보는 데 몇 초 정도 걸릴 수 있습니다. 업데이트된 상태를 보려면 페이지를 새로 고침하십시오.

![제품 액세스](./assets/product-access.png){width="600" zoomable="yes"}

## Experience Manager 인터페이스 액세스

사용자를 AEM Assets에 추가한 후 [!DNL Experience Manager]https://experience.adobe.com/[(으)로 이동하여 ](https://experience.adobe.com/){target="_blank"} 인터페이스에 액세스할 수 있습니다.

1. [!UICONTROL **빠른 액세스**] 섹션에서 [!UICONTROL **Experience Manager**]&#x200B;을 클릭하거나 [!UICONTROL **Experience Manager**]&#x200B;이 표시되지 않는 경우 [!UICONTROL **모두 보기**]&#x200B;를 클릭하십시오. 그런 다음 [!UICONTROL **Cloud Manager**]&#x200B;을 클릭하거나 직접 [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}(으)로 이동합니다.

1. [!UICONTROL **Cloud Manager**] 페이지에서 [!UICONTROL **프로그램 추가**]&#x200B;를 클릭하여 시작합니다.

1. [새 프로그램을 만듭니다](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/create-program){target="_blank"}.

1. [새 환경을 만듭니다](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/screens-as-cloud-service/onboarding-screens-cloud/creating-an-environment){target="_blank"}.

1. 환경을 만든 후 [Admin Console](https://adminconsole.adobe.com){target="_blank"}(으)로 돌아가서 [!UICONTROL **Adobe Experience Manager as a Cloud Service**]&#x200B;을(를) 선택하십시오.

1. 이제 새 제품 프로필이 표시됩니다. `- author -`이(가) 포함된 항목을 선택하십시오. 예: `<environment-name> - author - <program-id> - <environment-id>`.

1. [제품 프로필에 사용자 추가](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-manager/content/requirements/users-and-roles){target="_blank"}.

* [Commerce 메타데이터를 지원하도록 AEM Assets 구성](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/get-started/configure-aem)
* [자산 동기화를 위해 AEM Assets과 Commerce 통합](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/get-started/setup-synchronization)
