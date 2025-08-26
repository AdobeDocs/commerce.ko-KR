---
title: 이벤트 개요
description: ' [!DNL Adobe Commerce Optimizer] 이(가) 검색 및 권장 사항을 개선하는 데 사용하는 이벤트에 대해 알아봅니다.'
role: Admin, Developer
recommendations: noCatalog
exl-id: c102c558-a680-4622-80f0-6e5c34d497e9
source-git-commit: 7a77cc79be9b6f835668b394909ea2325b642b03
workflow-type: tm+mt
source-wordcount: '1398'
ht-degree: 0%

---

# 이벤트

이벤트는 실시간 데이터 인사이트를 활용하여 쇼핑 경험을 강화하고 전환을 유도하는 중요한 도구입니다.

[!DNL Adobe Commerce Optimizer]이(가) 상점 이벤트를 사이트에 자동으로 배포합니다. 이러한 이벤트는 사이트의 쇼핑객 상호 작용에서 데이터를 캡처합니다. 익명으로 처리된 이 데이터는 [권장 사항](../../manage-results/recommendation-performance.md), [제품 검색](../../manage-results/search-performance.md) 및 [성공 지표](../../manage-results/success-metrics.md)를 지원합니다.

>[!NOTE]
>
>데이터 수집에는 PII(개인 식별 정보)가 포함되지 않습니다. 쿠키 ID 및 IP 주소와 같은 모든 사용자 식별자는 엄격히 익명으로 처리됩니다. [자세히 알아보기](https://www.adobe.com/privacy/experience-cloud.html)

**이벤트** 페이지를 사용하여 수집 중인 상점 이벤트 데이터를 확인할 수 있습니다. 이벤트 데이터 수집을 조회하면 판매자는 상점 이벤트가 올바로 구현되었는지, 이벤트가 성공적으로 캡처되고 있는지 확인할 수 있습니다. 판매자는 이 페이지를 사용하여 잠재적인 문제를 식별하고 이벤트 문제를 해결하기 위한 단계를 수행할 수 있습니다.

## 이벤트 수

**이벤트 카운트** 탭은 검색, 클릭 수, 구매 수와 같은 쇼핑객 상호 작용을 추적하여 트렌드를 분석하고 쇼핑 경험을 개선하는 데 도움이 됩니다.

![이벤트 카운트](../../assets/event-counts.png){zoomable="yes"}

| 필드 | 설명 |
|---|---|
| **날짜 범위** | 데이터의 특정 하위 집합을 보려면 날짜 범위를 지정하겠습니다. |
| **시간당 Storefront 이벤트** | 상점에서 트리거된 이벤트 수를 보여 주는 그래프를 표시합니다. |
| **총 상점 이벤트** | 상점 전면에서 트리거된 모든 이벤트에 대한 세부 정보를 표시하는 필터링 가능한 테이블입니다. |

## 온전성 검사

**상태 검사** 탭은 각 동작 이벤트의 상태에 대한 통찰력을 제공하여 정확한 데이터 수집 및 기능을 보장합니다. &#x200B;

![상태 확인](../../assets/sanity-check.png){zoomable="yes"}

| 필드 | 설명 |
|---|---|
| **날짜 범위** | 데이터의 특정 하위 집합을 보려면 날짜 범위를 지정하겠습니다. |
| **제품 검색** | 제품 검색 결과를 개인화하는 데 필요한 이벤트를 표시합니다. **상태** 열은 이벤트가 수신되었는지 여부를 나타냅니다. |
| **권장 사항** | 제품 추천을 개인화하는 데 필요한 이벤트를 표시합니다. **상태** 열은 이벤트가 수신되었는지 여부를 나타냅니다. |

다음 섹션에서는 [제품 검색](#product-discovery) 및 [권장 사항](#recommendations)에 대한 이벤트 세부 정보를 설명합니다.

### 제품 검색

제품 검색은 이벤트를 사용하여 &quot;가장 많이 본 항목&quot; 및 &quot;이 항목을 보고 다른 항목을 본 항목&quot;과 같은 검색 알고리즘을 실행합니다.

이 표에서는 제품 검색 [순위 전략](../../merchandising/rules/add.md#intelligent-ranking)에서 사용되는 이벤트에 대해 설명합니다.

| 순위 전략 | 이벤트 | 페이지 |
| --- | --- | --- |
| 가장 많이 본 항목 | `page-view`<br>`product-view` | 제품 세부 사항 페이지 |
| 최다 구매 | `page-view`<br>`place-order` | 장바구니/체크아웃 |
| 장바구니에 가장 많이 추가됨 | `page-view`<br>`add-to-cart` | 제품 세부 사항 페이지<br>제품 목록 페이지<br>장바구니<br>위시리스트 |
| 이 항목을 보고 다른 항목도 보았습니다. | `page-view`<br>`product-view` | 제품 세부 사항 페이지 |

### 필수 대시보드 이벤트

일부 이벤트는 [검색 성능 대시보드](../../manage-results/search-performance.md)를 채우는 데 필요합니다.

| 대시보드 영역 | 이벤트 | 조인 필드 |
| ------------------- | ------------- | ---------- |
| 고유 검색 | `page-view`, `search-request-sent`, `search-response-received` | `searchRequestId` |
| 결과 없음 검색 | `page-view`, `search-request-sent`, `search-response-received` | `searchRequestId` |

### 권장 사항

권장 사항에 사용되는 데이터에는 두 가지 유형이 있습니다.

- **행동** - 제품 보기, 장바구니에 추가된 항목, 구매 등 사이트에 대한 쇼핑객 참여의 데이터.
- **카탈로그** - 이름, 가격, 가용성 등의 제품 메타데이터입니다.

Adobe Sensei은 행동 및 카탈로그 데이터를 집계하여 각 권장 사항 유형에 대한 권장 사항을 생성합니다. 그런 다음 Recommendations 서비스는 이러한 권장 사항을 권장 제품 _items_&#x200B;을(를) 포함하는 위젯 형태로 상점 앞에 배포합니다.

일부 추천 유형은 구매자의 행동 데이터를 사용하여 머신 러닝 모델을 교육하여 개인화된 추천을 구축합니다. 다른 권장 사항 유형은 카탈로그 데이터만 사용하며 동작 데이터는 사용하지 않습니다. 사이트에서 권장 사항 사용을 빠르게 시작하려면 `More like this` 권장 사항 유형을 사용할 수 있습니다.

#### 콜드 스타트

행동 데이터를 사용하는 권장 사항 유형은 언제 사용할 수 있습니까? 상황에 따라 다릅니다. 이를 _콜드 스타트_ 문제라고 합니다.

_콜드 스타트_ 문제는 모델이 교육하고 효과를 얻는 데 걸리는 시간을 나타냅니다. 권장 사항의 경우, 이는 Adobe Sensei이 사이트에 권장 사항 단위를 배포하기 전에 머신 러닝 모델을 교육할 충분한 데이터를 수집할 때까지 기다리는 것을 의미합니다. 모델에 데이터가 많을수록 권장 사항이 더 정확하고 유용합니다. 데이터 수집은 라이브 사이트에서 수행되므로 이 프로세스를 일찍 시작하는 것이 가장 좋습니다.

다음 표에서는 각 권장 사항 유형에 대해 충분한 데이터를 수집하는 데 걸리는 시간에 대한 일반적인 지침을 제공합니다.

| 추천 유형 | 교육 시간 | 메모 |
|---|---|---|
| 인기도 기반(`Most viewed`, `Most purchased`, `Most added to cart`) | 다양함 | 이벤트의 양에 따라 다릅니다. 보기가 가장 일반적이므로 더 빠르게 학습합니다. 그런 다음 장바구니에 추가한 다음 구매합니다. |
| `Viewed this, viewed that` | 추가 교육 필요 | 제품 조회수가 현저하게 많음 |
| `Viewed this, bought that`, `Bought this, bought that` | 가장 많은 교육 필요 | 구매 이벤트는 커머스 사이트에서 특히 제품 보기에 비해 가장 드문 이벤트입니다 |
| `Trending` | 인기도 기준을 설정하려면 3일의 데이터가 필요합니다. | 트렌딩은 자체 인기도 기준선과 비교하여 제품의 인기에서 최근 모멘텀을 측정하는 것입니다. 제품의 트렌드 점수는 전경 세트(24시간 동안의 최근 인기도)와 배경 세트(72시간 동안의 인기도 기준선)를 사용하여 계산됩니다. 항목의 인기가 기준선 인기보다 24시간 내에 크게 증가하면 높은 트렌드 점수를 받습니다. 모든 제품에는 이 점수가 있으며, 항상 점수가 높은 항목이 상위 트렌드 제품 집합을 구성합니다. |

교육에 필요한 시간에 영향을 줄 수 있는 기타 변수:

- 트래픽 양이 많을수록 학습 속도가 빨라집니다.
- 일부 권장 사항 유형은 다른 권장 사항보다 빠르게 교육됩니다
- [!DNL Adobe Commerce Optimizer]이(가) 매 4시간마다 동작 데이터를 다시 계산합니다. 권장 사항은 사이트에서 오래 사용될수록 더 정확해집니다.

각 권장 사항 유형의 교육 진행률을 시각화할 수 있도록 [권장 사항 만들기](../../merchandising/recommendations/create.md#readiness-indicators) 페이지에 준비 표시기가 표시됩니다.

라이브 사이트에서 데이터가 수집되고 기계 학습 모델이 교육되는 동안 권장 사항을 설정하는 데 필요한 다른 테스트 및 구성 작업을 완료할 수 있습니다. 이 작업을 마칠 때까지 모델에는 유용한 권장 사항을 만드는 데 필요한 데이터가 충분하므로 이를 상점에 배포할 수 있습니다.

사이트에 대부분의 제품 SKU에 대한 트래픽(보기, 구매, 트렌드)이 충분하지 않은 경우 학습 프로세스를 완료하는 데 필요한 데이터가 충분하지 않을 수 있습니다. 이렇게 하면 권장 사항 작업 영역의 준비 표시기가 중단된 것처럼 보일 수 있습니다. 준비 지표는 상인이 자신의 스토어에 더 나은 권장 사항 유형을 선택할 때 다른 데이터 포인트를 제공하기 위한 것입니다. 숫자는 안내서이며 100%에 도달할 수 없습니다. 준비 지표에 대해 [자세히 알아보기](../../merchandising/recommendations/create.md#readiness-indicators).

#### 백업 권장 사항

입력 데이터가 요청된 모든 권장 사항 항목을 한 단위로 제공하기에 충분하지 않으면 [!DNL Adobe Commerce Optimizer]에서 백업 권장 사항을 제공하여 권장 사항 단위를 채웁니다. 예를 들어, 홈 페이지에 `Recommended for you` 추천 유형을 배포하는 경우, 사이트에서 처음 구매하는 사람이 개인화된 제품을 정확히 추천하기에 충분한 행동 데이터를 생성하지 않았습니다. 이 경우 [!DNL Adobe Commerce Optimizer]은(는) `Most viewed` 추천 유형에 따라 이 구매자에게 항목을 표시합니다.

입력 데이터 수집이 부족한 경우 다음 추천 유형은 `Most viewed` 추천 유형으로 대체됩니다.

- `Recommended for you`
- `Viewed this, viewed that`
- `Viewed this, bought that`
- `Bought this, bought that`
- `Trending`
- `Conversion (view to purchase)`
- `Conversion (view to cart)`

#### 권장 사항별 이벤트

다음 표에는 쇼핑객이 상점 앞의 추천 단위와 상호 작용할 때 트리거되는 이벤트가 나열되어 있습니다. 수집된 이벤트 데이터는 [지표](../../manage-results/recommendation-performance.md)의 기능을 작동시켜 권장 사항이 얼마나 잘 수행되고 있는지 분석합니다.

| 이벤트 | 설명 |
| --- | --- |
| `impression-render` | 페이지에서 추천 단위가 렌더링될 때 전송됩니다. 페이지에 두 개의 추천 단위(구매, 보기)가 있으면 두 개의 `impression-render` 이벤트가 전송됩니다. 이 이벤트는 노출 지표를 추적하는 데 사용됩니다. |
| `rec-add-to-cart-click` | 쇼핑객이 추천 단위에서 항목에 대한 **장바구니에 추가** 단추를 클릭합니다. |
| `rec-click` | 쇼핑객이 추천 단위에서 제품을 클릭합니다. |
| `view` | 페이지 아래로 스크롤하는 것처럼 추천 단위가 적어도 50% 이상 볼 수 있게 되면 전송됩니다. 예를 들어 추천 단위에 두 개의 줄이 있는 경우 한 줄과 두 번째 줄의 한 픽셀이 쇼핑객에게 표시되면 `view` 이벤트가 전송됩니다. 쇼핑객이 페이지를 위아래로 여러 번 스크롤하는 경우 `view` 이벤트가 쇼핑객이 페이지에서 전체 추천 단위를 다시 볼 수 있는 횟수만큼 전송됩니다. |

#### 필수 대시보드 이벤트

[권장 사항 성능 대시보드](../../manage-results/recommendation-performance.md)를 채우려면 다음 이벤트가 필요합니다.

| 대시보드 열 | 이벤트 | 조인 필드 |
| ---------------- | --------- | ----------- |
| 노출 횟수 | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-unit-render` | `unitId` |
| 보기 | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-unit-render`, `recs-unit-view` | `unitId` |
| 클릭수 | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-item-click`, `recs-add-to-cart-click` | `unitId` |
| 매출 | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-item-click`, `recs-add-to-cart-click`, `place-order` | `unitId`, `sku`, `parentSku` |
| LT 수익 | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-item-click`, `recs-add-to-cart-click`, `place-order` | `unitId`, `sku`, `parentSku` |
| CTR | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-unit-render`, `recs-item-click`, `recs-add-to-cart-click` | `unitId`, `sku`, `parentSku` |
| vCTR | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-unit-render`, `recs-unit-view`, `recs-item-click`, `recs-add-to-cart-click` | `unitId`, `sku`, `parentSku` |

다음 이벤트는 Recommendations에만 해당되지 않지만 Adobe Sensei에서 쇼핑객 데이터를 올바르게 해석하는 데 필요합니다.

- `view`
- `add-to-cart`
- `place-order`

#### 권장 사항 유형

이 표에서는 각 권장 사항 유형에서 사용하는 이벤트에 대해 설명합니다.

| 권장 사항 유형 | 이벤트 | 페이지 |
| --- | --- | --- |
| 가장 많이 본 항목 | `page-view`<br>`product-view` | 제품 세부 사항 페이지 |
| 최다 구매 | `page-view`<br>`place-order` | 장바구니/체크아웃 |
| 장바구니에 가장 많이 추가됨 | `page-view`<br>`add-to-cart` | 제품 세부 사항 페이지<br>제품 목록 페이지<br>장바구니<br>위시리스트 |
| 이 항목을 보고 다른 항목도 보았습니다. | `page-view`<br>`product-view` | 제품 세부 사항 페이지 |
| 이 항목을 보고 다른 항목을 구입함 | `page-view`<br>`product-view` | 제품 세부 사항 페이지<br>장바구니/체크아웃 |
| 구매, 구매 | `page-view`<br>`product-view` | 제품 세부 사항 페이지 |
| 트렌딩 | `page-view`<br>`product-view` | 제품 세부 사항 페이지 |
| 전환: 구매로 보기 | `page-view`<br>`product-view` | 제품 세부 사항 페이지 |
| 전환: 구매로 보기 | `page-view`<br>`place-order` | 장바구니/체크아웃 |
| 전환: 장바구니로 보기 | `page-view`<br>`product-view` | 제품 세부 사항 페이지 |
| 전환: 장바구니로 보기 | `page-view`<br>`add-to-cart` | 제품 세부 사항 페이지<br>제품 목록 페이지<br>장바구니<br>위시리스트 |

## 지원

데이터 불일치가 발견되거나 권장 사항 및 검색 결과가 예상대로 작동하지 않는 경우 [지원 티켓을 제출](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide)하십시오.
