---
title: 패싯
description: '[!DNL Live Search] 패싯은 여러 차원의 특성 값을 검색 기준으로 사용합니다.'
exl-id: d036265e-1868-461d-ab4c-7f469b1c6f5b
TQID: https://experienceleague.adobe.com/bTE-Ow8xEDfK-saxGxotnvkgHZI4QThno1dCqRbjvCc
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 452
ht-degree: 0%

---

# 패싯

페이스팅은 속성 값의 여러 차원을 검색 기준으로 사용하는 고성능 필터링 방법입니다. 패싯된 검색은 비슷하지만 표준 [계층화된 탐색](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/navigation/navigation-layered.html)보다 훨씬 &quot;스마트합니다. 사용 가능한 필터 목록은 검색 결과에서 반환된 제품의 [필터링 가능한 특성](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/navigation/navigation-layered.html#filterable-attributes)에 의해 결정됩니다.

[!DNL Live Search]은(는) [!DNL Live Search]과(와) 관련된 얼굴 및 기타 데이터를 반환하는 `productSearch` 쿼리를 사용합니다. 코드 예는 개발자 설명서에서 [`productSearch` 쿼리](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/)를 참조하십시오.

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

[!DNL Live Search]의 패싯 요구 사항에 대한 자세한 내용은 [경계 및 제한](./boundaries-limits.md#facets)을 참조하세요.

경합할 속성이 많은 경우 속성을 하나의 &quot;meta-attribute&quot;로 결합하는 것이 좋습니다. 예를 들어, 신발은 일반적으로 숫자 크기를 가지지만 셔츠는 일반적으로 &quot;S/M/L/XL&quot; 크기를 갖습니다. 이 두 가지 유형의 크기를 하나의 검색 가능한 속성으로 결합할 수 있습니다.

| 설정 | 설명 |
|--- |--- |
| [범주 표시 설정](https://experienceleague.adobe.com/docs/commerce-admin/catalog/categories/create/categories-display-settings.html) | 앵커 - `Yes` |
| [특성 속성](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/create/attribute-product-create.html) | [카탈로그 입력 형식](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/attributes-input-types.html) - `Yes/No`, `Dropdown`, `Multiple Select`, `Price`, `Visual swatch`(위젯 전용), `Text swatch`(위젯 전용) |
| 속성 storefront 속성 | 검색 결과 계층 탐색 - `Yes`에 사용 |

## Facet 집계

Facet 집계는 다음과 같이 수행됩니다. 상점 앞에 세 패싯(카테고리, 색상 및 가격)이 있고 쇼핑객 필터가 세 패싯 모두에 있는 경우(색상 = 파랑, 가격은 $10.00-50.00, 카테고리 = `promotions`).

* `categories` 집계 - `categories`을(를) 집계한 다음 `color` 및 `price` 필터를 적용하지만 `categories` 필터는 적용하지 않습니다.
* `color` 집계 - `color`을(를) 집계한 다음 `price` 및 `categories` 필터를 적용하지만 `color` 필터는 적용하지 않습니다.
* `price` 집계 - `price`을(를) 집계한 다음 `color` 및 `categories` 필터를 적용하지만 `price` 필터는 적용하지 않습니다.
