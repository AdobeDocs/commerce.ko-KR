---
title: 상점 설정
description: ' [!DNL Adobe Commerce Optimizer] Storefront를 설정하는 방법에 대해 알아봅니다.'
role: Developer
source-git-commit: 425c801a852de566120504563e256b0351df588e
workflow-type: tm+mt
source-wordcount: '2287'
ht-degree: 0%

---

# 상점 설정

>[!NOTE]
>
>이 설명서는 초기 액세스 개발 상태의 제품에 대해 설명하고 일반 가용성을 위한 모든 기능을 반영하지는 않습니다.

이 튜토리얼에서는 [!DNL Adobe Commerce Optimizer] 인스턴스의 데이터를 사용하는 강력하고, 확장 가능하며, 안전한 Adobe Commerce 상점 만들기를 위해 Edge Delivery Services에서 제공하는 [Commerce 상점 첫 페이지를 설정하고 사용하는 방법을 보여 줍니다.](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/)


## 사전 요구 사항

* 저장소를 만들 수 있고 로컬 개발용으로 구성된 GitHub 계정(github.com)이 있는지 확인합니다.

* Adobe Commerce Storefront 설명서의 [개요](https://experienceleague.adobe.com/developer/commerce/storefront/get-started)를 검토하여 Adobe Edge Delivery Services용 Storefront 만들기와 관련된 기본 워크플로 및 용어를 숙지하십시오.
* 개발 환경 설정


### 개발 환경 설정

개발 환경을 설정하려면 필요한 Node.js 버전 및 Sidekick 브라우저 확장 기능을 설치하십시오.

#### Node.js 설치

Edge Delivery Services 프로젝트에서 로컬로 [!DNL Adobe Commerce Optimizer] 상점 전면을 개발 및 테스트하려면 Node.js 버전 22.13.1 LTS가 필요합니다.

필요한 경우 다음 단계를 완료하여 NVM(Node Version Manager) 및 필요한 Node.js 버전을 설치합니다.

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
>이 설정은 [!DNL Adobe Commerce Optimizer] 및 Adobe Commerce Edge Delivery Service Storefront를 사용하여 개발하기 위한 것입니다. [!DNL Adobe Commerce Optimizer] 솔루션 확장 및 사용자 정의를 위한 추가 리소스는 [App Builder for Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder) 및 [API Mesh for Adobe Developer App Builder](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/api-mesh/getting-started-api-mesh)를 통해 사용할 수 있습니다. 액세스 및 사용 정보는 Adobe 계정 담당자에게 문의하십시오.

#### Sidekick 설치

Sidekick 브라우저 확장 프로그램을 설치하여 상점 첫 화면 컨텐츠를 편집, 미리보기 및 게시합니다. [Sidekick 설치 지침](https://www.aem.live/docs/sidekick#installation)을 참조하세요.


## 상점 만들기

[!DNL Adobe Commerce Optimizer] 프로젝트에 대해 만드는 Storefront는 Edge Delivery Services Storefront Boilerplate의 사용자 지정된 Adobe Commerce 버전을 사용하여 빌드되었습니다. 보일러판은 상점 건물을 짓는 시작점을 제공하는 파일 및 폴더 집합입니다.

이 Storefront 설정 프로세스는 특히 [!DNL Adobe Commerce Optimizer] 프로젝트에 대해 사용자 지정됩니다. 흐름이 Edge Delivery Services Storefront의 표준 [Adobe Commerce](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/) 설정에 대한 흐름과 다릅니다.

>[!NOTE]
>
>이 자습서에서는 macOS, Chrome 및 Visual Studio 코드를 개발 환경으로 사용합니다. 화면이 캡처되고 해당 설정이 지침에 반영됩니다. 다른 운영 체제, 브라우저 및 코드 편집기를 사용할 수 있지만 표시되는 UI와 수행해야 하는 단계는 그에 따라 다릅니다.

### 워크플로우 개요

다음 단계에 따라 Adobe Commerce Optimizer에 사용할 상점 전면을 설정합니다.

1. **[컨텐츠 폴더 만들기](#step-1-create-a-content-folder)**-Google 드라이브 또는 Sharepoint에 공유 컨텐츠 폴더를 만듭니다. 이 폴더에는 상점용 샘플 콘텐츠 및 에셋이 포함되어 있습니다.

1. **[코드 리포지토리 만들기](#step-1-create-a-code-repository)**-Adobe Commerce + Edge Delivery Services boilerplate 템플릿에서 GitHub 리포지토리를 만듭니다. 소스 저장소의 모든 분기를 포함합니다.
1. **[Storefront Boilerplate 업데이트](#step-2-update-the-storefront-boilerplate)**-저장소의 `aco` 분기에서 사용자 지정 Boilerplate 템플릿을 업데이트하여 콘텐츠 폴더를 Storefront에 연결하고 Adobe Commerce Optimizer 데모 인스턴스에서 Storefront로 데이터를 전달하는 Storefront 구성을 검토하십시오.
1. **[업데이트된 storefront 보일러판 코드를 업로드합니다](#step-3-upload-the-updated-boilerplate-code)**-`main` 분기의 코드를 `aco` 분기의 업데이트된 코드로 덮어씁니다.
1. **[CodeSync 앱을 추가](#step-4-add-the-aem-code-sync-app)**-저장소를 Edge Delivery 서비스에 연결합니다. 소스 코드 사용자 지정을 완료하고 코드를 `main` 분기로 푸시할 준비가 될 때까지 코드 동기화 앱을 연결하지 마십시오.
1. **[콘텐츠 미리 보기 및 게시](#step-5-preview-and-publish-your-content)** - Sidekick 확장을 사용하여 콘텐츠 폴더의 사이트 콘텐츠를 미리 보고 상점에 게시합니다.
1. **[사이트 미리 보기 및 샘플 데이터 보기](#step-6-preview-your-site-and-view-sample-data)**-상점 사이트에 연결하여 [!DNL Adobe Commerce Optimizer] 데모 인스턴스의 샘플 콘텐츠와 데이터를 확인하세요.
1. **[로컬 환경에서 상점 개발](#step-7-develop-the-storefront-in-your-local-environmentdevelop-the-storefront-in-your-local-environment)**-필요한 종속성 설치 로컬 개발 서버를 시작하고 Adobe에서 제공한 [!DNL Adobe Commerce Optimizer] 인스턴스에 연결하도록 Storefront 구성을 업데이트합니다.
1. **[사이트 콘텐츠 관리](#step-8-manage-site-content)** - 사이트 콘텐츠 업데이트 및 관리에 대해 자세히 알아봅니다.

### 1단계: 컨텐츠 폴더 만들기

Adobe Commerce Storefront 설명서의 지침에 따라 Google Drive 또는 Sharepoint에 공유 콘텐츠 폴더를 추가하고 샘플 콘텐츠를 추가합니다. 샘플 콘텐츠에는 이미지, 텍스트 및 사이트를 구성하는 기타 에셋이 포함됩니다.

* [Google 드라이브 또는 Sharepoint 폴더를 만들고 공유](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/#create-and-share-folder)
* [샘플 콘텐츠를 폴더에 로드](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/#add-sample-content)합니다.

### 2단계: 코드 저장소 만들기

Edge Delivery Services + Adobe Commerce Boilerplate 템플릿을 사용하여 GitHub에서 코드 리포지토리를 만듭니다. 이 템플릿은 상점 첫 화면의 상용구 코드를 제공합니다.

1. GitHub 계정에 로그인합니다.

1. [aem-boilerplate-commerce](https://github.com/hlxsites/aem-boilerplate-commerce) GitHub 저장소로 이동합니다.

1. **이 템플릿 사용**&#x200B;을 선택한 다음 드롭다운 메뉴에서 **새 저장소 만들기**&#x200B;를 선택합니다.

   ![[!DNL Create github repo from storefront boilerplate template]](./assets/storefront-create-github-repo.png){width="700" zoomable="yes"}

   저장소 구성 페이지가 열립니다.

   ![[!DNL Configure github repo to pull all branches from boilerplate repo]](./assets/storefront-configure-github-repo.png){width="700" zoomable="yes"}

1. 다음 세부 정보를 사용하여 구성 양식을 작성합니다.

   * **저장소 템플릿**—`hlxsites/aem-boilerplate-commerce`(기본값).
   * **모든 분기 포함**—모든 분기를 포함하는 옵션을 선택합니다.
   * **소유자**—조직 또는 계정입니다(필수).
   * **저장소 이름**—새 저장소의 고유한 이름입니다(필수).
   * **설명**—저장소에 대한 간략한 설명입니다(선택 사항).
   * **공개 또는 비공개**—Adobe에서는 공개(기본값)를 권장합니다.

1. **저장소 만들기**&#x200B;를 선택합니다.

   1~2분 후 새 저장소가 열립니다.

   새 저장소에 표시되는 가져오기 요청 알림을 무시합니다.

### 3단계: 상점 보일러판 업데이트

이 섹션에서는 다음 작업을 완료합니다.

* 리포지토리의 `aco` 분기를 체크 아웃하여 [!DNL Adobe Commerce Optimizer] 프로젝트에 대한 사용자 지정 표준 서식 파일을 업데이트하십시오.
* 콘텐츠 폴더를 가리키도록 `fstab.yaml` 파일을 업데이트하여 콘텐츠 폴더를 상점 앞에 연결합니다.
* Storefront 구성 파일 `config.json`을(를) 검토합니다.
* 공유 컨텐츠 폴더의 컨텐츠를 편집, 미리보기 및 게시하도록 Sidekick 확장을 구성합니다.

이 단계를 완료하려면 다음 정보가 필요합니다.

* **2단계의 GitHub 저장소 URL**— `github.com/{ORG}/{SITE}`

   * `{ORG}`은(는) 저장소의 조직 이름 또는 사용자 이름입니다.

   * `{SITE}`은(는) 내 저장소 이름입니다.

* **1단계의 콘텐츠 폴더 URL**— `https://drive.google.com/drive/folders/{YOUR_FOLDER_ID}`

  `{YOUR_FOLDER_ID}`은(는) 샘플 콘텐츠 데이터로 만든 폴더의 ID입니다.

#### 컨텐츠 폴더에 연결하도록 상용구 코드 업데이트

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

1. 콘텐츠 URL을 가리키도록 storefront 구성 파일을 업데이트합니다.

   1. [fstab.yaml](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/#vocabulary) 구성 파일을 엽니다.

      ```json
      mountpoints:
       /: {YOUR_MOUNTPOINT_URL}
      
      folders:
       /products/: /products/default
      ```

   1. `{YOUR_MOUNTPOINT_URL}`을(를) 콘텐츠 관리 시스템의 URL로 바꾸십시오.

      예를 들어 Google 드라이브를 사용하는 경우 업데이트된 코드는 다음과 같아야 합니다.

      ```json
       mountpoints:
        /: https://drive.google.com/drive/folders/{YOUR_FOLDER_ID}
      ```

   1. 파일을 저장합니다.

#### 데이터 연결 구성 검토

데이터 연결은 Adobe Commerce Optimizer과 상점 간의 통신을 구축하여 카탈로그 데이터가 상점 앞으로 원활하게 전달되도록 합니다. 이 프로세스는 [!DNL Adobe Commerce Optimizer]에 필요한 검색 구성 요소, 제품 목록 및 제품 세부 사항 페이지를 포함하여 다양한 상점 인터페이스를 채웁니다.

초기 Storefront 설정의 경우 Adobe은 샘플 데이터를 사용하여 Adobe Commerce Optimizer 데모 인스턴스에 연결하는 기본 구성 파일을 제공합니다.

```json
{
  "public": {
    "default": {
      "commerce-core-endpoint": "https://www.aemshop.net/graphql",
      "commerce-endpoint": "https://na1-sandbox.api.commerce.adobe.com/Fwus6kdpvYCmeEdcCX7PZg/graphql",
      "headers": {
        "cs": {
          "ac-channel-id": "9ced53d7-35a6-40c5-830e-8288c00985ad",
          "ac-environment-id": "Fwus6kdpvYCmeEdcCX7PZg",
          "ac-price-book-id": "west_coast_inc",
          "ac-scope-locale": "en-US"
        }
      },
      "analytics": {
        "base-currency-code": "USD",
        "environment": "Production",
        "store-id": 1,
        "store-name": "ACO Demo",
        "store-url": "https://www.aemshop.net",
        "store-view-id": 1,
        "store-view-name": "Default Store View",
        "website-id": 1,
        "website-name": "Main Website"
      }
    }
  }
}
```

저장소의 Storefront 구성 파일을 검토하여 데이터 연결이 설정되는 방식을 이해합니다.

1. 코드 저장소에서 루트 디렉토리로 이동합니다.

1. `config.json` 파일을 엽니다.

   이 파일에서 다음 키 값은 연결할 Adobe Commerce Optimizer 인스턴스를 지정하고 상점 앞으로 흐르는 데이터를 결정합니다.

   * `commerce-endpoint`은(는) 연결할 Adobe Commerce Optimizer 인스턴스를 정의합니다.
   * `headers`은(는) 상점 앞으로 흐르는 데이터를 결정합니다.
      * `ac-channel-id`이(가) `west_coast_inc`(으)로 설정되어 있습니다.
      * `ac-price-book-id`이(가) `west_coast_inc`(으)로 설정되어 있습니다.
      * `ac-scope-locale`이(가) `en-US`(으)로 설정되어 있습니다.
      * `ac-price-book-id`이(가) `west_coast_inc`(으)로 설정되어 있습니다.

   이 값은 채널 ID, 로케일 및 가격 장부 ID를 설정하여 카탈로그 데이터를 특정 판매 채널에 보내고 지정된 로케일 및 가격 장부 값을 기준으로 해당 데이터를 필터링합니다. 나중에 Adobe Commerce Optimizer 인스턴스를 변경하고 헤더를 업데이트하여 어떤 데이터가 상점 앞에 전달되는지 정의하는 방법을 배웁니다.

1. 파일을 검토한 후 파일을 닫고 자습서를 계속합니다.


#### Sidekick 확장 구성

Sidekick 확장에 대한 프로젝트 구성을 추가합니다. Sidekick을 사용하여 상점 콘텐츠를 편집하고 미리 보고 게시할 수 있습니다. 이 구성을 사용하면 Sidekick을 사용하여 공유 컨텐츠 폴더와 스테이징 및 프로덕션 환경에 게시된 사이트 페이지의 컨텐츠를 관리할 수 있습니다.

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

   * `{ORG}`은(는) 코드 저장소의 저장소 이름 또는 사용자 이름입니다.

   * `{SITE}`은(는) 저장소 이름입니다.

1. 파일을 저장합니다.

### 4단계: 업데이트된 상용구 코드 업로드

사용자 지정된 Storefront Boilerplate 코드를 사용하려면 `main` 분기의 코드를 업데이트로 덮어씁니다.

1. 편집기 또는 IDE에서 업데이트한 파일을 커밋하고 저장합니다.

   ```bash
   git add .
   ```

   ```bash
   git commit -m "Update storefront boilerplate for Adobe Commerce Optimizer"
   ```

1. `aco` 분기의 변경 내용을 푸시하고 `main` 분기를 덮어씁니다.

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

1. 양식에서 **저장소만 선택**&#x200B;을 선택하고 만든 저장소를 선택합니다.

1. **설치**&#x200B;를 선택하여 저장소에 AEM 코드 동기화 앱을 추가합니다.

   앱이 성공적으로 설치되었다는 메시지가 표시됩니다.

### 6단계: 콘텐츠 미리보기 및 게시

스토어프론트에 콘텐츠를 추가하려면 Sidekick 확장을 사용하여 콘텐츠를 미리 보고 게시해야 합니다.

1. Google 드라이브 또는 Sharepoint에서 컨텐츠 폴더를 엽니다.

1. 브라우저 도구 모음에서 Sidekick 아이콘을 클릭하여 Sidekick을 켭니다.

   ![[!DNL Turn on Sidekick from browser toolbar]](./assets/storefront-enable-sidekick-toolbar.png){width="700" zoomable="yes"}

1. Sidekick 도구 모음을 사용하여 콘텐츠를 미리 보고 게시할 수 있습니다.

   ![[미리 보고 게시할 파일 선택]](./assets/storefront-content-preview-publish.png){width="700" zoomable="yes"}

1. 각 폴더의 파일을 별도로 선택하고 Sidekick 도구 모음을 사용하여 모든 파일을 미리 보고 게시할 수 있습니다.

   * **미리 보기**-스테이징 환경에 콘텐츠를 업로드합니다. Storefront 스테이징 URL이 `.aem.page`(으)로 끝납니다.

   * **게시**-프로덕션 환경에 콘텐츠를 업로드합니다. 프로덕션 URL이 `aem.live`(으)로 끝납니다.

자세한 내용은 Adobe Experience Manager [Sidekick](https://www.aem.live/docs/sidekick) 설명서를 참조하십시오.

### 7단계: 사이트 미리보기

사이트를 미리 보고 샘플 콘텐츠와 Adobe Commerce Optimizer 데모 데이터가 모두 올바르게 표시되는지 확인하십시오.

* **샘플 콘텐츠**&#x200B;는 공유 콘텐츠 폴더에서 제공됩니다. 여기에는 Sidekick을 사용하여 게시한 페이지 레이아웃, 배너 및 기타 콘텐츠가 포함됩니다.
* **샘플 데이터**&#x200B;는 [!DNL Adobe Commerce Optimizer] 데모 인스턴스에서 제공됩니다. 데이터에는 제품 특성, 이미지, 제품 설명 및 Storefront 구성 파일 `config.json`에 지정된 값을 기반으로 채워진 가격이 포함된 제품 데이터가 포함됩니다.


#### 사이트에 연결하여 샘플 콘텐츠 및 데이터 보기

1. `https://main--{SITE}--{ORG}.aem.live`(으)로 이동하여 사이트에 연결합니다.

   `{ORG}` 및 `{SITE}`을(를) 상용구 저장소의 조직 및 이름으로 바꾸십시오.

   ![[!DNL ACO storefront site with boilerplate]](./assets/aco-storefront-site-boilerplate.png){width="700" zoomable="yes"}

   페이지가 404를 반환하는 경우 Sidekick 확장을 사용하여 콘텐츠를 게시했는지 확인합니다. 또한 업데이트된 `fstab.yaml` 파일에서 콘텐츠 폴더의 URL을 사용하고 있는지 다시 확인하십시오.

1. Commerce Optimizer 데모 인스턴스에서 제공하는 샘플 카탈로그 데이터를 봅니다.

   1. 사용 가능한 타이어 제품의 드롭다운 목록을 보려면 `tires`을(를) 검색하십시오.

   ![[!DNL Discover Adobe Commerce Optimizer products]](./assets/storefront-site-with-aco-data.png){width="700" zoomable="yes"}

   검색 구성 요소는 storefront 보일러플레이트 코드의 일부입니다. 검색 결과 데이터는 Storefront 구성을 기반으로 채워집니다.

   1. 제품 목록 페이지를 보려면 **Enter**&#x200B;를 누르십시오.

      ![[!DNL View product details page]](./assets/storefront-with-aco-pdp-page.png){width="675" zoomable="yes"}

   1. 페이지에서 타이어 제품을 선택하여 제품 세부 사항 페이지를 봅니다.

      상점 전면을 탐색하는 경우 일부 구성 요소가 작동하지 않습니다. 예를 들어 장바구니에 제품을 추가하면 오류가 반환되고 계정 관리 구성 요소가 작동하지 않습니다. 이는 이러한 구성 요소가 Commerce 백엔드에서 데이터를 수신하도록 구성되지 않았기 때문입니다. Adobe Commerce Optimizer 인스턴스의 데이터는 검색 구성 요소, 제품 목록 및 제품 세부 사항 페이지만 채웁니다.

   1. 상점을 둘러본 후 튜토리얼을 계속합니다.


### 8단계: 로컬 환경에서 상점 개발

이 섹션에서는 Adobe에서 제공한 [!DNL Adobe Commerce Optimizer] 인스턴스에 Storefront를 연결하여 로컬 개발 환경에서 Storefront 구성을 실험해 봅니다.

연결하려면 온보딩 이메일에 제공된 머천다이징 서비스에 대한 GraphQL 엔드포인트가 필요합니다.

```text
https://na1-sandbox.api.commerce.adobe.com/{tenantId}/graphql
```

#### 로컬 개발 시작

1. IDE에서 GitHub 코드 저장소의 주 분기를 체크아웃합니다.

   ```bash
   git checkout main
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

      드롭다운 목록이 채워지지 않습니다.

   1. 제품 목록 페이지를 표시하려면 **Enter**&#x200B;를 누르십시오.

      ![헤더 값이 잘못된 빈 검색 결과](./assets/storefront-configuration-with-incorrect-headers.png){width="675" zoomable="yes"}

      storefront 구성 파일의 헤더가 데모 인스턴스를 기반으로 헤더 값을 사용하므로 검색은 결과를 반환하지 않습니다. 이제 구성이 제공된 [!DNL Adobe Commerce Optimizer] 인스턴스를 가리키므로 해당 값이 잘못되었습니다.

### 다음 단계

[!DNL Adobe Commerce Optimizer] 인스턴스의 값을 사용하여 Storefront 구성을 업데이트하여 Storefront의 콘텐츠를 표시하는 방법에 대해 알아보려면 [Storefront 및 카탈로그 관리자 엔드투엔드 사용 사례](./use-case/admin-use-case.md)를 참조하세요.

>[!MORELIKETHIS]
>
>* Adobe Commerce 백 엔드 없이 [!DNL Adobe Commerce Optimizer]을(를) 사용하려는 경우 [Adobe Experience Manager 상점 첫 화면 설명서](https://experienceleague.adobe.com/developer/commerce/storefront/)를 참조하여 사이트 콘텐츠를 업데이트하고 Commerce 프론트엔드 구성 요소 및 백 엔드 데이터와 통합하는 방법에 대해 자세히 알아보십시오.
></br></br>
>* Adobe Commerce 백엔드와 함께 [!DNL Adobe Commerce Optimizer]을(를) 사용하려면 [Adobe Commerce Storefront 설명서](https://experienceleague.adobe.com/developer/commerce/storefront/)를 참조하여 콘텐츠를 업데이트하고 계정 관리, 체크아웃 및 기타 기능을 위해 Storefront 구성 요소를 구성하는 방법에 대해 알아보십시오.
