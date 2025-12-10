---
title: 라이브 검색 설정
description: ' [!DNL Live Search] 작업 영역은 검색 성능을 구성, 관리 및 모니터링하는 데 사용됩니다.'
exl-id: 07c32b26-3fa4-4fae-afba-8a10866857c3
source-git-commit: c6725fc524e9d239ccc0f16701e92ad5d2fc7729
workflow-type: tm+mt
source-wordcount: '2117'
ht-degree: 0%

---

# 라이브 검색 설정

작업 영역에서는 [!DNL Live Search]의 성능을 구성, 관리 및 모니터링합니다. 맨 위에 있는 메뉴를 통해 각 기능 영역의 도구에 액세스할 수 있습니다. 사용 가능한 기능은 현재 메뉴 선택을 반영합니다.

![Workspace](assets/workspace.png)

## 데이터 수집

작업 영역의 각 기능 영역에 올바른 데이터가 포함되어 있는지 확인하려면 선택한 Storefront 구현을 기반으로 데이터 수집을 구성해야 합니다.

1. Luma - 데이터 수집은 즉시 사용할 수 있습니다.
1. Headless - 데이터 수집은 상점 구현에 따라 수동으로 구성해야 합니다.

Headless Storefront를 사용하는 경우 다음 설명서를 참조하여 추가해야 하는 필수 이벤트에 대한 자세한 내용을 확인하십시오.

- Live Search 대시보드에 대한 [필수 이벤트](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#live-search).
- 필수 구성 요소로 추가해야 하는 [Storefront 이벤트 수집기](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/).
- 이벤트 구조의 [예](https://github.com/adobe/commerce-events/tree/main/examples).

### 의료 서비스 고객

의료 서비스 고객이고 [데이터 연결](../data-connection/hipaa-readiness.md#installation) 확장의 일부인 [데이터 서비스 HIPAA 확장](../data-connection/overview.md)을 설치한 경우 [!DNL Live Search]에서 사용하는 Storefront 이벤트 데이터는 더 이상 캡처되지 않습니다. 이는 storefront 이벤트 데이터가 클라이언트측에서 생성되기 때문입니다. 상점 이벤트 데이터를 계속 캡처하고 보내려면 [!DNL Live Search]에 대한 이벤트 컬렉션을 다시 사용하도록 설정하십시오. 자세한 내용은 [일반 구성](https://experienceleague.adobe.com/ko/docs/commerce-admin/config/general/general#data-services)을 참조하세요.

## 범위 설정

처음에는 모든 [&#x200B; 설정의 &#x200B;](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html?lang=ko#scope-settings)범위[!DNL Live Search]이(가) `Default Store View`(으)로 설정되어 있습니다. [!DNL Commerce] 설치에 여러 저장소 보기가 포함된 경우 Facet 설정이 적용되는 **저장소 보기**(으)로 [범위](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html?lang=ko)를 설정합니다.

## 메뉴 옵션

| 옵션 | 설명 |
|--- |--- |
| [성능](performance.md) | 대시보드는 insight에 제품 검색 성능을 제공합니다. |
| [페이스팅](facets.md) | 여러 차원의 속성 값을 사용하여 검색 기준을 구체화하는 고성능 필터링입니다. |
| [동의어](synonyms.md) | 쇼핑객이 카탈로그에 있는 것과 다른 제품을 찾는 데 사용할 수 있는 단어를 포함하도록 검색 범위를 확장하십시오. |
| [머천다이징 검색](rules.md) | 예약된 작업을 트리거하는 논리 규칙으로 검색 환경을 구성합니다. 비즈니스 목표를 지원하기 위해 검색 결과를 보정하기 위해 제품을 증폭, 매몰, 고정 또는 숨깁니다. |
| [카테고리 머천다이징](category-merch.md) | 카테고리 수준에서 규칙 및 지능형 머천다이징을 적용합니다. |
| [GraphQL](graphql.md) | 저장소 관리자에 로그인한 개발자는 실제 카탈로그 데이터로 쿼리를 작성하고 테스트할 수 있습니다. 자세한 내용을 보려면 [&#x200B; 개발자 설명서에서 &#x200B;](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/)GraphQL 개요[!DNL Live Search]로 이동하십시오. |
| [설정](settings.md) | 가격 패싯 값을 상점 가격 범위별로 그룹화하는 방법을 결정하고 색인화 언어를 설정합니다. |

## 속성을 검색 가능한 것으로 설정

고도로 타깃팅된 결과를 만들려면 [검색 가능](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/product-attributes.html?lang=ko)&#x200B;(`searchable=true`) 제품 특성 집합을 검토하십시오. 관련성을 보장하려면 명확하고 간결한 의미가 있는 콘텐츠가 포함된 경우에만 속성을 검색할 수 있도록 하십시오. 기본적으로 검색을 사용할 수 있지만 검색 결과의 정밀도를 낮출 수 있는 `description`과(와) 같이 정확도가 낮고 긴 텍스트가 포함된 특성은 사용하지 마십시오. 예를 들어, &quot;반바지&quot;를 검색하는 사람이 &quot;반팔&quot;이라는 용어가 포함된 설명이 있는 셔츠가 있으면 해당 셔츠가 검색 결과에 포함됩니다.

속성을 검색할 수 있도록 허용하려면 다음 단계를 완료하십시오.

1. 관리자의 경우 **스토어** > *특성* > **제품**(으)로 이동합니다.
1. 검색할 특성을 선택하십시오(예: `color`).
1. **Storefront 속성**&#x200B;을(를) 선택하고 **검색에 사용**&#x200B;을(를) `yes`(으)로 설정합니다.

[!DNL Live Search]은(는) Adobe Commerce 내에 설정된 제품 특성의 [weight](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/search/search-results.html?lang=ko#weighted-search)도 준수합니다. 가중치가 높은 속성은 검색 결과 내에서 더 높게 표시됩니다.

다음 속성은 항상 검색할 수 있습니다.

- `sku`
- `name`
- `categories`

### 복잡한 제품의 속성 동작

복잡한 제품 유형(구성 가능한 제품, 번들 제품 및 그룹화된 제품)의 경우 [!DNL Live Search]은(는) 상위 제품 및 하위 제품 모두의 속성 값을 인덱싱하므로 상위 제품을 동일한 속성의 여러 값과 연결할 수 있습니다. 이렇게 하면 변형 기반 필터링이 가능합니다. 예를 들어 상위 제품에 색상 세트가 없더라도 변형에 파란색이 있으면 &quot;파란색&quot;으로 필터링할 때 구성 가능한 셔츠가 나타납니다.

이 기능은 색상 및 크기와 같은 특성에 잘 작동하지만 `new_arrival`, `product_ranking`, `promotion_label` 또는 사용자 지정 가격 특성과 같은 특성에 예기치 않은 결과가 발생할 수 있습니다. 예를 들어 구성 가능한 제품(SKU-001)에 `new_arrival = true`이(가) 있지만 하위 변형(SKU-001-01)에 `new_arrival = false`이(가) 있는 경우 상위 제품 SKU-001은 두 값(`true` 및 `false`) 모두로 인덱싱되므로 두 조건에 대한 검색 결과에 표시될 수 있습니다.

### 계층화된 검색 및 검색 유형 확장

계층화된 검색 또는 검색 내의 검색은 기존의 검색 기능을 확장하여 추가 검색 매개 변수를 포함하도록 하는 강력한 속성 기반 필터링 시스템입니다. 이러한 추가 검색 매개 변수를 사용하면 보다 정확하고 유연한 제품 검색을 수행할 수 있습니다.

>[!NOTE]
>
>계층화된 검색은 라이브 검색 4.6.0에서 사용할 수 있습니다.

계층화된 검색을 사용하여 다음과 같은 작업을 수행할 수 있습니다.

- 쇼핑객이 검색 결과 내에서 검색할 수 있도록 활성화합니다.
- 계층화된 검색의 두 번째 레이어에서 `startsWith` 및 `contains` 검색 색인을 사용하여 결과를 세분화합니다.

고급 검색 기능은 특정 연산자를 사용하여 `filter` 쿼리[`productSearch`의 &#x200B;](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/) 매개 변수를 통해 구현됩니다.

- **계층화된 검색** - 다른 검색 컨텍스트에서 검색 - 이 기능을 사용하면 검색 쿼리에 대해 최대 두 개의 계층을 검색할 수 있습니다. For example:

   - **계층 1 검색** - `product_attribute_1`에서 &quot;모터&quot;를 검색합니다.
   - **계층 2 검색** - `product_attribute_2`에서 &quot;부품 번호 123&quot;을 검색합니다. 이 예제에서는 결과 내에서 &quot;motor&quot;에 대해 &quot;part number 123&quot;을 검색합니다.

  아래에 설명된 대로 계층화된 검색의 두 번째 계층에서 `startsWith` 검색 인덱싱과 `contains` 검색 인덱싱을 모두 사용할 수 있습니다.

- **검색 인덱싱으로 시작** - `startsWith` 인덱싱을 사용하여 검색 이 새로운 기능을 통해 다음과 같은 작업을 수행할 수 있습니다.

   - 속성 값이 지정된 문자열로 시작하는 제품을 검색합니다.
   - 구매자가 속성 값이 특정 문자열로 끝나는 제품을 검색할 수 있도록 &quot;다음으로 끝남&quot; 검색을 구성합니다. &quot;다음으로 끝남&quot; 검색을 활성화하려면 제품 속성을 역순으로 수집해야 하며 API 호출도 역순 문자열이어야 합니다. 예를 들어 &quot;pants&quot;로 끝나는 제품 이름을 검색하려면 이 이름을 &quot;stnap&quot;으로 보내야 합니다.

- **검색 인덱싱을 포함** - 포함 인덱싱을 사용하여 특성을 검색합니다. 이 새로운 기능을 통해 다음과 같은 작업을 수행할 수 있습니다.

   - 더 큰 문자열 내에서 쿼리를 검색하고 있습니다. 예를 들어 구매자가 문자열 &quot;HAPE-123&quot;에서 제품 번호 &quot;PE-123&quot;을 검색하는 경우,

      - 참고: 이 검색 유형은 자동 완성 검색을 수행하는 기존 [구 검색](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#phrase)과(와) 다릅니다. 예를 들어 제품 속성 값이 &quot;outdoor pants&quot;인 경우 구문 검색은 &quot;out pan&quot;에 대한 응답을 반환하지만 &quot;or ants&quot;에 대한 응답은 반환하지 않습니다. 그러나 에는 검색이 포함되어 있으며 &quot;or ants&quot;에 대한 응답을 반환합니다.

이러한 새 조건은 검색 결과를 구체화하기 위한 검색 쿼리 필터링 메커니즘을 향상시킵니다. 이러한 새 조건은 기본 검색 쿼리에 영향을 주지 않습니다.

#### 구현

1. 관리에서 [제품 특성을 검색 가능하도록 설정](https://experienceleague.adobe.com/ko/docs/commerce-admin/catalog/product-attributes/product-attributes-add#step-5-describe-the-storefront-properties)합니다.

   검색 가능한 [특성](https://experienceleague.adobe.com/ko/docs/commerce-admin/catalog/product-attributes/attributes-input-types) 목록을 확인하세요.

1. **포함**(기본값) 또는 **다음으로 시작**&#x200B;과 같이 해당 특성에 대한 검색 기능을 지정하십시오. **포함**&#x200B;에 대해 최대 6개의 특성을 사용할 수 있도록 지정하고 **다음으로 시작**&#x200B;에 대해 최대 6개의 특성을 사용할 수 있도록 지정할 수 있습니다. 또한 **Contains** 인덱싱의 경우 문자열 길이는 50자 이하로 제한됩니다.

   ![검색 기능 지정](./assets/search-filters-admin.png)

1. 새로운 [&#x200B; 및 &#x200B;](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#filtering-using-search-capability) 검색 기능을 사용하여 [!DNL Live Search] API 호출을 업데이트하는 방법에 대한 예는 `contains`개발자 설명서`startsWith`를 참조하십시오.

   검색 결과 페이지에서 이러한 새 조건을 구현할 수 있습니다. 예를 들어, 쇼핑객이 검색 결과를 더 구체화할 수 있는 페이지에 새 섹션을 추가할 수 있습니다. 구매자가 &quot;제조업체&quot;, &quot;부품 번호&quot; 및 &quot;설명&quot;과 같은 특정 제품 속성을 선택할 수 있도록 할 수 있습니다. 여기에서 `contains` 또는 `startsWith` 조건을 사용하여 해당 특성 내에서 검색합니다.

### 패싯이 아닌 계층화된 검색을 사용해야 하는 경우

계층화된 검색 및 패싯은 제품 검색에서 서로 다른 용도로 사용되며, 둘 중 선택은 특정 사용 사례에 따라 다릅니다.

**다음의 경우 계층화된 검색 사용:**

- 여러 기준을 사용하여 검색 결과 내에서 검색해야 합니다.
- 사용자가 부분 정보를 알고 있는 부품 번호, SKU 또는 기술 사양으로 작업
- 쇼핑객은 중첩된 기준으로 단계별 결과 범위를 좁힐 필요가 있다.
- 단일 쿼리에서 여러 검색 기준을 결합하여 API 호출 수를 줄이려고 합니다.
- 표준 패싯 탐색을 넘어서는 비즈니스별 검색 패턴을 구현해야 합니다.

**패싯을 사용할 때:**

- 일반적인 카테고리, 가격, 브랜드 및 속성 필터링 제공
- 사용자가 쉽게 이해하고 선택할 수 있는 직관적인 필터 옵션 제공
- 현재 검색 결과에 따라 사용 가능한 옵션 표시
- 사용자가 사용 가능한 옵션을 이해하는 데 도움이 되는 필터 카운트 및 범위 표시
- 색상, 크기, 재질 등과 같은 일반적인 제품 특성을 사용하여 작업

**모범 사례:** 사용자가 특정 기준을 가지고 있는 복잡한 기술 검색에 대해 계층화된 검색을 사용하고, 사용자가 시각적으로 탐색 및 옵션 범위를 좁히고자 하는 표준 전자 상거래 필터링에 패싯을 사용합니다.

## 패싯 및 동의어

패싯과 동의어는 쇼핑객을 위한 검색 경험을 향상시킬 수 있는 또 다른 방법입니다.

[Facet](facets.md)은(는) 필터링 가능하도록 [!DNL Live Search]에 정의된 제품 특성입니다. 필터링 가능한 특성을 [!DNL Live Search]에서 패싯으로 설정할 수 있지만 한 번에 검색할 수 있는 패싯 수에 대한 [제한](boundaries-limits.md)이 있습니다.

>[!NOTE]
>
>제품 특성 구성에 필수 속성이 있는 경우에만 제품 특성을 필터링할 수 있습니다. *검색에 사용 = 예*, *검색 결과에 사용 계층 탐색=예* 및 *계층 탐색에 사용=필터링 가능(결과 포함)*. 이러한 속성이 없거나 올바르게 설정되지 않으면 Facet 구성에 속성이 표시되지 않습니다. 구성 지침은 [패싯 추가](facets-add.md#add-a-facet)를 참조하십시오.

[동의어](synonyms.md)은(는) 사용자가 올바른 제품을 사용하도록 안내하기 위해 정의할 수 있는 용어입니다. 바지를 찾는 사용자들은 &quot;바지&quot; 또는 &quot;바지&quot;를 타이핑할 수 있습니다. 이러한 검색어가 사용자에게 &quot;바지&quot; 결과를 가져오도록 동의어를 설정할 수 있습니다.

## Commerce 구성 설정

다음 섹션에서는 [!DNL Live Search]에 대해 지원되는 Commerce 구성 설정과 지원되지 않는 구성 설정에 대해 설명합니다.

### 지원되는 구성 값

>[!IMPORTANT]
>
>라이브 검색 4.0.0에서 기본적으로 활성화되어 있는 제품 목록 위젯을 사용하는 것이 좋습니다. 위젯은 향후 릴리스에서 어댑터 구현을 완전히 대체하도록 타깃팅됩니다. 자세한 내용은 [제품 목록 위젯 사용](install.md#enable-product-listing-widgets)을 참조하세요.

| Commerce 구성 설정 | 설명 | 팝오버에서 지원됨 | 어댑터에서 지원 |
|---|---|---|---|
| 스토어 > 구성 > 카탈로그 > 카탈로그 > 카탈로그 검색 > 페이지당 모든 제품 허용 | `Yes`(으)로 설정된 경우 &quot;페이지당 표시&quot; 컨트롤에 `ALL` 옵션을 포함합니다. | 예. 최대 500개 제품 | 예. 최대 500개 제품 |
| 저장소 > 구성 > 카탈로그 > 카탈로그 > 카탈로그 검색 > 최소 쿼리 길이 | 카탈로그 검색에 허용되는 최소 문자 수입니다. | 예 | 예 |
| 스토어 > 구성 > 카탈로그 > 카탈로그 > 카탈로그 검색 > 그리드 허용 값의 페이지당 제품 | 눈금 보기에 표시되는 제품 수를 결정합니다. | 예 | 예 |
| 스토어 > 구성 > 카탈로그 > 카탈로그 > 카탈로그 검색 > 그리드의 페이지당 제품 기본값 | 그리드 보기에서 기본적으로 페이지당 표시되는 제품 수를 결정합니다. | 예. 최대 500개 제품 | 예. 최대 500개 제품 |
| 스토어 > 구성 > 카탈로그 > 재고 > 재고 부족 제품 표시 | 품절된 제품을 표시합니다. | 예 | 예 |
| Stores > Configuration > Currency > Default Display Currency | 가격을 표시하는 데 사용되는 기본 통화. | 예 | 예 |
| 스토어 > 구성 > 일반 > 통화 설정 > 통화 옵션 > 기본 통화 | 모든 온라인 결제 거래에 사용되는 기본 통화. | 예 | 예 |

위젯 제품 목록 페이지 및 팝오버의 가격은 구성된 환율을 사용하여 기본 표시 통화로 전환됩니다.

### 지원되지 않는 구성 값

| Commerce 구성 설정 | 설명 | 메모 |
|---|---|---|
| 스토어 > 구성 > 카탈로그 > 상점 > 목록 모드 | 검색 결과 목록의 형식을 결정합니다. | 올바르게 렌더링되지만 일부 페이지 상호 작용에 대해 이벤트가 전송되지 않음 |
| 저장소 > 구성 > 카탈로그 > 카탈로그 > 카탈로그 검색 > 최대 쿼리 길이 | 카탈로그 검색에 허용되는 최대 문자 수. | 구현되지 않음. 검색 서비스는 최대 255자를 허용합니다. |
| 구성 > 판매 > 세금 > 가격 표시 설정 > 카탈로그에 제품 가격 표시 | 카탈로그에 게시된 제품 가격에 세금이 포함되는지 또는 제외되는지 여부를 결정하거나 두 가지 버전의 가격을 표시합니다(하나는 세금이 포함됨). |  |
| 스토어 > 구성 > 카탈로그 > 상점 > 제품 목록 정렬 기준 | 검색 결과 목록의 정렬 순서를 결정합니다. | [!DNL Live Search] [제품 목록 페이지 위젯](plp-styling.md)에 적용되지 않음 |

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
