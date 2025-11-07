---
title: ADL Commerce 랩 사전 요구 사항
description: 등급 확장 랩에 대한 사전 요구 사항을 알아봅니다.
role: Developer
hide: true
hidefromtoc: true
source-git-commit: ba4d096bcb99420c029d0b0674fc00f1f1445cea
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 0%

---

# Adobe Developers Live - Adobe Commerce 랩 사전 요구 사항

이 페이지에는 [ratings extension lab](./workbook.md)에 대한 필수 구성 요소와 기타 수동 설정 단계가 나열됩니다. 연구실에는 이러한 단계의 대부분을 자동화하는 스크립트도 포함되어 있다.

## 확장 사전 요구 사항

시작하기 전에 다음 사전 요구 사항을 완료하십시오.

* [!DNL Adobe I/O CLI] 설치

  ```bash
  npm install -g @adobe/aio-cli
  ```

* Commerce 플러그인 설치

  ```bash
  aio plugins:install https://github.com/adobe-commerce/aio-cli-plugin-commerce
  ```

* [Cursor](https://cursor.com/download)&#x200B;(권장)과 같은 AI 지원 IDE를 다운로드하거나, 클라우드 코드, Gemini CLI 또는 Copilot과 같은 다른 IDE도 지원되지만, 이 자습서에서는 프롬프트 및 기타 단계를 수정해야 할 수 있습니다.
<!-- 
### Create a new project on Adobe Developer Console

1. Navigate to [Adobe Developer Console](https://developer.adobe.com/).
1. Click [!UICONTROL **Create project from a template**].
1. Select the [!UICONTROL **App Builder**] template.
1. Enter a [!UICONTROL **Project Title**] and [!UICONTROL **App Name**].
1. Ensure the **[!UICONTROL Include Runtime]** checkbox is marked.

   ![Create project with App Builder template](./assets/app-builder-template.png){width="600" zoomable="yes"}

1. Click **Save**.

### Add APIs to the workspace

1. Click the [!UICONTROL **Stage**] workspace and then repeat the following steps for each API.

   ![APIs added to workspace](./assets/add-apis-workspace.png){width="600" zoomable="yes"}

1. Click [!UICONTROL **Add Service**] and select [!UICONTROL **API**].

1. Select the [!UICONTROL **Adobe Services**] filter and select one of the following APIs:

   * [!UICONTROL **I/O Management API**]
   * [!UICONTROL **I/O Events**]

1. Select the [!UICONTROL **Experience Cloud**] filter and select one of the following APIs:

   * [!UICONTROL **Adobe I/O Events for Adobe Commerce**]

1. Click [!UICONTROL **Next**].

1. Click[!UICONTROL **Save configured API**].

1. Repeat the previous steps until all APIs are added to the workspace.

   ![APIs added to workspace](./assets/apis-added.png){width="600" zoomable="yes"} -->

### AIO CLI 구성

1. 기존 구성을 지웁니다.

   ```bash
   aio config clear
   ```

   AIO CLI를 사용하여 로그인합니다.

   ```bash
   aio auth login -f
   ```

1. 다음 각 명령을 사용하여 조직, 프로젝트 및 작업 영역을 선택합니다.

   ```bash
   aio console org select
   ```

   ```bash
   aio console project select
   ```

   ```bash
   aio console workspace select
   ```

   ![CLI 구성](./assets/cli-configuration.png){width="600" zoomable="yes"}

### 클론 통합 시작 키트

Commerce 통합 시작 키트 저장소를 복제하고 프로젝트를 준비합니다.

```bash
git clone --branch adl https://github.com/adobe/commerce-integration-starter-kit.git extension
cd extension
```

![시작 키트 복제](./assets/clone-starter-kit.png){width="600" zoomable="yes"}

### .env 파일 만들기

환경 구성 파일 만들기:

```bash
cp env.dist .env
```

<!-- Open the `.env` file in a text editor and add the following OAuth credentials:

```text
OAUTH_CLIENT_ID=
OAUTH_CLIENT_SECRET=
OAUTH_TECHNICAL_ACCOUNT_ID=
OAUTH_TECHNICAL_ACCOUNT_EMAIL=
OAUTH_ORG_ID=
```

You can copy these values from the **[!UICONTROL Credential details]** page in [Developer Console](https://developer.adobe.com/) by clicking the **[!UICONTROL OAuth Server-to-Server]** tab on your workspace.

![OAuth credentials](./assets/oauth-credentials.png){width="600" zoomable="yes"}

#### Add the Commerce configuration

Add the following Commerce instance details to your `.env` file:

```text
COMMERCE_BASE_URL=
COMMERCE_GRAPHQL_ENDPOINT=
```

To find these values:

1. Go to [Commerce Cloud Service instances](https://experience.adobe.com/#/@commerce/commerce/cloud-service/instances).
1. Click the information icon next to your assigned seat.
1. Copy the REST endpoint as `COMMERCE_BASE_URL`.
1. Copy the GraphQL Endpoint as `COMMERCE_GRAPHQL_ENDPOINT`.

#### Set event prefix

Set a temporary value for the event prefix:

```text
EVENT_PREFIX=test
```
 -->

### 작업 공간 구성 다운로드

다음 명령을 실행하여 작업 영역 구성 파일을 다운로드합니다.

```bash
aio console workspace download workspace.json
```

### 로컬 작업 영역을 원격 작업 영역에 연결

로컬 프로젝트를 원격 작업 영역에 연결합니다.

```bash
aio app use workspace.json -m
```

![작업 영역에 연결](./assets/connect-workspace.png){width="600" zoomable="yes"}

## Storefront 사전 요구 사항

다음 항목은 이 자습서의 [storefront](#connect-to-the-storefront) 섹션을 완료하고 스토어에서 제품 등급을 확인해야 합니다.
<!-- 
* Install [!DNL Node.js] (version `22.x.x`) and npm (`9.0.0` or higher). Verify your installation:

   ```bash
   node --version
   npm --version
   ```

* Install [Git](https://git-scm.com) (Optional) - Required only if [cloning the repository directly](#option-a-clone-the-repository-recommended)(recommended), not needed if you [download the zip file](#option-b-download-the-zip-file). Verify your installation:

  ```bash
  git --version
  ```

* Bash shell
  * macOS/Linux: No installation required
  * Windows: Use [Git Bash](https://git-scm.com/install) or [Windows Subsystem for Linux (WSL)](https://learn.microsoft.com/en-us/windows/wsl/install).

* [Google Chrome](https://www.google.com/chrome/) - Required for testing the storefront -->

### 프로젝트 파일 가져오기

다음 두 가지 방법 중 하나로 프로젝트 파일을 가져올 수 있습니다.

<!-- 
#### Option A: Clone the repository (recommended) -->

[!DNL Git]이(가) 설치되어 있으면 터미널을 열고 저장소를 복제합니다.

```bash
git clone --branch agentic-dev https://github.com/hlxsites/aem-boilerplate-commerce.git storefront
cd storefront
```

<!-- #### Option B: Download the zip file

If you don't have [!DNL Git] installed:

1. Download the project zip file from: [https://github.com/hlxsites/aem-boilerplate-commerce/archive/refs/heads/agentic-dev.zip](https://github.com/hlxsites/aem-boilerplate-commerce/archive/refs/heads/agentic-dev.zip)
1. Extract the zip file to a folder on your machine.
1. Open your terminal and navigate into the unzipped folder:

   ```bash
   cd path/to/aem-boilerplate-commerce-agentic-dev
   ``` -->

### 루트 종속성 설치

기본 프로젝트 종속성 설치:

```bash
npm install
```

상점 응용 프로그램에 필요한 모든 패키지가 설치됩니다.

### MCP 서버 종속성 설치

MCP 서버 디렉토리로 이동하여 해당 종속성을 설치합니다.

```bash
cd mcp-server
npm install
cd ..
```

<!-- ### Configure environment variables

The MCP server requires certain environment variables to connect to the RAG service.

Create a `.env` file in the `mcp-server` directory:

```bash
cd mcp-server
cp env.example .env
```

Edit the `.env` file and add the following values (we'll provide the actual URL during the lab):

```env
RAG_MODE=worker
WORKER_RAG_URL=<provided-during-lab>
```

>[!NOTE]
>
>The actual value for `WORKER_RAG_URL` will be provided by the lab facilitator at the start of the session. -->

### 커서에서 MCP 활성화

MCP(Model Context Protocol) 서버는 AI 에이전트에게 [!DNL Adobe Commerce] Storefront 설명서에 대한 액세스 권한을 제공합니다.

#### 커서 MCP 설정 열기

![커서 MCP 설정 열기](./assets/cursor-mcp-settings.png){width="600" zoomable="yes"}

1. [!DNL Cursor] 열기
1. **[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Tools & MCP]**(으)로 이동

#### MCP 기능 활성화 및 구성

프로젝트에 `.cursor/mcp.json`에 MCP 구성 파일이 포함되어 있습니다. 이 파일은 로컬 MCP 서버를 사용하도록 이미 구성되어 있어야 합니다.

MCP 구성 확인:

1. commerce-documentation-rag 서버가 나열되고 활성화되어 있는지 확인합니다.

구성은 다음과 유사해야 합니다.

![MCP 구성](./assets/mcp-configuration.png){width="600" zoomable="yes"}

>[!NOTE]
>
>`start-mcp.sh` 스크립트는 `.env` 디렉터리에 있는 `mcp-server` 파일의 환경 변수를 자동으로 로드합니다.

#### 재시작 커서

MCP를 활성화하고 서버를 구성한 후:

1. [!DNL Cursor] 완전히 끝내기
1. [!DNL Cursor]을(를) 다시 열고 `aem-boilerplate-commerce` 프로젝트 열기

#### MCP 연결 확인

MCP 서버가 올바르게 실행 중인지 확인합니다.

1. [!DNL Cursor]에서 새 채팅 열기
1. MCP 서버가 연결되어 있음을 보여주는 표시기를 찾습니다(일반적으로 채팅 인터페이스).
1. &quot;Storefront 문서에서 슬롯에 대한 정보를 검색하십시오&quot;와 같은 질문을 해 보십시오.

MCP 서버가 작동하는 경우 관련 설명서 결과를 볼 수 있습니다.

![MCP 연결 확인됨](./assets/mcp-connection-verified.png){width="600" zoomable="yes"}

### 개발 서버 시작

로컬 개발 서버를 시작합니다.

```bash
npm run start
```

개발 서버가 `http://localhost:3000`에 시작됩니다.

`http://localhost:3000/apparel`의 의류 페이지로 이동합니다.

![실행 중인 개발 서버](./assets/development-server-running.png){width="600" zoomable="yes"}
