---
title: ' [!DNL Live Search]에서 품절 제품 관리'
description: Adobe Commerce용  [!DNL Live Search] 에서 품절 제품을 관리하는 방법을 알아봅니다. 인벤토리 표시, inStock 필터 및 GraphQL API 필터링을 구성합니다.
feature: Services, Search
role: Admin, Developer
level: Intermediate
source-git-commit: bc8f35434c9f01f1a920745fe42617df2003ca60
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 0%

---

# 품절 제품 관리

재고 구성, 쿼리 시간 필터 및 선택적 백엔드 기능 플래그를 사용하여 [!DNL Live Search] 검색 및 범주 결과에 재고 부족 제품이 표시되는 방식을 제어할 수 있습니다. 이러한 옵션에는 중요한 제한이 있으므로 이 항목에서 설명합니다.

## 재고 상태 필터

Adobe Commerce 스톡 특성 `quantity_and_stock_status`은(는) 패싯으로 지원되지 않으며 **[!UICONTROL Add Facet]** 대화 상자에 나타나지 않습니다. 그러나 [!DNL Live Search]은(는) 쿼리 시간에 필터로 사용할 수 있는 `inStock` 필드를 노출합니다.

## 품절 제품 숨기기

다음 방법 중 하나를 사용하여 품절 제품을 숨깁니다.

### Commerce 구성

1.*관리자*&#x200B;에서 **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**>**[!UICONTROL Catalog]**>**[!UICONTROL Inventory]**(으)로 이동합니다.

&#x200B;1. **[!UICONTROL Display Out of Stock Products]**&#x200B;을(를) **[!UICONTROL No]**(으)로 설정합니다.

1. **[!UICONTROL Save Config]**&#x200B;을(를) 클릭합니다.

**[!UICONTROL Display Out of Stock Products]**&#x200B;이(가) `No`(으)로 설정되어 있으면 [!DNL Live Search]이(가) PLP 위젯을 통해 상점 앞에 있는 쿼리에 `inStock = 'no`을(를) 추가하므로 품절 제품이 반환되지 않습니다.

### API 필터

[!DNL Live Search] API를 직접 호출하는 경우(GraphQL 또는 REST), 다음과 같이 품절 제품을 명시적으로 필터링합니다.

```graphql
query productSearchInStockOnly {
  productSearch(
    phrase: ""
    filter: [
      { attribute: "inStock", eq: "true" }
    ]
  ) {
    total_count
    items {
      productView {
        sku
        name
        inStock
      }
    }
  }
}
```

[라이브 검색 PLP 위젯](plp-styling.md)을 통해 요청을 라우팅하지 않는 경우 이 방법을 사용하십시오.

### 재고 발생 후 재고 부족 표시

결과 세트에서 품절된 제품을 유지하지만 관련성을 기준으로 정렬할 때 항상 품절 상태 제품을 유지하려면 Adobe에서 환경에 대한 내부 기능 플래그를 활성화할 수 있습니다.

- 이 기능 플래그는 [!DNL Live Search] 관리 UI에 노출되지 않습니다.
- 요청하려면 [Adobe 지원에 문의](https://experienceleague.adobe.com/ko/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide){target="_blank"}하고 기능을 참조하여 재고 부족 제품을 검색 결과 끝으로 이동하십시오.

>[!NOTE]
>
>플래그를 활성화하면 *관련성*&#x200B;을 기준으로 정렬할 때 결과 집합에 남아 있는 모든 재고 부족 제품이 맨 아래로 이동합니다. 다른 정렬 순서(예: *가격* 또는 *제품 이름*)는 영향을 받지 않습니다.

### 머천다이징 규칙 및 재고 검색

검색 머천다이징 규칙은 쿼리 기반이며 재고 상태 또는 Facet 값을 기준으로 전체 그룹이 아닌 개별 제품을 대상으로 합니다.

- 규칙 조건은 구매자의 검색 구문(`Query is`, `Query contains`, `Query starts with`, `Query ends with`)에만 따라 다릅니다.
- 규칙 이벤트(증폭, 저장, 고정, 숨기기)는 이벤트당 하나의 SKU에 적용됩니다.

이러한 제한 때문에:

- 재고 상태만 기준으로 모든 재고 부족 제품을 구매하거나 숨기는 규칙을 만들 수 없습니다.
- 규칙에 이벤트로 추가하는 특정 SKU를 수동으로 숨기거나 삭제할 수 있습니다(규칙당 50개 규칙 및 25개 이벤트 제한에 따름).

카탈로그 전체에서 재고 부족 제품을 숨기거나 우선 순위를 낮추려면 검색 머천다이징 규칙 대신 이 항목에 설명된 인벤토리 구성 및 `inStock` 필터(및 옵션 기능 플래그)를 사용하십시오.

>[!MORELIKETHIS]
>
> - [머천다이징 규칙 검색](rules.md)
> - [Inventory management 글로벌 옵션 구성](https://experienceleague.adobe.com/ko/docs/commerce-admin/inventory/configuration/configuration)
