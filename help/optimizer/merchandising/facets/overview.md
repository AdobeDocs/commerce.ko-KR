---
title: 패싯 개요
description: ' [!DNL Adobe Commerce Optimizer] 의 패싯과 패싯이 검색 결과를 개선하는 방법에 대해 알아봅니다.'
badgeSaas: label="SaaS만" type="Positive" url="https://experienceleague.adobe.com/ko/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."
source-git-commit: 3020386cd051b4453ed6b90d2c694a5bb31dfb24
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---

# 패싯

패싯은 속성 값의 여러 차원을 검색 기준으로 사용하는 고성능 필터링 방법입니다.

![필터링된 검색 결과](../../assets/storefront-search-results-run.png)

패싯 내에서 쇼핑객은 &quot;스타일&quot; 아래에 &quot;기본&quot; 및 &quot;청결&quot;과 같은 여러 옵션을 선택할 수 있고 검색 결과가 업데이트되어 해당 스타일만 표시됩니다. 마찬가지로, 쇼핑객이 &quot;스타일&quot; 아래에 &quot;기본&quot;을 선택하고 &quot;기후&quot; 아래에 &quot;실내&quot;를 선택하는 경우 검색 결과가 업데이트되어 선택한 스타일과 선택한 기후를 표시합니다.

정의된 패싯을 URL 매개 변수로 사용할 수 있으며 매개 변수 값 `http://yourstore.com?brand=acme&color=red`을(를) 기준으로 결과가 필터링됩니다.

## Facet 집계

Facet 집계는 다음과 같이 수행됩니다. 상점 앞에 세 패싯(카테고리, 색상 및 가격)이 있고 쇼핑객 필터가 세 패싯 모두에 있는 경우(색상 = 파랑, 가격은 $10.00-50.00, 카테고리 = `promotions`).

- `categories` 집계 - `categories`을(를) 집계한 다음 `color` 및 `price` 필터를 적용하지만 `categories` 필터는 적용하지 않습니다.
- `color` 집계 - `color`을(를) 집계한 다음 `price` 및 `categories` 필터를 적용하지만 `color` 필터는 적용하지 않습니다.
- `price` 집계 - `price`을(를) 집계한 다음 `color` 및 `categories` 필터를 적용하지만 `price` 필터는 적용하지 않습니다.

## 기본 속성 값

다음 [제품 특성](https://developer-stage.adobe.com/commerce/services/composable-catalog/data-ingestion/api-reference/#operation/createProductMetadata)은(는) [!DNL Adobe Commerce Optimizer]에서 사용되며 기본적으로 활성화되어 있습니다.

| 속성 | 설명 | 속성 |
|---|---|---|
| 정렬 가능 | 제품 목록에서 정렬에 사용됨 | `price` |
| 검색 가능 | 검색에 사용 | `price` <br />`sku`<br />`name` |

## 기본 비시스템 속성 속성

다음 표에서는 비시스템 속성의 기본 검색 및 필터링 가능한 속성을 보여 줍니다. *검색에 사용* 특성 속성을 `Yes`(으)로 설정하면 [!DNL Adobe Commerce Optimizer]에서 특성을 검색할 수 있습니다.

| 속성 코드 | 검색 가능 |
|--- |--- |
| 활동 | 예 |
| attributes_brand | 예 |
| 브랜드 | 예 |
| 기후 | 예 |
| 고리 | 예 |
| 색상 | 예 |
| 비용 | 예 |
| eco_collection |
| 성별 | 예 |
| 제조업체 | 예 |
| 재질 | 예 |
| 목적 | 예 |
| strap_bags | 예 |
| style_general | 예 |

## 기본 시스템 속성 속성

다음 표에서는 시스템 속성의 기본 검색 및 필터링 가능한 속성을 보여 줍니다.

| 속성 코드 | 검색 가능 |
|--- |--- |
| allow_open_amount | 예 |
| 설명 | 예 |
| 이름 | 예 |
| 가격 | 예 |
| short_description | 예 |
| sku | 예 |
| 상태 | 예 |
| tax_class_id | 예 |
| url_key | 예 |
| 두께 | 예 |
