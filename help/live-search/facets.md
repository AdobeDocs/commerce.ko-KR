---
title: 패싯
description: '[!DNL Live Search] 패싯은 여러 차원의 특성 값을 검색 기준으로 사용합니다.'
exl-id: d036265e-1868-461d-ab4c-7f469b1c6f5b
source-git-commit: 269f68868f5df14b1ca3709c01f6c17e6775df05
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 0%

---

# 패싯

페이스팅은 속성 값의 여러 차원을 검색 기준으로 사용하는 고성능 필터링 방법입니다. 패싯된 검색은 비슷하지만 표준 [계층화된 탐색](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/navigation/navigation-layered.html?lang=ko)보다 훨씬 &quot;스마트합니다. 사용 가능한 필터 목록은 검색 결과에서 반환된 제품의 [필터링 가능한 특성](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/navigation/navigation-layered.html?lang=ko#filterable-attributes)에 의해 결정됩니다.

[!DNL Live Search]은(는) `productSearch`과(와) 관련된 얼굴 및 기타 데이터를 반환하는 [!DNL Live Search] 쿼리를 사용합니다. 코드 예는 개발자 설명서에서 [`productSearch` 쿼리](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/)를 참조하십시오.

![필터링된 검색 결과](assets/storefront-search-results-run.png)

패싯 내에서 쇼핑객은 &quot;스타일&quot; 아래에 &quot;기본&quot; 및 &quot;청결&quot;과 같은 여러 옵션을 선택할 수 있고 검색 결과가 업데이트되어 해당 스타일만 표시됩니다. 마찬가지로, 쇼핑객이 &quot;스타일&quot; 아래에 &quot;기본&quot;을 선택하고 &quot;기후&quot; 아래에 &quot;실내&quot;를 선택하는 경우 검색 결과가 업데이트되어 선택한 스타일과 선택한 기후를 표시합니다.

정의된 패싯을 URL 매개 변수로 사용할 수 있으며 매개 변수 값 `http://yourstore.com?brand=acme&color=red`을(를) 기준으로 결과가 필터링됩니다.

## 요구 사항 충족

얼굴에 대한 카테고리 및 제품 속성 요구 사항은 계층 탐색에 사용된 필터링 가능한 속성과 유사합니다. 속성의 각 상점 속성은 &quot;검색 결과에서 사용 계층화된 탐색&quot; 값을 &quot;예&quot;로 설정해야 합니다. 관리자의 [!DNL Stores] > [!DNL Attribute] 메뉴에서 특성 구성을 검토하고 업데이트할 수 있습니다.

>[!NOTE]
>
>제품 범주를 패싯으로 정의하는 경우 패싯에는 범주와 하위 범주의 `url_path`이(가) 표시됩니다.
>
>![범주 패싯](assets/facet-category.png)

[의 패싯 요구 사항에 대한 자세한 내용은 &#x200B;](./boundaries-limits.md#facets)경계 및 제한[!DNL Live Search]을 참조하세요.

경합할 속성이 많은 경우 속성을 하나의 &quot;meta-attribute&quot;로 결합하는 것이 좋습니다. 예를 들어, 신발은 일반적으로 숫자 크기를 가지지만 셔츠는 일반적으로 &quot;S/M/L/XL&quot; 크기를 갖습니다. 이 두 가지 유형의 크기를 하나의 검색 가능한 속성으로 결합할 수 있습니다.

| 설정 | 설명 |
|--- |--- |
| [범주 표시 설정](https://experienceleague.adobe.com/docs/commerce-admin/catalog/categories/create/categories-display-settings.html?lang=ko) | 앵커 - `Yes` |
| [특성 속성](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/create/attribute-product-create.html?lang=ko) | [카탈로그 입력 형식](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/attributes-input-types.html?lang=ko) - `Yes/No`, `Dropdown`, `Multiple Select`, `Price`, `Visual swatch`(위젯 전용), `Text swatch`(위젯 전용) |
| 속성 storefront 속성 | 검색 결과 계층 탐색 - `Yes`에 사용 |

## Facet 집계

Facet 집계는 다음과 같이 수행됩니다. 상점 앞에 세 패싯(카테고리, 색상 및 가격)이 있고 쇼핑객 필터가 세 패싯 모두에 있는 경우(색상 = 파랑, 가격은 $10.00-50.00, 카테고리 = `promotions`).

* `categories` 집계 - `categories`을(를) 집계한 다음 `color` 및 `price` 필터를 적용하지만 `categories` 필터는 적용하지 않습니다.
* `color` 집계 - `color`을(를) 집계한 다음 `price` 및 `categories` 필터를 적용하지만 `color` 필터는 적용하지 않습니다.
* `price` 집계 - `price`을(를) 집계한 다음 `color` 및 `categories` 필터를 적용하지만 `price` 필터는 적용하지 않습니다.

## 기본 속성 값

다음 제품 특성에는 [에서 사용하고 기본적으로 활성화된 &#x200B;](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/product-attributes.html?lang=ko)상점 속성[!DNL Live Search]이 있습니다.

| 속성 | Storefront 속성 | 속성 |
|---|---|---|
| 정렬 가능 | 제품 목록에서 정렬에 사용됨 | `price` |
| 검색 가능 | 검색에 사용 | `price` <br />`sku`<br />`name` |
| 필터링 가능한 검색 | 레이어 탐색에서 사용 - 필터링 가능(결과 포함) | `price`<br />`visibility`<br />`category_name` |

## 기본 비시스템 속성 속성

다음 표는 Luma 샘플 데이터와 관련된 속성을 포함하여 비시스템 속성의 기본 검색 및 필터링 가능한 속성을 보여 줍니다. *검색에 사용* 특성 속성을 `Yes`(으)로 설정하면 [!DNL Live Search] 및 기본 Adobe Commerce 모두에서 특성을 검색할 수 있습니다.

| 속성 코드 | 검색 가능 | 레이어 탐색에서 사용 |
|--- |--- |--- |
| 활동 | 예 | 필터링 가능(결과 포함) |
| attributes_brand | 예 | 아니요 |
| 브랜드 | 예 | 아니요 |
| 기후 | 예 | 필터링 가능(결과 포함) |
| 고리 | 예 | 필터링 가능(결과 포함) |
| 색상 | 예 | 필터링 가능(결과 포함) |
| 비용 | 예 | 아니요 |
| eco_collection | 예 | 필터링 가능(결과 포함) |
| 성별 | 예 | 필터링 가능(결과 포함) |
| 제조업체 | 예 | 필터링 가능(결과 포함) |
| 재질 | 예 | 필터링 가능(결과 포함) |
| 목적 | 예 | 필터링 가능(결과 포함) |
| strap_bags | 예 | 필터링 가능(결과 포함) |
| style_general | 예 | 필터링 가능(결과 포함) |

## 기본 시스템 속성 속성

다음 표에서는 시스템 속성의 기본 검색 및 필터링 가능한 속성을 보여 줍니다.

| 속성 코드 | 검색 가능 | 레이어 탐색에서 사용 |
|--- |--- |--- |
| allow_open_amount | 예 | 필터링 가능(결과 포함) |
| 설명 | 예 | 아니요 |
| 이름 | 예 | 아니요 |
| 가격 | 예 | 필터링 가능(결과 포함) |
| short_description | 예 | 아니요 |
| sku | 예 | 아니요 |
| 상태 | 예 | 아니요 |
| tax_class_id | 예 | 아니요 |
| url_key | 예 | 아니요 |
| 두께 | 예 | 아니요 |
