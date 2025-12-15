---
title: 확장을 위한 AI 코딩 도구
description: Commerce App Builder 확장을 만드는 AI 도구를 사용하는 방법을 알아봅니다.
badgeSaas: label="SaaS만" type="Positive" url="https://experienceleague.adobe.com/ko/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."
role: Developer
hide: true
hidefromtoc: true
source-git-commit: c160632905631949c9503ceaf896b47e7a71fe55
workflow-type: tm+mt
source-wordcount: '1849'
ht-degree: 0%

---

# 확장을 위한 AI 코딩 도구

[!DNL Adobe Commerce as a Cloud Service]&#x200B;(으)로 마이그레이션할 때 AI 코딩 도구를 사용하여 기존 [!DNL Adobe Commerce] PHP 확장을 [!DNL Adobe Developer App Builder] 확장으로 변환할 수 있습니다. 새 [!DNL App Builder] 확장을 만드는 데도 사용할 수 있습니다.

AI 코딩 도구를 사용하면 다음과 같은 이점이 있습니다.

* **향상된 개발 워크플로**: 통합 Adobe Commerce 개발 도구.
* **AI 기반 지원**: 컨텍스트 인식 코드 생성 및 디버깅.
* **Commerce 관련 기능**: Adobe Commerce App Builder 개발을 위한 특수 도구입니다.
* **자동화된 워크플로**: 개발 및 배포 프로세스가 간소화되었습니다.

## 사전 요구 사항

* 다음 코딩 에이전트 중 하나:
   * [커서](https://cursor.com/download)&#x200B;(권장)
   * [Github Copilot](https://github.com/features/copilot)
   * [Google Gemini CLI](https://github.com/google-gemini/gemini-cli)
   * [클라우드 코드](https://www.claude.com/product/claude-code)
* [Node.js](https://nodejs.org/en/download): LTS 버전
* 패키지 관리자: [npm](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm) 또는 [yarn](https://classic.yarnpkg.com/lang/en/docs/install/#mac-stable)
* [Git](https://github.com/git-guides/install-git): 리포지토리 복제 및 버전 제어용

## 설치

1. 전체적으로 최신 [Adobe I/O CLI](https://github.com/adobe/aio-cli)를 설치합니다.

   ```bash
   npm install -g @adobe/aio-cli
   ```

1. 다음 플러그인을 설치합니다.

   * [Adobe I/O CLI Commerce](https://github.com/adobe-commerce/aio-cli-plugin-commerce)
   * [Adobe I/O CLI 런타임](https://github.com/adobe/aio-cli-plugin-runtime)
   * [App Builder CLI](https://github.com/adobe/aio-cli-plugin-app-dev)

   ```bash
   aio plugins:install https://github.com/adobe-commerce/aio-cli-plugin-commerce @adobe/aio-cli-plugin-app-dev @adobe/aio-cli-plugin-runtime
   ```

1. Commerce [통합 시작 키트](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/create-integration)를 복제합니다.

   ```bash
   git clone git@github.com:adobe/commerce-integration-starter-kit.git
   ```

1. Starter Kit 디렉토리로 이동합니다.

   ```bash
   cd commerce-integration-starter-kit
   ```

1. 다음 대화형 설치 명령을 실행하여 Commerce AI 확장성 도구를 설치합니다.

   ```bash
   aio commerce extensibility tools-setup
   ```

설치 프로세스에서 구성 옵션을 묻는 메시지가 표시됩니다. 설치 위치에 대해 &quot;현재 디렉토리&quot;를 선택하여 현재 작업공간에 도구를 설치합니다.

```shell-session
? Where would you like to setup the tools?
❯ Current directory
  New directory
```

Adobe 코딩 에이전트를 선택할 때는 최상의 개발 환경을 위해 `Cursor`을(를) 선택하는 것이 좋습니다.

```shell-session
? Which coding agent would you like to use?
❯ Cursor
  Copilot
  Gemini CLI
  Claude Code
```

Adobe 패키지 관리자를 선택할 때는 일관성을 위해 `npm`을(를) 사용하는 것이 좋습니다.

```shell-session
? Which package manager would you like to use?
❯ npm
  yarn
```

1. 코딩 도구를 성공적으로 설치한 후 설치 프로세스는 다음을 구성합니다.

   * Adobe Commerce 개발을 위한 MCP 서버 통합
   * 향상된 개발 경험을 위한 커서 IDE 규칙
   * Commerce 전용 개발 도구 및 워크플로

   다음 파일이 작업 공간에 추가됩니다.

   **커서**

   * MCP 구성: `.cursor/mcp.json`
   * 규칙 디렉터리: `.cursor/rules/`

   **Copilot**

   * MCP 구성: `.vscode/mcp.json`
   * 규칙 디렉터리: `.github/copilot-instructions.md`

>[!NOTE]
>
>프로젝트를 배포하기 전에 다음 구성 작업을 완료해야 합니다.
>
>* Adobe I/O CLI를 사용하여 [Adobe Developer Console](https://developer.adobe.com/console)에 로그인합니다.
>* App Builder 프로젝트를 만듭니다([프로젝트 설정](https://developer.adobe.com/commerce/extensibility/events/project-setup) 참조).
>* `.env` 파일에서 환경 변수를 설정합니다.
>
>이러한 구성 단계를 수동으로 완료하거나 AI 코딩 도구를 활용하여 프로세스를 안내할 수 있습니다. 자세한 구성 지침은 [통합 만들기](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/create-integration/)를 참조하십시오.

## 설치 후 구성

### [!DNL Adobe I/O CLI]에 로그인

[!DNL Adobe I/O CLI]을(를) 설치한 후 MCP 서버를 사용하려면 언제든지 로그인해야 합니다.

```bash
aio auth login
```

로그인했는지 확인하려면 다음 명령을 실행합니다.

```bash
aio where
```

문제가 발생하면 로그아웃했다가 다시 로그인하십시오.

```bash
aio auth logout
aio auth login
```

>[!NOTE]
>
>MCP 서버의 일부 기능은 로그인하지 않고 작동하지만 RAG(Retrieval-Augmented Generation) 서비스는 작동하지 않습니다. RAG 서비스는 AI 코딩 에이전트에게 전체 Adobe Commerce 설명서 세트에 대한 실시간 액세스를 제공하여 최신 Commerce 개발 사례, API 및 아키텍처 패턴을 기반으로 질문에 답변하고 코드를 생성할 수 있도록 합니다.
>
>향후 릴리스에서는 RAG 서비스를 다른 도구를 설치하지 않고도 독립적으로 액세스할 수 있습니다.

### 커서

1. Cursor IDE를 다시 시작하여 새 MCP 도구 및 구성을 로드합니다.

1. 규칙이 `.cursor/rules/` 폴더 아래에 있는지 확인하여 설치를 확인합니다.

1. MCP 서버 활성화:

   * **Cmd+Shift+P**(macOS) 또는 **Ctrl+Shift+P**(Windows 및 Linux)을 사용하여 커서 MCP 설정을 엽니다.
   * 유형 **보기: MCP 설정 열기**
   * 목록에서 **commerce-extensibility MCP 서버**&#x200B;를 찾습니다.
   * 코딩 도구를 사용하려면 서버 **ON**&#x200B;을(를) 전환하십시오.

1. 서버 상태 확인 - Commerce 확장성 MCP 서버가 다음과 같이 표시되어야 합니다.

   ```shell-session
   Status: Connected/Active
   Server: commerce-extensibility
   Configuration: Automatically configured via .cursor/mcp.json
   ```

1. 다음 프롬프트를 사용하여 에이전트가 MCP 서버를 사용하는지 확인하십시오. 그렇지 않은 경우, 에이전트에게 사용 가능한 MCP 도구를 사용하도록 명시적으로 요청하십시오.

```shell-session
What are the differences between Adobe Commerce PaaS and Adobe Commerce as a Cloud Service when configuring a webhook that activates an App Builder runtime action?
```

### 부조종사

1. Visual Studio 코드를 다시 시작하여 새 MCP 도구 및 구성을 로드합니다.

1. `copilot-instructions.md` 파일이 `.github` 폴더에 있는지 확인하여 설치를 확인합니다.

1. MCP 서버 활성화:

   * 왼쪽 사이드바의 활동 표시줄에서 **확장** 아이콘을 클릭하거나 **Cmd+Shift+X**(macOs) 또는 **Ctrl+Shift+X**(Windows 및 Linux)를 사용하여 확장 패널을 엽니다.
   * **MCP 서버 - 설치됨**&#x200B;을 클릭합니다.
   * **commerce-extensibility MCP 서버** 옆에 있는 톱니바퀴 아이콘을 클릭하고 서버가 중지된 경우 **서버 시작**&#x200B;을 선택합니다.
   * 톱니바퀴 아이콘을 다시 클릭하고 **출력 표시**&#x200B;를 선택합니다.

1. 서버 상태를 확인합니다. `MCP:commerce-extensibility` 출력은 다음과 일치해야 합니다.

   ```shell-session
   2025-11-13 12:58:50.652 [info] Starting server commerce-extensibility
   2025-11-13 12:58:50.652 [info] Connection state: Starting
   2025-11-13 12:58:50.652 [info] Starting server from LocalProcess extension host
   2025-11-13 12:58:50.657 [info] Connection state: Starting
   2025-11-13 12:58:50.657 [info] Connection state: Running
   
   (...)
   
   2025-11-13 12:58:50.753 [info] Discovered 10 tools
   ```

1. 다음 프롬프트를 사용하여 에이전트가 MCP 서버를 사용하는지 확인하십시오. 그렇지 않은 경우, 에이전트에게 사용 가능한 MCP 도구를 사용하도록 명시적으로 요청하십시오.

   ```shell-session
   What are the differences between Adobe Commerce PaaS and SaaS when configuring a webhook that activates an App Builder runtime action?
   ```

## 샘플 프롬프트

다음 샘플 프롬프트는 주문이 있을 때 알림을 전송하는 확장을 만듭니다.

```shell-session
Implement an Adobe Commerce SaaS extension that will send an ERP notification when a customer places an order. The ERP notification must be sent as a POST HTTP call to <ERP URL> with the following details in the request JSON body:

Order ID -> orderID
Order Total -> total
Customer Email ID -> emailID
Payment Type -> pType
```

## 프롬프트 명령

메시지를 표시하는 것 외에도 `/search-commerce-docs` 명령을 사용하여 에이전트와의 대화에서 설명서를 검색할 수 있습니다. For example:

```shell-session
/search-commerce-docs "How do I subscribe to Commerce events?"
```

## 우수 사례

Adobe은 AI 코딩 도구를 사용할 때 다음 모범 사례를 권장합니다.

### 체크리스트

개발 세션을 시작하기 전에:

* `REQUIREMENTS.md` 확인
* MCP 도구가 작동하는지 확인
* 현재 단계 및 목표 검토
* 샘플 코드 또는 스캐폴딩 프로젝트로 시작

개발 중:

* 4단계 [프로토콜](#protocol)을(를) 신뢰합니다.
* 복잡한 개발을 위한 구현 계획 요청
* 사용 가능한 경우 MCP 도구 사용
* 구현 후 각 기능 테스트
* 먼저 로컬에서 테스트한 다음 배포하고 다시 테스트합니다.
* 테스트 지원을 위한 코딩 툴 활용
* 불필요한 복잡성 질문
* 신속한 개발을 위해 점진적으로 구축

새 채팅을 시작할 때:

* 적절한 세션 전달 제공
* `@`이(가) 있는 키 파일 참조
* 세션에 대한 명확한 목표 설정
* 위상 기반 경계 사용

### 워크플로

AI 코딩 도구를 사용하여 개발할 때는 샘플 코드 또는 스캐폴딩 프로젝트로 시작하십시오. 이 접근 방식을 사용하면 처음부터 새로 시작하지 않고 탄탄한 기반을 구축하는 동시에 AI 개발 워크플로를 최적화할 수 있습니다.

또한 Adobe의 템플릿을 활용하고 입증된 패턴 및 아키텍처를 기반으로 하며, 설정된 디렉터리 구조 및 규칙을 유지할 수 있습니다.

시작하려면 다음 리소스를 참조하십시오.

* [통합 시작 키트](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/create-integration)
* [Adobe Commerce 스타터 키트 템플릿](https://github.com/adobe/adobe-commerce-samples/tree/main/starter-kit)
* [Adobe I/O Events 스타터 템플릿](https://experienceleague.adobe.com/ko/docs/commerce-learn/tutorials/adobe-developer-app-builder/io-events/getting-started-io-events)
* [App Builder 샘플 응용 프로그램](https://developer.adobe.com/app-builder/docs/resources/sample_apps)

#### 이러한 리소스를 사용해야 하는 이유

* **입증된 패턴**: 시작 키트는 Adobe의 모범 사례 및 아키텍처 결정을 구현합니다.
* **개발 속도 향상**: 보일러판 및 구성에 소요되는 시간 단축
* **일관성**: 확장이 설정된 규칙을 따르는지 확인합니다.
* **유지 관리**: 표준 패턴을 따르는 경우 유지 관리 및 업데이트가 더 쉬워집니다
* **설명서**: 시작 키트에 예제와 설명서가 함께 제공됩니다
* **커뮤니티 지원**: 표준 접근 방식을 사용할 때 보다 쉽게 도움말을 확인할 수 있습니다.
* **AI 컨텍스트 효율성**: 익숙한 패턴 및 구조를 사용하여 작업함으로써 광범위한 설명의 필요성을 줄이고 코드 생성 정확도를 개선합니다
* **토큰 사용량 감소**: 처음부터 모든 것을 생성하는 대신 기존 패턴을 참조하여 보다 효율적인 대화와 적은 컨텍스트 요약으로 이어집니다.

### 프로토콜

다음 4상 프로토콜은 규칙 시스템에 의해 자동으로 시행된다. 확장을 개발할 때 도구는 이 프로토콜을 자동으로 따라야 합니다.

* 1단계: 요구 사항 분석 및 설명
   * 질문을 명확히 하는 경우 완전한 답변을 제공합니다.
* 2단계: 아키텍처 계획 및 사용자 승인
   * 계획을 제시하면 신중히 검토한 후 승인합니다.
* 3단계: 코드 생성 및 구현
* 4단계: 설명서 및 유효성 검사

### 복잡한 개발을 위한 구현 계획 요청

여러 런타임 작업, 접점 또는 통합이 포함된 복잡한 개발의 경우 AI 도구에서 세부 구현 계획을 생성하도록 명시적으로 요청합니다. [2단계](#protocol)에서 여러 구성 요소가 포함된 높은 수준의 계획이 표시되면 이를 관리 가능한 작업으로 분류하기 위한 자세한 구현 계획을 요청하십시오.

```shell-session
Create a detailed implementation plan for this complex development.
```

복잡한 Adobe Commerce 확장에는 다음과 같은 사항이 자주 포함됩니다.

* 여러 런타임 작업
* 여러 터치포인트에서 이벤트 구성
* 외부 시스템과의 통합
* 상태 관리 요구 사항
* 여러 구성 요소 간 테스트

### MCP 도구 사용

>[!NOTE]
>
>MCP 도구를 사용하기 전에 [Adobe I/O CLI에 로그인했는지 확인](#log-in-to-the-adobe-io-cli)하세요.

툴은 기본적으로 MCP 툴로 설정되지만 특정 상황에서는 CLI 명령을 대신 사용할 수도 있습니다. MCP 도구 사용을 확인하려면 프롬프트에서 명시적으로 요청하십시오.

CLI 명령이 사용되고 있고 MCP 도구를 대신 사용하려면 다음 프롬프트를 사용하십시오.

```shell-session
Use only MCP tools and not CLI commands
```

* MCP 도구: aio-app-deploy, aio-app-dev, aio-dev-invoke
* CLI 명령: aio app deploy, aio app dev

CLI 명령은 다음과 같은 경우에 사용할 수 있습니다.

* 복잡한 배포 시나리오
* 특정 문제 디버깅
* MCP 도구에 제한이 있는 경우
* MCP 통합의 혜택을 받지 못하는 일회성 작업

### 개발

AI 도구로 인해 발생하는 불필요한 복잡성에 의문을 제기하는 것이 중요하다.

단순 읽기 전용 끝점에 대해 불필요한 파일이 추가되면(`validator.js`, `transformer.js`, `sender.js`) 다음 프롬프트를 사용하십시오.

```shell-session
Why do we need these files for a simple read-only endpoint?
Perform a root cause analysis before adding complexity
Verify if simpler solutions exist
```

### 테스트

테스트할 때 다음 모범 사례 사용:

#### 구현 후 각 기능 테스트

구현 계획에서 기능 개발을 완료한 후 즉시 테스트하십시오. 조기 테스트는 복합 문제를 방지하고 디버깅을 더 쉽게 만듭니다.

* 모든 기능이 완료될 때까지 기다리지 마십시오.
* 문제를 조기에 파악하기 위해 점진적으로 테스트
* 다음 기능으로 이동하기 전에 기능 유효성 검사

#### 로컬에서 먼저 테스트

항상 먼저 `aio-app-dev` 도구를 사용하여 로컬에서 테스트하십시오. 이를 통해 즉각적인 피드백을 제공하고 반복 주기를 단축하고 디버깅을 쉽게 할 수 있으며 배포 오버헤드가 발생하지 않습니다.

1. 로컬 개발 서버 시작:

   ```bash
   aio-app-dev
   ```

1. 로컬에서 작업 테스트:

   ```bash
   aio-dev-invoke action-name --parameters '{"test": "data"}'
   ```

#### 배포 및 다시 테스트

로컬 테스트가 성공하면 런타임 환경에서 배포하고 테스트합니다. 런타임 환경은 로컬 개발과 다른 동작을 가질 수 있습니다.

1. 런타임에 배포:

   ```bash
   aio-app-deploy
   ```

1. 배포된 작업 테스트

1. 웹 브라우저 또는 직접 HTTP 요청 사용

1. 디버깅에 대한 활성화 로그 확인

#### 테스트 지원을 위한 코딩 툴 활용

테스트에 대한 도움을 요청합니다. 이 도구는 특정 런타임 작업에 대한 디버깅, 로그 분석 및 적절한 테스트 데이터 작성에 도움이 될 수 있습니다.

**런타임 동작 테스트**:

```shell-session
Help me test the customer-created runtime action running locally
```

**디버그 실패**:

```shell-session
Why did the subscription-updated runtime action activation fail?
```

**로그 확인**:

```shell-session
Help me check the logs for the last stock-monitoring runtime action invocation
```

**테스트 페이로드 만들기**:

```shell-session
Generate test data for this Commerce event
```

```shell-session
Create a test payload for the customer_save_after event
```

**런타임 끝점 찾기**:

```shell-session
What's the URL for this deployed action?
```

**인증 처리**:

```shell-session
How do I authenticate with this external API?
```

**문제 해결**:

```shell-session
Help me debug why this action is returning 500 errors
```

### 디버깅

일이 잘못되었을 때를 멈춰서 평가하라. 문제가 발생하는 경우:

* 중단 및 평가 - 중단 상태에서 계속 진행하지 않음
* 로그 확인 - 활성화 로그를 사용하여 문제 식별
* 간소화 - 복잡성을 제거하여 문제 파악
* 점진적으로 테스트 - 한 번에 한 문제씩 해결
* 유효성 검사 - 계속하기 전에 각 수정 사항 테스트

### 배포

배포 시 다음 모범 사례 사용:

#### 점진적으로 배포

개발 속도를 높이기 위해 수정된 작업만 배포합니다. 이렇게 하면 기존 기능이 손상될 위험이 줄어들고 변경 사항에 대한 피드백이 빨라집니다. 또한 기존 기능을 손상시킬 위험도 줄어듭니다.

* MCP 도구를 사용하여 특정 작업 배포

  ```bash
  aio-app-deploy --actions action-name
  ```

* 로컬에서 테스트한 후 개별 작업 배포
* 점진적으로 배포하고 개발 중에 전체 애플리케이션을 배포하지 않음

#### 런타임 정리

주요 변경 사항 후 도구를 활용하여 고립된 작업을 정리합니다. AI 툴링이 정리 프로세스를 체계적으로 처리할 수 있도록 하면 고립된 작업을 효율적으로 식별하고 상태를 확인하고 수동 개입 없이 안전하게 제거할 수 있습니다.

```shell-session
Help me identify and clean up orphaned runtime actions
```

AI 도구를 요청하여 배포된 작업 나열 및 사용하지 않은 작업 식별

```shell-session
List all deployed actions and identify which ones are no longer needed
```

적절한 명령을 사용하여 AI 도구로 분리된 작업을 제거하도록 합니다.

```shell-session
Remove the orphaned actions that are no longer part of the current implementation
```

### 모니터링

응용 프로그램을 모니터링할 때는 다음 모범 사례를 사용하십시오.

#### 컨텍스트 품질 표시기 감시

* **올바른 컨텍스트**: AI가 최근 결정을 기억하고 올바른 파일을 참조합니다
* **잘못된 컨텍스트**: AI가 이전에 제공한 정보를 요청하고 해결된 문제를 반복합니다

#### 개발 속도 추적

* **고속**: 진행 상황을 지우고 최소한의 확인이 필요합니다.
* **낮은 속도**: 반복된 설명, AI 혼동, 느린 진행

#### 비용 효율성 모니터링

토큰 사용 패턴 추적:

* **효율성**: 토큰 사용량이 적고 컨텍스트 요약이 거의 없습니다.
* **비효율성**: 높은 토큰 사용, 여러 요약, 반복 작업

## 피해야 할 사항

AI 코딩 도구를 사용할 때는 다음과 같은 안티 패턴을 피해야 합니다.

* **설명 단계를 건너뛰지 마십시오** - 구현 전에 항상 1단계가 완료되었는지 확인하십시오.
* **각 기능 후에 테스트를 건너뛰지 마십시오** - 증분 테스트, 모든 작업이 완료될 때까지 기다리지 마십시오.
* **근본 원인 분석 없이 복잡성을 추가하지 마십시오** - 불필요한 파일 추가에 대해 질문하고 적절한 조사를 요청하십시오.
* **실제 데이터 테스트 없이 성공을 선언하지 마십시오** - 항상 경계 사례뿐만 아니라 실제 데이터로 테스트하십시오.
* **런타임 정리를 잊지 마십시오** - 주요 변경 사항 후 항상 분리된 작업을 정리합니다.
