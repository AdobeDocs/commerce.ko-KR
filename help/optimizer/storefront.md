---
title: 상점 설정
description: ' [!DNL Adobe Commerce Optimizer] Storefront를 설정하는 방법에 대해 알아봅니다.'
role: Developer
badgeSaas: label="SaaS만" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."
source-git-commit: 3131cc27a25d1bf958071b973f1d4bf1a68be152
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 0%

---

# 상점 설정

이 튜토리얼에서는 [!DNL Adobe Commerce Optimizer] 인스턴스의 데이터를 사용하는 강력하고, 확장 가능하며, 안전한 Adobe Commerce 상점 만들기를 위해 Edge Delivery Services에서 제공하는 [Commerce 상점](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/)을(를) 설정하고 사용하는 방법을 보여 줍니다.


## 사전 요구 사항

- 저장소를 만들 수 있고 로컬 개발용으로 구성된 GitHub 계정(github.com)이 있는지 확인합니다.

- Adobe Commerce Storefront 설명서의 [개요](https://experienceleague.adobe.com/developer/commerce/storefront/get-started)를 검토하여 Adobe Edge Delivery Services에서 Commerce Storefront를 개발하는 개념과 워크플로에 대해 알아봅니다.
- 개발 환경 설정


### 개발 환경 설정

Edge Delivery Services에서 [!DNL Adobe Commerce Optimizer] 상점을 개발하고 테스트하는 데 필요한 Node.js 및 Sidekick 브라우저 확장 기능을 설치하십시오.

#### Node.js 설치

NVM(Node Version Manager) 및 필요한 Node.js 버전(22.13.1 LTS)을 설치합니다.

1. NVM(노드 버전 관리자)을 설치합니다.

   ```bash
   curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
   ```

1. Node.js 및 NPM을 설치합니다. 자세한 내용은 [Node.js](https://nodejs.org/en/)를 참조하십시오.

   ```bash
   nvm install 22
   ```

   ```bash
   npm install -g npm
   ```

1. 설치를 확인합니다.

   ```bash
   npm -v
   ```

>[!TIP]
>
>[!DNL Adobe Commerce Optimizer] 솔루션 확장 및 사용자 정의를 위한 추가 리소스는 [App Builder for Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder) 및 [API Mesh for Adobe Developer App Builder](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/api-mesh/getting-started-api-mesh)를 통해 사용할 수 있습니다. 액세스 및 사용 정보는 Adobe 계정 담당자에게 문의하십시오.

#### Sidekick 설치

Sidekick 브라우저 확장 프로그램을 설치하여 콘텐츠를 편집하고 미리 보고 상점 앞에 게시할 수 있습니다. [Sidekick 설치 지침](https://www.aem.live/docs/sidekick#installation)을 참조하세요.

## 상점 만들기

[!DNL Adobe Commerce Optimizer] 프로젝트에 대해 만든 Storefront는 Edge Delivery Services Storefront 보일러플레이트에 사용자 지정된 버전의 Adobe Commerce을 사용합니다. 보일러판은 상점 개발의 시작점을 제공하는 파일 및 폴더 집합입니다. 이 설정 프로세스는 [Edge Delivery Services Storefront의 Adobe Commerce](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/)에 대한 표준 설정 프로세스와 다릅니다.

>[!NOTE]
>
>이 자습서에서는 macOS, Chrome 및 Visual Studio 코드를 개발 환경으로 사용합니다. 화면이 캡처되고 해당 설정이 지침에 반영됩니다. 다른 운영 체제, 브라우저 및 코드 편집기를 사용할 수 있지만 표시되는 UI와 수행하는 단계가 그에 따라 달라집니다.

### 워크플로우 개요

[!DNL Adobe Commerce Optimizer]에서 사용할 상점 전면을 설정하려면 다음 단계를 따르십시오.

1. **[코드 리포지토리 만들기](#step-1-create-site-code-repository)**-Adobe Commerce + Edge Delivery Services boilerplate 템플릿에서 GitHub 리포지토리를 만듭니다. 소스 저장소의 모든 분기를 포함합니다.
1. **[Storefront Boilerplate 업데이트](#step-2-update-the-storefront-boilerplate)** - `aco` 분기에서 사용자 지정 Boilerplate 템플릿을 업데이트하여 콘텐츠 폴더를 Storefront에 연결합니다.
1. **[변경 내용 배포](#step-3-deploy-changes)**-`main` 분기의 코드를 `aco` 분기의 업데이트된 코드로 덮어씁니다.
1. **[CodeSync 앱을 추가](#step-5-add-the-aem-code-sync-app)**-저장소를 Edge Delivery 서비스에 연결합니다. 소스 코드 사용자 지정을 완료하고 코드를 `main` 분기에 푸시할 때까지 코드 동기화 앱을 연결하지 마십시오.
1. **[콘텐츠 추가](#step-6-add-content)**-데모 콘텐츠 복제 도구를 사용하여 `https://da.live`에 호스팅된 문서 작성 환경에서 상점 콘텐츠를 만들고 초기화합니다.
1. **[데모 사이트 미리 보기](#step-7-preview-demo-site)**-상점 사이트에 연결하여 [!DNL Adobe Commerce Optimizer] 데모 인스턴스에서 샘플 콘텐츠 및 데이터를 확인합니다.
1. **[로컬 환경에서 개발](#step-8-develop-in-your-local-environment)**-필요한 종속성을 설치합니다. 로컬 개발 서버를 시작하고 Adobe에서 제공한 [!DNL Adobe Commerce Optimizer] 인스턴스에 연결하도록 Storefront 구성을 업데이트합니다.
1. **[다음 단계](#next-steps)**-상점에서의 콘텐츠 및 데이터 관리 및 표시에 대해 자세히 알아봅니다.


### 1단계: 사이트 코드 저장소 만들기

Edge Delivery Services + Adobe Commerce Boilerplate 템플릿을 사용하여 상점용 사이트 보일러플레이트 코드에 대한 GitHub 리포지토리를 만듭니다.

1. GitHub 계정에 로그인합니다.

1. [aem-boilerplate-commerce](https://github.com/hlxsites/aem-boilerplate-commerce) GitHub 저장소로 이동합니다.

1. **이 템플릿 사용**&#x200B;을 선택한 다음 드롭다운 메뉴에서 **새 저장소 만들기**&#x200B;를 선택합니다.

   ![[!DNL Create github repo from storefront boilerplate template]](./assets/storefront-create-github-repo.png){width="700" zoomable="yes"}

   저장소 구성 페이지가 표시됩니다.

   ![[!DNL Configure github repo to pull all branches from boilerplate repo]](./assets/storefront-configure-github-repo.png){width="700" zoomable="yes"}

1. 다음 세부 정보를 사용하여 구성 양식을 작성합니다.

   - **저장소 템플릿**—`hlxsites/aem-boilerplate-commerce`(기본값).
   - **모든 분기 포함**—모든 분기를 포함하는 옵션을 선택합니다.
   - **소유자**—조직 또는 계정입니다(필수).
   - **저장소 이름**—새 저장소의 고유한 이름입니다(필수).
   - **설명**—저장소에 대한 간략한 설명입니다(선택 사항).
   - **공개 또는 비공개**—Adobe에서는 공개(기본값)를 권장합니다.

1. **저장소 만들기**&#x200B;를 선택합니다.

   몇 분 후에 새 저장소가 열립니다.

   GitHub 사용자 인터페이스에 표시되는 가져오기 요청 알림을 무시합니다.

### 2단계: 상점 보일러판 업데이트

Storefront 보일러플레이트 코드를 업데이트하려면 다음 정보가 필요합니다.

- **2단계의 GitHub 저장소 URL**— `github.com/{ORG}/{SITE}`
   - `{ORG}`은(는) 저장소의 조직 이름 또는 사용자 이름입니다.
   - `{SITE}`은(는) 내 저장소 이름입니다.
- **1단계의 콘텐츠 폴더 URL**— `https://drive.google.com/drive/folders/{YOUR_FOLDER_ID}`
   - `{YOUR_FOLDER_ID}`은(는) 샘플 콘텐츠 데이터로 만든 폴더의 ID입니다.

#### 저장소를 문서 작성 환경에 연결합니다.

1. 로컬 컴퓨터에 저장소를 복제합니다.

   ```bash
   git clone https://github.com/{ORG}/{SITE}.git
   ```

   저장소를 복제할 때 오류가 발생하면 GitHub 설명서의 [복제 오류 문제 해결](https://docs.github.com/en/repositories/creating-and-managing-repositories/troubleshooting-cloning-errors)을 참조하십시오.

1. 터미널 또는 IDE에서 저장소를 엽니다.

1. `aco` 분기 체크 아웃

   ```bash
   git checkout aco
   ```

1. `default-fstab.yaml` 파일을 `fstab.yaml`에 복사하여 구성 파일을 만듭니다.

   ```bash
   cp default-fstab.yaml fstab.yaml
   ```

1. storefront 구성 파일에서 마운트 지점을 업데이트하여 콘텐츠 URL을 가리킵니다.

   1. [fstab.yaml](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/#vocabulary) 구성 파일을 엽니다.

      ```yaml
      mountpoints:
        /:
          url: https://content.da.live/{org}/{site}/
          type: markup
      
      folders:
       /products/: /products/default
      ```

   1. `{ORG}` 및 `{SITE}` 문자열을 상용구 코드용으로 만든 GitHub 저장소의 값으로 바꿉니다.

      예를 들어 업데이트된 코드는 다음과 같아야 합니다.

      ```yaml
      mountpoints:
        /:
          url: https://content.da.live/owner-name/aco-storefront/
          type: markup
      ```

   1. 파일을 저장합니다.

#### Sidekick 확장 구성

1. Sidekick 확장에 대한 프로젝트 구성을 추가합니다. 이 구성을 통해 Sidekick에서 Storefront 프로젝트의 콘텐츠를 관리할 수 있습니다.

>[!NOTE]
>
>브라우저에 [Sidekick 확장](https://www.aem.live/docs/sidekick#installation)을 설치했는지 확인하십시오.

1. `tools/sidekick/config.json` 파일을 엽니다.

   +++Sidekick 구성 파일

   ```json
   {
     "project": "Boilerplate",
     "plugins": [
       {
         "id": "cif",
         "title": "Commerce",
         "environments": [
           "edit"
         ],
         "url": "https://main--{SITE}--{ORG}.aem.live/tools/picker/dist/index.html",
         "isPalette": true,
         "paletteRect": "top: 54px; left: 5px; bottom: 5px; width: 300px; height: calc(100% - 59px); border-radius: var(--hlx-sk-button-border-radius); overflow: hidden; resize: horizontal;"
       },
       {
         "id": "personalisation",
         "title": "Personalisation",
         "environments": [
           "edit"
         ],
         "url": "https://main--{SITE}--{ORG}.aem.live/tools/segments/dist/index.html",
         "isPalette": true,
         "paletteRect": "top: 54px; left: 5px; bottom: 5px; width: 300px; height: calc(100% - 59px); border-radius: var(--hlx-sk-button-border-radius); overflow: hidden; resize: horizontal;"
       }
     ]
   }
   ```

   자세한 내용은 [Sidekick 라이브러리 설명서](https://www.aem.live/docs/sidekick-library)를 참조하세요.

   +++

1. `url` 키 값을 GitHub 저장소의 값으로 업데이트합니다.

   - `{ORG}` 문자열을 저장소의 조직 또는 사용자 이름으로 바꾸십시오.

   - `{SITE}` 문자열을 저장소 이름으로 바꾸기

   +++업데이트된 구성 파일의 예

   GitHub 저장소 이름이 `aco-storefront`이고 조직이 `early-adopter`인 경우 업데이트된 URL은 다음과 같이 표시됩니다.

   ```json
   {
     "project": "Boilerplate",
     "plugins": [
       {
         "id": "cif",
         "title": "Commerce",
         "environments": [
           "edit"
         ],
         "url": "https://main--aco-storefront--early-adopter.aem.live/tools/picker/dist/index.html",
         "isPalette": true,
         "paletteRect": "top: 54px; left: 5px; bottom: 5px; width: 300px; height: calc(100% - 59px); border-radius: var(--hlx-sk-button-border-radius); overflow: hidden; resize: horizontal;"
       },
       {
         "id": "personalisation",
         "title": "Personalisation",
         "environments": [
           "edit"
         ],
         "url": "https://main--aco-storefront--early-adopter.aem.live/tools/segments/dist/index.html",
         "isPalette": true,
         "paletteRect": "top: 54px; left: 5px; bottom: 5px; width: 300px; height: calc(100% - 59px); border-radius: var(--hlx-sk-button-border-radius); overflow: hidden; resize: horizontal;"
       }
     ]
   }
   ```
