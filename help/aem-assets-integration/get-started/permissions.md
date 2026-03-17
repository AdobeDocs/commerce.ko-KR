---
title: AEM Assets 통합에 대한 IMS 사용자 권한 구성
description: IMS ID와 Admin Console 프로필을 통해 AEM Assets 게재 액세스, 에셋 선택기 및 자동 채워진 Commerce 구성 필드를 활성화하는 방법을 알아봅니다.
feature: CMS, Media, Configuration
source-git-commit: 0fd98bf86555c914f7a5b1e177c31c37764dbf84
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 0%

---

# 사용자 권한 및 IMS

**IMS**(Adobe Identity Management 시스템)이 인증 계층입니다. Adobe Commerce as a Cloud Service의 경우 IMS 인증은 기본적으로 관리자에서 활성화됩니다. Adobe Commerce on cloud 또는 온-프레미스의 경우 IMS는 선택 사항입니다.[Commerce에 대해 IMS를 사용하도록 설정](https://experienceleague.adobe.com/docs/commerce-admin/start/admin/ims/adobe-ims-config.html?lang=ko){target=_blank}에서는 향상된 구성 UI(자산 선택기, 자동으로 채워진 드롭다운)를 제공하지만, **프로그램 ID** 및 **환경 ID**&#x200B;를 수동으로 입력하여 IMS 없이 통합을 구성할 수 있습니다.

IMS를 사용할 때도 AEM Assets 통합에는 특정 **Adobe Admin Console 제품 프로필**&#x200B;이 필요합니다. Commerce 관리에서 통합을 구성하는 사용자는 **AEM Assets DM OpenAPI 사용자 - 게재** 제품 프로필 또는 **작성자** 제품 프로필이 대체 항목으로 필요합니다. 이는 사용자의 IMS 조직에서 Admin Console 제품 프로필을 통해 제어되며 다음을 활성화합니다.

* **자산 선택기**&#x200B;에서는 범주 이미지나 Page Builder 콘텐츠를 관리할 때 AEM Assets에서 이미지를 선택할 수 있습니다.
* Admin Console 제품 프로필(게재 또는 작성자)을 기반으로 사용자의 IMS 세션에서 값을 가져오는 **구성 필드 자동 채우기**(예: **프로그램 ID**, **환경 ID**, **도메인 매핑** 드롭다운).

올바른 권한이 없으면 에셋 선택기를 사용할 수 없으며, 이러한 필드는 비어 있거나 수동으로 입력해야 합니다.
>[!BEGINSHADEBOX]

**IMS와 권한이 함께 작동하는 방식**

Adobe IMS는 사용자 ID와 조직 컨텍스트를 제공하는 반면 Adobe Admin Console은 보유하고 있는 **제품 프로필**(권한)을 정의합니다. AEM Assets 통합은 IMS 세부 정보와 할당된 프로필을 사용하여 구성 필드를 자동으로 채우고 에셋 선택기를 활성화할 수 있는지 여부를 결정합니다.

>[!ENDSHADEBOX]

## 제품 프로필이 필요한 이유

통합은 프로필에 매핑된 도메인만 로드할 수 있습니다. 따라서 사용자는 다음 제품 프로필을 보유할 수 있습니다.

* **AEM 배달 제품 프로필**. 사용자에게 작성자 및 게재 프로필이 모두 있는 경우 에셋 선택기 및 구성 UI에 필요합니다. 가능한 경우 통합에서 AEM 게재 제품 프로필을 사용합니다.

* **작성자 제품 프로필**. AEM Assets UI에 액세스하는 데 필요합니다. 또한, 사용자에게 Admin Console에 AEM 게재 제품 프로필이 없는 경우 에셋 선택기 및 구성 UI에 대한 대체 역할을 합니다.

도메인(프로그램 ID, 환경 ID 및 도메인 매핑 포함)은 AEM 게재 제품 프로필에 할당됩니다. 통합은 사용 가능한 경우 **AEM 배달 제품 프로필**&#x200B;에서 도메인을 로드하거나, AEM 배달 제품 프로필이 사용자의 Admin Console에 없는 경우 **작성자 제품 프로필**(으)로 돌아갑니다. 다음과 같은 작업을 수행하려면 다음 프로필 중 하나가 필요합니다.

* Commerce 관리 구성에서 **프로그램 ID**, **환경 ID** 및 **도메인 매핑** 드롭다운을 채웁니다.
* 에셋 선택기를 사용하여 AEM Assets에서 에셋을 찾아보고 선택합니다.

두 프로필 모두 구성되지 않은 경우 사용자가 **프로그램 ID** 및 **환경 ID**&#x200B;를 수동으로 입력할 수 있지만 자산 선택기를 사용할 수 없습니다.

## 배포 유형별 권한 부여

>[!BEGINTABS]

>[!TAB Adobe Commerce as a Cloud Service]

[!BADGE SaaS만]{type=Positive tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."}

IMS 인증은 기본적으로 활성화되어 있습니다. 사용자에게 AEM Assets 배달 제품 프로필이 없는 경우 **Adobe Admin Console**&#x200B;의 [AEM Admin Console DM OpenAPI 사용자 - 배달](https://adminconsole.adobe.com/) 제품 프로필 또는 **작성자** 제품 프로필(예: `<environment-name> - author - <program-id> - <environment-id>`)에 사용자를 대체 항목으로 추가합니다.

>[!NOTE]
>
> Commerce 및 AEM Assets에도 사용자를 추가해야 합니다. 전체 설정에 대해서는 [사용자 및 Identity Management](https://experienceleague.adobe.com/ko/docs/commerce/cloud-service/user-management#add-a-user-to-aem-assets-or-product-visuals){target=_blank} 안내서에서 _AEM Assets 또는 제품 비주얼에 사용자 추가_&#x200B;를 참조하십시오.

![AEM Assets 게재용 Admin Console 제품 프로필](../assets/aem-assets-delivery-product-profile.png){width="600" zoomable="yes"}

>[!TAB 클라우드 또는 온-프레미스의 Adobe Commerce]

[!BADGE PaaS만]{type=Informative tooltip="Adobe Commerce on Cloud 프로젝트에만 적용됩니다(Adobe 관리 PaaS 인프라)."}

자산 선택기를 사용하려면 PaaS에 **IMS 클라이언트 ID**&#x200B;가 필요합니다. OpenAPI를 사용하여 Dynamic Media를 활성화할 때 IMS 클라이언트 ID를 가져오는 방법을 포함한 필수 구성 요소는 [AEM Assets 프로젝트 구성](configure-aem.md#prerequisites)을(를) 참조하십시오.

자산 선택기 및 자동 채워진 구성 필드(프로그램 ID, 환경 ID, 도메인 매핑)를 사용하려면 다음을 수행하십시오.

1. Commerce 관리자가 IMS 인증을 사용하고 사용자의 Admin Console 제품 프로필을 읽을 수 있도록 [Commerce에 대해 Adobe IMS를 사용](https://experienceleague.adobe.com/docs/commerce-admin/start/admin/ims/adobe-ims-config.html?lang=ko){target=_blank}합니다.

1. 자산 선택기에 대한 사용자 지정 IMS 클라이언트 ID를 요청하려면 [지원 티켓을 엽니다](https://experienceleague.adobe.com/ko/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#support-cases).

1. [Adobe Admin Console](https://adminconsole.adobe.com/)에서 사용자를 **AEM Assets DM OpenAPI 사용자 - 배달** 제품 프로필에 추가하거나 사용자에게 Admin Console에 AEM 배달 제품 프로필이 없는 경우 **작성자** 제품 프로필(예: `<environment-name> - author - <program-id> - <environment-id>`)에 대체 항목으로 추가합니다.

IMS가 없어도 Commerce 관리자에서 프로그램 ID와 환경 ID를 수동으로 입력하여 통합을 구성할 수 있습니다.

>[!ENDTABS]

## 관련 설명서

* [AEM Assets 통합에 대한 IMS 사용자 권한 구성](setup-synchronization.md) - Commerce을 AEM Assets에 연결하고 일치하는 규칙을 구성합니다.
* [수동 자산 선택](../synchronize/asset-selector-integration.md) - 범주 이미지 및 페이지 빌더에 자산 선택기를 사용합니다.
* [AEM Assets 또는 제품 비주얼에 사용자 추가](https://experienceleague.adobe.com/ko/docs/commerce/cloud-service/user-management#add-a-user-to-aem-assets-or-product-visuals){target=_blank} - ACCS의 경우 먼저 Commerce 및 AEM Cloud Manager(비즈니스 소유자, 배포 관리자)에 사용자를 추가하십시오. **AEM Assets DM OpenAPI 사용자 - 게재** 프로필(또는 **작성자** 프로필을 대체 프로필)은 자산 선택기와 자동 채우기 기능에 대한 추가 요구 사항입니다.
* [팀원을 AEM 배달 계층에 할당](https://experienceleague.adobe.com/ko/docs/experience-manager-cloud-service/content/onboarding/journey/assign-profiles-aem#add-team-members){target=_blank}. 게재 액세스를 위한 AEM 설명서.
