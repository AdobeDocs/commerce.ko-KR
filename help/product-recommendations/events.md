---
title: 데이터 수집
description: 이벤트가  [!DNL Product Recommendations]에 대한 데이터를 수집하는 방법을 알아봅니다.
feature: Services, Recommendations, Eventing
exl-id: 0d5317e3-c049-4fcd-a8e4-228668d89386
source-git-commit: fe96b2922583c0fcb0fcadbdacead6267806f44b
workflow-type: tm+mt
source-wordcount: '1343'
ht-degree: 0%

---

# 데이터 수집

[[!DNL Product Recommendations]](install-configure.md) 또는 [[!DNL Live Search]](../live-search/install.md)과(와) 같은 SaaS 기반 Adobe Commerce 기능을 설치하고 구성하면 모듈이 동작 데이터 수집을 상점 앞에 배포합니다. 이 메커니즘은 쇼핑객으로부터 익명으로 처리된 행동 데이터를 수집하고 [!DNL Product Recommendations]을(를) 실행합니다. 예를 들어 `view` 이벤트는 `Viewed this, viewed that` 권장 사항 유형을 계산하는 데 사용되고 `place-order` 이벤트는 `Bought this, bought that` 권장 사항 유형을 계산하는 데 사용됩니다.

>[!NOTE]
>
>[!DNL Product Recommendations]을(를) 위한 데이터 수집에는 PII(개인 식별 정보)가 포함되지 않습니다. 쿠키 ID 및 IP 주소와 같은 모든 사용자 식별자는 엄격히 익명으로 처리됩니다. [자세히](https://www.adobe.com/privacy/experience-cloud.html)를 알아보세요.

## 의료 서비스 고객

의료 서비스 고객이고 [데이터 연결](../data-connection/hipaa-readiness.md#installation) 확장의 일부인 [데이터 서비스 HIPAA 확장](../data-connection/overview.md)을 설치한 경우 [!DNL Product Recommendations]에서 사용하는 Storefront 이벤트 데이터는 더 이상 캡처되지 않습니다. 이는 storefront 이벤트 데이터가 클라이언트측에서 생성되기 때문입니다. 상점 이벤트 데이터를 계속 캡처하고 보내려면 [!DNL Product Recommendations]에 대한 이벤트 컬렉션을 다시 사용하도록 설정하십시오. 자세한 내용은 [일반 구성](https://experienceleague.adobe.com/en/docs/commerce-admin/config/general/general.html#data-services)을 참조하세요.

## 데이터 유형 및 이벤트

제품 권장 사항에 사용되는 데이터에는 두 가지 유형이 있습니다.

- **행동** - 제품 보기, 장바구니에 추가된 항목, 구매 등 사이트에 대한 쇼핑객 참여의 데이터.
- **카탈로그** - 이름, 가격, 가용성 등의 제품 메타데이터입니다.

`magento/product-recommendations` 모듈을 설치하면 Adobe Sensei에서 동작 및 카탈로그 데이터를 집계하여 각 권장 사항 유형에 대한 제품 권장 사항을 만듭니다. 그런 다음 제품 추천 서비스는 이러한 추천을 권장 제품 _items_&#x200B;을(를) 포함하는 위젯 형태로 상점 앞에 배포합니다.

일부 추천 유형은 구매자의 행동 데이터를 사용하여 머신 러닝 모델을 교육하여 개인화된 추천을 구축합니다. 다른 권장 사항 유형은 카탈로그 데이터만 사용하며 동작 데이터는 사용하지 않습니다. 사이트에서 제품 추천 사용을 빠르게 시작하려면 다음과 같은 카탈로그 전용 추천 유형을 사용할 수 있습니다.

- `More like this`
- `Visual similarity`

### 콜드 스타트

행동 데이터를 사용하는 권장 사항 유형은 언제 사용할 수 있습니까? 상황에 따라 다릅니다. 이를 _콜드 스타트_ 문제라고 합니다.

_콜드 스타트_ 문제는 모델이 교육하고 효과를 얻는 데 걸리는 시간을 나타냅니다. 제품 추천의 경우, 이는 Adobe Sensei이 사이트에 추천 단위를 배포하기 전에 머신 러닝 모델을 교육할 충분한 데이터를 수집할 때까지 대기하는 것을 의미합니다. 모델에 데이터가 많을수록 권장 사항이 더 정확하고 유용합니다. 데이터 수집은 라이브 사이트에서 수행되므로 `magento/production-recommendations` 모듈을 설치하고 설정하여 이 프로세스를 일찍 시작하는 것이 좋습니다.

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
- Adobe Commerce은 4시간마다 행동 데이터를 다시 계산합니다. 권장 사항은 사이트에서 오래 사용될수록 더 정확해집니다.

각 권장 사항 유형의 교육 진행률을 시각화할 수 있도록 [권장 사항 만들기](create.md#readiness-indicators) 페이지에 준비 표시기가 표시됩니다.

라이브 사이트에서 데이터가 수집되고 기계 학습 모델이 교육되는 동안 권장 사항을 설정하는 데 필요한 다른 테스트 및 구성 작업을 완료할 수 있습니다. 이 작업을 마칠 때까지 모델에는 유용한 권장 사항을 만드는 데 필요한 데이터가 충분하므로 이를 상점에 배포할 수 있습니다.

사이트에 대부분의 제품 SKU에 대한 트래픽(보기, 구매, 트렌드)이 충분하지 않은 경우 학습 프로세스를 완료하는 데 필요한 데이터가 충분하지 않을 수 있습니다. 이로 인해 관리자의 준비 표시기가 중단된 것처럼 보일 수 있습니다. 준비 지표는 상인이 자신의 스토어에 더 나은 권장 사항 유형을 선택할 때 다른 데이터 포인트를 제공하기 위한 것입니다. 숫자는 안내서이며 100%에 도달할 수 없습니다. 준비 지표에 대해 [자세히 알아보기](create.md#readiness-indicators).

### 백업 권장 사항 {#backuprecs}

입력 데이터가 요청한 모든 권장 사항 항목을 한 단위로 제공하기에 충분하지 않은 경우 Adobe Commerce에서 백업 권장 사항을 제공하여 권장 사항 단위를 채웁니다. 예를 들어, 홈 페이지에 `Recommended for you` 추천 유형을 배포하는 경우, 사이트에서 처음 구매하는 사람이 개인화된 제품을 정확히 추천하기에 충분한 행동 데이터를 생성하지 않았습니다. 이 경우 Adobe Commerce은 `Most viewed` 추천 유형에 따라 이 구매자에게 항목을 표시합니다.

입력 데이터 수집이 부족한 경우 다음 추천 유형은 `Most viewed` 추천 유형으로 대체됩니다.

- `Recommended for you`
- `Viewed this, viewed that`
- `Viewed this, bought that`
- `Bought this, bought that`
- `Trending`
- `Conversion (view to purchase)`
- `Conversion (view to cart)`

### 이벤트

[Adobe Commerce Storefront 이벤트 수집기](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/#quick-start)는 Storefront에 배포된 모든 이벤트를 나열합니다. 해당 목록에 [!DNL Product Recommendations]과(와) 관련된 이벤트의 하위 집합이 있습니다. 이러한 이벤트는 쇼핑객이 상점 위의 추천 단위와 상호 작용할 때 데이터를 수집하여 지표에 권한을 부여하여 추천의 실적을 분석합니다.

| 이벤트 | 설명 |
| --- | --- |
| `impression-render` | 페이지에서 추천 단위가 렌더링될 때 전송됩니다. 페이지에 두 개의 추천 단위(구매, 보기)가 있으면 두 개의 `impression-render` 이벤트가 전송됩니다. 이 이벤트는 노출 지표를 추적하는 데 사용됩니다. |
| `rec-add-to-cart-click` | 쇼핑객이 추천 단위에서 항목에 대한 **장바구니에 추가** 단추를 클릭합니다. |
| `rec-click` | 쇼핑객이 추천 단위에서 제품을 클릭합니다. |
| `view` | 페이지 아래로 스크롤하는 것처럼 추천 단위가 적어도 50% 이상 볼 수 있게 되면 전송됩니다. 예를 들어 추천 단위에 두 개의 줄이 있는 경우 한 줄과 두 번째 줄의 한 픽셀이 쇼핑객에게 표시되면 `view` 이벤트가 전송됩니다. 쇼핑객이 페이지를 위아래로 여러 번 스크롤하는 경우 `view` 이벤트가 쇼핑객이 페이지에서 전체 추천 단위를 다시 볼 수 있는 횟수만큼 전송됩니다. |

제품 추천 지표는 Luma 상점 첫 번째 면에 최적화되어 있지만 다른 상점 첫 번째 구현과도 작동합니다.

- [Edge Delivery 상점](https://experienceleague.adobe.com/developer/commerce/storefront/setup/analytics/instrumentation/?lang=ko)
- [PWA Studio](https://developer.adobe.com/commerce/pwa-studio/integrations/product-recommendations/)
- [사용자 지정 프런트 텐트(React, Vue JS)](headless.md)

#### 필수 대시보드 이벤트

[[!DNL Product Recommendations] 대시보드](workspace.md)를 채우려면 다음 이벤트가 필요합니다.

| 대시보드 열 | 이벤트 | 조인 필드 |
| ---------------- | --------- | ----------- |
| 노출 횟수 | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-unit-render` | `unitId` |
| 보기 | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-unit-render`, `recs-unit-view` | `unitId` |
| 클릭수 | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-item-click`, `recs-add-to-cart-click` | `unitId` |
| 매출 | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-item-click`, `recs-add-to-cart-click`, `place-order` | `unitId`, `sku`, `parentSku` |
| LT 수익 | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-item-click`, `recs-add-to-cart-click`, `place-order` | `unitId`, `sku`, `parentSku` |
| CTR | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-unit-render`, `recs-item-click`, `recs-add-to-cart-click` | `unitId`, `sku`, `parentSku` |
| vCTR | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-unit-render`, `recs-unit-view`, `recs-item-click`, `recs-add-to-cart-click` | `unitId`, `sku`, `parentSku` |

다음 이벤트는 제품 추천에만 해당되지 않지만, Adobe Sensei에서 쇼핑객 데이터를 올바르게 해석하는 데 필요합니다.

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
| 이 항목을 보고 다른 항목을 구입함 | 제품 Recs | `page-view`<br>`product-view` | 제품 세부 사항 페이지<br>장바구니/체크아웃 |
| 구매, 구매 | 제품 Recs | `page-view`<br>`product-view` | 제품 세부 사항 페이지 |
| 트렌딩 | `page-view`<br>`product-view` | 제품 세부 사항 페이지 |
| 전환: 구매로 보기 | 제품 Recs | `page-view`<br>`product-view` | 제품 세부 사항 페이지 |
| 전환: 구매로 보기 | 제품 Recs | `page-view`<br>`place-order` | 장바구니/체크아웃 |
| 전환: 장바구니로 보기 | 제품 Recs | `page-view`<br>`product-view` | 제품 세부 사항 페이지 |
| 전환: 장바구니로 보기 | 제품 Recs | `page-view`<br>`add-to-cart` | 제품 세부 사항 페이지<br>제품 목록 페이지<br>장바구니<br>위시리스트 |

#### 주의 사항

- 광고 차단기 및 개인 정보 설정을 사용하면 이벤트가 캡처되지 않을 수 있으며, 이로 인해 참여 및 매출 [지표](workspace.md#column-descriptions)이(가) 제대로 보고되지 않을 수 있습니다. 또한 페이지 또는 네트워크 문제로 인해 일부 이벤트가 전송되지 않을 수 있습니다.
- [Headless 구현](headless.md)은(는) 제품 권장 사항 대시보드를 제공하는 이벤트를 구현해야 합니다.
- 구성 가능한 제품의 경우 제품 권장 사항은 권장 사항 단위에서 상위 제품의 이미지를 사용합니다. 구성 가능한 제품에 이미지가 지정되지 않은 경우 해당 특정 제품에 대한 추천 단위가 비어 있게 됩니다.

>[!NOTE]
>
>[쿠키 제한 모드](https://experienceleague.adobe.com/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law.html?lang=ko)가 활성화된 경우, Adobe Commerce은 구매자가 쿠키 사용에 동의할 때까지 행동 데이터를 수집하지 않습니다. 쿠키 제한 모드 가 비활성화되면 Adobe Commerce은 기본적으로 동작 데이터를 수집합니다.
