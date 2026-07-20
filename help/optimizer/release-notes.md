---
title: Adobe Commerce Optimizer 릴리스 노트
description: 상점 카탈로그 데이터 검색을 위한 데이터 수집 REST API 및 GraphQL API에 대한 업데이트를 포함하여  [!DNL Adobe Commerce Optimizer]에 대한 월별 릴리스 정보입니다.
feature: Release Notes
role: Admin, Developer, User, Leader
recommendations: noCatalog
badgeSaas: label="SaaS만" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 [!DNL Adobe Commerce Optimizer] 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."
exl-id: e420d461-9ea2-4e32-aa37-230b14a297d7
TQID: https://experienceleague.adobe.com/apcpxN0AOniRcHDCa5MMAVWysxRO5mTcudXXXjET-Lo
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 27cbf66e4851f0d21ecc039fd53aa838b4c211ba
workflow-type: tm+mt
source-wordcount: 1365
ht-degree: 0%

---

# 릴리스 정보

다음 릴리스 노트에는 다음을 포함하여 [!DNL Adobe Commerce Optimizer]에 대한 업데이트가 포함되어 있습니다.

* [[!DNL Adobe Commerce Optimizer Studio]](overview.md#quick-tour)의 새로운 기능 및 향상된 기능.
* [데이터 수집 REST API](https://developer.adobe.com/commerce/services/reference/rest/) 및 [상점 카탈로그 데이터 검색을 위한 GraphQL API](https://developer.adobe.com/commerce/services/reference/graphql/)에 대한 업데이트.

  {{aco-api-updates-and-dropins}}

## 2026년 7월

>[!BEGINSHADEBOX]

_2026년 7월 20일_

![수정](../assets/fix.svg) **범주 탐색 성능** - 범주 서비스에 성능 최적화를 적용하여 `CategoryNavigation` 쿼리에 대해 처리량이 증가하고 P99 지연이 감소하여 높은 부하 상태에서 서비스 응답성과 전반적인 사용자 환경이 개선되었습니다.
<!--DATA-7131 DATA-7250-->

{{aco-release}}

>[!ENDSHADEBOX]

## 2026년 6월

>[!BEGINSHADEBOX]

_2026년 6월 24일_

<!-- v1.3 -->

![새로 만들기](../assets/new.svg) **새 `canEditQuantity` 필드**—카탈로그 서비스 GraphQL의 `ProductViewOptionValueProduct`에 `canEditQuantity`을(를) 추가했습니다. Commerce 관리자의 번들 선택에 대해 선택적 **사용자 정의** 수량 설정을 노출하므로 상점 소비자는 번들 선택 수량을 편집할 수 있는지 여부를 결정할 수 있습니다.
<!--COMOPT-2050-->

### 의미 체계 검색

[!DNL Adobe Commerce Optimizer]은(는) 이제 **[!UICONTROL Settings]**&#x200B;의 [**고급 검색**](./settings.md#advanced-search) 탭에서 **[의미 체계 검색]**&#x200B;을(를) 지원합니다. 시맨틱 검색은 키워드 검색과 함께 AI를 사용하여 의미와 컨텍스트별로 제품을 일치시켜 자연어 쿼리에 대한 빈 검색 페이지를 줄입니다. 적격한 영어 카탈로그에 대해 기본적으로 활성화되어 있습니다. 동일한 탭에서 **[!UICONTROL Semantic boost]**, **[!UICONTROL Similarity threshold]** 및 **[!UICONTROL Fuzzy search]**&#x200B;을(를) 선택적으로 조정할 수 있습니다. 속성 설정 또는 상점 첫 화면 변경이 필요하지 않습니다. [자세히 알아보기](./setup/semantic-search.md)

### 권장 가격 필터(베타)

이제 제품 추천 단위는 **[!UICONTROL Filter products]** 단계에서 [**가격 필터**](./merchandising/recommendations/filters.md#price)&#x200B;를 지원합니다. 권장 제품을 현재 표시된 제품의 활성 가격 장부에서 **최종 계산된 가격**&#x200B;과 비교하는 제품 세부 정보 페이지에서 **정적** 최소 및 최대 범위 또는 **동적** 규칙을 사용하여 후보를 포함하거나 제외합니다. 가격 규칙은 후보 세트를 필터링합니다. 제품의 등급을 다시 매기지 않습니다. [자세히 알아보기](./merchandising/recommendations/filters.md#price)

{{aco-release}}

>[!ENDSHADEBOX]

## 2026년 5월

>[!BEGINSHADEBOX]

### 지능형 순위 증가

[&#128279;](./merchandising/rules/add.md#intelligent-ranking-boost)검색, 기본 제품 목록 및 [범주 페이지](./merchandising/rules/add.md#rule-types)에 대한 머천다이징 규칙에 이제 **[!UICONTROL Intelligent Ranking Boost]**&#x200B;이(가) 포함됩니다. **가장 많이 본 항목** 또는 **트렌드**&#x200B;와 같은 전략이 범주 목록의 검색 및 동작 신호에 대한 텍스트 관련성과 관련하여 제품 순서에 미치는 영향을 얼마나 강력하게 조정할 수 있습니다. 규칙 미리 보기는 사용자의 설정을 반영합니다. 부스트는 쿼리 시간에 적용되므로 변경할 때 카탈로그를 다시 동기화할 필요가 없습니다.

### API 업데이트

_2026년 5월 28일_

<!-- v1.2 -->

![수정](../assets/fix.svg) **전체 탐색 트리**—경로에 태그가 지정되지 않은 중간 노드가 있으면 태그가 지정된 하위 범주가 패밀리가 필터링된 `navigation` 트리에 올바르게 포함됩니다. 이 수정 사항을 통해 쇼핑객은 탐색에서 모든 관련 카테고리를 볼 수 있으므로 항목을 더 쉽게 탐색하고 검색할 수 있습니다.
<!--DATA-7183-->

![수정](../assets/fix.svg) **`categoryTree` 요청의 빈 슬러그 처리**—`slugs` 인수에 빈 문자열이 포함된 경우 [`categoryTree`](https://developer.adobe.com/commerce/services/graphql-api/merchandising-api/index.html#query-categoryTree) 쿼리에서 내부 서버 오류를 반환하는 문제를 해결했습니다. 이제 빈 슬러그 값이 무시되므로 상점 및 통합은 실패한 요청 없이 카테고리 데이터를 계속 확인합니다.
<!--DATA-7184-->

![수정](../assets/fix.svg) **`searchCategory`요청이 대소문자를 구분하지 않고 알파벳순으로 결과를 반환합니다** - 이제 `searchCategory` 쿼리가 대소문자를 구분하지 않고 알파벳순으로 검색 결과를 정렬하여 일관되고 예측 가능한 순서를 유지합니다. 접두사가 더 짧은 범주는 이름이 동일하지 않은 경우 먼저 나타납니다.
<!--COMOPT-2142-->

_2026년 5월 4일_

<!--v1.53-->

**올바른 통화 표시** - 이제 상점 제품 가격에 모든 제품 유형에 대한 올바른 통화 코드(예: USD)가 표시됩니다. 이전에는 일부 제품에 예상 통화가 아닌 `NONE`이(가) 표시되어 가격이 누락되었습니다.

<!--DATA-7115-->

{{aco-release}}

>[!ENDSHADEBOX]

## 2026년 4월

**릴리스 날짜**: 2026년 4월 7일

>[!BEGINSHADEBOX]

### 카탈로그 규칙

[카테고리 규칙](./merchandising/rules/add.md)은(는) 머천다이징 규칙을 확장하므로 카테고리를 타겟팅하고 카테고리 페이지의 제품 순서를 검색과 동일한 순위 및 작업(고정, 증폭, 저장)으로 제어할 수 있습니다.

### 가격 필터(베타)

이제 권장 사항 필터에 [가격 범위 필터](./merchandising/recommendations/filters.md#price)(최소 및 최대)가 포함됩니다.

### API 업데이트

_2026년 4월 29일_

<!--v1.52 release-->

**요청 일괄 처리 필요** - 이제 GraphQL API는 카탈로그 데이터를 검색할 때 요청당 최대 100개의 SKU를 적용합니다. [문서화된 제한 및 경계](https://experienceleague.adobe.com/en/docs/commerce/optimizer/boundaries-limits#product-discovery)를 참조하십시오.

<!--DATA-7156-->

_2026년 4월 17일_

<!--v1.51 release-->

**GraphQL을 사용하여 이름별로 범주 찾기** — 새 [`searchCategory`](https://developer.adobe.com/commerce/services/reference/graphql/) 쿼리가 상점 및 통합에 대한 페이지 매김과 일치하는 범주를 반환합니다. 매개 변수 및 응답 필드에 대해서는 API 참조 를 참조하십시오. <!--COMOPT-1819-->

_2026년 4월 7일_

<!--v1.50 release-->

**간단한 범주 조회** — [categoryTree](https://developer.adobe.com/commerce/services/graphql-api/merchandising-api/index.html#query-categoryTree) 쿼리는 `family`을(를) 선택 항목으로 처리하므로 패밀리를 제공하지 않고 슬러그로 범주를 해결할 수 있습니다.

{{aco-release}}

>[!ENDSHADEBOX]

## 2026년 3월

이번 달에는 [[!DNL Adobe Commerce Optimizer Studio]](overview.md#quick-tour) 릴리스가 없습니다. 아래 API 업데이트 를 참조하십시오.

>[!BEGINSHADEBOX]

### API 업데이트

_2026년 3월 24일_

이제 다이내믹 번들이 계산된 가격 범위를 반환합니다. <!--DATA-7014-->

{{aco-release}}

>[!ENDSHADEBOX]

## 2026년 2월

**릴리스 날짜**: 2026년 2월 19일

>[!BEGINSHADEBOX]

### 머천다이징 규칙 및 권장 사항에 대한 카탈로그 보기

이제 [추천 단위를 만들기](./merchandising/recommendations/create.md) 또는 [머천다이징 규칙](./merchandising/rules/add.md)할 때 카탈로그 보기를 지정할 수 있습니다.

### API 업데이트

_2026년 2월 19일_

<!--v1.48-->

**더 풍부한 상점 카테고리 컨텐츠** — [categoryTree](https://developer.adobe.com/commerce/services/graphql-api/merchandising-api/index.html#query-categoryTree) 쿼리는 이제 설명, 이미지 및 SEO 메타 태그를 반환하므로 상점이 더 풍부한 범주 페이지를 렌더링할 수 있습니다.<!--DATA-6933-->

_2026년 2월 12일_

<!--v1.49-->

**카테고리별 제품 데이터 향상** - GraphQL API는 [`CategoryProductView`](https://developer.adobe.com/commerce/services/graphql-api/merchandising-api/index.html#definition-CategoryProductView){target="blank"} 유형을 추가하므로 적은 횟수로 카테고리별로 제품을 쿼리하고 필터링할 수 있습니다.

{{aco-release}}

>[!ENDSHADEBOX]

## 2026년 1월

이번 달에는 [[!DNL Adobe Commerce Optimizer Studio]](overview.md#quick-tour) 릴리스가 없습니다. 아래 API 업데이트 를 참조하십시오.

>[!BEGINSHADEBOX]

### API 업데이트

_2026년 1월 19일_

* **REST API로 더 풍부한 범주 지원** — [범주 API](https://developer.adobe.com/commerce/services/reference/rest/#operation/createCategories) 작업은 이제 `families` 외에 선택적 `metaTags`, `images` 및 `description` 값을 허용하므로 범주에 더 풍부한 머천다이징 및 SEO 세부 정보를 제공할 수 있습니다.

{{aco-release}}

>[!ENDSHADEBOX]

## 2025년 12월

**릴리스 날짜**: 2025년 12월 10일

>[!BEGINSHADEBOX]

### 영업 기회

이제 머천다이저는 [Adobe Sites Optimizer](./manage-results/opportunities.md)를 통해 AI 기반 권장 사항을 얻어 사이트 문제를 감지하고 성능 수정 사항을 제안할 수 있습니다.

### 카탈로그 레이어

이제 머천다이저는 소스 카탈로그를 편집하지 않고 [카탈로그 계층](./setup/catalog-layer.md)을 사용하여 제품 데이터를 오버레이하고 계층 우선 순위를 관리하며 Adobe Sites Optimizer 자동 수정을 사용할 수 있습니다.

{{aco-release}}

>[!ENDSHADEBOX]

## 2025년 11월

이번 달에는 [[!DNL Adobe Commerce Optimizer Studio]](overview.md#quick-tour) 릴리스가 없습니다. 아래 API 업데이트 를 참조하십시오.

>[!BEGINSHADEBOX]

### API 업데이트

_2025년 11월 21일_

**데이터 수집 REST API에 대한 인증 지침을 업데이트했습니다** — 이 지침은 이제 데이터 수집 서비스에 대한 올바른 Developer Console 자격 증명 범위와 OAuth 액세스 토큰을 참조합니다. 자격 증명 범위가 오래된 경우 계속 액세스할 수 있도록 다시 생성합니다.

_2025년 11월 3일_

<!-- v1.43 -->

**GraphQL의 계층화된 지역화된 제품 콘텐츠** - 이제 [!DNL Adobe Commerce Optimizer]에서 채널별 로케일 인식 제품 콘텐츠를 제공할 수 있습니다.

* 고객 세그먼트에 따라 제품 콘텐츠 맞춤화
* 기본 카탈로그 데이터를 복제하지 않고 로케일별 재정의 적용
* 레이어 마스크로 필드 수준 무시 제어
* 프리미엄, 시즌 및 모바일에 최적화된 콘텐츠 레이어 사용

GraphQL API 스키마 변경 없음: 레이어는 기존 `products` 쿼리 및 요청 헤더를 통해 적용됩니다. [카탈로그 계층](./setup/catalog-layer.md)을 참조하세요.

{{aco-release}}

>[!ENDSHADEBOX]

## 2025년 10월

**릴리스 날짜**: 2025년 10월 14일

>[!BEGINSHADEBOX]

### Commerce Optimizer Salesforce Commerce 커넥터

[!DNL Commerce Optimizer Salesforce Commerce Connector]은(는) Salesforce B2C Commerce 카탈로그 데이터를 [!DNL Commerce Optimizer]에 동기화하는 새로운 App Builder 시작 키트입니다.<!--COMOPT-536-->

**관리자용:**

* Salesforce 카탈로그 변경 내용(제품, 가격, 메타데이터, 가격 장부)은 [!DNL Commerce Optimizer]에 자동으로 동기화됩니다.
* 더 적은 통합 접점을 위해 [!DNL Adobe Commerce] 외부에서 실행됩니다.
* 예약된 업데이트는 머천다이징 및 권장 사항에 대한 [!DNL Commerce Optimizer] 데이터를 최신 상태로 유지합니다.

**개발자용:**

* Salesforce 카탈로그를 SaaS 머천다이징 서비스에 수집하기 위한 확장 가능한 프레임워크입니다.
* 더 빠른 빌드 및 문제 해결을 위해 구현, 디자인 문서 및 코드 샘플을 참조하십시오.

### 계층화된 검색

* **계층화된 검색(GA)** — 이제 제품 검색에서 `startsWith` 및 `contains` 일치를 지원합니다. [계층화된 검색 및 확장된 검색 유형](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#layered-search-and-expansion-of-search-types)을 참조하세요.

### API 업데이트

* _2025년 10월 17일_

  **제품 계층 수집을 위한 REST API 지원 추가** — [카탈로그 계층 API](https://developer.adobe.com/commerce/services/reference/rest/#tag/Product-Layers)를 사용하여 특정 컨텍스트, 로케일 또는 비즈니스 요구 사항에 대한 기본 제품 데이터를 사용자 지정하고 재정의합니다. 레이어를 만든 후 [Adobe Commerce Optimizer Studio](./setup/catalog-layer.md)에서 적용하고 관리할 수 있습니다.<!--DATA-6632-->

* _2025년 10월 14일_

  **프로그래밍 범주 트리** - REST(전역 또는 채널별)를 통해 탐색과 그룹화에 사용할 범주 트리를 최대 10,000개의 트리와 트리당 500개의 범주로 만들고 업데이트하고 관리합니다. _카탈로그 데이터 수집 REST API 참조_&#x200B;에서 [범주](https://developer.adobe.com/commerce/services/reference/rest/#tag/Categories){target="blank"}을 참조하십시오.<!--DCAT-2649-->

* _2025년 10월 8일_

  **데이터 수집을 위한 더 명확한 범주 매핑** — 범주 슬러그 형식 및 계층 규칙을 설명하고 제품 `routes.path` 값이 기존 범주 슬러그와 일치해야 함을 명확히 하는 새로운 지침입니다(예: `men/clothing`).

{{aco-release}}

>[!ENDSHADEBOX]

## 2025년 9월

이번 달에는 [[!DNL Adobe Commerce Optimizer Studio]](overview.md#quick-tour) 릴리스가 없습니다. 아래 API 업데이트 를 참조하십시오.

>[!BEGINSHADEBOX]

### API 업데이트

_2025년 9월 23일_

* **REST API를 사용하여 범주 관리** — [범주 API](https://developer.adobe.com/commerce/services/reference/rest/#operation/createCategories)를 사용하여 범주를 만들고 관리합니다. 범주는 제품을 논리 그룹으로 구성하고 슬러그 기반 경로를 통해 중첩된 계층을 지원합니다. 제품에 범주를 할당한 후 GraphQL `[navigation](https://developer.adobe.com/commerce/services/reference/graphql/#navigation)` 및 `[categoryTree](https://developer.adobe.com/commerce/services/reference/graphql/#categorytree)` 쿼리를 사용하여 해당 범주를 검색하여 상점 메뉴와 범주 트리를 렌더링합니다.<!--DCAT-2626-->

{{aco-release}}

>[!ENDSHADEBOX]

## 2025년 8월

**릴리스 날짜**: 2025년 8월 28일

>[!BEGINSHADEBOX]

### 현재 사용 가능한 EU 지역

IMS 조직에서 EU 프로덕션 지역(**eu1**)을 사용할 수 있습니다. Cloud Manager에서 [인스턴스  [!DNL Commerce Optimizer] 추가](./get-started.md#step-1-create-an-instance)할 때 **[!UICONTROL European Union]**&#x200B;을(를) **[!UICONTROL Region]**(프로덕션 전용)으로 선택합니다.

유럽 연합 지역의 기본 프로덕션 URL은 다음과 같습니다.

* 책임자: `https://eu1.admin.commerce.adobe.com`
* REST 및 GraphQL: `https://eu1.api.commerce.adobe.com`

![지역 필드가 있는 Cloud Manager 인스턴스 만들기 대화 상자](./assets/create-instance.png){width="600" align="center" zoomable="yes"}

{{aco-release}}

>[!ENDSHADEBOX]

