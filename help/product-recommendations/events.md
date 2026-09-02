---
title: 데이터 수집
description: 이벤트가  [!DNL Product Recommendations]에 대한 데이터를 수집하는 방법을 알아봅니다.
feature: Services, Recommendations, Eventing
exl-id: 0d5317e3-c049-4fcd-a8e4-228668d89386
TQID: https://experienceleague.adobe.com/efHRMj3u3w-xvUgMnEYDpX0D-BDCUyjhhrkMaa3n-xg
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c4147b6e-073b-4d3c-9ab1-d60f2f4434ef
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: eb30f47f-d87a-400f-8f78-63ce7979ff56
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 88a0b1a238090dec85e0f79082d264b720999fee
workflow-type: tm+mt
source-wordcount: 937
ht-degree: 0%

---

# 데이터 수집

[[!DNL Product Recommendations]](install-configure.md)을(를) 설치하고 구성할 때 모듈은 동작 데이터 수집을 상점 앞에 배포합니다. 이 메커니즘은 쇼핑객으로부터 익명으로 처리된 행동 데이터를 수집하고 [!DNL Product Recommendations]을(를) 실행합니다. 예를 들어 `view` 이벤트는 `Viewed this, viewed that` 권장 사항 유형을 계산하는 데 사용되고 `place-order` 이벤트는 `Bought this, bought that` 권장 사항 유형을 계산하는 데 사용됩니다.

[!DNL Product Recommendations] 이벤트가 수집하는 동작 데이터에 대한 자세한 내용은 [개발자 설명서](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#product-recommendations)를 참조하세요.

>[!NOTE]
>
>[!DNL Product Recommendations]을(를) 위한 데이터 수집에는 PII(개인 식별 정보)가 포함되지 않습니다. 쿠키 ID 및 IP 주소와 같은 모든 사용자 식별자는 엄격히 익명으로 처리됩니다. [자세히](https://www.adobe.com/privacy/experience-cloud.html)를 알아보세요.

## 의료 서비스 고객

의료 고객이고 [데이터 연결](../data-connection/overview.md) 확장에 포함된 [데이터 서비스 HIPAA 확장](../data-connection/hipaa-readiness.md#installation)을 설치한 경우 [!DNL Product Recommendations]은(는) 클라이언트 측에서 생성되므로 상점 이벤트 데이터 수집을 중지합니다.

Storefront 이벤트 데이터 수집 및 전송을 재개하려면 [!DNL Product Recommendations]에 대한 이벤트 수집을 다시 활성화하십시오. 자세한 내용은 [일반 구성](https://experienceleague.adobe.com/en/docs/commerce-admin/config/general/general#data-services)을 참조하세요.

## 데이터 유형 및 이벤트

제품 권장 사항에 사용되는 데이터에는 두 가지 유형이 있습니다.

- **행동** - 제품 보기, 장바구니에 추가된 항목, 구매 등 사이트에 대한 쇼핑객 참여의 데이터.
- **카탈로그** - 이름, 가격, 가용성 등의 제품 메타데이터입니다.

`magento/product-recommendations` 모듈을 설치하면 Adobe AI에서 동작 및 카탈로그 데이터를 집계하여 각 권장 사항 유형에 대한 제품 권장 사항을 만듭니다. 그런 다음 제품 추천 서비스는 이러한 추천을 권장 제품 _items_&#x200B;을(를) 포함하는 위젯 형태로 상점 앞에 배포합니다.

일부 추천 유형은 구매자의 행동 데이터를 사용하여 머신 러닝 모델을 교육하고 개인화된 추천을 생성합니다. 다른 것들은 카탈로그 데이터에만 의존합니다. 제품 권장 사항을 빠르게 사용하려면 다음 카탈로그 전용 권장 사항 유형 중에서 선택합니다.

- `More like this`
- `Visual similarity`

### 콜드 스타트

행동 데이터를 사용하는 권장 사항 유형은 언제 사용할 수 있습니까? 상황에 따라 다릅니다. 이 상황을 _콜드 스타트_ 문제라고 합니다.

_콜드 시작_ 문제는 효과적인 권장 사항을 생성하기 전에 머신 러닝 모델을 교육하는 데 필요한 시간입니다. 제품 추천의 경우, Adobe AI은 추천 단위를 배포하기 전에 모델을 교육할 충분한 데이터를 수집해야 합니다. 일반적으로 더 많은 데이터가 추천 정확도와 유용성을 향상시킵니다. 데이터 수집은 라이브 사이트에서 수행되므로 `magento/product-recommendations` 모듈을 설치 및 구성하여 이 프로세스를 일찍 시작하십시오.

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

라이브 사이트에서 데이터를 수집하고 머신 러닝 모델이 트레이닝되는 동안 나머지 테스트 및 구성 작업을 완료하십시오. 모델에 유용한 권장 사항을 생성하기에 충분한 데이터가 있으면 권장 사항 단위를 상점에 배포합니다.

대부분의 제품 SKU에 대해 사이트에 충분한 트래픽(보기, 구매 또는 트렌드)이 수신되지 않으면 학습 프로세스가 완료되지 않아 관리자의 준비 표시기가 중단될 수 있습니다. 준비 지표는 상인이 자신의 점포에 가장 적합한 추천 유형을 선택하는 데 도움이 되지만, 안내서일 뿐이며 절대 100%에 도달하지 못할 수 있습니다. 준비 지표에 대해 자세히 알아보십시오. 준비 지표에 대해 [자세히 알아보기](create.md#readiness-indicators).

### 백업 권장 사항 {#backuprecs}

입력 데이터가 부족하면 추천 단위에서 요청된 모든 항목을 반환하지 못하는 경우 Adobe Commerce에서 백업 추천 항목으로 채웁니다. 예를 들어, 홈 페이지에 `Recommended for you` 권장 사항 유형을 배포한 후 처음 구매하는 사람이 개인화된 권장 사항에 대해 충분한 행동 데이터를 생성하지 않았을 수 있습니다. 이 경우 Adobe Commerce은 `Most viewed `권장 사항 유형에 따라 항목을 표시합니다.

입력 데이터 수집이 부족한 경우 다음 추천 유형은 `Most viewed` 추천 유형으로 대체됩니다.

- `Recommended for you`
- `Viewed this, viewed that`
- `Viewed this, bought that`
- `Bought this, bought that`
- `Trending`
- `Conversion (view to purchase)`
- `Conversion (view to cart)`

#### 주의 사항

- 광고 차단기 및 개인 정보 설정을 사용하면 이벤트가 캡처되지 않을 수 있으며, 이로 인해 참여 및 매출 [지표](workspace.md#column-descriptions)이(가) 제대로 보고되지 않을 수 있습니다. 또한 쇼핑객이 페이지 또는 네트워크 문제로 인해 일부 이벤트가 전송되지 않습니다.
- [Headless 구현](headless.md)은(는) 제품 권장 사항 대시보드를 제공하는 이벤트를 구현해야 합니다.
- 구성 가능한 제품의 경우 제품 권장 사항은 상위 제품의 이미지를 사용합니다. 상위 제품에 이미지가 없으면 해당 제품이 권장 사항 단위에 나타나지 않습니다.

>[!NOTE]
>
>[쿠키 제한 모드](https://experienceleague.adobe.com/en/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law)가 활성화된 경우, Adobe Commerce은 구매자가 쿠키 사용에 동의할 때까지 행동 데이터를 수집하지 않습니다. 쿠키 제한 모드 가 비활성화되면 Adobe Commerce은 기본적으로 동작 데이터를 수집합니다.
