---
title: AEM Assets 프로젝트 구성
description: assets-commerce 패키지를 배포하고 Adobe Commerce 프로젝트에서 Commerce 메타데이터를 구성하여 AEM과 AEM Assets 간에 자산을 동기화하는 방법에 대해 알아봅니다.
feature: CMS, Media, Integration
exl-id: a5d2cbab-5ea1-446b-8ab2-2c638128a40c
TQID: https://experienceleague.adobe.com/QPlM-eeRjJ0gwmpGO4SSYR4PLtL97O-NeozWorDWtv0
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: da3860b0-d637-47df-bef0-273751180266
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 0c2e50338cbf286704239b6d1f628180e85a3bef
workflow-type: tm+mt
source-wordcount: 1741
ht-degree: 1%

---

# AEM Assets 프로젝트 구성

이 항목에서는 AEM 제작 환경에서 Commerce 네임스페이스, 메타데이터 스키마 및 [!UICONTROL Commerce] 탭을 사용할 수 있도록 AEM Assets 프로젝트를 구성하는 방법에 대해 설명합니다. 이러한 리소스에 대한 배경은 [AEM Assets의 Commerce 메타데이터](../metadata.md)를 참조하십시오.

AEM Assets 프로젝트를 구성하는 두 가지 옵션이 있습니다.

* [!BADGE 권장]{type=Positive} **셀프 서비스 온보딩** — AEM 릴리스 `2026.5.26309` 이상에서 환경 변수를 설정하고 OpenAPI 기능을 사용하는 Dynamic Media를 활성화하여 Cloud Manager에서 통합을 사용하도록 설정하십시오. 사용자 지정 코드 배포가 필요하지 않습니다. [Commerce 통합 사용(셀프 서비스)](#enable-aem-commerce-self-service)을 참조하세요.

* **수동 구성** — Cloud Manager 파이프라인을 통해 `assets-commerce` 패키지를 배포합니다. 사용자 지정 패키지 코드를 배포해야 하는 경우 또는 `2026.5.26309` 이전 버전의 AEM 릴리스에 있는 경우 이러한 수동 단계를 사용합니다. [자산 상거래 패키지 수동으로 설치](#install-the-assets-commerce-package-manually)를 참조하십시오.

>[!TIP]
>
>오른쪽 상단 메뉴에서 현재 AEM 버전을 확인할 수 있습니다. **[!UICONTROL Help]** > **[!UICONTROL About AEM]**.

## Commerce 통합 활성화(셀프서비스) {#enable-aem-commerce-self-service}

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} AEM 릴리스 `2026.5.26309` 이상

지원되는 AEM 릴리스에서는 사용자 지정 코드를 배포하지 않고 Cloud Manager에서 Commerce 통합을 활성화합니다. Author 서비스에서 통합을 사용하도록 설정하면 Commerce 네임스페이스, 메타데이터 스키마 및 **[!UICONTROL Commerce]** 탭이 자동으로 제공됩니다.

### 셀프서비스 사전 요구 사항

* 프로그램 및 배포 관리자 역할을 사용하여 [AEM Cloud Manager 프로그램 및 환경에 액세스](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager#access-sysadmin-bo).

* 릴리스 `2026.5.26309` 이상의 AEM 프로그램.

* Commerce 인스턴스의 **IMS 조직 ID**.

  Commerce 인스턴스와 AEM Assets 작성 환경은 모두 동일한 IMS 조직에 있어야 합니다.

### 1단계: 프로그램 및 환경 만들기

Cloud Manager에서 프로그램을 만드는 것은 단일 마법사 프로세스입니다. 프로그램과 해당 환경은 여러 단계에 걸쳐 구성되며 마지막에 함께 저장됩니다.

1. Cloud Manager에서 **[!UICONTROL Add Program]**&#x200B;을(를) 선택합니다.

1. **[!UICONTROL Set up for production]**&#x200B;을(를) 선택하고 프로그램 이름을 입력한 다음 **[!UICONTROL Continue]**&#x200B;을(를) 선택합니다.

1. **[!UICONTROL Solutions & Add-ons]** 단계에서 **[!UICONTROL Dynamic Media]**&#x200B;을(를) 포함하여 프로젝트에 필요한 솔루션 및 추가 기능을 선택한 다음 **[!UICONTROL Continue]**&#x200B;을(를) 선택합니다.

   ![Cloud Manager 솔루션 및 추가 기능 단계(Dynamic Media 선택)](../assets/aem-cloud-manager-program-addons.png){width="600" zoomable="yes"}

1. **[!UICONTROL Add Environment]** 단계에서 **프로덕션** 및 **스테이징** 환경의 이름을 입력한 다음 지역을 선택하십시오.

   ![프로덕션 및 스테이징 세부 정보가 포함된 Cloud Manager 환경 추가 대화 상자](../assets/aem-cloud-manager-add-environment.png){width="600" zoomable="yes"}

1. 환경을 사용하여 프로그램을 만들려면 **[!UICONTROL Save]**&#x200B;을(를) 선택하십시오.

### 2단계: Commerce 통합 변수 활성화

Cloud Manager에서 1단계에서 생성한 환경을 연 다음 다음을 수행합니다.

1. **[!UICONTROL Configuration]** 탭을 선택합니다.

1. 다음 값이 있는 환경 변수를 추가한 다음 **[!UICONTROL Add]** 및 **[!UICONTROL Save]**&#x200B;을(를) 선택합니다.

   | 필드 | 값 |
   |---|---|
   | 이름 | `COMMERCE_INTEGRATION_ENABLED` |
   | 값 | `true` |
   | 서비스 적용됨 | 작성자 |
   | 유형 | 변수 |

   작성자 서비스에 COMMERCE_INTEGRATION_ENABLED 변수가 적용된 ![Cloud Manager 환경 구성](../assets/aem-cloud-manager-commerce-integration-variable.png){width="600" zoomable="yes"}

   환경이 업데이트되어 구성이 적용됩니다. 환경 상태가 **[!UICONTROL Running]**(으)로 돌아올 때까지 기다리십시오.

### 3단계: OpenAPI 기능을 사용하여 Dynamic Media 활성화

1. 환경 **[!UICONTROL General]** 탭에서 **[!UICONTROL Dynamic Media]**&#x200B;을(를) 찾습니다.

1. *OpenAPI 기능을 사용할 수 있습니다* 옆에 있는 **[!UICONTROL Click to activate]**&#x200B;을(를) 선택하십시오.

   ![Dynamic Media OpenAPI 활성화 링크를 표시하는 환경 일반 탭](../assets/aem-cloud-manager-dynamic-media-activate.png){width="600" zoomable="yes"}

   활성화는 백그라운드에서 실행됩니다. 완료되면 환경은 Commerce 통합을 위해 준비됩니다.

   >[!NOTE]
   >
   > **[!UICONTROL Click to activate]**&#x200B;을(를) 사용할 수 없는 경우 지원 티켓을 열어 OpenAPI 기능을 사용하는 Dynamic Media를 활성화하십시오.

### 4단계: 구성 유효성 검사

**AEM Assets 작성자 환경**(으)로 전환하고 자산을 엽니다. 속성을 편집하고 기본 메타데이터 스키마에 **[!UICONTROL Commerce]** 탭이 포함되어 있으며 **[!UICONTROL Product Data]** 및 **[!UICONTROL Eligible for Commerce]** 필드가 표시되는지 확인합니다.

## assets-commerce 패키지를 수동으로 설치

>[!NOTE]
>
> 사용자 지정 패키지 코드를 배포하거나 `2026.5.26309` 이전 AEM 릴리스에 있는 경우 이 수동 방법을 사용하십시오. 지원되는 릴리스에서 대신 [Commerce 통합 사용(셀프 서비스)](#enable-aem-commerce-self-service)을 사용하십시오.

### 사전 요구 사항

`assets-commerce` 패키지 코드를 AEM Assets as a Cloud Service AEM 환경에 배포하려면 다음 리소스와 권한이 필요합니다.

* 프로그램 및 배포 관리자 역할을 사용하여 [AEM Assets Cloud Manager 프로그램 및 환경에 액세스](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager#access-sysadmin-bo).

* [로컬 AEM 개발 환경](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview) 및 AEM 로컬 개발 프로세스에 익숙합니다.

* [AEM 프로젝트 구조](https://experienceleague.adobe.com/ko/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure) 및 Cloud Manager을 사용하여 사용자 지정 콘텐츠 패키지를 배포하는 방법을 이해합니다.

* Commerce 인스턴스의 **IMS 조직 ID**. Commerce 인스턴스와 AEM Assets 작성 환경은 모두 동일한 IMS 조직에 있어야 합니다.

* OpenAPI 기능을 사용하여 [Dynamic Media를 활성화하려면](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/dynamic-media-open-apis-overview#enable-dynamic-media-open-apis):

>[!BEGINTABS]

>[!TAB 제품 시각화]

OpenAPI 기능이 있는 [!BADGE SaaS 전용]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."} Dynamic Media는 AEM Assets에서 제공하는 제품 비주얼에 대해 셀프서비스입니다.

1. Cloud Manager으로 이동합니다.

1. 원하는 환경을 선택합니다.

1. OpenAPI 기능을 사용하여 **Dynamic Media를 활성화**&#x200B;합니다.

   **OpenAPI 기능이 있는 Dynamic Media** 단추가 활성화되지 않은 경우 지원 티켓을 엽니다.

>[!TAB AEM Assets]

AEM as a Cloud Service에서 [!BADGE PaaS 전용]{type=Informative tooltip="Adobe Commerce on Cloud 프로젝트에만 적용됩니다(Adobe 관리 PaaS 인프라)."}, 다음 정보가 포함된 Adobe 지원 티켓을 제출하십시오.

* 제목: Dynamic Media OpenAPI를 활성화하여 Adobe Commerce을 AEM Assets과 완전히 통합

   * 지원 티켓 컨텐츠:

      * **[!UICONTROL AEM Program ID]**
      * **[!UICONTROL Adobe Commerce URL]**
      * **[!UICONTROL AEM Environment ID]**
      * **[!UICONTROL IMS Org ID]**

지원 티켓을 제출하면 Adobe이 Cloud Services 환경에서 OpenAPI 기능을 갖춘 Dynamic Media를 활성화하고 IMS 클라이언트 ID 등의 세부 정보를 공유하여 통합을 계속할 수 있습니다.

>[!ENDTABS]

### 설치 단계

1. AEM Cloud Manager으로 이동하여 프로그램을 선택한 다음 Adobe Commerce과 통합할 [프로덕션 및 스테이징 환경 만들기](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/create-environments#creating-environments)를 선택합니다.

1. 선택한 프로그램에 대해 [Adobe 관리 git 저장소를 복제](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/administering/site-creation/quick-site/retrieve-access#repo-access)합니다.

   ![Cloud Manager 저장소 자격 증명 및 복제 명령](../assets/cloud-manager-repository-info.png){width="600" zoomable="yes"}

   Cloud Manager **파이프라인**&#x200B;에서 **[!UICONTROL Access Repo Info]**&#x200B;을(를) 선택하여 **[!UICONTROL Repository Info]**&#x200B;을(를) 엽니다. **[!UICONTROL URL]** 또는 **[!UICONTROL Git command line]** 값을 복사하고 필요한 경우 액세스 암호를 생성한 다음 Git 클라이언트로 로컬로 복제합니다.

1. GitHub에서 [AEM Assets Commerce 저장소](https://github.com/ankumalh/assets-commerce)에서 패키지 코드를 다운로드합니다.

1. [로컬 AEM 개발 환경](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview)에서 다운로드한 코드를 기존 Adobe 관리 저장소에 수동으로 복사하십시오.

1. 프로젝트의 모든 `filter.xml` 및 `pom.xml` 파일에서 모든 &lt;my-app>을 사용자의 앱 이름으로 바꾸십시오.

   >[!NOTE]
   >
   > 또는 사용자 지정 코드를 AEM Assets 프로젝트 구성에 **Maven** 패키지로 설치할 수 있습니다.

1. 변경 사항을 커밋하고 로컬 개발 분기를 Cloud Manager Git 저장소로 푸시합니다.

1. [배포 파이프라인](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/administering/site-creation/quick-site/pipeline-setup#create-front-end-pipeline)을 구성하거나 파이프라인이 선택한 환경에 변경 내용을 배포할 수 있는지 확인하십시오.

   ![Cloud Manager 파이프라인](../assets/cloud-manager-pipelines.png){width="600" zoomable="yes"}

   파이프라인이 있으면 작업 메뉴(**...**)를 엽니다. **[!UICONTROL Run]**, **[!UICONTROL Edit]**, **[!UICONTROL View/Edit variables]** 또는 기타 작업까지—위에 연결된 Cloud Manager 파이프라인 설명서를 참조하십시오.

1. AEM Cloud Manager에서 [파이프라인을 사용하여 코드를 배포하여 AEM 환경을 업데이트](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code#deploying-code-with-cloud-manager)합니다.

1. 변경 내용을 확인하려면 임의의 자산으로 이동하여 해당 속성을 편집하십시오.

   * 기본 메타데이터 스키마에는 **Commerce** 탭이 포함되어 있습니다.

   * 제품 SKU 및 `Eligible for Commerce` 필드가 표시됩니다.

### Commerce 탭이 속성에 표시되지 않음

**Commerce** 탭이 속성에 나타나지 않으면 메타데이터 스키마 편집기에서 다음 단계를 수동으로 완료해야 합니다.

1. 메타데이터 스키마 편집기로 이동합니다.

1. 기본 메타데이터 스키마 양식을 수정하려면 **편집**&#x200B;을 선택하십시오.

1. **Commerce** 탭을 만들고 선택합니다.

1. **Product** 구성 요소를 **Commerce** 탭으로 끌어다 놓고 속성 `commerce:skus`에 매핑합니다.

1. **역할 표시** 및 **순서 표시**&#x200B;에 대한 확인란을 선택하십시오.

1. **checkbox** 구성 요소를 **Commerce** 탭으로 끌어다 놓고 속성 `commerce:isCommerce`에 매핑합니다. 옵션으로 **예** 및 **아니요**&#x200B;를 정의합니다.

다른 문제가 발생하면 [지원 티켓](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket)을 만들거나 AEM Assets 통합 영업 담당자에게 도움을 요청하십시오.

## 메타데이터 프로필 구성(선택 사항)

AEM Assets 작성 환경에서 메타데이터 프로필을 만들어 Commerce 에셋 메타데이터에 대한 기본값을 설정합니다. 이러한 기본값을 자동으로 사용하려면 새 프로필을 AEM 자산 폴더에 적용하십시오. 이 구성은 수동 단계를 줄여 자산 처리를 간소화합니다.

메타데이터 프로필을 구성할 때는 다음 구성 요소만 구성해야 합니다.

* Commerce 탭을 추가합니다. 이 탭에서는 템플릿에서 추가한 Commerce 특정 구성 설정을 사용할 수 있습니다.

* Commerce 탭에 `Eligible for Commerce` 필드를 추가합니다.

제품 데이터 UI 구성 요소는 템플릿을 기반으로 자동으로 추가됩니다.

### 메타데이터 프로필 정의

1. Adobe Experience Manager 작성자 환경에 로그인합니다.

1. Adobe Experience Manager 작업 영역에서 Adobe Experience Manager 아이콘을 클릭하여 AEM Assets용 작성자 컨텐츠 관리 작업 영역으로 이동합니다.

   ![AEM Assets 작성](../assets/aem-assets-authoring.png){width="600" zoomable="yes"}

1. 망치 아이콘을 선택하여 관리자 도구를 엽니다.

   ![AEM 작성자 관리자 관리 메타데이터 프로필](../assets/aem-manage-metadata-profiles.png){width="600" zoomable="yes"}

1. **[!UICONTROL Metadata Profiles]**&#x200B;을(를) 클릭하여 프로필 구성 페이지를 엽니다.

1. Commerce 통합을 위한 메타데이터 프로필을 **[!UICONTROL Create]**&#x200B;합니다.

   ![AEM 작성자 관리자 메타데이터 프로필 추가](../assets/aem-create-metadata-profile.png){width="600" zoomable="yes"}

1. Commerce 메타데이터에 대한 탭을 추가합니다.

   1. 왼쪽에서 **[!UICONTROL Settings]**&#x200B;을(를) 클릭합니다.

   1. 탭 섹션에서 **[!UICONTROL +]**&#x200B;을(를) 클릭한 다음 **[!UICONTROL Tab Name]**, `Commerce`을(를) 지정합니다.

1. 양식에 `Eligible for Commerce` 필드를 추가합니다.

   ![AEM 작성자 관리자가 프로필에 메타데이터 필드 추가](../assets/aem-edit-metadata-profile-fields.png){width="600" zoomable="yes"}

   * **[!UICONTROL Build form]**&#x200B;을(를) 클릭합니다.

   * `Single Line text` 필드를 양식으로 끕니다.

   * **[!UICONTROL Field Label]**&#x200B;을(를) 클릭하여 레이블에 대한 `Eligible for Commerce` 텍스트를 추가합니다.

   * 설정 탭에서 레이블 텍스트를 **필드 레이블**&#x200B;에 추가합니다.

   * 자리 표시자 텍스트를 `yes`(으)로 설정하십시오.

   * **[!UICONTROL Map to Property]** 필드에서 다음 값을 복사하여 붙여 넣습니다.

     ```terminal
     ./jcr:content/metadata/commerce:isCommerce
     ```

1. 선택 사항입니다. 승인된 Commerce 자산이 AEM Assets 환경에 업로드될 때 자동으로 동기화하려면 `Basic` 탭의 _[!UICONTROL Review Status]_&#x200B;필드에 대한 기본값을 `approved`(으)로 설정합니다.

1. 업데이트를 저장합니다.

### Commerce 에셋 소스 폴더에 메타데이터 프로필 적용

1. **[!UICONTROL Metadata Profiles]** 페이지에서 Commerce 통합 프로필을 선택합니다.

1. 작업 메뉴에서 **[!UICONTROL Apply Metadata Profiles to Folders]**&#x200B;을(를) 선택합니다.

1. Commerce 자산이 포함된 폴더를 선택합니다.

   Commerce 폴더가 없는 경우 만듭니다.

1. **[!UICONTROL Apply]**&#x200B;을(를) 선택합니다.

## 다음 단계

* [!BADGE Paa만]{type=Informative tooltip="Adobe Commerce on Cloud 프로젝트에만 적용됩니다(Adobe 관리 PaaS 인프라)."} [Adobe Commerce 패키지 설치](configure-commerce.md).

* [!BADGE SaaS만 해당]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."} [관리자로부터 통합 구성](setup-synchronization.md).
