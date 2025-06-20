---
title: 상점 설정
description: ' [!DNL Adobe Commerce as a Cloud Service] storefront를 설정하는 스캐폴딩 도구를 실행하는 방법에 대해 알아봅니다.'
role: Developer
exl-id: 02928dc4-1777-483e-b0ee-b04fc813864d
badgeSaas: label="SaaS만" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."
source-git-commit: c9869e45ed9eb8f04cf3e1bfb3542a42bbf97c0f
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 0%

---

# 상점 설정

{{accs-early-access}}

다음 단계에서는 `aio commerce init` 명령을 사용하여 Edge Delivery에서 제공하는 Adobe Commerce Storefront를 빠르게 설정하는 방법을 보여 줍니다. 이 프로세스는 다음을 설정합니다.

* [Edge Delivery Services에서 제공하는 Commerce 상점](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/) - Adobe의 Edge Delivery Services에서 제공하는 성능이 뛰어나고 확장 가능하며 안전한 상점.
* [Adobe Developer App Builder용 API Mesh](https://developer.adobe.com/graphql-mesh-gateway/mesh/) - 개발자가 여러 데이터 소스를 하나의 GraphQL 엔드포인트로 결합할 수 있는 API 플랫폼입니다. API Mesh는 단일 게이트웨이를 통해 Adobe API로 서드파티 API를 조정합니다. 단일 GraphQL 엔드포인트에 대한 하나의 쿼리는 여러 소스의 결과를 반환할 수 있습니다.
* [Adobe Developer Console](https://developer.adobe.com/developer-console/docs/guides/) - API, 이벤트, 런타임 함수 및 플러그인에 액세스할 수 있는 개발자 도구의 컬렉션으로, Adobe 애플리케이션용 프로젝트를 빌드하는 데 사용할 수 있습니다.
* [Adobe I/O Runtime](https://developer.adobe.com/runtime/docs/) - 이벤트에 응답하고 클라우드에서 함수를 실행하는 사용자 지정 코드를 배포하기 위한 서버를 사용하지 않는 엔진입니다.

## 사전 요구 사항

`aio commerce init` 명령을 실행하기 전에 다음 필수 구성 요소를 완료해야 합니다.

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

1. [Adobe I/O Runtime CLI](https://developer.adobe.com/runtime/docs/guides/tools/cli_install/)를 설치합니다.

   ```bash
   npm install -g @adobe/aio-cli
   ```

1. Adobe I/O API Mesh 플러그인을 설치합니다.

   ```bash
   aio plugins:install @adobe/aio-cli-plugin-api-mesh
   ```

1. Adobe I/O Commerce 플러그인을 설치합니다.

   ```bash
   aio plugins:install https://github.com/adobe-commerce/aio-cli-plugin-commerce
   ```

1. 기존 플러그인을 업데이트합니다.

   ```bash
   aio plugins:update
   ```

1. Adobe Experience Cloud 계정에 로그인합니다.

   ```bash
   aio login
   ```

   `aio login` 명령이 브라우저 창을 시작하지 않으면 [문제 해결](#troubleshooting) 섹션을 참조하십시오.

1. IMS 조직, 프로젝트 및 작업 공간을 선택합니다. 화살표 키를 사용하고 **Enter**&#x200B;를 눌러 선택합니다. `aio` 명령에 대한 자세한 내용은 [Adobe I/O CLI 설명서](https://github.com/adobe/aio-cli-plugin-console?tab=readme-ov-file#commands)를 참조하세요.

   ```bash
   aio console org select
   ```

   ```bash
   aio console project select
   ```

   ```bash
   aio console workspace select
   ```

1. 아직 수락하지 않았다면 https://developer.adobe.com/console/home으로 이동한 후 **수락 및 계속**&#x200B;을 클릭하여 Adobe Developer 콘솔에서 개발자 사용 약관에 동의하십시오.

## `aio commerce init` 명령 실행

다음 명령을 실행하면 Commerce 상점 첫 화면의 스캐폴딩이 생성됩니다. 이 스캐폴딩은 상점을 구축하고 이해할 수 있는 좋은 출발점을 제공합니다. Storefront 작업에 대한 자세한 내용은 [Adobe Commerce Storefront 설명서](https://experienceleague.adobe.com/developer/commerce/storefront/)를 참조하십시오.


1. `init` 명령 실행:

   ```bash
   aio commerce init
   ```

1. GitHub에 이미 로그인한 경우 `Y`을(를) 입력하여 사용자 이름 아래에 리포지토리를 만드십시오.

1. 만들려는 저장소의 이름을 입력합니다.

1. 다음 옵션 중 하나를 선택합니다.

   * **데모 Adobe Commerce 테넌트 사용** - 데모 테넌트 사용
      * 이 옵션을 선택하면 브라우저 창에 AEM 코드 동기화 보트를 설치하라는 메시지가 표시됩니다. 생성한 저장소를 지정하고 보트를 승인해야 합니다. CLI로 돌아가서 `y`을(를) 입력하여 AEM 코드 동기화 보트 설치를 확인합니다.
   * **사용 가능한 Adobe Commerce 테넌트 선택** - 선택한 조직에서 기존 Commerce 테넌트를 선택합니다.
      * 이 옵션을 선택하는 경우 메쉬를 생성할 프로젝트와 작업 영역을 선택해야 합니다.
   * **자체 Adobe Commerce 테넌트 API URL을 제공** - 조기 액세스 프로그램 참가자인 경우 이 옵션을 선택합니다. Adobe 온보딩 이메일에 제공된 API URL을 입력합니다.

   >[!NOTE]
   >
   >`Pick an available API (Mesh -> SaaS)` 옵션을 선택하는 경우 Adobe Developer Console에 기존 프로젝트와 Workspace이 있어야 합니다. [템플릿 프로젝트 만들기](https://developer.adobe.com/developer-console/docs/guides/projects/projects-template/)와(과) App Builder을 선택하면 필요한 작업 영역이 자동으로 만들어집니다.

1. 프로세스가 완료되면 다음 방법을 사용하여 스토어를 사용자 정의할 수 있습니다.

   * 코드 사용자 지정: `https://github.com/<username or org>/<repo name>`
   * 콘텐츠 편집: `https://da.live/#/<username or org>/<repo name>`
   * 구성 관리: `https://da.live/sheet#/<username or org>/<repo name>/configs-stage`
   * 상점 미리 보기: `https://main--<repo name>--<username or org>.aem.page/`
   * 로컬에서 실행: `aio commerce:dev`

상점을 사용자 지정하려면 [Adobe Commerce 상점 설명서](https://experienceleague.adobe.com/developer/commerce/storefront/)를 참조하세요.

## 문제 해결

`aio login` 명령에 문제가 발생하면 Adobe에서는 CLI 및 브라우저에서 완전히 로그아웃한 다음 다시 로그인하는 것이 좋습니다.

1. CLI에서 로그아웃하려면 다음을 실행합니다.

   ```bash
   aio logout
   ```

1. 브라우저에서 [Adobe Developer Console](https://developer.adobe.com/console)&#x200B;(으)로 이동하고 오른쪽 상단에서 프로필 아이콘을 클릭한 다음 **로그아웃**&#x200B;을 선택합니다.

1. CLI로 돌아가서 `aio login` 명령을 다시 실행하여 로그인하려면 브라우저 창을 시작해야 합니다. 그런 다음 조직, 프로젝트 및 작업 영역을 계속 선택할 수 있습니다.

   ```bash
   aio console org select
   ```

   ```bash
   aio console workspace select
   ```

   ```bash
   aio console project select
   ```
