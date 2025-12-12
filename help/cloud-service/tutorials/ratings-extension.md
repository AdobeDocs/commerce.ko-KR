---
title: 등급 확장 튜토리얼
description: App Builder 및 AI 지원 개발 도구를 사용하여 Adobe Commerce as a Cloud Service에 대한 제품 등급 확장을 빌드하는 방법을 알아봅니다.
role: Developer
hide: true
hidefromtoc: true
source-git-commit: d0b9fd3ebbf0c88abbbf12821c5c4825ffcf10f0
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---

# 등급 확장 자습서(Beta)

>[!NOTE]
>
>이 자습서에서 사용되는 AI 도구는 현재 Beta에 있으며 버그 또는 기타 문제를 포함할 수 있습니다.

이 튜토리얼에서는 [!DNL Adobe Commerce as a Cloud Service] 및 AI 지원 개발 도구를 사용하여 [!DNL Adobe App Builder]에 대한 제품 등급 확장을 빌드하는 방법을 안내합니다.

시작하기 전에 [필수 구성 요소](./tutorial-prerequisites.md)를 완료하십시오.

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

이전 명령 중 필요한 결과를 반환하지 않는 명령이 있는 경우 [필수 구성 요소](tutorial-prerequisites.md)에서 자세한 내용을 확인하십시오.

## 확장 개발

이 섹션에서는 AI 지원 개발 도구를 사용하여 Adobe Commerce as a Cloud Service에 대한 등급 확장을 개발하는 프로세스를 안내합니다.

1. **[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Tools & MCP]**(으)로 이동하여 `commerce-extensibility` 도구 집합이 오류 없이 활성화되었는지 확인합니다. 오류가 표시되면 도구 세트를 끄고 켜십시오.

   ![커서 설정](../assets/cursor-settings.png){width="600" zoomable="yes"}

   >[!NOTE]
   >
   >AI 지원 개발 도구를 사용하여 작업할 때 에이전트가 생성하는 코드 및 응답에는 자연스러운 변형이 있을 것입니다.
   >코드에 문제가 발생하면 언제든지 에이전트에게 디버그를 지원하도록 요청할 수 있습니다.

1. 커서 컨텍스트에 추가된 설명서가 있는 경우 이를 비활성화합니다.

   - [!UICONTROL **커서**] > [!UICONTROL **설정**] > [!UICONTROL **커서 설정**] > [!UICONTROL **색인화 및 문서**]&#x200B;(으)로 이동하여 나열된 문서를 삭제합니다.

   ![설명서 비활성화](../assets/disable-documentation.png){width="600" zoomable="yes"}

1. 제품 등급 확장에 대한 코드를 생성합니다.
   - 커서 채팅 창에서 **에이전트** 모드를 선택하십시오.
   - 다음 프롬프트를 입력합니다.

   ```plain
   Implement an Adobe Commerce as a Cloud Service extension to handle Product Ratings.
   
   Implement a REST API to handle GET ratings requests.
   
   GET requests will have to support the following query parameters:
   
   sku -> product SKU
   ```

   >[!NOTE]
   >
   >에이전트가 문서 검색을 요청하는 경우 이를 허용합니다.

1. 에이전트의 질문에 정확하게 답변하여 최상의 코드를 생성할 수 있도록 도와줍니다.

   ![커서에 프롬프트 입력](../assets/enter-prompt.png){width="600" zoomable="yes"}

   ![에이전트가 명확한 질문을 합니다](../assets/agent-questions.png){width="600" zoomable="yes"}

1. 다음 예제 텍스트를 사용하여 무작위 등급 데이터를 설정하려면 에이전트의 질문에 응답하십시오.

   ```plain
   Yes, this headless extension is for Adobe Commerce as a Cloud Service storefront,
   but we do not need any authentication for the GET API because guest users should be able to use it on the storefront.
   
   This extension will be called directly from the storefront, no async invocation, such as events or webhooks, is required.
   
   Start with just the GET API for now, we will implement other CRUD operations at a later time.
   
   We do not need a DB or storage mechanism right now, just return random ratings data between 1 and 5 and a ratings count between 1 and 1000.
   
   The API should only return the average rating for the product and the total number of ratings.
   We do not need to add tests right now.
   ```

   에이전트에서 구현에 대한 신뢰할 수 있는 원본 역할을 하는 `requirements.md` 파일을 만듭니다.

   ![요구 사항 파일을 만들었습니다](../assets/requirements-file.png){width="600" zoomable="yes"}

1. `requirements.md` 파일을 검토하고 계획을 확인합니다.

   모든 항목이 올바르게 표시되면 에이전트에게 **2단계 - 아키텍처 계획**(으)로 이동하도록 지시합니다.
1. 아키텍처 계획을 검토합니다.
1. 코드 생성을 진행하도록 에이전트에 지시합니다.

   에이전트는 필요한 코드를 생성하고 다음 단계와 함께 자세한 요약을 제공합니다.

   ![아키텍처 계획](../assets/architecture-planning.png){width="600" zoomable="yes"}

   ![코드 생성 요약](../assets/code-generation-summary.png){width="600" zoomable="yes"}

   ![다음 단계](../assets/next-steps.png){width="600" zoomable="yes"}

### 로컬 테스트

1. 에이전트에게 코드를 로컬에서 테스트하도록 요청합니다.

   ```plain
   Test the ratings API locally on a dev server using cURL.
   ```

1. 에이전트의 지침을 따라 API가 로컬에서 작동하는지 확인합니다.

   ![로컬 테스트](../assets/local-testing.png){width="600" zoomable="yes"}

   ![로컬 테스트 결과](../assets/local-testing-1.png){width="600" zoomable="yes"}

### 확장 배포

1. 생성된 코드를 확인한 후 다음 프롬프트를 사용하여 확장을 배포합니다.

   ```plain
   Deploy the ratings API.
   ```

   에이전트는 배포 전에 배포 전 준비 상태 평가를 수행합니다.

   ![배포 전 평가](../assets/pre-deployment-assessment.png){width="600" zoomable="yes"}

1. 평가 결과가 확실하면 에이전트에게 배포를 진행하도록 지시합니다.

   에이전트는 MCP 툴킷을 사용하여 자동으로 확인, 빌드 및 배포합니다.

   ![배포](../assets/deployment-process.png){width="600" zoomable="yes"}

### 배포 후

API를 상점 앞에 통합하기 전에 테스트할 수 있습니다. 에이전트는 새 작업의 위치와 테스트 전략을 제공해야 합니다.

![전략 테스트](../assets/testing-strategy.png){width="600" zoomable="yes"}

터미널에서 cURL을 사용하여 API를 수동으로 테스트할 수도 있습니다.

```bash
curl -s "https://<your-site>.adobeioruntime.net/api/v1/web/ratings/ratings?sku=TEST-SKU-123"
```

![cURL 테스트](../assets/curl-test.png){width="600" zoomable="yes"}

### Edge Delivery Services과 통합

등급 API를 [!DNL Adobe Commerce]에서 제공하는 [!DNL Edge Delivery Services] 상점 첫 라인과 통합하려면 에이전트에게 등급 API에 대한 요구 사항이 포함된 서비스 계약을 만들도록 요청하십시오.

```plain
Create a service contract for the ratings api that I can pass on to the storefront agent. Name it RATINGS_API_CONTRACT.md
```

![서비스 계약](../assets/create-contract.png){width="600" zoomable="yes"}

![서비스 계약 세부 정보](../assets/contract.png){width="600" zoomable="yes"}
<!-- 
Return to the terminal and run the following command in the `extension` folder to copy the file to the `storefront` folder:

```bash
cp RATINGS_API_CONTRACT.md ../storefront
``` -->

### 다음 단계

이제 등급 API 계약이 있으므로 등급 확장의 상점(프론트엔드) 부분을 빌드할 수 있습니다.

<!-- 
## Connect to the storefront

This section teaches you how to implement real storefront features and communicate effectively with AI agents when working with [!DNL Adobe Commerce] dropins and [!DNL Edge Delivery Services].

>[!NOTE]
>
>The prompts provided are starting points. Although you can use them without modification, consider having a natural conversation with the agent.
>
>When working with AI-assisted development tools, there are always natural variations in the code and responses generated by the agent.
>
>If you encounter any issues with your code, ask the agent to help you debug it.

### Ratings stars and review count implementation

1. Navigate to the `storefront` folder:

   ```bash
   cd storefront
   ```

1. Open the storefront folder in a new Cursor window.

    Alternatively, if you have the [Cursor CLI](https://cursor.com/docs/configuration/shell#installing-cli-commands) installed, open the window by using the following command in your terminal:

   ```bash
   cursor .
   ```

1. Start the local development server:

   ```bash
   npm run start
   ```

1. In a browser, navigate to the Apparel page:

   ```plain
   http://localhost:3000/apparel
   ```

1. Observe the boilerplate storefront UI layout and note the lack of visual product ratings.

1. Use the following prompt with your agent:

   ```plain
   Implement product ratings in the storefront.

   Add a 5-star rating display with a review count underneath each product name on the product list page, product details page, and product recommendations.

   Use the dropin slot system where available.

   Use @RATINGS_API_CONTRACT.md to understand how to use the ratings API.
   ```

1. Observe the changes in the codebase, and watch the Apparel page for updates.

   You should see the following changes in your development environment and browser:

   * A product rating "component" is automatically created.
   * The component is integrated into product-details, product-list-page, and product-recommendations blocks using [dropin slots](https://experienceleague.adobe.com/developer/commerce/storefront/dropins/customize/slots).
   * Stars display with proper fill proportions based on mock rating values.

![Product Ratings Implementation](../assets/product-ratings-implementation.png){width="600" zoomable="yes"}

## Tutorial recap

Here is a summary of the topics covered in this tutorial:

* **Feature implementation**: How to describe new functionality to an AI agent.
* **Iterative changes**: Making quick modifications to existing code.
* **Complex UI components**: Building interactive features with visual references.
* **Dropin integration**: Working with [!DNL Adobe Commerce] dropin containers and slots.
* **Component reusability**: Creating shared components used across multiple blocks.

## Next steps

For further experimentation with this tutorial, use the following suggestions to further customize your ratings extension, or create your own modifications:

### Change the star colors

Use the following prompt to your agent:

```plain
Change the star fill color to red.
```

**Expected outcome:**

The stars are changed to red.

![Red Star Colors](../assets/red-star-colors.png){width="600" zoomable="yes"}

### Add rating distribution modal

The following steps show how the agent handles complex UI features with visual references.

1. **Before starting:** Save the following mock image and paste it into the chat with your storefront agent.

   ![Rating Distribution Mockup](../assets/rating-distribution-mockup.png){width="600" zoomable="yes"}

1. Follow these steps to create the ratings distribution modal using the reference image as a guide:

   * Update the API to return additional data representing the ratings distribution.
   * Update the API Contract.
   * Update the contact in the storefront codebase.
   * Ask the storefront agent to use the reference image and updated API Contract to add the ratings distribution to the PDP page.

1. Observe the following changes in the codebase, and watch the Apparel page for updates:

   * How the agent interprets the visual mockup
   * Whether it uses appropriate HTML structure for accessibility
   * How it handles the positioning and interaction states

#### Troubleshooting

* If the modal does not appear, check the browser console for errors.
* If positioning is off, ask the agent to fix it using the following format:

   ```plain
   adjust the modal position to be...
   ```

![Rating Distribution Modal](../assets/rating-distribution-modal.png){width="600" zoomable="yes"}
 -->
