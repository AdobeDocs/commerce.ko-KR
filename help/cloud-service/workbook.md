---
title: 등급 확장 튜토리얼
description: App Builder 및 AI 지원 개발 도구를 사용하여 Adobe Commerce as a Cloud Service에 대한 제품 등급 확장을 빌드하는 방법을 알아봅니다.
role: Developer
hide: true
hidefromtoc: true
source-git-commit: 453b21f89d2024a8d6927fa082affdd5abb6e5cd
workflow-type: tm+mt
source-wordcount: '1337'
ht-degree: 0%

---

# Adobe Developers Live - Adobe Commerce 랩 워크북

이 실습에서는 [!DNL Adobe Commerce as a Cloud Service] 및 AI 지원 개발 도구를 사용하여 [!DNL Adobe App Builder]에 대한 제품 등급 확장을 빌드하는 과정을 안내합니다.

## 전제 조건 확인

다음 사전 요구 사항이 설치되어 있는지 확인합니다.

```bash
# Check Node.js version (should be 22.x.x)
node --version

# Check npm version (should be 9.0.0 or higher)
npm --version

# Check Git
git --version

# Check Bash
bash --version
```

## Adobe Developer Console에 로그인

1. [Adobe Developer Console](https://developer.adobe.com/console){target="_blank"}(으)로 이동합니다.
1. 이미 로그인한 경우 오른쪽 상단의 프로필 아이콘을 클릭하고 **로그아웃** 단추를 클릭합니다.
1. 시트에 입력한 랩 이메일 ID 및 암호를 사용하여 로그인합니다.
1. 보조 전자 메일 주소 또는 전화 번호를 추가하라는 메시지가 표시되면 **지금 아님**&#x200B;을 클릭합니다.
1. 조직 프로필을 선택하라는 메시지가 표시되면 **Adobe Commerce Labs**&#x200B;를 선택합니다.

   ![조직 선택](./assets/select-org.png){width="600" zoomable="yes"}

1. 약관에 동의하라는 메시지가 표시되면 링크를 클릭하여 약관을 읽은 다음 **동의 및 계속**&#x200B;을 클릭합니다.

   ![약관 동의](./assets/accept-terms.png){width="600" zoomable="yes"}

## 설치 스크립트 실행

[필수 구성 요소](#verify-prerequisites)가 설치되어 있고 Adobe Developer Console에 로그인한 경우 설치 스크립트를 다운로드하여 실행하십시오. 또는 [랩 필수 구성 요소](workbook-prerequisites.md) 단계를 따라 스크립트를 수동으로 설정할 수 있습니다.

1. 설치 스크립트가 포함된 저장소를 복제합니다.

   ```bash
   git clone https://github.com/adobe-commerce/commerce-adl-2025.git
   ```

   >[!NOTE]
   >
   >스크립트가 실패하면 [필수 구성 요소](workbook-prerequisites.md)를 참조하여 스크립트에 오류가 발생한 위치를 계속합니다.

1. 저장소로 이동합니다.

   ```bash
   cd commerce-adl-2025
   ```

1. 설치 스크립트를 실행합니다.

   ```bash
   bash adl-setup.sh
   ```

   스크립트가 실행되는 동안 사용자 이름과 암호를 입력하라는 메시지가 나타나며, 이 메시지는 실습 도중 제공됩니다. 사용자 이름은 위치와 좌석 번호를 반영합니다. 예를 들어, CA 산호세, 좌석 123에 있는 경우 사용자 이름은 `sjc-adl-123@adobeeventlab.com`입니다.

   또한 시트 번호 및 **stage** 작업 영역에 해당하는 프로젝트를 선택해야 합니다. 프로젝트 이름은 위치와 시트 번호를 반영합니다. 예를 들어, CA 산호세, 좌석 123에 있는 경우 프로젝트 이름은 `SJC ADL 123`이(가) 됩니다.

## 확장 개발

이 섹션에서는 AI 지원 개발 도구를 사용하여 Adobe Commerce as a Cloud Service에 대한 등급 확장을 개발하는 프로세스를 안내합니다.

### 확장성 AI 도구 설치

`extension` 폴더에서 AI 지원 개발 도구를 설정합니다.

```bash
cd extension
```

```bash
aio commerce extensibility tools-setup
```

![AI 도구 설치](./assets/install-ai-tools.png){width="600" zoomable="yes"}

### 커서 열기

>[!NOTE]
>
>AI 지원 개발 도구를 사용하여 작업할 때 에이전트가 생성하는 코드 및 응답에는 자연스러운 변형이 있을 것입니다.
>코드에 문제가 발생하면 언제든지 에이전트에게 디버그를 지원하도록 요청할 수 있습니다.

[!DNL Cursor] 응용 프로그램을 열고 `extension` 폴더로 이동하거나 [Cursor CLI](https://cursor.com/docs/configuration/shell#installing-cli-commands)가 설치되어 있는 경우 터미널에 다음 명령을 입력하십시오.

```bash
cursor .
```

![커서 열기](./assets/open-cursor.png){width="600" zoomable="yes"}

이 시점에서 모든 [!DNL Cursor] 규칙이 `.cursor/rules` 폴더에 설치됩니다. **의** MCP 설정[!DNL Cursor]에서 MCP 도구를 찾을 수 있습니다. `commerce-extensibility` 도구 집합이 오류 없이 사용하도록 설정되어 있는지 확인하십시오. 오류가 표시되면 도구 세트를 끄고 켜십시오.

![커서 설정](./assets/cursor-settings.png){width="600" zoomable="yes"}

Cursor의 컨텍스트에 추가된 설명서가 있는 경우 이를 비활성화해야 합니다. [!UICONTROL **커서**] > [!UICONTROL **설정**] > [!UICONTROL **커서 설정**] > [!UICONTROL **색인화 및 문서**]&#x200B;(으)로 이동하여 나열된 문서를 삭제합니다.

![설명서 비활성화](./assets/disable-documentation.png){width="600" zoomable="yes"}

### 코드 생성

이 섹션에서는 AI 지원 도구를 사용하여 제품 등급 확장에 대한 코드를 생성하는 방법을 보여줍니다.

#### 요구 사항 정의

제품 등급을 API로 제공하는 확장을 구현합니다. [!DNL App Builder] 확장은 지정된 SKU에 대한 등급 세부 정보에 응답합니다.

**초기 프롬프트:**

[!DNL Cursor]에서 다음 프롬프트 사용:

1. 커서에서 채팅 창을 엽니다.
1. **에이전트** 모드를 선택하십시오.
1. 다음 프롬프트를 입력합니다.

   ```text
   Implement an Adobe Commerce as a Cloud Service extension to handle Product Ratings.
   Implement a REST API to handle GET ratings requests.
   GET requests will have to support the following query parameters:
   
   sku -> product SKU
   ```

1. 에이전트가 문서 검색을 요청하는 경우 이를 허용합니다.

![커서에 프롬프트 입력](./assets/enter-prompt.png){width="600" zoomable="yes"}

상담원은 요구사항을 조사하고 질문을 명확히 합니다. 에이전트의 질문에 정확하게 답변하여 최상의 코드를 생성할 수 있도록 도와줍니다.

![에이전트가 명확한 질문을 합니다](./assets/agent-questions.png){width="600" zoomable="yes"}

**응답 프롬프트:**

다음 응답을 사용하여 에이전트의 질문에 답변합니다.

```text
Yes, this headless extension is for Adobe Commerce as a Cloud Service storefront,
but we do not need any authentication for the GET API because guest users should be able to use it on the storefront.
This extension will be called directly from the storefront,
no async invocation, such as events or webhooks, is required.
Let's start with just the GET API for now,
we will implement other CRUD operations at a later time.
We do not need a DB or storage mechanism right now,
just return random ratings data between 1 and 5 and a ratings count between 1 and 1000.
The API should only return the average rating for the product and the total number of ratings.
We do not need to add tests right now.
```

에이전트에서 구현에 대한 신뢰할 수 있는 원본 역할을 하는 `requirements.md` 파일을 만듭니다.

![요구 사항 파일을 만들었습니다](./assets/requirements-file.png){width="600" zoomable="yes"}

#### 요구 사항 확인 및 아키텍처 계획

1. `requirements.md` 파일을 검토하십시오.
1. 모든 항목이 올바르게 표시되면 에이전트에게 **2단계 - 아키텍처 계획**(으)로 이동하도록 지시합니다.
1. 아키텍처 계획을 검토합니다.
1. 코드 생성을 진행하도록 에이전트에 지시합니다.

![아키텍처 계획](./assets/architecture-planning.png){width="600" zoomable="yes"}

#### 코드 생성

에이전트는 필요한 코드를 생성하고 다음 단계와 함께 자세한 요약을 제공합니다.

![코드 생성 요약](./assets/code-generation-summary.png){width="600" zoomable="yes"}

![다음 단계](./assets/next-steps.png){width="600" zoomable="yes"}

### 로컬 테스트

에이전트에게 코드를 로컬에서 테스트하도록 요청합니다.

```text
Test the ratings API locally on a dev server using cURL.
```

에이전트의 지침을 따라 API가 로컬에서 작동하는지 확인합니다.

![로컬 테스트](./assets/local-testing.png){width="600" zoomable="yes"}

![로컬 테스트 결과](./assets/local-testing-1.png){width="600" zoomable="yes"}

### 확장 배포

생성된 코드를 확인한 후에는 다음 프롬프트를 사용하여 확장을 배포할 준비가 되었습니다.

```text
Deploy the ratings API.
```

#### 배포 전 평가

에이전트는 배포 전에 배포 전 준비 상태 평가를 수행합니다.

![배포 전 평가](./assets/pre-deployment-assessment.png){width="600" zoomable="yes"}

#### 배포

평가 결과가 확실하면 에이전트에게 배포를 진행하도록 지시합니다. 에이전트는 MCP 툴킷을 사용하여 자동으로 확인, 빌드 및 배포합니다.

![배포](./assets/deployment-process.png){width="600" zoomable="yes"}

### API 테스트

API를 상점 앞에 통합하기 전에 테스트할 수 있습니다.

에이전트는 새 작업의 위치와 테스트 전략을 제공합니다.

![전략 테스트](./assets/testing-strategy.png){width="600" zoomable="yes"}

#### cURL을 사용하여 수동으로 테스트

터미널에서 cURL을 사용하여 API를 수동으로 테스트합니다.

```bash
curl -s "https://<your-site>.adobeioruntime.net/api/v1/web/ratings/ratings?sku=TEST-SKU-123"
```

![cURL 테스트](./assets/curl-test.png){width="600" zoomable="yes"}

### Edge Delivery Services과 통합

등급 API를 [!DNL Adobe Commerce]에서 제공하는 [!DNL Edge Delivery Services] 상점 첫 라인과 통합하려면 에이전트에게 등급 API에 대한 요구 사항이 포함된 서비스 계약을 만들도록 요청하십시오.

```text
Create a service contract for the ratings api that I can pass on to the storefront agent. Name it RATINGS_API_CONTRACT.md
```

![서비스 계약](./assets/create-contract.png){width="600" zoomable="yes"}

![서비스 계약 세부 정보](./assets/contract.png){width="600" zoomable="yes"}

터미널로 돌아가서 `extension` 폴더에서 다음 명령을 실행하여 파일을 `storefront` 폴더에 복사합니다.

```bash
cp RATINGS_API_CONTRACT.md ../storefront
```

## 상점 앞에 연결

이 섹션은 [!DNL Adobe Commerce]개의 드로핀 및 [!DNL Edge Delivery Services]을(를) 사용하여 작업할 때 AI 에이전트와 효과적으로 통신하는 방법을 보여 주는 실제 상점 전면 기능을 구현하는 데 도움이 됩니다.

>[!NOTE]
>
>제공된 프롬프트는 시작점이며, 에이전트와 자연스럽게 대화할 수 있습니다. AI 지원 개발 도구를 사용하여 작업할 때 에이전트가 생성하는 코드 및 응답에는 자연스러운 변형이 있을 것입니다.
>
>코드에 문제가 발생하면 언제든지 에이전트에게 디버그를 지원하도록 요청할 수 있습니다.

### 평가 별 및 검토 수 구현

1. `storefront` 폴더로 이동:

   ```bash
   cd storefront
   ```

1. 새 커서 창에서 상점 폴더를 엽니다. [커서 CLI](https://cursor.com/docs/configuration/shell#installing-cli-commands)가 설치되어 있으면 터미널에 다음 명령을 입력하십시오.

   ```bash
   cursor .
   ```

1. 로컬 개발 서버를 시작합니다.

   ```bash
   npm run start
   ```

1. 브라우저에서 의류 페이지로 이동합니다.

   ```text
   http://localhost:3000/apparel
   ```

1. 보일러판 상점 UI 레이아웃을 관찰합니다.

1. 에이전트에 대해 다음 프롬프트를 사용합니다.

   ```text
   Implement product ratings to the storefront.
   Add a 5-star rating display with a review count underneath each product name on the product list page, product details page, and product recommendations.
   Use the dropin slot system where available.
   
   Use the @RATINGS_API_CONTRACT.md to understand how to use the ratings api.
   ```

   >[!NOTE]
   >
   >로컬 개발 서버를 시작하라는 메시지가 표시되면 에이전트가 이미 실행 중임을 알립니다.

1. 코드베이스의 변경 사항을 관찰하고 Apparel 페이지에서 업데이트를 확인하십시오.

**예상 결과:**

* 제품 등급 &quot;구성 요소&quot;가 자동으로 만들어집니다.
* 구성 요소는 슬롯을 사용하여 제품 세부 사항, 제품 목록 페이지 및 제품 권장 사항 블록에 통합됩니다.
* 별표는 모의 등급 값에 따라 적절한 채우기 비율로 표시됩니다.

![제품 등급 구현](./assets/product-ratings-implementation.png){width="600" zoomable="yes"}

### 별 색상 변경

에이전트에 대해 다음 프롬프트를 사용합니다.

```text
Change the star fill color to red.
```

**예상 결과:**

별들이 붉은색으로 바뀌었습니다.

![빨강 별 색](./assets/red-star-colors.png){width="600" zoomable="yes"}

## Storefront 요약

이 자습서에서는 다음 주제를 다룹니다.

* **기능 구현**: AI 에이전트에 대한 새로운 기능을 설명하는 방법입니다.
* **반복적인 변경**: 기존 코드를 빠르게 수정합니다.
* **복잡한 UI 구성 요소**: 시각적 참조를 사용하여 대화형 기능을 빌드합니다.
* **Dropin 통합**: [!DNL Adobe Commerce]개의 Dropin 컨테이너 및 슬롯을 사용하여 작업합니다.
* **구성 요소 재사용 가능성**: 여러 블록에서 사용되는 공유 구성 요소를 만드는 중입니다.

## 다음 단계

시간이 허용되면 다음 기능을 추가하여 등급 확장을 추가로 사용자 정의할 수 있습니다.

### 등급 분포 양식 추가(선택 사항)

다음 단계에서는 에이전트가 시각적 참조를 사용하여 복잡한 UI 기능을 처리하는 방법을 보여 줍니다.

1. **시작하기 전:** 다음 모의 이미지를 저장하고 상점 에이전트와 채팅에 붙여 넣으십시오.

   ![등급 배포 목업](./assets/rating-distribution-mockup.png){width="600" zoomable="yes"}

1. 다음 단계를 사용하여 참조 이미지를 기반으로 등급 분포 모달을 만드는 과정을 안내합니다.

   * 등급 분포를 나타내는 추가 데이터를 반환하도록 API를 업데이트합니다.
   * API 계약을 업데이트합니다.
   * 상점 코드베이스에서 연락처를 업데이트합니다.
   * PDP 페이지에 등급 분포를 추가하려면 참조 이미지와 업데이트된 API 계약을 사용하도록 상점 에이전트에 요청합니다.

1. 코드베이스에서 다음 변경 사항을 관찰하고 Apparel 페이지에서 업데이트를 확인하십시오.

   * 에이전트가 시각적 모형을 해석하는 방법
   * 접근성에 적절한 HTML 구조를 사용하는지 여부
   * 위치 지정 및 상호 작용 상태를 처리하는 방법

**문제 해결:**

* 모달이 나타나지 않으면 브라우저 콘솔에서 오류를 확인합니다.
* 위치가 해제되어 있으면 에이전트에게 다음 작업을 요청할 수 있습니다.

  ```text
  adjust the modal position to be...
  ```

![등급 배포 모달](./assets/rating-distribution-modal.png){width="600" zoomable="yes"}
