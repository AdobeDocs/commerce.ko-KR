---
title: 게재 예상 확장 튜토리얼
description: App Builder, Edge Delivery Services 및 AI 지원 개발 도구를 사용하여 Adobe Commerce as a Cloud Service에 대한 게재 날짜 예상 확장을 빌드하는 방법을 알아봅니다.
solution: Commerce
feature: App Builder, Cloud
feature-set: Commerce
role: Developer
level: Intermediate
type: Tutorial
hide: true
hidefromtoc: true
source-git-commit: 3fc8982613df7b1155cdfb08ac4b56de6d1ce4f6
workflow-type: tm+mt
source-wordcount: '3334'
ht-degree: 0%

---

# 게재 예상 확장 튜토리얼

이 자습서에서는 [!DNL Adobe Commerce as a Cloud Service], [!DNL Adobe App Builder] 및 AI 지원 개발 도구를 사용하여 [!DNL Edge Delivery Services]에 대한 게재 날짜 예상 확장을 빌드하는 과정을 안내합니다. 확장은 외부 API의 배송 시간 및 배송 날짜 예상치를 가져와서 상점 전체에 표시합니다.

다음 두 가지 부분을 작성합니다.

- **App Builder 확장** — 외부 게재 예상 API를 래핑하는 BFF(Backend-for-Frontend) 작업, 체크아웃 시 게재 날짜를 포함하는 다양한 전달 방법을 제공하는 웹후크 및 다시 배포하지 않고 설정을 관리하는 관리 UI 구성 페이지입니다.
- **Storefront 통합** — [!DNL Edge Delivery Services] 드롭 인 구성 요소와 공유 클라이언트 모듈을 사용하여 PDP(제품 세부 사항 페이지), 장바구니 페이지 및 체크아웃 페이지에 표시되는 게재 날짜 예상치입니다.

>[!NOTE]
>
>AI 에이전트는 결정적이지 않습니다. 이 자습서의 프롬프트, 질문 및 출력은 예입니다. 상담원은 다양한 질문, 요구 사항 또는 아키텍처 제안을 제시할 수 있습니다. 이 자습서의 예를 사용하여 에이전트를 유사한 결과로 유도합니다.

시작하기 전에 [필수 구성 요소](./tutorial-prerequisites.md)를 완료하십시오. 이 자습서에서는 **체크아웃 시작 키트**&#x200B;를 사용합니다. 사전 요구 사항 페이지에 설명된 설치 단계를 완료하고 이미 복제했는지 확인합니다.

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

- **쇼핑객 계정**&#x200B;이 있습니다. 기본 배송 주소가 저장된 [!DNL Commerce]에 등록된 고객입니다. PDP 및 장바구니 페이지의 예상 게재는 로그인한 구매자에게만 표시됩니다. 체크아웃 시 인증 상태에 관계없이 모든 구매자에 대한 예상 값이 표시됩니다.

>[!IMPORTANT]
>
>이 자습서에서는 **체크아웃 스타터 키트**(통합 스타터 키트가 아님)를 사용합니다. Checkout Starter Kit은 결제, 배송, 세금 및 이벤트에 대한 웹후크 기반의 확장성을 제공합니다. 체크아웃 키트에서 부트스트랩해야 합니다.

## 모의 게재 예상 API 설정

확장은 외부 게재 예상 API를 호출하여 배송 날짜 및 시간 예상치를 가져옵니다. 이 자습서에서는 모의 API를 사용하여 실제 통신사 계정 없이 전체 흐름을 실행할 수 있습니다. 두 가지 옵션을 사용할 수 있습니다.

- **옵션 A: Pipedream 워크플로** — 프리 티어, 빠른 설정이지만 월별 호출 제한이 있습니다.
- **옵션 B: App Builder 런타임 작업** — 백엔드 개발 단계 중에 생성된 외부 종속성이 없습니다.

>[!TIP]
>
>개발 중에 프리 티어 호출 할당량에 도달한 경우 Pipedream(옵션 A)으로 시작하고 런타임 작업(옵션 B)으로 전환할 수 있습니다. 두 옵션 모두 동일한 API 계약을 구현합니다.

### API 사양

모의 API는 POST 요청을 수락하고 통신사, 환승 일수, 컷오프 시간 및 최적 추정치와 함께 게재 날짜 추정치를 반환합니다.

**요청 본문**(모든 필드는 모음에 선택 사항):

```json
{
  "origin": { "country_code": "US", "postal_code": "90210", "city": "Beverly Hills" },
  "destination": { "country_code": "US", "postal_code": "10001", "city": "New York" },
  "ship_date": "2026-03-10",
  "carriers": ["standard", "express"],
  "service_levels": ["standard", "express"]
}
```

**응답(200 OK):**

```json
{
  "estimates": [
    {
      "carrier_code": "standard",
      "service_code": "ground",
      "delivery_date": "2026-03-14",
      "safe_delivery_date": "2026-03-15",
      "transit_days": 4,
      "cutoff_datetime_utc": "2026-03-10T17:00:00.000Z"
    },
    {
      "carrier_code": "express",
      "service_code": "2day",
      "delivery_date": "2026-03-12",
      "safe_delivery_date": "2026-03-12",
      "transit_days": 2,
      "cutoff_datetime_utc": "2026-03-10T12:00:00.000Z"
    }
  ],
  "best_estimation": { "carrier_code": "express", "delivery_date": "2026-03-12", "transit_days": 2 }
}
```

**오류 응답:** 401(누락/잘못된 API 키), 400(잘못된 `ship_date` 형식), 503(시뮬레이션된 가동 중지 시간).

### 모의 설정

>[!BEGINTABS]

>[!TAB Pipedream 워크플로]

Pipedream 옵션은 전달자 토큰 인증을 사용하고 워크플로우 트리거 URL에 대한 POST 요청을 수락합니다.

| 항목 | 설명 |
|------|-------------|
| 기본 URL | 전체 Pipedream 워크플로 트리거 URL(예: `https://<id>.m.pipedream.net`) |
| 인증 | `Authorization: Bearer <API_KEY>` |
| 방법 | POST |

{style="table-layout:auto"}

**워크플로 만들기:**

1. [Pipedream](https://pipedream.com){target="_blank"}에서 새 워크플로우를 만듭니다(**[!UICONTROL Workflows]** > **[!UICONTROL New Workflow]**).

1. POST에 대해 구성된 **HTTP/Webhook** 트리거를 추가합니다. Pipedream이 웹후크 URL을 할당합니다.

1. **Node.js 코드 실행** 단계를 추가하고 다음 처리기 코드를 붙여넣습니다.

   ```javascript
   const DEFAULT_CARRIERS = [
     { carrier_code: "standard", service_code: "ground", transit_days: 4 },
     { carrier_code: "express", service_code: "2day", transit_days: 2 },
     { carrier_code: "priority", service_code: "overnight", transit_days: 1 },
   ];
   
   const ISO_DATE = /^\d{4}-\d{2}-\d{2}$/;
   
   function parseShipDate(shipDate) {
     if (shipDate == null || typeof shipDate !== "string") return null;
     if (!ISO_DATE.test(shipDate)) return null;
     const d = new Date(shipDate + "T12:00:00.000Z");
     if (Number.isNaN(d.getTime())) return null;
     return shipDate;
   }
   
   function addBusinessDays(isoDate, days) {
     const d = new Date(isoDate + "T12:00:00.000Z");
     let added = 0;
     while (added < days) {
       d.setUTCDate(d.getUTCDate() + 1);
       const dow = d.getUTCDay();
       if (dow !== 0 && dow !== 6) added += 1;
     }
     return d.toISOString().slice(0, 10);
   }
   
   function cutoffUtc(isoDate, hour = 17) {
     return `${isoDate}T${String(hour).padStart(2, "0")}:00:00.000Z`;
   }
   
   function getBearerToken(headers) {
     const auth = headers?.Authorization ?? headers?.authorization ?? "";
     if (typeof auth !== "string" || !auth.startsWith("Bearer ")) return null;
     return auth.slice(7).trim() || null;
   }
   
   function handleDeliveryEstimate(body) {
     const shipDate = parseShipDate(body?.ship_date);
     const baseDate = shipDate ?? new Date().toISOString().slice(0, 10);
     let carriers = DEFAULT_CARRIERS;
     if (Array.isArray(body?.carriers) && body.carriers.length > 0) {
       const set = new Set(body.carriers.map((c) => String(c).toLowerCase()));
       carriers = DEFAULT_CARRIERS.filter((c) => set.has(c.carrier_code.toLowerCase()));
     }
     if (Array.isArray(body?.service_levels) && body.service_levels.length > 0) {
       const set = new Set(body.service_levels.map((s) => String(s).toLowerCase()));
       carriers = carriers.filter(
         (c) => set.has(c.service_code.toLowerCase()) || set.has(c.carrier_code.toLowerCase())
       );
     }
     if (carriers.length === 0) {
       return { status: 200, body: { estimates: [], best_estimation: null } };
     }
     const estimates = carriers.map((c) => {
       const delivery_date = addBusinessDays(baseDate, c.transit_days);
       const safe_delivery_date = addBusinessDays(baseDate, c.transit_days + 1);
       const cutoff_datetime_utc = cutoffUtc(baseDate, 17 - c.transit_days);
       return {
         carrier_code: c.carrier_code,
         service_code: c.service_code,
         delivery_date,
         safe_delivery_date,
         transit_days: c.transit_days,
         cutoff_datetime_utc,
       };
     });
     return { status: 200, body: { estimates, best_estimation: estimates[0] } };
   }
   
   export default defineComponent({
     async run({ steps, $ }) {
       const event = steps.trigger?.event ?? steps.trigger ?? {};
       const body = event.body ?? {};
       const headers = event.headers ?? {};
       const auth = getBearerToken(headers);
       const expectedKey =
         (typeof process.env.MOCK_API_KEY === "string" && process.env.MOCK_API_KEY.trim()) || null;
       if (expectedKey && (!auth || auth !== expectedKey)) {
         await $.respond({
           immediate: true,
           status: 401,
           headers: { "Content-Type": "application/json" },
           body: { error: "unauthorized", message: "Missing or invalid API key." },
         });
         return;
       }
       if (body?.ship_date != null && !parseShipDate(body.ship_date)) {
         await $.respond({
           immediate: true,
           status: 400,
           headers: { "Content-Type": "application/json" },
           body: { error: "bad_request", message: "Invalid ship_date; use YYYY-MM-DD." },
         });
         return;
       }
       const { status, body: responseBody } = handleDeliveryEstimate(body);
       await $.respond({
         immediate: true,
         status,
         headers: { "Content-Type": "application/json" },
         body: responseBody,
       });
     },
   });
   ```

1. (선택 사항) 전달자 토큰 인증을 적용하려면 워크플로 설정에 `MOCK_API_KEY` 환경 변수를 추가하십시오. 설정하지 않으면 모든 요청이 수락됩니다.

1. 워크플로우를 배포합니다.

   엔드포인트는 웹후크 트리거 URL입니다.

**모의 테스트:**

```bash
curl -X POST \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer mock-api-key" \
  -d '{"destination": {"country_code": "US", "postal_code": "10001"}}' \
  "https://<your-endpoint>.m.pipedream.net"
```

>[!TAB App Builder 런타임 작업]

App Builder 런타임 작업 옵션은 동일한 [!DNL App Builder] 프로젝트 내에서 모의 작업을 런타임 작업으로 배포합니다. 이 방법에는 외부 종속성이 없으며 호출 할당량이 없습니다.

에이전트에게 모의 작업을 만들라는 메시지를 표시합니다.

```shell-session
Add a new runtime action to this project that implements the API in @docs/PIPEDREAM_API_SPEC.md
- Add it to a separate package
- Use the code in docs/pipedream as inspiration
```

에이전트는 Pipedream 옵션과 동일한 API 계약을 사용하여 `actions/mock-delivery-api/index.js`을(를) 만듭니다. 배포 후 끝점은 다음과 같습니다.

```shell-session
https://<namespace>.adobeioruntime.net/api/v1/web/mock-delivery-api/delivery-estimate
```

`MOCK_API_KEY`의 `.env` 환경 변수에 대해 인증이 확인되었습니다.

>[!ENDTABS]

## 확장 개발

이 섹션에서는 게재 예상 확장을 위한 [!DNL App Builder] 백엔드를 개발하는 방법을 안내합니다. 백엔드는 다음 세 가지 작업을 제공합니다.

| 액션 | 유형 | 목적 |
|--------|------|---------|
| `delivery-estimates` | 독립 실행형 웹 작업 | BFF for storefront — PDP and cart는 배달 날짜에 대해 이를 호출합니다. |
| `shipping-methods` | Webhook 작업 | 체크아웃 시 `additional_data`의 배송 날짜를 통해 배송율을 높임 |
| `delivery-estimates-config` | 관리 백엔드 작업 | `aio-lib-state`에 저장된 구성에 대한 CRUD |

{style="table-layout:auto"}

1. 코딩 에이전트의 MCP 설정에서 `commerce-extensibility` 도구 집합이 오류 없이 사용하도록 설정되어 있는지 확인하십시오.

   예를 들어 커서에서 **[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Tools & MCP]**(으)로 이동합니다.

   오류가 표시되면 도구 세트를 끄고 켜십시오.

   >[!NOTE]
   >
   >AI 지원 개발 도구를 사용하여 작업할 때 에이전트가 생성하는 코드 및 응답에서 자연스러운 변형을 예상하십시오.
   >코드에 문제가 발생하는 경우 에이전트에게 디버그를 지원하도록 요청합니다.

1. 커서 컨텍스트에 추가된 설명서가 있는 경우 비활성화합니다.

   **[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Indexing & Docs]**(으)로 이동하여 나열된 설명서를 삭제합니다.

### 1단계: 초기 프롬프트 제공

에이전트에 컨텍스트에 대한 외부 API 사양을 지정하고 시작하라는 메시지를 표시합니다. 에이전트에게 중지하여 질문하도록 하는 것은 구현을 조기에 제어하는 데 도움이 됩니다.

에이전트의 채팅 창에 다음 메시지를 입력합니다.

```shell-session
I want to build an Adobe App Builder extension that extends the checkout with shipping date and time estimates taken from an external API described in @docs/API_SPEC.md.
Delivery dates for a product will be shown in the product details page and on the cart page.
Implement this feature by using the skills in this workspace for backend code, and a separate workspace with storefront skills. For this extension, focus on the backend skills and create an API_SPEC to hand work over to the storefront skills.

STOP and ask me clarifying questions about the requirements before you do any work.
```

>[!TIP]
>
>프롬프트에서 외부 API 사양 파일(`@docs/API_SPEC.md`)을 참조하면 서드파티 API 계약에 대한 구체적인 컨텍스트가 에이전트에 제공됩니다. 에이전트는 이 옵션을 사용하여 BFF 작업, 공유 HTTP 클라이언트 및 관리 UI 구성 필드를 디자인합니다. 에이전트에게 STOP과 ASK를 지시하는 것은 안내가 있는 워크플로우를 트리거하며 구현을 조기에 제어하는 데 도움이 됩니다.

### 2단계: 에이전트의 질문에 답변

에이전트는 대상 환경(PaaS 및 SaaS), 범위(독립형 BFF 작업, 웹후크 보강 또는 둘 다), 원본 주소 소스, 캐싱 전략 및 테스트 환경 설정과 같은 주제를 다루는 일련의 명확한 질문과 함께 반환됩니다. 다음 예제는 일반적인 질문과 답변을 보여 줍니다. 상담원은 다른 질문을 할 수 있지만 주제는 일반적으로 동일합니다.

**에이전트 질문 예:**

1. **Target 환경** — PaaS(온-프레미스) 또는 SaaS(Adobe Commerce as a Cloud Service)용으로 빌드하고 있습니까?
2. **범위** — 독립 실행형 BFF 작업(Storefront에서 직접 호출), Webhook 강화(체크아웃 시 배송 방법 확장) 또는 둘 다여야 합니까?
3. **관리자 구성 기능** — API URL, API 키 및 원본 주소와 같은 설정을 Commerce 관리자를 통해 구성할 수 있거나 `.env`에 저장해야 합니까?
4. **원본 주소** — 배송 원본(창고) 주소는 어디에서 가져오나요? 정적 구성이어야 합니까? 아니면 동적으로 해결해야 합니까?
5. **캐싱** — 외부 API에 대한 호출을 줄이기 위해 서버 측에서 게재 예상 값이 캐시되어야 합니까? 그렇다면 TTL은 무엇입니까?

**예제 답변:**

```shell-session
Clarifications:
1. Let's build for SaaS
2. Let's do this:
(A) Can the PDP/cart call the 3rd party API directly — or are there any benefits of wrapping this call with a runtime action?
(B) Let's use the shipping-methods webhook
3. Let's use a Single-page application (SPA) that uses the Admin UI SDK to integrate with the admin. Since we are adding this config screen, let's make anything else that makes sense configurable to avoid redeployments when changing settings
4. Static configuration — origin address should be configurable in the Admin UI (e.g. warehouse address)
5. Yes, cache on the server side; suggest a TTL (e.g. 30 minutes) and make it configurable in the Admin UI
```

>[!TIP]
>
>대리점이 서드파티 API를 직접 호출할지 또는 런타임 작업을 수행할지 여부를 묻는 것은 유용한 아키텍처 토론을 트리거합니다. 에이전트는 BFF(Backend-for-Frontend) 패턴의 이점을 설명합니다. API 키는 서버측에서 유지되며, CORS가 처리되고, 캐싱이 중앙 집중화되며, 공급업체가 추상화됩니다. 관리 UI 구성 기능을 요청하면 에이전트가 모든 설정을 `aio-lib-state` 대신 `.env`에 저장하도록 푸시하고 설정을 변경할 때 재배포를 제거합니다.

>[!NOTE]
>
>상담원은 다른 질문을 할 수 있습니다. 이러한 답변을 사용하여 동일한 기능 결과를 위해 에이전트를 설정하는 지침으로 사용하십시오. 예를 들어, 상점 호출을 위한 BFF 작업, 체크아웃 강화를 위한 배송 방법 웹후크 및 `aio-lib-state`에 설정을 저장하는 관리 UI 구성 페이지가 있습니다.

### 3단계: 요구 사항 및 아키텍처 검토

에이전트는 사용자가 검토할 요구 사항 및 아키텍처 문서를 생성합니다. 요구 사항이 제공된 답변과 일치하고 아키텍처가 다음을 충족하는지 확인합니다.

- **BFF 작업**(`delivery-estimates`) — 상점 측에서 PDP 및 장바구니 페이지에서 호출하는 독립 실행형 웹 작업입니다. `aio-lib-state`에서 구성을 읽고 외부 게재 예상 API를 호출한 다음 형식이 지정된 예상 값을 반환합니다.
- **Webhook 작업**(`shipping-methods`) — 체크아웃 중에 `additional_data`의 배달 날짜를 사용하여 배송 속도를 높입니다. `plugin.out_of_process_shipping_methods.api.shipping_rate_repository.get_rates` Webhook 메서드를 사용합니다.
- **관리자 구성 작업**(`delivery-estimates-config`) — `aio-lib-state`에 저장된 구성(API URL, API 키, 원본 주소, 통신사, 캐시 TTL)에 대한 CRUD입니다.
- **공유 라이브러리** — 외부 API에 대한 HTTP 클라이언트 및 `aio-lib-state`을(를) 읽고 쓰기 위한 구성 모듈입니다.

>[!NOTE]
>
>AI 에이전트는 비결정적이며 모델과 IDE에 따라 행동이 다릅니다. 요구 사항 및 아키텍처가 다른 다양한 질문 세트를 받을 수 있습니다. 그렇다면 계속 진행하기 전에 구현이 이 자습서에 제시된 것과 거의 일치하도록 하는 방향으로 에이전트를 제어하십시오.

### 4단계: 구현 계획 선택

에이전트는 자세한 구현 계획을 작성하거나 직접 구현을 완료할 수 있는 옵션을 제공합니다.

- 더 많은 제어로 단계적으로 실행할 수 있는 미리 보기 계획이 필요하면 첫 번째 옵션을 선택합니다.
- 에이전트가 최소한의 개입으로 전체 구현을 수행하도록 하려면 두 번째 옵션을 선택합니다.

### 5단계: 정리 및 배포

에이전트가 구현을 완료하면 정리 작업을 진행합니다. 배송 도메인만 사용 중이므로 에이전트는 사용하지 않은 스캐폴딩을 제거합니다.

- 결제 작업 및 구성(`validate-payment/`, `filter-payment/`, `payment-methods.yaml`)
- 세금 작업 및 구성(`collect-taxes/`, `collect-adjustment-taxes/`, `tax-integrations.yaml`)
- 이벤트 작업 및 구성(`commerce-events/`, `3rd-party-events/`, `events.config.yaml`)
- 일반 스캐폴딩(`generic/`)
- 다른 도메인(예: 세금 관련 페이지 및 후크)의 관리자 UI SPA 구성 요소
- 사용하지 않는 스크립트, 테스트 파일 및 환경 변수

>[!TIP]
>
>에이전트에게 관리 UI SPA에서 다른 도메인의 남은 내용도 확인하도록 요청하십시오. 세금 분류 페이지와 해당 후크는 여전히 스타터 키트 스캐폴딩에서 존재할 수 있으며 제거해야 합니다.

정리 후 다음 단계를 사용하여 **다음 순서로 배포**:

```bash
# 1. Copy env template and fill in credentials.
cp env.dist .env

# 2. Select your App Builder workspace.
aio app use --merge

# 3. Sync OAuth credentials from workspace.
npm run sync-oauth-credentials

# 4. Deploy the extension.
aio app deploy

# 5. Register shipping carriers in Commerce.
npm run create-shipping-carriers
```

>[!IMPORTANT]
>
>단계를 건너뛰거나 재정렬하지 마십시오. 단계 1-3은 배포를 위한 사전 요구 사항입니다. 자격 증명이 구성되지 않은 경우 `aio app deploy` 명령이 실패합니다.

### 6단계: Webhook 및 관리자 UI 구성

배포 후 배송 웹후크를 구성합니다. 에이전트는 프로그래밍 방식으로 구독하는 스크립트를 만들 수 있습니다.

```bash
npm run subscribe-webhook
```

이 명령은 다음 설정으로 배송 웹후크를 구독합니다.

| 필드 | 값 |
|-------|-------|
| Webhook 메서드 | `plugin.out_of_process_shipping_methods.api.shipping_rate_repository.get_rates` |
| Webhook 유형 | `after` |
| 필수 | 선택 사항(기본 배송으로 대체 허용) |
| 시간 초과 | 5000ms |

{style="table-layout:auto"}

>[!NOTE]
>
>SaaS의 경우 Webhook 메서드 이름이 경로에서 `magento.`을(를) 삭제합니다. PaaS의 웹후크 이름은 `plugin.magento.out_of_process_shipping_methods...`이고 SaaS의 웹후크 이름은 `plugin.out_of_process_shipping_methods...`입니다.

다음으로 관리 UI를 구성합니다.

1. **관리 UI SDK**(**[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL Configuration]** > **[!UICONTROL Adobe Services]** > **[!UICONTROL Admin UI SDK]** > **[!UICONTROL Enable]** > **[!UICONTROL Yes]**)을(를) 사용하도록 설정합니다.

1. [!DNL App Builder] 작업 영역 및 확장을 선택하여 확장을 구성합니다.

1. **[!UICONTROL Refresh registrations]**&#x200B;을(를) 클릭합니다.

1. **[!UICONTROL Apps]** 사이드바에서 **[!UICONTROL Delivery Estimates]** > [!DNL Admin]&#x200B;(으)로 이동합니다.

1. 기능을 활성화하고 API URL 및 API 키, 원본 주소, 기본 통신사, 캐시 TTL 및 통신사 코드 매핑을 포함한 필수 설정을 지정하여 구성을 완료합니다.

### 7단계: 확장 테스트

게재 예상 BFF 작업을 직접 테스트합니다.

```bash
curl -s -X POST \
  -H "Content-Type: application/json" \
  -d '{"destination": {"country_code": "US", "postal_code": "10001"}}' \
  "https://<your-runtime-url>/api/v1/web/commerce-checkout-starter-kit/delivery-estimates" | jq .
```

응답은 다음과 유사해야 합니다.

```json
{
  "estimates": [
    {
      "carrier": "standard",
      "service_level": "ground",
      "delivery_date": "2026-03-12",
      "safe_delivery_date": "2026-03-13",
      "transit_days": 4,
      "cutoff_datetime_utc": "2026-03-06T18:00:00Z"
    },
    {
      "carrier": "express",
      "service_level": "2day",
      "delivery_date": "2026-03-10",
      "safe_delivery_date": "2026-03-10",
      "transit_days": 2,
      "cutoff_datetime_utc": "2026-03-06T20:00:00Z"
    }
  ],
  "best_estimation": {
    "carrier": "express",
    "delivery_date": "2026-03-10",
    "transit_days": 2
  }
}
```

### 서비스 계약 만들기

백엔드가 완료되면 에이전트에게 상점 작업에 대한 서비스 계약을 만들도록 요청합니다.

```shell-session
Produce a spec called STOREFRONT_API_SPEC that I can use in the storefront workspace with the corresponding agent. Also give me a prompt that I could use in that workspace.
```

에이전트는 전체 BFF 끝점 계약(요청 및 응답 형식, 예: 페이로드, 오류 처리)과 상점 작업 공간에 대한 사용 준비 프롬프트가 있는 `docs/STOREFRONT_API_SPEC.md`을(를) 생성합니다.

Storefront 개발 단계를 시작하기 전에 이 파일을 Storefront 프로젝트에 복사하십시오.

>[!TIP]
>
>에이전트가 서비스 계약 **과(와)**&#x200B;을(를) 모두 생성하도록 하면 다른 작업 영역에 대한 프롬프트가 표시되므로 백엔드와 상점 팀(또는 에이전트) 간에 깔끔한 핸드오프가 가능합니다. Storefront 에이전트는 API에 대한 질문을 할 필요 없이 즉시 작업을 시작할 수 있습니다.

## 상점 앞에 연결

이 섹션에서는 [!DNL Edge Delivery Services] 및 AI 지원 개발 도구를 사용하여 게재 예상 확장의 상점 역할을 구현하는 방법을 안내합니다. PDP, 장바구니 페이지 및 체크아웃 페이지에 게재 날짜 예상치를 추가합니다.

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
- `STOREFRONT_API_SPEC.md` 파일이 Storefront 프로젝트의 `docs/` 폴더로 복사되었습니다.

### 1단계: 환경 유효성 검사

`config.json` 파일을 열고 `commerce-core-endpoint` 및 `commerce-endpoint`의 값이 [!DNL Adobe Commerce as a Cloud Service] GraphQL 끝점을 가리키는지 확인하십시오.

```json
"commerce-core-endpoint": "https://na1-sandbox.api.commerce.adobe.com/<your-instance-id>/graphql",
"commerce-endpoint": "https://na1-sandbox.api.commerce.adobe.com/<your-instance-id>/graphql",
```

### 2단계: 초기 프롬프트 제공

프로젝트에 서비스 계약이 이미 있는 경우 에이전트에게 storefront 통합을 구현하라는 메시지를 표시합니다. 에이전트에서 사용 가능한 경우 **계획** 모드를 사용하여 에이전트가 계획 없이 진행되지 않도록 합니다.

```shell-session
I need to implement delivery date estimates on the storefront for an Adobe Commerce (SaaS) store using Edge Delivery Services with storefront drop-ins. The backend is already built and deployed as an App Builder extension.

The full integration contract is in the `docs/STOREFRONT_API_SPEC.md` file— please read it first. It covers two integration points:

PDP and Cart pages — Call the delivery-estimates BFF action (HTTP POST) to fetch estimates for a destination and display the best delivery date.

Checkout shipping step — Delivery dates are already injected into each shipping method's `additional_data` by a webhook. No API call is needed. Just read `additional_data` from the shipping methods and display the delivery date next to each option.

Requirements:
- Show "Get it by [date]" on PDP using best_estimation.delivery_date
- Show a delivery date range on the cart page using delivery_date / safe_delivery_date
- Show delivery dates next to each shipping method at checkout, reading from additional_data
- Show "Order within X hours" countdown using cutoff_datetime_utc where appropriate
- Cache estimates client-side in sessionStorage to avoid redundant calls
- Never block the purchase flow — if estimates are unavailable, hide the UI silently

STOP and ask me any clarifying questions you have about the requirements before you do any work.
```

>[!TIP]
>
>전체 API 계약은 이미 백엔드 에이전트에서 사용할 수 있으므로 프롬프트가 자세히 표시됩니다. 에이전트는 `@docs/STOREFRONT_API_SPEC.md`을(를) 참조하여 정확한 끝점 URL, 요청 및 응답 형식, 오류 처리를 파악합니다. 명시적 요구 사항 목록은 에이전트가 범위를 인벤터리하지 못하도록 합니다. 특히 계획 모드 요청은 구현을 조기에 제어하는 데 도움이 되는 단계별 워크플로우를 트리거합니다.

### 3단계: 명확한 질문에 답변

에이전트는 인증 범위, 체크아웃 접근 방식 및 스타일에 대한 질문과 함께 반환됩니다. 다음 예제는 일반적인 질문과 답변을 보여 줍니다.

**에이전트 질문 예:**

1. **익명의 사용자와 로그인한 사용자 비교** — 예상 값이 모든 구매자의 PDP 및 장바구니 페이지에 표시되어야 합니까, 아니면 인증된 사용자만 표시되어야 합니까?
2. **체크아웃 방법** — ShippingMethods 드롭인 컨테이너는 `additional_data`을(를) 노출하지 않으므로 에이전트에서 다음 두 가지 옵션을 제안합니다.
   - **옵션 A:** 체크아웃 및 DOM 주입 배달 날짜에 BFF를 호출합니다(더 간단하고 PDP/Cart와 일치).
   - **옵션 B:** `overrideGQLOperations`을(를) 통해 체크아웃 GraphQL 조각을 확장하여 `additional_data` 포함
3. **스타일** — 이모티콘과 기존 디자인 토큰 비교

**예제 답변:**

```shell-session
1. Only for logged-in users — that way we can use the shopper's default shipping address and avoid a zip code input
2. Let's do Option A if feasible
3. Use anything that matches the current styling
```

>[!TIP]
>
>로그인한 쇼핑객에 대해서만 예상 값을 표시하는 것은 실용적인 선택입니다. 상담원은 (GraphQL을 통해) 구매자의 기본 배송 주소를 자동으로 사용할 수 있으므로 우편번호 입력이 필요하지 않습니다. PDP 및 Cart의 익명 쇼핑객은 우편 번호를 입력해야 하며, 이렇게 하면 마찰이 추가됩니다. 체크아웃 시 배송 주소가 이미 입력되어 모든 쇼핑객에게 배송 날짜가 표시됩니다.

>[!NOTE]
>
>상담원은 다른 질문을 할 수 있습니다. 다음 답변을 지침으로 사용하십시오.
>
>- 로그인한 구매자에 대해서만 PDP 및 장바구니 예상 값을 표시합니다(우편 번호 입력이 필요하지 않음).
>- 체크아웃의 경우 간소화를 위해 옵션 A(BFF 호출 + DOM 주입)를 사용합니다.
>- 스타일링에 기존 디자인 토큰을 사용합니다.

### 4단계: 요구 사항 및 아키텍처 검토

에이전트는 공유 모듈 아키텍처를 설계합니다. 다음을 포함하는지 확인합니다.

| 구성 요소 | 목적 |
|-----------|---------|
| `scripts/delivery-estimates.js` | 공유 모듈 — BFF 클라이언트, 캐싱(sessionStorage, 30분 TTL), 날짜 형식 지정, 카운트다운 논리, 고객 주소 조회, 통신사 매핑 |
| PDP 통합 | 가격과 설명 사이에 선택적인 카운트다운이 있는 &quot;[날짜]까지 가져오기&quot;를 표시합니다. |
| 장바구니 통합 | 주문 요약 위의 오른쪽 열에 날짜 범위(&quot;3월 12일 목요일 - 3월 13일&quot;)를 표시합니다 |
| 체크아웃 통합 | 배송 단계가 활성화된 경우 BFF를 호출하고 `MutationObserver`을(를) 통해 DOM에서 배달 날짜를 주입합니다. |

{style="table-layout:auto"}

확인할 주요 디자인 결정:

- 모든 BFF 호출은 비차단됩니다. 페이지가 먼저 렌더링되고 예상치가 비동기적으로 표시됩니다.
- 모든 오류가 조용합니다. `console.debug`만 표시되고 구매자 표시 오류가 없습니다.
- `CARRIER_MAP`은(는) Commerce 통신사 코드(DPS, Fedex)를 BFF 통신사 코드(표준, 익스프레스)에 매핑합니다.
- 동적 `import()`은(는) 게재 모듈을 중요한 렌더링 경로에서 벗어나게 합니다.

>[!NOTE]
>
>AI 에이전트는 비결정적이며 모델과 IDE에 따라 행동이 다릅니다. 요구 사항 및 아키텍처가 다른 다양한 질문 세트를 받을 수 있습니다. 그렇다면 계속 진행하기 전에 구현이 이 자습서에 제시된 것과 거의 일치하도록 하는 방향으로 에이전트를 제어하십시오.

### 5단계: 구현 계획 선택

에이전트는 자세한 구현 계획을 작성하거나 직접 구현을 완료할 수 있는 옵션을 제공합니다.

- 더 많은 제어로 단계적으로 실행할 수 있는 미리 보기 계획이 필요하면 첫 번째 옵션을 선택합니다.
- 에이전트가 최소한의 개입으로 전체 구현을 수행하도록 하려면 두 번째 옵션을 선택합니다.

구현 중에 에이전트는 다음 파일을 만들고 수정합니다.

**새 파일:**

- `scripts/delivery-estimates.js` — `fetchDeliveryEstimates()`, `getCustomerShippingAddress()`, `formatDeliveryDate()`, `buildCountdownText()`, `findEstimateForCarrier()`이(가) 있는 공유 모듈

**수정된 파일:**

- `blocks/product-details/product-details.js` + `.css` — 오른쪽 열의 게재 예상 div, 기본 렌더링 후 비동기 가져오기
- `blocks/commerce-cart/commerce-cart.js` + `.css` — 주문 요약 위의 게재 예상 div
- `blocks/commerce-checkout/commerce-checkout.js`, `containers.js`, `.css` — 배송 방법 레이블에 대한 `MutationObserver` 기반 DOM 삽입

생성되는 코드를 시청하고 필요한 경우 질문하거나 에이전트를 리디렉션합니다.

### 6단계: 서버 시작 및 테스트

에이전트가 구현을 완료한 후 개발 서버를 시작하고 게재 예상치를 테스트합니다.

1. 로컬 개발 서버를 시작합니다.

   ```bash
   npm run start
   ```

1. 브라우저에서 쇼핑객 계정에 로그인합니다.

   PDP 및 장바구니에서 예상 게재를 사용하려면 저장된 기본 배송 주소가 있는 인증된 세션이 필요합니다.

1. 제품 페이지로 이동하여 다음 결과를 확인합니다.

   | 페이지 | 예상 결과 | 인증 필요 |
   |------|-----------------|---------------|
   | PDP | &quot;3월 12일 목요일까지 다운로드&quot;(옵션) 카운트다운이 포함된 | 예(로그인된 경우에만) |
   | 장바구니 | &quot;예상 배송: 3월 12일 목요일 - 3월 13일 금요일&quot; | 예(로그인된 경우에만) |
   | 체크아웃 | 배송 방법별 &quot;예상 배송: 3월 12일 목요일&quot; | 아니요(체크아웃 시 입력된 주소) |

   {style="table-layout:auto"}

>[!NOTE]
>
>일치하는 운송회사가 없는 운송 방법(예: 정액 요금)에는 예상 값이 표시되지 않습니다. 기본적으로 사용됩니다. `CARRIER_MAP`에 매핑된 통신사만 배달 날짜를 가져옵니다.

수동 테스트를 수행하거나 에이전트에게 브라우저 기능을 사용하여 테스트하도록 요청할 수 있습니다.

```shell-session
Run complete browser testing using the following product page 'http://localhost:3000/products/<product-slug>/<sku>'
```

### 7단계: 정리

테스트를 건너뛰거나 완료한 후에는 정리 작업을 진행하라는 메시지가 표시됩니다. 확인 시 에이전트는 구현 중에 생성된 모든 문서 아티팩트를 보관합니다.

## 문제 해결

자습서 도중 문제가 발생하는 경우 다음 팁을 사용하십시오.

### 백엔드(App Builder)

| 증상 | 원인 | 수정 |
|---------|-------|-----|
| 관리자 UI 구성 작업이 &quot;요청이 허용되지 않는 매개 변수(예약된 속성)&quot;를 사용하여 `400 Bad Request`을(를) 반환합니다. | 프런트 엔드 후크에서 요청 본문의 `__ow_method`을(를) 보내고 있습니다. 접두사가 `__ow_`인 속성은 OpenWhsk에서 예약되어 있으며 작업에 `final: true`이(가) 있으면 거부됩니다. | `method` 대신 사용자 지정 `__ow_method` 속성을 보냅니다. 백 엔드 작업은 먼저 `params.method`을(를) 읽은 다음 `params.__ow_method`(런타임에서 자동으로 제공)으로 돌아갑니다. |
| `aio app deploy`이(가) &quot;maxVersion이 productDependencies에 필요합니다&quot;와(과) 함께 실패합니다. | CLI 유효성 검사에는 `minVersion` 제품 종속성에 `maxVersion`과(와) `app.config.yaml`이(가) 모두 필요합니다. | `maxVersion`의 각 `productDependencies` 항목에 `app.config.yaml` 값을 추가하십시오. |
| 배포 명령 실패 | 배포하기 전에 자격 증명이 구성되지 않았습니다. `.env`, 작업 영역 선택 및 OAuth 동기화를 먼저 수행해야 합니다. | 올바른 순서를 따르십시오. `cp env.dist .env` > `aio app use --merge` > `npm run sync-oauth-credentials` > `aio app deploy`. |

{style="table-layout:auto"}

### Storefront(Edge Delivery Services)

| 증상 | 원인 | 수정 |
|---------|-------|-----|
| 로그인한 구매자에 대해 PDP 게재 예상치가 표시되지 않음 | PDP 블록이 `account` 드롭인을 초기화하지 않으므로 `getCustomerAddress()`이(가) 자동으로 실패하고 예상 값을 가져오지 않습니다. | 계정 드롭 인 API에 의존하는 대신 `CORE_FETCH_GRAPHQL.fetchGraphQl()`을(를) 사용하여 구매자 주소를 쿼리하십시오. 모든 페이지에서 작동합니다. |
| GraphQL 수정 후에도 PDP가 여전히 표시되지 않음 | 메서드 이름 `CORE_FETCH_GRAPHQL.fetch()`의 오타가 `CORE_FETCH_GRAPHQL.fetchGraphQl()` 대신 사용되었습니다. | 올바른 메서드 이름을 사용하십시오. `fetchGraphQl`(대문자 Q, 소문자 l). |
| 첫 번째 로드 시 체크아웃 게재 날짜가 표시되지 않음 | `checkout/updated`이(가) 이미 실행된 후에 `checkout/initialized` 이벤트 수신기가 등록되었으므로 초기 데이터가 누락되었습니다. | 등록 전에 내보낸 이벤트를 catch하려면 `checkout/initialized`이(가) 있는 `{ eager: true }` 수신기를 추가하십시오. 이후의 변경 내용에 대해 `checkout/updated` 수신기를 유지합니다. |
| 장바구니 게재 예상이 표시되지 않음 | `block.appendChild(fragment)`이(가) 조각에서 모든 하위 항목을 이동하므로 `fragment.querySelector('.cart__delivery-estimate')`이(가) null을 반환합니다. | 추가 작업 후 `block` 대신 `fragment`에서 쿼리 |
| 정액 요금 배송 시 체크아웃 시 배송 날짜가 표시되지 않음 | 기본적으로 `CARRIER_MAP`은(는) DPS를 표준에 매핑하고 Fedex를 표현합니다. 정액 요금에는 외부 API에 해당하는 통신사가 없습니다. | 버그가 아닙니다. 다른 통신사에 대한 예상 값을 추가하려면 `CARRIER_MAP`에서 `scripts/delivery-estimates.js`을(를) 확장하고 백 엔드 확장에서 통신사를 구성하십시오. |

{style="table-layout:auto"}

### Commerce SaaS 샌드박스

| 증상 | 원인 | 수정 |
|---------|-------|-----|
| Webhook이 `429 Too Many Requests`을(를) 반환합니다. | [!DNL App Builder] 작업 영역이 디버그 모드이며 분당 비율 제한이 엄격합니다. [!DNL Commerce]은(는) 체크아웃 중에 자주 배송 요금을 다시 계산하므로 할당량이 초과됩니다. | 프로덕션 작업 영역에 배포합니다(`aio app use`을(를) 전환한 다음 `aio app deploy`). 프로덕션 작업 공간에는 디버그 속도 제한이 없습니다. |
| 웹후크 소프트 시간 초과 경고(>1,000ms) | 배송 방법 웹후크 작업이 [!DNL Commerce] 1000ms 소프트 시간 제한보다 오래 걸렸습니다. | `aio-lib-state`에서 서버측 캐싱을 더 적극적으로 사용하거나 [!DNL Commerce Admin]에서 웹후크 시간 제한을 늘리십시오(Commerce 웹후크 구성). |

{style="table-layout:auto"}

## 튜토리얼 요약

다음은 이 자습서에서 다루는 항목에 대한 요약입니다.

- **모의 API 설정:** Pipedream 또는 [!DNL App Builder] 런타임 작업을 사용하여 모의 게재 예상 API를 만듭니다.
- **BFF 패턴:** 외부 API를 래핑하고 자격 증명을 서버측에서 유지하며 캐싱을 중앙 집중화하는 백 엔드의 프론트엔드 작업을 빌드합니다.
- **Webhook 데이터 보강:** 배달 방법 Webhook를 확장하여 체크아웃 시 각 배달 옵션에 배달 날짜를 삽입합니다.
- **관리 UI 구성 기능:** 판매자가 다시 배포하지 않고 API 설정, 원본 주소 및 통신사 매핑을 관리할 수 있도록 [!DNL Admin UI SDK]을(를) 사용하여 구성 페이지를 추가합니다.
- **서비스 계약:** 백엔드 확장 및 상점 구현을 연결하는 API 계약을 만듭니다.
- **Storefront 통합:** 공유 클라이언트 모듈을 사용하여 PDP(&quot;Get it by&quot;), 장바구니(날짜 범위) 및 체크아웃(배송 방법별)에 게재 예상 값을 표시합니다.
- **비차단 UX:** 게재 예상 값이 구매 흐름을 차단하지 않도록 합니다. 페이지가 먼저 렌더링되고 예상 값이 비동기적으로 표시됩니다.

## 다음 단계

게재 예상 서비스를 확장하려면 다음 제안을 사용하십시오.

- **실제 통신사 API 연결:** [!DNL Admin UI]에서 서비스 URL 및 API 키를 변경하여 UPS, FedEx 또는 USPS와 같은 실시간 배송 API로 모의 항목을 바꿉니다.
- **익명 쇼핑객 지원:** 로그인하지 않은 쇼핑객이 게재 예상치를 볼 수 있도록 PDP 및 장바구니 페이지에 우편 번호 입력을 추가합니다.
- **통신사 매핑 확장:** `CARRIER_MAP`에 통신사 코드를 더 추가하여 추가 배송 방법에 대한 배달 날짜를 표시합니다.
- **서버측 캐싱 추가:** BFF 작업에서 `aio-lib-state` 캐싱을 구현하여 반복되는 원본 및 대상 쌍에 대한 외부 API 호출을 줄입니다.
- **주문 확인 시 예상 게재 날짜 표시:** 주문 확인 페이지와 트랜잭션 전자 메일에 예상 게재 날짜를 표시합니다.
