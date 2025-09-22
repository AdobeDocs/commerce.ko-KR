---
title: 라이브 검색 설정
description: ' [!DNL Live Search] 작업 영역은 검색 성능을 구성, 관리 및 모니터링하는 데 사용됩니다.'
exl-id: 07c32b26-3fa4-4fae-afba-8a10866857c3
source-git-commit: bb212bf88ba7bad3deb2d2d699124413f4dd76ff
workflow-type: tm+mt
source-wordcount: '1068'
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

의료 서비스 고객이고 [데이터 연결](../data-connection/hipaa-readiness.md#installation) 확장의 일부인 [데이터 서비스 HIPAA 확장](../data-connection/overview.md)을 설치한 경우 [!DNL Live Search]에서 사용하는 Storefront 이벤트 데이터는 더 이상 캡처되지 않습니다. 이는 storefront 이벤트 데이터가 클라이언트측에서 생성되기 때문입니다. 상점 이벤트 데이터를 계속 캡처하고 보내려면 [!DNL Live Search]에 대한 이벤트 컬렉션을 다시 사용하도록 설정하십시오. 자세한 내용은 [일반 구성](https://experienceleague.adobe.com/en/docs/commerce-admin/config/general/general#data-services)을 참조하세요.

## 범위 설정

처음에는 모든 [ 설정의 ](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html#scope-settings)범위[!DNL Live Search]이(가) `Default Store View`(으)로 설정되어 있습니다. [!DNL Commerce] 설치에 여러 저장소 보기가 포함된 경우 Facet 설정이 적용되는 **저장소 보기**(으)로 [범위](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html)를 설정합니다.

## 메뉴 옵션

| 옵션 | 설명 |
|--- |--- |
| [성능](performance.md) | 대시보드는 insight에 제품 검색 성능을 제공합니다. |
| [페이스팅](facets.md) | 여러 차원의 속성 값을 사용하여 검색 기준을 구체화하는 고성능 필터링입니다. |
| [동의어](synonyms.md) | 쇼핑객이 카탈로그에 있는 것과 다른 제품을 찾는 데 사용할 수 있는 단어를 포함하도록 검색 범위를 확장하십시오. |
| [머천다이징 검색](rules.md) | 예약된 작업을 트리거하는 논리 규칙으로 검색 환경을 구성합니다. 비즈니스 목표를 지원하기 위해 검색 결과를 보정하기 위해 제품을 증폭, 매몰, 고정 또는 숨깁니다. |
| [카테고리 머천다이징](category-merch.md) | 카테고리 수준에서 규칙 및 지능형 머천다이징을 적용합니다. |
| [GraphQL](graphql.md) | 저장소 관리자에 로그인한 개발자는 실제 카탈로그 데이터로 쿼리를 작성하고 테스트할 수 있습니다. 자세한 내용을 보려면 [ 개발자 설명서에서 ](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/)GraphQL 개요[!DNL Live Search]로 이동하십시오. |
| [설정](settings.md) | 가격 패싯 값을 상점 가격 범위별로 그룹화하는 방법을 결정하고 색인화 언어를 설정합니다. |

## 속성을 검색 가능한 것으로 설정

고도로 타깃팅된 결과를 만들려면 [검색 가능](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/product-attributes.html)&#x200B;(`searchable=true`) 제품 특성 집합을 검토하십시오. 관련성을 보장하려면 명확하고 간결한 의미가 있는 콘텐츠가 포함된 경우에만 속성을 검색할 수 있도록 하십시오. 기본적으로 검색을 사용할 수 있지만 검색 결과의 정밀도를 낮출 수 있는 `description`과(와) 같이 정확도가 낮고 긴 텍스트가 포함된 특성은 사용하지 마십시오. 예를 들어, &quot;반바지&quot;를 검색하는 사람이 &quot;반팔&quot;이라는 용어가 포함된 설명이 있는 셔츠가 있으면 해당 셔츠가 검색 결과에 포함됩니다.

속성을 검색할 수 있도록 허용하려면 다음 단계를 완료하십시오.

1. 관리자의 경우 **스토어** > *특성* > **제품**(으)로 이동합니다.
1. 검색할 특성을 선택하십시오(예: `color`).
1. **Storefront 속성**&#x200B;을(를) 선택하고 **검색에 사용**&#x200B;을(를) `yes`(으)로 설정합니다.

   ![Workspace](assets/attribute-searchable.png)

[!DNL Live Search]은(는) Adobe Commerce 내에 설정된 제품 특성의 [weight](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/search/search-results.html#weighted-search)도 준수합니다. 가중치가 높은 속성은 검색 결과 내에서 더 높게 표시됩니다.

다음 속성은 항상 검색할 수 있습니다.

- `sku`
- `name`
- `categories`

[Facet](facets.md)은(는) 필터링 가능하도록 [!DNL Live Search]에 정의된 제품 특성입니다. 필터링 가능한 특성을 [!DNL Live Search]에서 패싯으로 설정할 수 있지만 한 번에 검색할 수 있는 패싯 수에 대한 [제한](boundaries-limits.md)이 있습니다.

>[!NOTE]
>
>제품 특성 구성에 필수 속성이 있는 경우에만 제품 특성을 필터링할 수 있습니다. *검색에 사용 = 예*, *검색 결과에 사용 계층 탐색=예* 및 *계층 탐색에 사용=필터링 가능(결과 포함)*. 이러한 속성이 누락된 경우 Facet 구성에 속성이 표시되지 않습니다. 구성 지침은 [패싯 추가](facets-add.md#add-a-facet)를 참조하십시오.

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

### 검색어

[!DNL Live Search]은(는) Luma 및 기타 php 기반 테마와 같이 Adobe Commerce이 라우팅을 처리하는 구현에서 [검색어 리디렉션](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/search/search-terms.html)을 지원합니다.
