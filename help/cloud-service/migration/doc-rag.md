---
title: 설명서 RAG 서비스
description: Adobe Commerce 개발을 위해 AI 기반 설명서 검색 서비스를 사용하는 방법에 대해 알아봅니다.
badgeSaas: label="SaaS만" type="Positive" url="https://experienceleague.adobe.com/ko/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."
role: Developer
hide: true
hidefromtoc: true
source-git-commit: 28396828516645abec3b42a2c6874afe9134dfb8
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 0%

---

# 설명서 RAG 서비스(Beta)

>[!NOTE]
>
>설명서 RAG 서비스는 현재 Beta에 있으며 경험은 변경될 수 있습니다.

설명서 RAG(Retrieval-Augmented Generation) 서비스는 관련 Adobe Commerce 및 App Builder 설명서 전반에서 AI 기반의 의미 체계 검색 기능을 제공합니다.

이 RAG는 Adobe Commerce에 대한 질문을 할 수 있는 IDE 인터페이스를 제공하며 애플리케이션 개발 및 기타 마이그레이션 작업에 대한 모범 사례를 조언할 수 있습니다.

RAG 서비스는 커서 및 기타 MCP 호환 AI 도우미와 통합되는 [Commerce 확장성 도구](./coding-tools.md) MCP(Model Context Protocol) 서버의 일부입니다.

## 사용 가능한 설명서

다음 표에서는 RAG 서비스에서 현재 인덱싱되는 설명서와 관련 인덱스 검색을 트리거하는 데 사용할 수 있는 키워드에 대해 설명합니다. 포함된 설명서는 RAG 서비스를 개발함에 따라 계속 확장될 예정입니다.

| 범주 | 색인 | 포함된 콘텐츠 | 키워드 |
|-------|---------|---------|------------------------|
| [Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=ko) | commerce-storefront-docs | Edge Delivery Services, 드롭인, 상점 첫 화면 구성 요소 | storefront, 드롭인, EDS, 제품 목록, 체크아웃 |
| [확장성](https://developer.adobe.com/commerce/extensibility/) | commerce-extensibility-docs | Webhooks, 이벤트, 확장, 통합 | webhook, 이벤트, 확장, API mesh, GraphQL |
| [Commerce](https://experienceleague.adobe.com/ko/docs/commerce/cloud-service/overview) | commerce-core-docs | 핵심 Commerce(카탈로그, 고객, 주문) | 카탈로그, 제품, 고객, 주문, 재고 |
| [App Builder](https://developer.adobe.com/app-builder/docs/intro_and_overview/) | app-builder-docs | App Builder, 런타임 작업, UI 확장 | 앱 빌더, 런타임 작업, React Spectrum |

인덱스 선택에 대한 자세한 내용은 [자동 인덱스 선택](#automatic-index-selection-recommended) 및 [명시적 인덱스 선택](#explicit-index-selection)을 참조하세요.

각 인덱스에 포함된 설명서에 대한 자세한 내용은 [수집된 소스 목록](https://github.com/adobe-commerce/azure-commerce-documentation-agent/blob/develop/docs/INGESTED_SOURCES.md)을 참조하세요.

## 보안 및 개인 정보 보호

* **IMS 인증** - 모든 API 호출은 Adobe IMS OAuth2 토큰을 사용합니다.
* **데이터 저장소가 없음** - MCP 서버가 자격 증명 또는 데이터를 저장하지 않습니다.
* **로컬 실행** - 모든 도구는 컴퓨터에서 로컬로 실행됩니다.
* **보안 통신** - 문서 검색에서 토큰 유효성 검사와 함께 HTTPS를 사용합니다.

프로덕션 끝점은 [Azure Front Door](https://learn.microsoft.com/en-us/azure/frontdoor/front-door-overview)에 의해 보호되며, 다음 보호가 포함됩니다.

* Microsoft 기본 RuleSet 2.1 및 Bot Manager RuleSet 1.0이 포함된 웹 애플리케이션 방화벽(WAF)
* 미국 수출 금지 지역 (쿠바, 이란, 북한, 시리아, 크림, 루한스크, 도네츠크)
* 에지 부분의 DDoS 보호
* API 관리 백엔드가 잠겨서 프론트도어의 트래픽만 수락합니다.

다양한 보안 요구 사항의 경우 사용자 지정 끝점을 사용할 수 있습니다. 자세한 내용은 [사용자 지정 현관 끝점](#custom-front-door-endpoint)을 참조하십시오.

## 사전 요구 사항

설치하기 전에 다음을 확인하십시오.

* [Node.js](https://nodejs.org/en/download){target="_blank"} 18+(LTS 권장)
* [커서 IDE](https://cursor.com/download){target="_blank"}(권장) 또는 다른 MCP 호환 IDE

  >[!NOTE]
  >
  >다른 MCP 호환 IDE가 지원되지만 최상의 경험을 위해 Cursor가 권장 IDE입니다. 다른 IDE를 사용하는 경우 선택한 IDE에서 작동하도록 설명서의 프롬프트 및 기타 단계를 수정해야 합니다.

## 설치

1. 전체적으로 [Adobe I/O CLI](https://developer.adobe.com/runtime/docs/guides/tools/cli_install/)를 설치합니다.

   ```bash
   npm install -g @adobe/aio-cli
   ```

1. Adobe IMS로 인증:

   ```bash
   aio auth login
   ```

1. Commerce 확장성 도구 저장소를 복제하고 다음 디렉토리로 이동합니다.

   ```bash
   git clone https://github.com/adobe-commerce/commerce-extensibility-tools.git
   cd commerce-extensibility-tools
   ```

1. 종속성 설치:

   ```bash
   npm install
   ```

1. `.cursor/mcp.json` MCP 서버를 포함하도록 Commerce 프로젝트 디렉터리(전역적이지 않음)에서 `commerce-extensibility-tools`을(를) 만들거나 업데이트합니다.

   ```json
   {
     "mcpServers": {
       "commerce-extensibility-tools": {
         "command": "node",
         "args": [
           "/<your-project-directory>/commerce-extensibility-tools/index.js"
         ],
         "env": {
           "NODE_ENV": "production"
         }
       }
     }
   }
   ```

   `<your-project-directory>`을(를) 리포지토리를 복제한 실제 경로로 바꾸십시오.

   >[!NOTE]
   >
   >Windows에서 프로젝트 디렉터리에 경로를 제공하는 데 문제가 발생하면 [경로 문제 해결](#path-issues-windows)을 참조하십시오.

1. Cursor IDE를 다시 시작하여 MCP 서버를 로드합니다.

1. AI 도우미에 요청하여 설치를 확인합니다.

   ```shell-session
   Can you show me the available Adobe Commerce tools?
   ```

## 사용

설치 후 색인을 [자동으로](#automatic-index-selection-recommended) 또는 [명시적으로](#explicit-index-selection)에 호출할 수 있습니다. [`/search-commerce-docs` 명령](#command-based-search)을 사용할 수도 있습니다.

>[!NOTE]
>
>RAG 서비스는 가장 관련성이 높은 상위 5개의 결과를 반환합니다.

### 자동 색인 선택(권장)

Commerce 프로젝트에 대한 자연어 질문을 통해 적절한 설명서 색인을 자동으로 검색하고 관련 정보를 제공합니다.

>[!BEGINSHADEBOX]

다음 프롬프트에서 `commerce-storefront-docs` 인덱스를 자동으로 선택합니다.

```shell-session
"How do I use Edge Delivery Services drop-ins for product listing?"
```

다음 프롬프트에서 `commerce-extensibility-docs` 인덱스를 자동으로 선택합니다.

```shell-session
"How do I create a webhook in Adobe Commerce?"
```

다음 프롬프트에서 `commerce-core-docs` 인덱스를 자동으로 선택합니다.

```shell-session
"How to configure product catalog settings?"
```

다음 프롬프트에서 `app-builder-docs` 인덱스를 자동으로 선택합니다.

```shell-session
"What are App Builder runtime action best practices?"
```

>[!ENDSHADEBOX]

### 명시적 인덱스 선택

또는 프롬프트에서 사용할 색인을 지정할 수 있습니다.

```shell-session
Search commerce-storefront-docs for authentication drop-in
```

```shell-session
Using app-builder-docs, how do I deploy runtime actions?
```

### 명령 기반 검색

RAG 서비스를 사용하려면 `/search-commerce-docs` Cursor 명령을 수동으로 호출하여 프롬프트를 통해 설명서를 검색할 수 있습니다.

```shell-session
/search-commerce-docs "How do I subscribe to Commerce events?"
```

## 사용자 지정 전면 도어 엔드포인트

기본적으로 설명서 검색은 WAF 보호 기능을 사용하여 프로덕션 [Azure Front Door](https://learn.microsoft.com/en-us/azure/frontdoor/front-door-overview) 끝점을 사용합니다. 테스트 또는 개발 목적으로 `FRONT_DOOR_URL` 환경 변수로 재정의할 수 있습니다.

사용자 지정 끝점을 사용하려면 이 끝점을 커서 MCP 구성에 추가하십시오.

```json
{
  "mcpServers": {
    "commerce-extensibility-tools": {
      "command": "node",
      "args": ["/<your-project-directory>/commerce-extensibility-tools/index.js"],
      "env": {
        "NODE_ENV": "production",
        "FRONT_DOOR_URL": "https://<custom-endpoint>.azurefd.net"
      }
    }
  }
}
```

>[!NOTE]
>
>대부분의 개발자는 기본 프로덕션 끝점을 사용해야 하며 `FRONT_DOOR_URL` 변수를 설정할 필요가 없습니다.

## 문제 해결

다음 섹션에서는 설명서 RAG 서비스를 사용할 때 발생할 수 있는 일반적인 문제에 대한 문제 해결 팁을 제공합니다.

### 인증 오류

설명서 검색 도구를 사용하려면 Adobe IMS 인증이 필요합니다. 인증 오류가 발생하면 다음 절차에 따라 문제를 해결하고 해결하십시오.

1. 로그인했는지 확인:

   ```bash
   aio where
   ```

1. IMS 토큰을 볼 수 있는지 확인합니다.

   ```bash
   aio auth login --bare
   ```

1. 인증 오류가 지속되면 로그아웃했다가 다시 로그인하십시오.

   ```bash
   aio auth logout
   aio auth login
   ```

### MCP 서버가 로드되지 않음

MCP 서버가 연결되지 않거나 에이전트가 RAG에 연결할 수 없다고 하는 경우 다음 단계를 사용하여 문제를 해결하고 해결하십시오.

1. **Cmd ,**(macOS) 또는 **Ctrl ,**(Windows 및 Linux)을 사용하여 커서 설정을 엽니다.

1. &quot;MCP&quot;를 검색하고 `commerce-extensibility-tools`이(가) 나열되고 활성화되어 있는지 확인하십시오.

1. MCP 설정 패널에서 오류 메시지를 확인합니다.

1. `mcp.json` 파일이 프로젝트에 있는지 확인합니다.

   ```bash
   cat .cursor/mcp.json
   ```

1. 경로가 올바르고 절대적인지 확인합니다.

   ```bash
   ls -la /<your-project-directory>/commerce-extensibility-tools/index.js
   ```

### 도구를 찾을 수 없음

1. Cursor를 종료하고 다시 엽니다.

1. **Cmd+Shift+P**(macOS) 또는 **Ctrl+Shift+P**(Windows/Linux)을 사용하고 &quot;Developer: Open Logs Folder&quot;를 검색하여 MCP 서버 로그를 Cursor의 개발자 콘솔에 확인합니다.

1. 설치 확인:

   ```bash
   cd commerce-extensibility-tools
   npm install
   node index.js
   ```

   서버는 오류 없이 시작해야 합니다.

### 경로 문제(Windows)

Windows에서는 슬래시 `/` 또는 이스케이프 처리된 백슬래시 `\\`을(를) 사용합니다.

```json
{
  "args": ["C:/Users/yourname/projects/commerce-extensibility-tools/index.js"]
}
```

```json
{
  "args": ["C:\\Users\\yourname\\projects\\commerce-extensibility-tools\\index.js"]
}
```

## 추가 리소스

* [Adobe Commerce 개발자 설명서](https://developer.adobe.com/commerce/docs/){target="_blank"}
* [App Builder 설명서](https://developer.adobe.com/app-builder/docs/){target="_blank"}
* [모델 컨텍스트 프로토콜](https://modelcontextprotocol.io/){target="_blank"}
* [커서 IDE](https://cursor.sh/docs){target="_blank"}
