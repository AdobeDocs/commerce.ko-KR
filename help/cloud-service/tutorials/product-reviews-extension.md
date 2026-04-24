---
title: 제품 리뷰 확장 튜토리얼
description: App Builder, Edge Delivery Services 및 AI 지원 개발 도구를 사용하여 Adobe Commerce as a Cloud Service에 대한 제품 리뷰와 Q&A 확장을 빌드하는 방법을 알아봅니다.
solution: Commerce
feature: App Builder, Cloud
feature-set: Commerce
role: Developer
level: Intermediate
type: Tutorial
hide: true
hidefromtoc: true
source-git-commit: ba445bf33ec9334c853245fce125af12cd244367
workflow-type: tm+mt
source-wordcount: '2533'
ht-degree: 0%

---

# 제품 리뷰 확장 튜토리얼

이 튜토리얼에서는 고객이 [!DNL Adobe App Builder] 및 AI 지원 개발 도구를 사용하여 [!DNL Adobe Commerce as a Cloud Service] 백엔드를 통해 상점에 대한 제품 검토 및 질문 및 답변(Q&amp;A) 콘텐츠를 제출할 수 있는 확장을 빌드하는 방법을 안내합니다. 확장은 구매자가 제품 리뷰와 질의응답(Q&amp;A) 콘텐츠를 보고 제출하고 제품 세부 정보 페이지(PDP)에 표시할 수 있도록 REST API 엔드포인트를 제공합니다.

다음 두 가지 부분을 작성합니다.

- **App Builder 확장** — `aio-lib-state`에서 유효성 검사, 페이지 매김 및 지속성을 통해 제품 검토 및 Q&amp;A 콘텐츠를 만들고 보기 위한 GET 및 POST 작업을 포함하는 REST API입니다.
- **Storefront 통합** - 리뷰 및 Q&amp;A를 표시하는 PDP의 제품 리뷰 블록으로서, 구매자가 리뷰, 질문 및 답변을 제출할 수 있는 양식이 있습니다.

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

이전 명령 중 필요한 결과를 반환하지 않는 명령이 있는 경우 [필수 구성 요소](./tutorial-prerequisites.md)에서 자세한 내용을 확인하십시오.

또한 다음을 확인하십시오.

- 제품 데이터가 있는 [!DNL Adobe Commerce as a Cloud Service] 인스턴스가 있습니다. [Commerce Cloud 서비스 인스턴스](https://experienceleague.adobe.com/en/docs/commerce/cloud-service/overview){target="_blank"}를 참조하세요.
- [!DNL Commerce] 인스턴스에 연결된 Storefront 프로젝트가 있습니다. 항목이 없으면 [상점 만들기](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/){target="_blank"}의 단계를 따릅니다.
- `aem` CLI가 설치되어 있습니다.

  ```bash
  npm install -g @adobe/aem-cli
  ```

## 확장 개발

이 섹션에서는 AI 지원 개발 도구를 사용하여 [!DNL Adobe Commerce as a Cloud Service] 백엔드를 사용하는 스토어프론트용 확장에 대한 제품 검토 및 Q&amp;A 콘텐츠를 제출하고 볼 수 있는 확장 개발을 안내합니다. 확장은 제품 리뷰와 Q&amp;A 콘텐츠를 제출하고 보고 PDP에 표시할 수 있는 REST API를 제공합니다.

1. 코딩 에이전트의 MCP 설정으로 이동합니다. 예를 들어 커서에서 **[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Tools & MCP]**(으)로 이동합니다. `commerce-extensibility` 도구 집합이 오류 없이 사용하도록 설정되어 있는지 확인하십시오. 오류가 표시되면 도구 세트를 끄고 켜십시오.

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
I want to build an Adobe Commerce as a Cloud Service extension that allows shoppers to submit and view product review and question and answer (Q&A) content that displays on product detail pages (PDP).

## Product Reviews
The application has REST API endpoints that can be called by a storefront to retrieve and submit product reviews for a given SKU.

The GET endpoint accepts the following query parameters:
- sku (string, required): The SKU of the product to fetch reviews for
- limit (integer, optional): The maximum number of reviews to return (default: 10)
- offset (integer, optional): The number of reviews to skip for pagination (default: 0)

The POST endpoint accepts the following JSON body parameters:
- sku (string, required): The SKU of the product to submit a review for
- rating (integer, required): The rating for the product (1-5)
- review (string, optional): The text of the review
- user (string, optional): The name of the user submitting the review

The POST endpoint validates the input and returns appropriate error responses for invalid data. The reviews are stored and associated with the corresponding product SKU.

## Questions and Answers
The application has REST API endpoints that can be called by a storefront to retrieve and submit questions and answers for a given SKU.

The GET endpoint accepts the following query parameters:
- sku (string, required): The SKU of the product to fetch questions and answers for
- limit (integer, optional): The maximum number of questions and answers to return (default: 10)
- offset (integer, optional): The number of questions and answers to skip for pagination (default: 0)

The POST endpoint accepts the following JSON body parameters:
- sku (string, required): The SKU of the product to submit a question or answer for
- type (string, required): The type of submission ("question" or "answer")
- questionId (string, required if type is "answer"): The ID of the question being answered
- content (string, required): The text of the question or answer
- user (string, optional): The name of the user submitting the question or answer

The POST endpoint validates the input and returns appropriate error responses for invalid data. The questions and answers are stored and associated with the corresponding product SKU. Answers are also associated with the corresponding question.

Do not require Adobe IMS authentication for these endpoints. They will be called directly from the storefront.

STOP and ask me any clarifying questions you have about the requirements before you do any work.
```

>[!TIP]
>
>계속하기 전에 에이전트에게 STOP을 알리고 질문하면 프로세스 초기에 구현을 조정할 수 있습니다. 이렇게 하면 주요 가정 및 누락된 요구 사항이 조기에 식별되고 이 자습서에서 안내식 워크플로우를 시작하는 데 필요합니다.

### 2단계: 에이전트의 질문에 답변

에이전트가 솔루션 구성을 시작하기 전에 답변해야 하는 일련의 질문과 함께 반환됩니다. 다음 예제는 일반적인 질문과 답변을 보여 줍니다. 상담원은 다른 질문을 할 수 있지만 주제는 일반적으로 동일합니다.

**에이전트 질문 예:**

1. **REST API — 호스트 및 소비자** — CRUD REST API가 상점 호출 시 이 App Builder 앱(Adobe I/O Runtime의 웹 작업)에 포함되어야 합니까? 이를 누가 EDS Storefront, 맞춤형/헤드리스 상점 또는 둘 다라고 합니까? CORS, 공개(인증되지 않은) 액세스가 필요합니까? 또는 호출자가 API 키 또는 OAuth를 사용합니까?
1. **데이터 모델** — &quot;검토&quot; 또는 &quot;질문&quot;은 무엇을 나타냅니까? 고객 식별자(이메일 전용 또는 고객 ID) 제품 식별자(SKU만 해당 또는 SKU + 스토어 보기) 동일한 고객이 동일한 SKU에 대해 여러 검토를 제출할 수 있습니까?
1. **지속성** — `aio-lib-state`이(가) 검토 및 Q&amp;A를 지속하기에 적절한 위치입니까? 아니면 외부 스토어가 있습니까? 디자인은 다중 임차인 또는 단일 임차인을 가정해야 합니까?
1. **페이지 매김 의미 체계** — Q&amp;A GET의 경우 `limit`이(가) 중첩된 답변이 있는 질문에만 적용됩니까? 또는 총 질문 수와 답변에 적용됩니까?

**예제 답변:**

```shell-session
1. The REST API should be part of this App Builder app. It will be called by the EDS Storefront. No authentication — public access for both GET and POST.
2. For reviews: sku, rating (1-5), optional review text, optional user name. For Q&A: sku, type (question or answer), content, optional user. Answers linked to questions via questionId. Allow multiple reviews per SKU from the same user.
3. Use aio-lib-state. Single tenant for now.
4. Pagination by question — limit and offset apply to questions; each question includes its nested answers.
```

>[!NOTE]
>
>상담원은 다른 질문을 할 수 있습니다. 리뷰 및 Q&amp;A가 포함된 공개 REST API, `aio-lib-state` 지속성, 인증 없음 등 동일한 기능 결과를 얻기 위한 에이전트의 지침으로 이 답변을 사용하십시오.

### 3단계: 요구 사항 및 아키텍처 검토

에이전트는 사용자가 검토할 요구 사항 및 아키텍처 문서를 생성합니다. 요구 사항이 제공된 답변과 일치하고 아키텍처가 다음을 충족하는지 확인합니다.

- 네 가지 웹 작업: `reviews-get`, `reviews-post`, `qa-get`, `qa-post`
- 허용되는 패턴(`[a-zA-Z0-9-_.]` — 콜론 없음)에 맞는 키를 사용하여 `aio-lib-state`을(를) 사용하는 지속성
- JSON 문자열로 저장된 상태 값(원시 개체 또는 배열이 아님)
- 자체 포함 패키지 — 번들을 이스케이프 처리하는 `../../` 경로를 통하지 않고 `product-reviews` 패키지 내에 공유된 코드(유틸리티, 상수)

>[!NOTE]
>
>AI 에이전트는 비결정적이며 모델과 IDE에 따라 행동이 다릅니다. 요구 사항 및 아키텍처가 다른 다양한 질문 세트를 받을 수 있습니다. 그렇다면 계속 진행하기 전에 구현이 이 자습서에 제시된 것과 거의 일치하도록 하는 방향으로 에이전트를 제어하십시오.

### 4단계: 구현 계획 선택

에이전트는 자세한 구현 계획을 작성하거나 직접 구현을 완료할 수 있는 옵션을 제공합니다.

- 더 많은 제어로 단계적으로 실행할 수 있는 미리 보기 계획이 필요하면 첫 번째 옵션을 선택합니다.
- 에이전트가 최소한의 개입으로 전체 구현을 수행하도록 하려면 두 번째 옵션을 선택합니다.

### 5단계: 확장 배포

에이전트가 구현을 완료한 후 확장을 배포합니다.

```bash
aio app deploy
```

에이전트가 작업에 `require-adobe-auth: true`을(를) 추가한 경우 상점 앞에서 끝점을 직접 호출할 수 있도록 인증을 제거하도록 요청하십시오.

```shell-session
Remove the requirement to provide a valid Adobe IMS access token from all product-reviews actions.
```

그런 다음 다시 배포합니다.

```bash
aio app deploy
```

### 6단계: 테스트를 위해 모의 데이터 만들기 및 미리 채우기

모의 데이터 파일을 만들고 curl을 사용하여 API를 미리 채우면 CLI 및 상점 첫 화면에서 테스트할 샘플 검토 및 Q&amp;A 콘텐츠가 제공됩니다.

1. 샘플 데이터를 사용하여 `docs/mock-product-reviews-data.json` 파일을 만듭니다. For example:

   ```json
   {
     "reviews": [
       { "sku": "ADB153", "rating": 5, "review": "Great product, highly recommend!", "user": "shopper@example.com" },
       { "sku": "ADB153", "rating": 4, "review": "Good value for money.", "user": "buyer@example.com" }
     ],
     "questions": [
       { "sku": "ADB153", "type": "question", "content": "Does this come in other colors?", "user": "curious@example.com" }
     ]
   }
   ```

1. curl을 사용하여 데이터를 배포된 API에 게시합니다.

   `<your-runtime-url>`을(를) 실제 App Builder 런타임 URL로 바꿉니다(예: `https://1172492-prodreviewqa135-stage.adobeioruntime.net`).

   ```bash
   API_URL="https://<your-runtime-url>/api/v1/web/product-reviews"
   
   # Submit reviews
   curl -s -X POST "$API_URL/reviews-post" \
     -H "Content-Type: application/json" \
     -d '{"sku":"ADB153","rating":5,"review":"Great product, highly recommend!","user":"shopper@example.com"}'
   
   curl -s -X POST "$API_URL/reviews-post" \
     -H "Content-Type: application/json" \
     -d '{"sku":"ADB153","rating":4,"review":"Good value for money.","user":"buyer@example.com"}'
   
   # Submit a question (save the returned id for the answer)
   curl -s -X POST "$API_URL/qa-post" \
     -H "Content-Type: application/json" \
     -d '{"sku":"ADB153","type":"question","content":"Does this come in other colors?","user":"curious@example.com"}'
   
   # Submit an answer (replace <QUESTION-UUID> with the id from the question response)
   curl -s -X POST "$API_URL/qa-post" \
     -H "Content-Type: application/json" \
     -d '{"sku":"ADB153","type":"answer","questionId":"<QUESTION-UUID>","content":"Yes, it comes in blue and red.","user":"seller@example.com"}'
   ```

1. GET 요청으로 데이터 확인:

   ```bash
   curl -s "$API_URL/reviews-get?sku=ADB153"
   curl -s "$API_URL/qa-get?sku=ADB153"
   ```

>[!TIP]
>
>리뷰와 Q&amp;A 콘텐츠가 모두 있는 제품에는 SKU `ADB153`을(를) 사용하고, 리뷰가 없는 제품에는 `ADB152`을(를) 사용합니다. 이 데이터 구성을 통해 상점 첫 화면에서 채워진 상태와 빈 상태를 모두 테스트할 수 있습니다.

### 7단계: 확장 테스트

에이전트에게 테스트 단계를 제공하도록 요청하거나 이전 단계의 curl 예를 사용합니다. 다음 예는 일반적인 테스트 명령을 보여 줍니다.

**리뷰 제출:**

```bash
API_URL="https://<your-runtime-url>/api/v1/web/product-reviews"
curl -s -X POST "$API_URL/reviews-post" \
  -H "Content-Type: application/json" \
  -d '{"sku":"ADB153","rating":5,"review":"Excellent!","user":"test@example.com"}'
```

**리뷰 나열:**

```bash
curl -s "$API_URL/reviews-get?sku=ADB153"
```

**질문 제출:**

```bash
curl -s -X POST "$API_URL/qa-post" \
  -H "Content-Type: application/json" \
  -d '{"sku":"ADB153","type":"question","content":"Is this dishwasher safe?","user":"test@example.com"}'
```

**답변 제출**(`questionId`(으)로 질문 응답의 `id` 사용):

```bash
curl -s -X POST "$API_URL/qa-post" \
  -H "Content-Type: application/json" \
  -d '{"sku":"ADB153","type":"answer","questionId":"<QUESTION-UUID>","content":"Yes, it is.","user":"support@example.com"}'
```

### 서비스 계약 만들기

서비스 구현이 완료되었으므로 이제 에이전트에게 Storefront 작업에 대한 서비스 계약을 작성하도록 요청하십시오.

```shell-session
Create a service contract for the Product Review and Q&A application that defines the API endpoints, request and response formats, and any necessary data models. Ensure that the service contract is clear and detailed enough for a frontend developer to implement the storefront integration without needing to ask additional questions about the API. Name this file PRODUCT_REVIEW_QA_CONTRACT.md
```

Storefront 에이전트가 참조할 수 있도록 이 파일을 Storefront 프로젝트에 복사합니다.

## 상점 앞에 연결

이 섹션에서는 [!DNL Edge Delivery Services] 및 AI 지원 개발 도구를 사용하여 제품 리뷰 및 Q&amp;A 확장의 상점 부분을 구현하는 방법을 안내합니다. PDP에 검토 및 Q&amp;A 콘텐츠를 모두 표시하고 구매자가 새 콘텐츠를 제출할 수 있도록 하는 제품 검토 블록을 추가합니다.

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
- `PRODUCT_REVIEW_QA_CONTRACT.md` 파일이 상점 프로젝트에 복사되었습니다.

### 1단계: 환경 유효성 검사

`config.json` 파일을 열고 `commerce-core-endpoint` 및 `commerce-endpoint`의 값이 [!DNL Adobe Commerce as a Cloud Service] GraphQL 끝점을 가리키는지 확인하십시오.

```json
"commerce-core-endpoint": "https://na1-sandbox.api.commerce.adobe.com/<your-instance-id>/graphql",
"commerce-endpoint": "https://na1-sandbox.api.commerce.adobe.com/<your-instance-id>/graphql",
```

### 2단계: 초기 프롬프트 제공

프로젝트에 서비스 계약이 이미 있는 경우 에이전트에게 제품 검토 블록을 구현하라는 메시지를 표시합니다. 에이전트에서 사용 가능한 경우 **계획** 모드를 사용하여 에이전트가 계획 없이 진행되지 않도록 합니다.

```shell-session
Analyze @PRODUCT_REVIEW_QA_CONTRACT.md and build a product review block using the API specified in the contract. The block displays both reviews and Q&A content on the product detail page, with forms for shoppers to submit reviews, questions, and answers. Use the project manager skill to plan this implementation.
```

>[!TIP]
>
>특히 프로젝트 관리자 스킬 사용을 요청하면 구현을 제어하는 데 도움이 되는 단계별 워크플로우를 트리거합니다. 이를 통해 주요 가정 및 누락된 요구 사항이 프로세스 초기에 식별됩니다.

### 3단계: 명확한 질문에 답변

에이전트가 솔루션 구성을 시작하기 전에 답변해야 하는 일련의 질문과 함께 반환됩니다. 다음 예제는 일반적인 질문과 답변을 보여 줍니다. 상담원은 다른 질문을 할 수 있지만 주제는 일반적으로 동일합니다.

**에이전트 질문 예:**

1. **API 기본 URL** — 상점 측에서 제품 리뷰 API 기본 URL을 어떻게 얻어야 합니까? 옵션에는 구성 블록(예: `apiBaseUrl`이 있는 테이블), 전역 자리 표시자 또는 다른 접근 방식이 포함될 수 있습니다.
1. **SKU 소스** — 블록이 PDP 컨텍스트(현재 제품) 또는 블록 구성에서 SKU를 읽어야 합니까?
1. **양식 동작** — 제출 후 양식을 숨기거나 성공 메시지를 표시하거나 표시되지만 비활성화되어야 합니까?

**예제 답변:**

```shell-session
1. Block table config with apiBaseUrl (required). Each block instance can point to its own deployment.
2. From block table if set; otherwise use getProductSku() so it works on PDP without authoring a SKU.
3. Show a success message above the form; keep the form visible but disabled.
```

>[!NOTE]
>
>블록 구성의 자리 표시자를 실제 App Builder 런타임 URL로 바꿉니다(예: `https://1172492-prodreviewqa135-stage.adobeioruntime.net`).
>
>상담원은 다른 질문을 할 수 있습니다. 다음 답변을 지침으로 사용하십시오.
>
>- 코드 수정 없이 변경할 수 있도록 API 기본 URL은 블록 테이블에서 가져와야 합니다.
>- 설정된 경우 블록 테이블의 SKU이고, 설정되지 않은 경우 PDP의 현재 제품에서 SKU입니다.
>- 제출 후 성공 메시지를 표시하고 양식을 비활성화합니다.

### 4단계: 요구 사항 및 아키텍처 검토

에이전트는 사용자가 검토할 수 있도록 요구 사항 문서를 업데이트합니다. 다음을 확인합니다.

- 이 블록은 리뷰(등급, 사용자, 날짜, 텍스트 포함)와 Q&amp;A(중첩된 답변이 포함된 질문)를 렌더링합니다.
- Forms은 리뷰, 질문 및 답변을 제출하기 위해 존재합니다.
- 페이지 매김은 리뷰와 Q&amp;A 콘텐츠 모두에 대해 지원됩니다.
- API 통합에서는 블록 테이블의 기본 URL을 사용합니다.
- 성공 및 오류 상태는 계약에 따라 처리됩니다.

>[!NOTE]
>
>AI 에이전트는 비결정적이며 모델과 IDE에 따라 행동이 다릅니다. 요구 사항 및 아키텍처가 다른 다양한 질문 세트를 받을 수 있습니다. 그렇다면 계속 진행하기 전에 구현이 이 자습서에 제시된 것과 거의 일치하도록 하는 방향으로 에이전트를 제어하십시오.

### 5단계: 구현 계획 선택

에이전트는 자세한 구현 계획을 작성하거나 직접 구현을 완료할 수 있는 옵션을 제공합니다.

- 더 많은 제어로 단계적으로 실행할 수 있는 미리 보기 계획이 필요하면 첫 번째 옵션을 선택합니다.
- 에이전트가 최소한의 개입으로 전체 구현을 수행하도록 하려면 두 번째 옵션을 선택합니다.

구현하는 동안 에이전트는 블록 파일을 만들고 수정합니다. 생성되는 코드를 시청하고 필요한 경우 질문하거나 에이전트를 리디렉션합니다. 블록이 렌더링되지 않으면 에이전트에 섹션 데코레이션을 분석하고 검색 패턴을 차단하도록 요청하십시오. 블록 요소는 프레임워크에서 해당 섹션을 찾을 수 있도록 섹션의 직접 하위 요소여야 합니다.

### 6단계: 문서 작성에서 제품 페이지에 블록 추가

모든 PDP에 표시되도록 제품 검토 블록을 제품 페이지 템플릿에 추가합니다. 문서 작성 서비스(da.live)를 사용하여 블록을 추가하고 구성합니다.

1. 문서 작성 서비스(예: [da.live](https://da.live/))를 엽니다.

1. 프로젝트 공간을 클릭하고 **제품** 폴더를 연 다음 **기본**(`products/default`)을 선택합니다.

1. 새 블록 섹션을 추가합니다.

   블록 테이블에서 블록 이름이 **product-review**(또는 에이전트가 만든 블록 이름)인 행을 추가합니다.

1. 필요한 설정으로 블록을 구성합니다.
   - **apiBaseUrl** - App Builder 런타임 URL(예: `https://<namespace>-<app-name>-stage.adobeioruntime.net`).
   - **sku** — PDP에서 현재 제품의 SKU를 사용하려면 비워 두거나 특정 SKU를 입력하여 해당 제품에 대한 리뷰만 표시합니다.

1. 변경 내용을 게시하려면 **[!UICONTROL Publish]**&#x200B;을(를) 클릭하십시오.

### 7단계: 서버 시작 및 테스트

문서 작성의 제품 페이지에 블록을 추가한 후 개발 서버를 시작하고 블록을 테스트합니다.

1. 로컬 개발 서버를 시작합니다.

   ```bash
   npm run start
   ```

1. 브라우저에서 리뷰 및 Q&amp;A 콘텐츠가 미리 채워진 제품 페이지로 이동합니다. For example:

   ```shell-session
   http://localhost:3000/products/<product-slug>/ADB153
   ```

1. 제품 검토 블록에 검토 및 Q&amp;A 콘텐츠가 표시되고 제출 양식이 작동하는지 확인합니다.

수동 테스트를 수행하거나 에이전트에게 브라우저 기능을 사용하여 테스트하도록 요청할 수 있습니다.

```shell-session
Run complete browser testing. Use the following product page 'http://localhost:3000/products/<product-slug>/ADB153'
```

### 8단계: 정리

테스트를 건너뛰거나 완료한 후 에이전트는 마지막 **정리** 단계로 진행하라는 메시지를 표시합니다. 확인 시 에이전트는 구현 중에 생성된 모든 문서 객체를 보관합니다.

## 문제 해결

자습서 도중 문제가 발생하는 경우 다음 팁을 사용하십시오.

### 백엔드(App Builder)

| 증상 | 원인 | 수정 |
|---------|-------|-----|
| GET 또는 POST가 500 &quot;모듈을 찾을 수 없음&quot;을 반환합니다. | 제품 검토 작업에서는 패키지 번들을 이스케이프 처리하는 `require("../../utils")` 또는 `require("../../constants")`을(를) 사용합니다. 이러한 파일은 패키지를 배포할 때 포함되지 않습니다. | 제품 리뷰 패키지를 자체 포함합니다. `actions/product-reviews/lib/constants.js` 및 `actions/product-reviews/lib/utils.js`을(를) 추가하고 `../../` 대신 `../lib/...`에서 요구하는 네 가지 작업을 모두 업데이트하십시오. |
| GET은 &quot;키가 패턴과 일치해야 함&quot;과 함께 500을 반환합니다. | 상태 키는 콜론을 사용합니다(예: `reviews:ADB153`). `aio-lib-state`은(는) `[a-zA-Z0-9-_.]`만 허용합니다. | 접두사를 `reviews:` 및 `qa:`에서 `reviews.` 및 `qa.`(으)로 변경합니다. SKU를 정리하는 `stateKey(prefix, sku)` 도우미를 추가합니다(잘못된 문자를 `_`(으)로 바꾸기). |
| POST에서 &quot;값은 문자열이어야 함&quot;과 함께 500 반환 | `aio-lib-state`은(는) 문자열 값만 허용합니다. 코드는 배열 또는 개체를 `state.put()`에 전달합니다. | 쓸 때는 `JSON.stringify()`을(를) 사용하고 읽을 때는 `JSON.parse()`을(를) 사용하여 직렬화합니다. 네 가지 작업을 모두 업데이트합니다. |

{style="table-layout:auto"}

### Storefront(Edge Delivery Services)

| 증상 | 원인 | 수정 |
|---------|-------|-----|
| 테스트 페이지에서 블록이 렌더링되지 않음 | 블록 요소가 추가 `div` 내부에 중첩되어 있으므로 `decorateSections` 후 블록 선택기(`div.section > div > div`)가 일치하지 않습니다. | 블록을 섹션의 직접 하위로 만듭니다. 구조: `section > div.product-review`(또는 해당 블록 클래스). `section > div > div.product-review`을(를) 사용하지 마십시오. |
| 잘못된 CSS 토큰 | 블록에서 `styles/styles.css`에 없는 디자인 토큰을 사용합니다(예: `--color-error-100`, `--type-detail-font-size`). | 에이전트에게 프로젝트의 `styles/styles.css`에 대해 토큰을 확인하고 잘못된 토큰을 기존 토큰으로 바꾸도록 요청하십시오(예: `--color-alert-*`, `--type-details-caption-*`). |

{style="table-layout:auto"}

## 튜토리얼 요약

다음은 이 자습서에서 다루는 항목에 대한 요약입니다.

- **확장 개발:** AI 에이전트에 대한 Adobe Commerce as a Cloud Service 백엔드를 사용하여 상점 첫 화면에서 제품 검토 및 Q&amp;A 콘텐츠를 만들고 보는 기능과 [!DNL App Builder]을(를) 사용하여 4개의 끝점이 있는 작업 REST API를 생성하여 이 기능을 구현하는 방법을 설명합니다.
- **지속성:** 올바른 키 형식 및 JSON 직렬화된 값이 있는 `aio-lib-state`을(를) 사용합니다.
- **모의 데이터 및 미리 채우기:** 모의 데이터 파일을 만들고 curl을 사용하여 CLI 및 상점 테스트를 위해 API를 미리 채웁니다.
- **서비스 계약:** 백엔드 확장 및 상점 구현을 연결하는 API 계약을 만듭니다.
- **단계적 상점 통합:** AI 지원 기술을 사용하여 요구 사항, 아키텍처 및 구현 작업을 수행합니다.
- **PDP 블록:** 제출 양식과 페이지 매김 기능이 있는 리뷰 및 Q&amp;A를 표시하는 PDP에 제품 리뷰 블록을 추가합니다.

## 다음 단계

제품 검토 서비스를 확장하려면 다음 제안을 사용하십시오.

- **중재 추가:** 게시하기 전에 검토 및 Q&amp;A 콘텐츠에 대한 중재 워크플로우를 구현합니다.
- **인증 추가:** 쇼핑객이 로그인하여 리뷰 또는 Q&amp;A 콘텐츠를 제출하고 제출 내용을 고객 계정과 연결해야 합니다.
- **구독 관리 페이지 추가:** 구매자가 리뷰를 보고 편집할 수 있는 상점 페이지를 만듭니다.
- **다중 테넌트 배포 지원:** 상태 관리를 확장하여 단일 App Builder 앱에서 여러 Commerce 테넌트를 지원합니다.
- **속도 제한 추가:** 남용을 방지하기 위해 API에 대한 속도 제한을 구현합니다.
