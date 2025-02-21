---
title: 패싯 유형
description: '[!DNL Live Search]개의 패싯이 동적이며 관련성이 있을 경우 필터 목록에 나타납니다.'
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---

# 패싯 유형

[!DNL Live Search]은(는) 다양한 패싯 유형을 사용하며 관련성이 있을 때만 *필터* 목록에 표시됩니다. 사용 가능한 패싯 목록은 반환된 제품에 따라 변경됩니다. 다음은 프레젠테이션과 동작에 영향을 주는 특성입니다.

* 고정 패싯 - 가장 일반적으로 사용되는 패싯을 목록의 맨 위에 고정할 수 있습니다. 나머지 패싯은 고정된 패싯 다음에 *정렬 형식* 순서로 나열됩니다.
* 동적 패싯 - [Adobe Sensei](https://www.adobe.com/sensei.html)이(가) 제품 집합 및 쿼리와 가장 관련이 있는 제품 특성입니다. 이 계산은 전체 카탈로그의 속성 메타데이터를 고려하고 쿼리 시간에 쿼리에 가장 적합한 패싯을 결정합니다.

  >[!NOTE]
  >
  >동적 패싯을 만든 후 GraphQL 쿼리 응답에 시간 초과 오류가 표시되는 경우 모든 패싯을 고정으로 변경하여 성능 문제가 해결되는지 확인하십시오.

* 인기 패싯 - 검색 결과에 가장 자주 표시되는 제품 속성.
* 가격 패싯 - 가격 범위별로 제품을 반환합니다. [*설정*](settings.md) 작업 영역에서 선택 항목 수와 가격 범위 간격을 지정할 수 있습니다.

쿼리 시간에 [!DNL Live Search]은(는) 동적 패싯과 인기 패싯 그룹으로 검색 결과를 생성합니다.

![패싯 - 가격](assets/storefront-search-results-run-price.png)

## Storefront 및 Headless 옵션

[!DNL Commerce] Storefront에 대해 렌더링되는 패싯은 요청을 라우팅하고 Storefront에서 결과를 렌더링하는 검색 어댑터에 의해 처리됩니다. 해당 특성에 할당된 입력 유형에 관계없이 모든 [!DNL Commerce] Storefront 패싯이 단일 선택 옵션으로 알파벳순으로 정렬됩니다. 상점 첫 화면에서 사용할 수 있는 패싯은 현재 테마에 따라 렌더링되며 계층화된 탐색 표시에 대한 모든 사용자 지정 사항을 반영합니다.

반대로 [headless](https://developer.adobe.com/commerce/php/architecture/technical-vision/web-api/) 구현은 API에서 처리되며 추가 옵션을 지원합니다. Headless 패싯은 알파벳순 또는 개수별로 정렬할 수 있으며 단일 또는 다중 선택 옵션을 가질 수 있습니다.

### Facet 레이블

[!DNL Commerce] 상점 앞면의 경우 Facet 레이블은 [*특성 속성*](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/create/attribute-product-create.html)에 의해 결정됩니다. 여러 보기가 있는 스토어의 경우 *레이블 관리*&#x200B;에서 추가 레이블을 정의할 수 있습니다. Headless 구현의 경우 레이블은 [작업 공간 구현](faceting-workspace.md)에서 편집됩니다.

### 정렬 유형

상점 앞에 대해 렌더링된 모든 패싯은 알파벳순으로 정렬됩니다. Headless 구현의 경우 패싯은 알파벳순 또는 개수별로 정렬할 수 있습니다.

| 정렬 유형 | 설명 |
|--- |--- |
| 알파벳 | 상점 *필터* 목록에서 패싯은 알파벳순으로 정렬됩니다. |
| 계수 | (Headless만 해당) Headless 구현의 경우 패싯은 현재 반환된 제품 세트에서 패싯당 찾은 값의 수로 정렬할 수도 있습니다. |
