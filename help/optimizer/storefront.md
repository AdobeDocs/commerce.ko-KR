---
title: 상점 설정
description: ' [!DNL Adobe Commerce Optimizer] Storefront를 설정하는 방법에 대해 알아봅니다.'
role: Developer
badgeSaas: label="SaaS만" type="Positive" url="https://experienceleague.adobe.com/ko/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."
exl-id: 2b4c9e98-a30c-4a33-b356-556de5bd721a
source-git-commit: 0d6d018b3c0d0bc7f267544844ceb8c6143394a3
workflow-type: tm+mt
source-wordcount: '1828'
ht-degree: 0%

---

# 상점 설정

>[!NOTE]
>
>이 설명서는 초기 액세스 개발 상태의 제품에 대해 설명하고 일반 가용성을 위한 모든 기능을 반영하지는 않습니다.

이 튜토리얼에서는 [!DNL Adobe Commerce Optimizer] 인스턴스의 데이터를 사용하는 강력하고, 확장 가능하며, 안전한 Adobe Commerce 상점 만들기를 위해 Edge Delivery Services에서 제공하는 [Commerce 상점](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/?lang=ko)을(를) 설정하고 사용하는 방법을 보여 줍니다.


## 사전 요구 사항

* 저장소를 만들 수 있고 로컬 개발용으로 구성된 GitHub 계정(github.com)이 있는지 확인합니다.

* Adobe Commerce Storefront 설명서의 [개요](https://experienceleague.adobe.com/developer/commerce/storefront/get-started?lang=ko)를 검토하여 Adobe Edge Delivery Services에서 Commerce Storefront를 개발하는 개념과 워크플로에 대해 알아봅니다.
* 개발 환경 설정


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
>[!DNL Adobe Commerce Optimizer] 솔루션 확장 및 사용자 정의를 위한 추가 리소스는 [App Builder for Adobe Commerce](https://experienceleague.adobe.com/ko/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder) 및 [API Mesh for Adobe Developer App Builder](https://experienceleague.adobe.com/ko/docs/commerce-learn/tutorials/adobe-developer-app-builder/api-mesh/getting-started-api-mesh)를 통해 사용할 수 있습니다. 액세스 및 사용 정보는 Adobe 계정 담당자에게 문의하십시오.

#### Sidekick 설치

Sidekick 브라우저 확장 프로그램을 설치하여 콘텐츠를 편집하고 미리 보고 상점 앞에 게시할 수 있습니다. [Sidekick 설치 지침](https://www.aem.live/docs/sidekick#installation)을 참조하세요.

## 상점 만들기

[!DNL Adobe Commerce Optimizer] 프로젝트에 대해 만든 Storefront는 Edge Delivery Services Storefront 보일러플레이트에 사용자 지정된 버전의 Adobe Commerce을 사용합니다. 보일러판은 상점 개발의 시작점을 제공하는 파일 및 폴더 집합입니다. 이 설정 프로세스는 [Edge Delivery Services Storefront의 Adobe Commerce](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/?lang=ko)에 대한 표준 설정 프로세스와 다릅니다.

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

   * **저장소 템플릿**—`hlxsites/aem-boilerplate-commerce`(기본값).
   * **모든 분기 포함**—모든 분기를 포함하는 옵션을 선택합니다.
   * **소유자**—조직 또는 계정입니다(필수).
   * **저장소 이름**—새 저장소의 고유한 이름입니다(필수).
   * **설명**—저장소에 대한 간략한 설명입니다(선택 사항).
   * **공개 또는 비공개**—Adobe에서는 공개(기본값)를 권장합니다.

1. **저장소 만들기**&#x200B;를 선택합니다.

   몇 분 후에 새 저장소가 열립니다.

   GitHub 사용자 인터페이스에 표시되는 가져오기 요청 알림을 무시합니다.

### 2단계: 상점 보일러판 업데이트

Storefront 보일러플레이트 코드를 업데이트하려면 다음 정보가 필요합니다.

* **2단계의 GitHub 저장소 URL**— `github.com/{ORG}/{SITE}`

   * `{ORG}`은(는) 저장소의 조직 이름 또는 사용자 이름입니다.

   * `{SITE}`은(는) 내 저장소 이름입니다.

* **1단계의 콘텐츠 폴더 URL**— `https://drive.google.com/drive/folders/{YOUR_FOLDER_ID}`

  `{YOUR_FOLDER_ID}`은(는) 샘플 콘텐츠 데이터로 만든 폴더의 ID입니다.

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

   1. [fstab.yaml](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/?lang=ko#vocabulary) 구성 파일을 엽니다.

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

   * `{ORG}` 문자열을 저장소의 조직 또는 사용자 이름으로 바꾸십시오.

   * `{SITE}` 문자열을 저장소 이름으로 바꾸기

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

   +++

1. 파일을 저장합니다.

### 3단계: 변경 사항 배포

사용자 지정된 Storefront Boilerplate 코드를 사용하려면 `main` 분기의 코드를 업데이트로 덮어씁니다.

1. 편집기 또는 IDE에서 업데이트한 파일을 커밋하고 저장합니다.

   ```bash
   git add .
   ```

1. 업데이트된 두 파일을 커밋하고 있는지 확인합니다.

   ```bash
   git status
   On branch aco
   Your branch is up to date with 'origin/aco'.
   
   Changes to be committed:
    (use "git restore --staged <file>..." to unstage)
        new file:   fstab1.yaml
        modified:   tools/sidekick/config.json
   ```

1. 변경 내용을 `aco` 분기에 커밋합니다.

   ```bash
   git commit -m "Update storefront boilerplate for Adobe Commerce Optimizer"
   ```

1. `main` 분기의 보일러판을 `aco` 분기의 변경 내용으로 덮어씁니다.

   ```bash
   git push origin aco:main -f
   ```

### 5단계: AEM 코드 동기화 앱 추가

AEM 코드 동기화 GitHub 앱을 저장소에 추가하여 저장소를 Edge Delivery 서비스에 연결합니다.

>[!IMPORTANT]
>
>업데이트된 상용구 코드를 GitHub 저장소의 주 분기에 업로드하기 전까지는 코드 동기화 앱을 연결하지 마십시오.

1. [AEM 코드 동기화 앱](https://github.com/apps/aem-code-sync) 구성 페이지를 엽니다.

1. **구성**&#x200B;을 선택한 다음 만든 리포지토리가 포함된 **조직** 또는 **계정**&#x200B;을(를) 사용하여 인증합니다.

1. 양식에서 **저장소만 선택**&#x200B;을 선택한 다음 만든 저장소를 선택합니다.

1. **설치**&#x200B;를 선택하여 저장소에 AEM 코드 동기화 앱을 추가합니다.

   앱이 성공적으로 설치되었다는 메시지가 표시됩니다.

### 6단계: 콘텐츠 추가

사이트 작성자 도구를 사용하여 `https://da.live`에 호스팅된 문서 작성 환경에서 상점 콘텐츠를 만들고 초기화합니다. 이 도구는 샘플 컨텐츠를 문서 작성 환경으로 가져오고 샘플 컨텐츠의 모든 문서에 대한 컨텐츠 미리 보기 및 게시 프로세스를 완료합니다. 샘플 콘텐츠에는 페이지 레이아웃, 배너, 레이블 및 상점을 채울 기타 요소가 포함됩니다.

1. [사이트 작성자 도구](https://da.live/hlxsites/aem-boilerplate-commerce/tools/site-creator/site-creator)를 엽니다.

1. 저장소 구성:

   * **[!UICONTROL Use Existing Repository]**&#x200B;을(를) 선택합니다.
   * Storefront 표준 프로젝트에 대한 **[!UICONTROL Organization/Username]**&#x200B;을(를) 입력하십시오.
   * **[!UICONTROL Repository Name]** 입력.

1. **사이트 만들기**&#x200B;를 선택하여 콘텐츠를 가져오고 미리 보고 문서 작성 환경에 게시합니다.

   ![[!DNL AEM demo content clone tool]](./assets/storefront-edit-initial-content.png){width="700" zoomable="yes"}

   사이트가 만들어지면 [!UICONTROL Edit content] 및 [!UICONTROL View Site] 섹션의 링크를 사용하여 데모 스토어프런트를 탐색할 수 있습니다.

   콘텐츠 및 사이트에 대한 기본 링크는 다음 형식을 따릅니다.

   * **루트 콘텐츠 폴더**— `https://da.live/#/{ORG}/{SITE}`
   * **사이트 미리 보기**—   `https://main--{SITE}--{ORG}.aem.page/`
   * **사이트 프로덕션:**— `https:/main--{SITE}--{ORG}.ae.live/`

1. 콘텐츠를 보려면 루트 콘텐츠 폴더 링크를 여십시오.

   ![[!DNL Storefront Document Author environment]](./assets/storefront-document-author-environment.png){width="700" zoomable="yes"}

   >[!TIP]
   >
   >측면 탐색에서 [!UICONTROL **학습**] 및 [!UICONTROL **검색**] 링크를 사용하여 사이트 및 사이트 콘텐츠 관리를 위한 학습 리소스에 액세스합니다.

### 7단계: 데모 사이트 미리보기

샘플 콘텐츠와 Adobe Commerce Optimizer 데모 인스턴스의 데이터가 모두 올바르게 표시되는지 확인합니다.

* **샘플 콘텐츠**&#x200B;는 문서 작성 환경의 콘텐츠 폴더에서 제공됩니다. 여기에는 사이트의 페이지 레이아웃, 배너 및 레이블이 포함됩니다.
* **샘플 데이터**&#x200B;는 [!DNL Adobe Commerce Optimizer] 데모 인스턴스에서 제공됩니다. 데이터에는 제품 특성, 이미지, 제품 설명 및 Storefront 구성 파일 `config.json`에 지정된 헤더 값을 기반으로 채워진 가격이 포함된 제품 데이터가 포함됩니다.

#### 사이트에 연결하여 샘플 콘텐츠 및 데이터 보기

1. `https://main--{SITE}--{ORG}.aem.live`(으)로 이동하여 사이트를 봅니다.

   `{ORG}` 및 `{SITE}`을(를) 상용구 저장소의 조직 및 이름으로 바꾸십시오.

   ![[!DNL ACO storefront site with boilerplate]](./assets/aco-storefront-site-boilerplate.png){width="700" zoomable="yes"}

   페이지가 404를 반환하는 경우 다음을 확인하십시오.

   * [`fstab.yaml` 파일의 탑재 지점이 올바른 콘텐츠 URL을 가리킵니다](#link-the-repository-to-the-document-author-environment): `https://content.da.live/{ORG}/{SITE}/`
   * [GitHub 저장소에 연결하도록 코드 동기화 앱을 구성했습니다](#step-5%3A-add-the-aem-code-sync-app).
   * [데모 콘텐츠 복제 도구를 사용하여 문서 작성 환경에 콘텐츠를 게시했습니다](#step-6%3A-add-content-documents-for-your-storefront).


1. Commerce Optimizer 기본 인스턴스에서 제공하는 샘플 카탈로그 데이터를 봅니다.

   1. storefront 헤더에서 돋보기를 클릭하여 `tires`을(를) 검색합니다.

      ![[!DNL View product list page]](./assets/storefront-site-with-aco-data.png){width="675" zoomable="yes"}

   1. 검색 결과 페이지를 보려면 **Enter**&#x200B;를 누르십시오.

      ![[!DNL View search results page]](./assets/storefront-with-aco-search-results-page.png){width="675" zoomable="yes"}

      검색 결과 페이지 구성 요소는 `search` 콘텐츠 문서에 의해 정의됩니다. 검색 결과 데이터는 `config.json`의 Storefront 구성을 기반으로 채워집니다.

   1. 페이지에서 타이어 제품을 선택하여 제품 세부 사항 페이지를 봅니다.

      ![[!DNL View product details page]](./assets/storefront-with-aco-pdp-page.png){width="675" zoomable="yes"}

      제품 세부 정보 페이지 구성 요소는 `product` 폴더의 `default` 콘텐츠 문서에 의해 정의됩니다.

### 8단계: 로컬 환경에서 개발

이 섹션에서는 로컬 개발 환경에서 Storefront 구성을 업데이트합니다.

* Adobe에서 제공한 [!DNL Adobe Commerce Optimizer] 인스턴스의 GraphQL 끝점에 연결하도록 Storefront 구성을 업데이트합니다.
* 헤더 값을 업데이트하여 인스턴스에서 데이터를 검색합니다.

#### 로컬 개발 시작

1. IDE에서 주 분기를 체크아웃하고 원격 분기의 마지막 커밋으로 재설정합니다.

   ```bash
   git checkout main
   git reset --hard origin/main
   ```

1. 필요한 종속성을 설치합니다.

   ```bash
   npm install
   ```

1. 로컬 개발 서버를 시작합니다.

   ```bash
   npm start
   ```

   `http://localhost:3000`의 브라우저에 보일러판 상점 첫 페이지가 표시됩니다.

   ![[!DNL Configure github repo to pull all branches from boilerplate repo]](./assets/aco-storefront-local-dev-env.png){width="700" zoomable="yes"}


#### Storefront 구성 업데이트

Storefront 구성 파일을 업데이트하고 로컬 개발 환경에서 변경 사항을 미리 봅니다.

1. IDE에서 Adobe에서 제공한 [!DNL Adobe Commerce Optimizer] 인스턴스에 연결하도록 Storefront 구성을 업데이트합니다.

   1. `config.json` 파일을 엽니다.

   1. [!DNL Adobe Commerce Optimizer] 인스턴스에 대한 끝점을 사용하여 다음 값을 업데이트합니다.

      * **`commerce-endpoint`**-기존 값을 끝점 URL로 바꿉니다.

        ```json
        "commerce-endpoint": "https://na1-sandbox.api.commerce.adobe.com/{tenantId}/graphql"
        ```

      * **`ac-environment-id`** - 기존 값을 끝점 URL의 테넌트 ID로 바꿉니다.

        ```json
        "ac-environment-id": "{tenantId}"
        ```

   1. 파일을 저장합니다.

      로컬 미리보기가 제대로 작동하는 경우 업데이트가 로컬 상점 앞에 적용됩니다.

1. 사이트를 확인하여 구성 변경 결과를 확인합니다.

   1. 브라우저에서 `http://localhost:3000`(으)로 이동하여 페이지를 새로 고칩니다.

   1. storefront 헤더에서 돋보기를 클릭하여 `tires`을(를) 검색합니다.

      ![타이어 검색](./assets/storefront-header-empty-search-list.png){width="675" zoomable="yes"}

   1. 검색 결과 페이지를 표시하려면 **Enter**&#x200B;를 누르십시오.

      ![헤더 값이 잘못된 빈 검색 결과](./assets/storefront-configuration-with-incorrect-headers.png){width="675" zoomable="yes"}

      storefront 구성 파일의 헤더 값은 기본 인스턴스를 기반으로 하므로 검색은 결과를 반환하지 않습니다. 이제 구성이 제공된 [!DNL Adobe Commerce Optimizer] 인스턴스를 가리키므로 해당 값이 잘못되었습니다.

### 다음 단계

상점에서 콘텐츠 및 데이터를 관리하고 표시하는 방법에 대한 자세한 내용은 [상점 및 카탈로그 관리자 엔드 투 엔드 사용 사례](./use-case/admin-use-case.md)를 참조하세요.

>[!MORELIKETHIS]
>
> 사이트 콘텐츠를 업데이트하고 Adobe Commerce 프론트엔드 구성 요소 및 백엔드 데이터와 통합하는 방법에 대한 자세한 내용은 [Commerce Storefront 설명서](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=ko)를 참조하십시오.
