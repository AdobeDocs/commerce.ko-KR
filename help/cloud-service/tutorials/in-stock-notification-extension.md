---
title: 재고 내 알림 확장 프로그램 자습서
description: App Builder, Edge Delivery Services 및 AI 지원 개발 도구를 사용하여 Adobe Commerce as a Cloud Service에 대한 재고 알림 확장을 빌드하는 방법을 알아봅니다.
solution: Commerce
feature: App Builder, Cloud
feature-set: Commerce
role: Developer
level: Intermediate
type: Tutorial
hide: true
hidefromtoc: true
source-git-commit: ce8882b8af21198a7bc57bc58124e8a2d1491a50
workflow-type: tm+mt
source-wordcount: '2599'
ht-degree: 0%

---

# 재고 내 알림 확장 튜토리얼

이 튜토리얼에서는 [!DNL Adobe Commerce as a Cloud Service] 및 AI 지원 개발 도구를 사용하여 [!DNL Adobe App Builder]에 대한 재고 알림 확장을 빌드하는 방법을 안내합니다. 확장 기능을 통해 구매자는 품절 상품에 가입하고 상품이 재입고되는 경우 알림을 받을 수 있습니다.

다음 두 가지 부분을 작성합니다.

- **App Builder 확장** - 이벤트 기반 및 예약된 재고 보충 검색을 사용하여 재고 부족 구독(만들기, 읽기, 삭제)을 관리하기 위한 REST API입니다.
- **Storefront 통합** - 선택한 제품 또는 변형의 재고가 없을 때만 표시되는 PDP(제품 세부 사항 페이지)의 구독 양식입니다.

>[!NOTE]
>
>AI 에이전트는 결정적이지 않습니다. 이 자습서의 프롬프트, 질문 및 출력은 예입니다. 상담원은 다양한 질문, 요구 사항 또는 아키텍처 제안을 제시할 수 있습니다. 이 자습서의 예를 사용하여 에이전트를 유사한 결과로 유도합니다.

시작하기 전에 [필수 구성 요소](./tutorial-prerequisites.md)를 완료하십시오. 이 자습서에서는 **통합 시작 키트**&#x200B;를 사용합니다. 사전 요구 사항 페이지에 설명된 설치 단계를 완료하고 이미 복제했는지 확인합니다.

## 전제 조건 확인

다음 사전 요구 사항이 설치되어 있는지 확인합니다.

```bash
# Check Node.js version (should be 22.x.x)
node --version

# Check npm version (should be 9.0.0 or higher)
npm --version

# Check Git installation
git --version

# Check Bash shell installation
bash --version
```

이전 명령 중 예상한 결과를 반환하지 않는 명령이 있는 경우 [필수 구성 요소](./tutorial-prerequisites.md)를 참조하십시오.

또한 다음을 확인하십시오.

- 제품 데이터가 있는 [!DNL Adobe Commerce as a Cloud Service] 인스턴스가 있습니다. [Commerce Cloud 서비스 인스턴스](https://experienceleague.adobe.com/ko/docs/commerce/cloud-service/overview){target="_blank"}를 참조하세요.
- [!DNL Commerce] 인스턴스에 연결된 Storefront 프로젝트가 있습니다. 항목이 없으면 [상점 만들기](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/?lang=ko){target="_blank"}의 단계를 따릅니다.
- `aem` CLI가 설치되어 있습니다.

  ```bash
  npm install -g @adobe/aem-cli
  ```

## 확장 개발

이 섹션에서는 AI 지원 개발 도구를 사용하여 [!DNL Adobe Commerce as a Cloud Service]에 대한 재고 알림 확장 기능을 개발하는 방법을 안내합니다. 확장은 구독 관리를 위한 REST API를 제공하며 Commerce 이벤트와 예정된 검사를 통해 제품이 재입고되는 시기를 감지합니다.

1. 코딩 에이전트의 MCP 설정으로 이동합니다.

   예를 들어 커서에서 **[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Tools & MCP]**(으)로 이동합니다. `commerce-extensibility` 도구 집합이 오류 없이 사용하도록 설정되어 있는지 확인하십시오. 오류가 표시되면 도구 세트를 끄고 켜십시오.

   >[!NOTE]
   >
   >AI 지원 개발 도구를 사용하여 작업할 때 에이전트가 생성하는 코드 및 응답에서 자연스러운 변형을 예상하십시오.
   >코드에 문제가 발생하는 경우 에이전트에게 디버그를 지원하도록 요청합니다.

1. 커서 컨텍스트에 추가된 설명서가 있는 경우 비활성화합니다.

   **[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Indexing & Docs]**(으)로 이동하여 나열된 설명서를 삭제합니다.

### 1단계: 초기 프롬프트 제공

구현을 시작하라는 메시지를 AI 에이전트에게 표시합니다. 에이전트에게 중지하여 질문하도록 하는 것은 구현을 조기에 제어하는 데 도움이 됩니다.

에이전트의 채팅 창에 다음 메시지를 입력합니다.

```shell-session
Implement an Adobe Commerce as a Cloud Service extension to handle out-of-stock notifications for products.

The service should provide REST API endpoints for basic create, read, update, and delete (CRUD) operations on out-of-stock notifications, allowing storefronts to manage notifications for specific product SKUs.

Back-in-stock is detected by an inventory or product event or a scheduled action that checks Commerce API and then calls the REST API to send the notification.

STOP and ask me any clarifying questions you have about the requirements before you do any work.
```

>[!TIP]
>
>계속하기 전에 에이전트에게 STOP을 알리고 질문하면 프로세스 초기에 구현을 제어할 수 있습니다. 이 프로세스를 통해 주요 가정 및 누락된 요구 사항이 조기에 식별되도록 하고 이 자습서에서 안내식 워크플로우를 시작하는 데 필요합니다.

### 2단계: 에이전트의 질문에 답변

상담원은 솔루션 구성을 시작하기 전에 필요한 일련의 질문과 함께 를 반환합니다. 다음 예제는 일반적인 질문과 답변을 보여 줍니다. 상담원은 다른 질문을 할 수 있지만 주제는 일반적으로 동일합니다.

**에이전트 질문 예:**

1. **REST API — 호스트 및 소비자** — CRUD REST API가 상점 호출을 받는 이 App Builder 앱(예: Adobe I/O Runtime의 웹 작업)의 일부여야 합니까? 이를 누가 EDS Storefront, 맞춤형/헤드리스 상점 또는 둘 다라고 합니까? CORS, 공개(인증되지 않은) 액세스가 필요합니까? 또는 호출자가 API 키, OAuth 또는 Commerce 토큰을 사용합니까?
1. **데이터 모델** — &quot;알림&quot;은 무엇을 나타내야 합니까? 고객 식별자(이메일 전용 또는 고객 ID) 제품 식별자(SKU만 해당 또는 SKU + 스토어 보기) 동일한 고객이 동일한 SKU에 여러 번 가입할 수 있습니까, 아니면 가입이 중복 제거되어야 합니까?
1. **재고 부족 감지 — 이벤트와 예약됨** — 이벤트 기반 감지(Commerce의 인벤토리/제품 이벤트에 반응), 예약된 감지(정기적으로 재고를 확인하는 예약된 작업) 또는 둘 다 수행하시겠습니까? &quot;알림 보내기&quot;는 무엇을 의미합니까(외부 웹후크 호출, 이메일 보내기 또는 로그)?
1. **재고 보충 — Commerce 소스** — 선호하는 이벤트 이름이 있습니까? 아니면 Commerce에서 제공하는 재고/재고 업데이트 이벤트를 디자인에 사용해야 합니까? 예약된 확인의 경우 SKU에서 재고 상태를 가져오는 데 사용해야 하는 API는 무엇입니까?
1. **지속성 및 다중 임차인** — `aio-lib-state`이(가) 구독을 지속하는 올바른 위치입니까? 아니면 외부 저장소가 있습니까? 디자인은 다중 임차인 또는 단일 임차인을 가정해야 합니까?
1. **CRUD 의미 체계 및 주기** — &quot;삭제&quot;는 구독을 취소해야 합니까? &quot;업데이트&quot;가 필요하십니까? 재입고 알림이 전송되면 구독이 자동으로 제거되거나 알림으로 표시되어야 합니까?
1. **작동하지 않음** — 적용되는 비율 제한 또는 최대 구독 수 준수 요구 사항(이중 옵트인, 동의 플래그)이 있습니까?

**예제 답변:**

```shell-session
1. The CRUD REST API should be part of thie App Builder app. It will be called by the EDS Storefront. For this implementation there is no need for API keys or security tokens.
2. For this initial implementation the customer identifier will be the email, product is identified by SKU, customer emails should not be able to subscribe to the same SKU multiple times.
3. Implement both. For now instead of sending the notification, log it so I can audit in the Adobe Developer Console.
4. Research and use what the best event to use that commerce already provides. Research the simplest way to get the stock status by SKU.
5. Use the aio-lib-state. Single tenant for now
6. Delete means cancel subscription. Skip Update, it does not apply for this service. After subscription is sent, it should be marked as notified or removed so it won't send again until the user subscribes again.
7. No limits. Implement minimal compliance requirements.
```

>[!NOTE]
>
>상담원은 다른 질문을 할 수 있습니다. 이러한 답변을 이메일 및 SKU 구독을 통한 REST API, 이벤트 기반 및 예약된 재고 보충 감지, `aio-lib-state` 지속성, 로그 기반 알림 등 동일한 기능 결과를 위한 에이전트 운영 지침으로 사용하십시오.

### 3단계: 요구 사항 및 아키텍처 검토

에이전트는 사용자가 검토할 요구 사항 및 아키텍처 문서를 생성합니다. 요구 사항이 제공된 답변과 일치하고 아키텍처가 다음을 충족하는지 확인합니다.

- 구독 CRUD(만들기, 읽기, 업데이트 및 삭제)에 대한 REST API 작업
- Commerce 인벤토리 이벤트에 의해 트리거된 이벤트 기반 재고 보충 핸들러
- 대체 항목으로 예약된 체크아웃 작업
- `aio-lib-state`을(를) 사용한 지속성

>[!NOTE]
>
>AI 에이전트는 비결정적이며 모델과 IDE에 따라 행동이 다릅니다. 요구 사항 및 아키텍처가 다른 다양한 질문 세트를 받을 수 있습니다. 그렇다면 계속 진행하기 전에 구현이 이 자습서에 제시된 것과 거의 일치하도록 하는 방향으로 에이전트를 제어하십시오.

### 4단계: 구현 계획 선택

에이전트는 자세한 구현 계획을 작성하거나 직접 구현을 완료할 수 있는 옵션을 제공합니다.

- 더 많은 제어로 단계적으로 실행할 수 있는 미리 보기 계획이 필요하면 첫 번째 옵션을 선택합니다.
- 에이전트가 최소한의 개입으로 전체 구현을 수행하도록 하려면 두 번째 옵션을 선택합니다.

### 5단계: 이벤트 배포, 온보드 및 구독

에이전트는 구현을 완료한 후 다음 명령을 사용하여 앱을 배포하고 Commerce 인스턴스를 온보딩하고 이벤트를 구독하는 다음 단계를 제공합니다.

1. 확장 배포:

   ```bash
   aio app deploy
   ```

1. 온보딩 스크립트를 실행하여 이벤트 공급자를 Commerce에 등록합니다.

   ```bash
   npm run onboard
   ```

1. Commerce 이벤트 구독:

   ```bash
   npm run commerce-event-subscribe
   ```

1. 이벤트 구독의 유효성을 검사합니다.

   Commerce 인스턴스로 이동하여 **[!UICONTROL System]** > **[!UICONTROL Event Subscriptions]**&#x200B;을(를) 엽니다.

   이벤트 레코드 테이블이 표시됩니다.

   ![이벤트 구독 섹션을 강조 표시하는 Commerce 관리 메뉴](../assets/in-stock-event-subscriptions.png){width="600" zoomable="yes"}

   ![등록된 이벤트 항목이 있는 이벤트 구독 테이블](../assets/in-stock-event-table.png){width="600" zoomable="yes"}

### 6단계: 확장 테스트

에이전트에게 테스트 단계를 요청하십시오. API 서비스이므로 명령줄 지침을 요청할 수 있습니다.

```shell-session
Give me step by step instructions to test the API service from the command line.
```

에이전트가 제공하는 단계를 따릅니다. 다음 예는 일반적인 테스트 명령을 보여 줍니다.

**SKU 가입:**

```bash
API_URL="https://<your-runtime-url>/api/v1/web/notify-out-of-stock/api"; curl -X POST "$API_URL" \
  -H "Content-Type: application/json" \
  -d '{"email":"test@example.com","sku":"ADB153"}'
```

응답은 다음과 비슷합니다.

```json
{
  "createdAt": "2026-03-06T22:11:00.308Z",
  "email": "test@example.com",
  "id": "b3353bf5-1007-4b10-989d-430892dd4a66",
  "sku": "ADB153"
}
```

**모든 구독 나열:**

```bash
curl -X GET "$API_URL"
```

응답은 모든 활성 구독 목록을 반환합니다.

```json
{
  "subscriptions": [
    {
      "createdAt": "2026-03-06T22:11:00.308Z",
      "email": "test@example.com",
      "id": "b3353bf5-1007-4b10-989d-430892dd4a66",
      "sku": "ADB153"
    }
  ]
}
```

**재고 보충 흐름 테스트:**

1. Commerce 인스턴스에서 구독을 만든 제품을 편집합니다.
1. 제품 재고 상태를 **[!UICONTROL Out of Stock]**(으)로 설정합니다.
1. 1분 정도 기다린 후 재고 상태를 다시 **[!UICONTROL In Stock]**(으)로 전환합니다.

   ![재고 및 재고 부족 옵션이 있는 재고 상태 드롭다운을 표시하는 Commerce 관리 제품 편집 페이지](../assets/in-stock-product-stock-status-toggle.png){width="600" zoomable="yes"}

1. 이벤트가 트리거되고 서비스로 전송될 때까지 약 5분 정도 기다립니다.

1. [!DNL Adobe Developer Console]에서 App Builder 로그 섹션으로 이동합니다.

   ![Adobe Developer Console App Builder 로그 섹션](../assets/in-stock-developer-console-logs.png){width="600" zoomable="yes"}

1. 로그에서 이벤트가 처리되었음을 확인하는 항목이 있고 올바른 이메일-SKU 구독 쌍이 식별되었는지 확인합니다.

   ![다시 시작 이벤트 처리를 보여 주는 App Builder 로그 항목](../assets/in-stock-log-entries.png){width="600" zoomable="yes"}

>[!TIP]
>
>알림 작업이 성공적으로 기록되었는지 확인하기 위해 에이전트에게 로그에서 찾을 내용을 요청할 수 있습니다. 로그 항목을 복사하여 붙여넣어 에이전트가 확인을 수행하도록 할 수도 있습니다.

재입고 이벤트 처리 후 알림 구독이 제거되므로 구독 목록을 요청하면 항목 수가 한 개 줄어듭니다.

### 서비스 계약 만들기

서비스 구현이 완료되었으므로 이제 에이전트에게 Storefront 작업에 대한 서비스 계약을 작성하도록 요청하십시오.

```shell-session
Create an API service contract for the Out of Stock notification service and its endpoints. Ensure that the service contract is clear and detailed enough for a frontend developer to implement the storefront UI integration without needing to ask additional questions about the API. Name this file OUT_OF_STOCK_NOTIFICATION_CONTRACT.md
```

Storefront 에이전트가 참조할 수 있도록 이 파일을 Storefront 프로젝트에 복사합니다.

## 상점 앞에 연결

이 섹션에서는 [!DNL Edge Delivery Services] 및 AI 지원 개발 도구를 사용하여 재고 알림 확장의 상점 첫 부분을 구현하는 방법을 안내합니다. 선택한 제품 또는 변형의 재고가 없을 때만 표시되는 PDP(제품 세부 사항 페이지)에 구독 양식을 추가합니다.

>[!NOTE]
>
>제공된 프롬프트는 시작점입니다. 수정 없이 사용할 수 있지만 에이전트와 자연스럽게 대화하는 것을 고려합니다.
>
>AI 지원 개발 도구를 사용하여 작업할 때 에이전트가 생성하는 코드 및 응답에는 항상 자연스러운 변형이 있습니다.
>
>코드에 문제가 발생하는 경우 에이전트에게 디버그를 지원하도록 요청합니다.

### Storefront 사전 요구 사항

Storefront 통합을 시작하기 전에 다음을 확인하십시오.

- [!DNL Commerce] 인스턴스에 연결된 Storefront 프로젝트
- Commerce storefront AI 도구 [CLI를 사용하여 설치](./tutorial-prerequisites.md#install-the-storefront-ai-tools)
- `OUT_OF_STOCK_NOTIFICATION_CONTRACT.md` 파일이 상점 프로젝트에 복사되었습니다.

### 1단계: 환경 유효성 검사

`config.json` 파일을 열고 `commerce-core-endpoint` 및 `commerce-endpoint`의 값이 [!DNL Adobe Commerce as a Cloud Service] GraphQL 끝점을 가리키는지 확인하십시오.

```json
"commerce-core-endpoint": "https://na1-sandbox.api.commerce.adobe.com/<your-instance-id>/graphql",
"commerce-endpoint": "https://na1-sandbox.api.commerce.adobe.com/<your-instance-id>/graphql",
```

### 2단계: 초기 프롬프트 제공

프로젝트에 이미 서비스 계약이 있는 경우, 제품 세부 사항 페이지에서 UI를 만들라는 메시지를 에이전트에게 보냅니다. 에이전트에서 사용 가능한 경우 **계획** 모드를 사용하여 에이전트가 계획 없이 진행되지 않도록 합니다.

```shell-session
Analyze @OUT_OF_STOCK_NOTIFICATION_CONTRACT.md. Add a form for subscribing to a notification for when a product is back in stock. Place this form on the product details page, underneath the add to cart and wishlist button. The form only displays when a product is out of stock. 

Use the project manager skill to plan this implementation.
```

>[!TIP]
>
>특히 프로젝트 관리자 스킬 사용을 요청하면 프로세스 초기에 구현을 제어하는 데 도움이 되는 단계별 워크플로우를 트리거합니다. 이 프로세스를 통해 주요 가정 및 누락된 요구 사항이 조기에 식별되도록 하고 에이전트에게 원래 프롬프트에서 제공하지 않았을 수 있는 세부 정보 및 요구 사항을 제공할 수 있는 기회를 제공합니다.

### 3단계: 계획 관련 질문에 답변하기

에이전트가 솔루션 구성을 시작하기 전에 답변해야 하는 일련의 질문과 함께 반환됩니다. 다음 예제는 일반적인 질문과 답변을 보여 줍니다. 상담원은 다른 질문을 할 수 있지만 주제는 일반적으로 동일합니다.

**에이전트 질문 예:**

1. **API 기본 URL** — 상점 첫 화면에서 Notify-Out-of-Stock API 기본 URL을 가져오는 방법은 무엇입니까? 옵션에는 구성 블록(예: `out-of-stock-api-base-url`이 있는 테이블), 전역 자리 표시자 또는 환경 변수 또는 다른 접근 방식이 포함될 수 있습니다.
1. **복사** — 구현이 성공 및 오류 메시지(예: 로컬라이제이션)에 자리 표시자를 사용해야 합니까? 아니면 이 구현에 정적 영어를 사용해야 합니까?
1. **가입이 성공한 후** — 양식을 숨기고 &quot;가입했습니다&quot;(A), 양식을 표시하지만 그 위에 성공 메시지가 있거나 다른 동작(B)이 있거나 사용할 수 없도록 설정해야 합니까?
1. **구성 가능한 제품** — 선택한 변형의 `inStock` 값을 기반으로 양식을 표시해야 하므로 선택한 변형의 재고가 부족한 경우 표시됩니다.

**예제 답변:**

```shell-session
1. Global placeholder with baseurl value of `https://<your-runtime-url>/api/v1/web/notify-out-of-stock/api`
2. Use placeholders with static English fallback
3. B
4. Use selected variant's inStock value
```

>[!NOTE]
>
>`<your-runtime-url>`을(를) App Builder 배포의 실제 [!DNL Adobe I/O Runtime] URL로 바꾸십시오.
>
>상담원은 다른 질문을 할 수 있습니다. 다음 답변을 지침으로 사용하십시오.
>
>- 코드를 수정하지 않고 변경할 수 있도록 API 기본 URL에 대한 전역 자리 표시자를 사용합니다.
>- 대체 요소로서 정적 영어를 사용하는 사용자 대면 사본에 자리 표시자를 사용합니다.
>- 가입이 성공하면 양식이 표시되지만 그 위에 성공 메시지가 표시되어 비활성화됩니다.
>- 구성 가능한 제품의 경우 선택한 변형의 `inStock` 값을 사용하여 양식 가시성을 제어하십시오.

### 4단계: 요구 사항 및 아키텍처 검토

에이전트는 사용자가 검토할 수 있도록 요구 사항 문서를 업데이트합니다. 다음을 확인합니다.

- 제품 또는 선택한 변형의 재고가 없을 때만 양식이 표시됩니다.
- 양식은 PDP의 장바구니에 추가 및 위시리스트 단추 아래에 배치됩니다.
- API 통합에서는 전역 자리 표시자의 기본 URL을 사용합니다.
- 성공 및 오류 상태는 계약에 따라 처리됩니다(201, 409, 400, 503/500).

>[!NOTE]
>
>AI 에이전트는 비결정적이며 모델과 IDE에 따라 행동이 다릅니다. 요구 사항 및 아키텍처가 다른 다양한 질문 세트를 받을 수 있습니다. 그렇다면 계속 진행하기 전에 구현이 이 자습서에 제시된 것과 거의 일치하도록 하는 방향으로 에이전트를 제어하십시오.

**2단계(아키텍처 계획)**&#x200B;에서 에이전트는 아키텍처를 제안하기 전에 설명서와 코드베이스를 조사합니다. 에이전트는 다음을 수행합니다.

- [!DNL Commerce] 설명서에서 PDP 드롭 인 컨테이너, 슬롯 및 이벤트 페이로드를 검색합니다.
- `blocks` 디렉터리 및 `scripts/initializers/` 폴더에서 기존 PDP 관련 코드를 검색합니다.
- 사용 가능한 컨테이너 및 슬롯 컨텍스트 셰이프에 대한 TypeScript 정의를 살펴보십시오.

그러면 에이전트가 아키텍처 옵션을 제공합니다. 계획을 검토하고 에이전트에게 계속 진행하도록 지시합니다.

### 5단계: 구현 계획 선택

에이전트는 자세한 구현 계획을 작성하거나 직접 구현을 완료할 수 있는 옵션을 제공합니다.

- 더 많은 제어로 단계적으로 실행할 수 있는 미리 보기 계획이 필요하면 첫 번째 옵션을 선택합니다.
- 에이전트가 최소한의 개입으로 전체 구현을 수행하도록 하려면 두 번째 옵션을 선택합니다.

**4단계(구현)** 동안 에이전트는 선택한 아키텍처를 기반으로 코드를 생성합니다. 접근 방식에 따라 에이전트는 다음과 같은 몇 가지 전문 기술을 사용합니다.

- **콘텐츠 모델링:** 새 블록이 필요한 경우 에이전트는 작성자에게 친숙한 콘텐츠 구조를 디자인합니다.
- **블록 개발:** 에이전트는 JavaScript 데코레이션 기능, 범위 CSS 스타일, 접근성을 위한 ARIA 레이블, 로드 및 오류 상태 처리 등 [!DNL Edge Delivery Services] 규칙에 따라 블록 파일을 만듭니다.
- **드롭인 사용자 지정:** 아키텍처가 슬롯 사용자 지정을 사용하는 경우 에이전트는 올바른 컨테이너를 가져오고 제품 제목 근처에 있는 확인된 슬롯을 사용하며 현재 SKU의 제품 데이터 이벤트를 구독합니다.

생성되는 코드를 시청하고 필요한 경우 질문하거나 에이전트를 리디렉션합니다.

### 6단계: 서버 시작 및 테스트

에이전트가 구현을 완료한 후 개발 서버를 시작하고 양식을 테스트합니다.

1. 로컬 개발 서버를 시작합니다.

   ```bash
   npm run start
   ```

1. 브라우저에서 품절 제품 페이지로 이동합니다. For example:

   ```shell-session
   http://localhost:3000/products/<out-of-stock-product-slug>/<sku>
   ```

1. 장바구니에 추가 및 위시리스트 단추 아래에 구독 양식이 표시되는지 확인합니다.

수동 테스트를 수행하거나 에이전트에게 브라우저 기능을 사용하여 테스트하도록 요청할 수 있습니다.

```shell-session
Run complete browser testing. Use the following out of stock product 'http://localhost:3000/products/<out-of-stock-product-slug>/<sku>'
```

![장바구니에 추가 단추 아래에 재고 부족 알림 양식을 표시하는 제품 세부 정보 페이지](../assets/in-stock-notification-form.png){width="600" zoomable="yes"}

### 7단계: 정리

테스트를 건너뛰거나 완료한 후 에이전트는 마지막 **정리** 단계로 진행하라는 메시지를 표시합니다. 확인 시 에이전트는 구현 중에 생성된 모든 문서 객체를 보관합니다.

## 문제 해결

자습서 도중 문제가 발생하는 경우 다음 팁을 사용하십시오.

- **API 오류:** CLI를 사용하여 동작을 확인하기 위해 API로 직접 요청을 보냅니다. 예를 들어 `curl`을(를) 사용하여 각 끝점을 독립적으로 테스트하십시오.
- **에이전트 오류:** 문제를 디버깅하는 데 도움이 되도록 에이전트 채팅 세션에 오류 메시지를 복사하여 붙여 넣으십시오. 에이전트는 환경 변수 누락 또는 잘못 구성된 작업과 같은 일반적인 문제를 진단할 수 있습니다.
- **이벤트 파이프라인:** 재고 부족 이벤트가 트리거되지 않으면 온보딩 및 이벤트 구독 단계를 완료했는지 확인하십시오. `workspace.json`이(가) 올바른 위치에 있고 Commerce 이벤트 모듈이 활성화되어 있는지 확인하십시오.
- **재고 상태 페이로드:** Commerce에서 `is_in_stock`을(를) 부울(`"1"`) 대신 문자열(`true`)로 보낼 수 있습니다. 재고 보충 핸들러가 트리거되지 않는 경우 에이전트에게 엄격한 유형 비교에 대해 소비자 코드를 확인하고 두 형식을 모두 처리하도록 업데이트하도록 요청합니다.

## 튜토리얼 요약

다음은 이 자습서에서 다루는 항목에 대한 요약입니다.

- **확장 개발:** AI 에이전트에 대한 새로운 기능을 설명하고 [!DNL App Builder]을(를) 사용하여 CRUD 작업으로 작동하는 REST API를 생성합니다.
- **이벤트 기반 아키텍처:** Commerce 이벤트 및 예약된 작업을 구성하여 제품의 재입고 시기를 감지합니다.
- **로컬 테스트 및 배포:** `curl`(으)로 API 테스트 및 [!DNL Adobe I/O CLI]&#x200B;(으)로 배포
- **서비스 계약:** 백엔드 확장 및 상점 구현을 연결하는 API 계약을 만듭니다.
- **단계적 상점 통합:** AI 지원 기술을 사용하여 요구 사항, 아키텍처 및 구현 작업을 수행합니다.
- **드롭인 통합:** [!DNL Adobe Commerce] 드롭인 컨테이너 및 슬롯을 사용하여 PDP에 구독 양식을 추가합니다.

## 다음 단계

재고 알림 서비스를 확장하려면 다음 제안을 사용하십시오.

- **실제 알림 보내기:** 로그 기반 알림을 [!DNL Adobe Campaign] 또는 타사 공급자와 같은 전자 메일 서비스로 바꿉니다.
- **구독 관리 페이지 추가:** 구매자가 활성 구독을 보고 취소할 수 있는 상점 페이지를 만듭니다.
- **다중 테넌트 배포 지원:** 상태 관리를 확장하여 단일 App Builder 앱에서 여러 Commerce 테넌트를 지원합니다.
- **속도 제한 추가:** 남용을 방지하기 위해 구독 API에 대한 속도 제한을 구현합니다.
