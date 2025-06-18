---
title: '[!DNL Retrieve catalog data with GraphQL]'
description: GraphQL 쿼리를 사용하여 카탈로그 데이터를 검색하여 Commerce 환경을 향상시킵니다.
role: Admin, Developer
feature: Services, API Mesh, Catalog Service
exl-id: 49bbdb3b-bbe9-4777-8ea7-3bd25ae53889
source-git-commit: ff5c717dbdd638e114bccc3f6dec26f4be269194
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---

# GraphQL으로 카탈로그 데이터 검색 {#graphql-queries}

GraphQL 쿼리를 사용하여 Adobe Commerce 카탈로그 SaaS 데이터 공간에서 제품, 가격 및 기타 데이터를 검색하고 이를 사용하여 기본 Adobe Commerce GraphQL 쿼리보다 더 빠르게 Commerce 경험을 렌더링합니다.

카탈로그 서비스는 다음 쿼리를 제공합니다.

| 쿼리 | 설명 | 사용 |
|-------|-------------|-------|
| `categories` | 범주 데이터를 반환합니다. 하위 트리 입력 개체가 지정된 경우 쿼리는 하위 범주에 대한 세부 정보를 반환합니다. | 상점 탐색 및 카테고리 페이지를 렌더링하는 데 유용합니다. [예제를 참조하십시오.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/) |
| `products` | 입력으로 지정된 SKU에 대한 세부 정보를 반환합니다. | 주로 제품 세부 사항 및 제품 비교 페이지의 콘텐츠를 렌더링하는 데 사용됩니다. [예제를 참조하십시오.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/) |
| `productSearch` | 검색 기준과 일치하는 제품 목록을 반환합니다. | 검색 입력을 기반으로 검색 결과 및 제품 목록 페이지를 렌더링하는 데 유용합니다. [예제를 참조하십시오.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/) |
| `refineProduct` | 복잡한 제품에 대해 실행되는 제품 쿼리의 결과를 좁혀 제품 변형에 대한 특정 정보를 반환합니다. | 쇼핑객이 제품 옵션을 선택할 때 업데이트된 제품 세부 사항 페이지를 렌더링하는 데 유용합니다. [예제를 참조하십시오.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/refine-product/) |
| `variants` | 제품의 모든 변형에 대한 세부 정보를 반환합니다. | 여러 API 요청을 제출하지 않고 제품 세부 사항에 변형 이미지를 표시하거나 페이지를 나열하는 데 유용합니다. [예제를 참조하십시오.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/product-variants/) |

이러한 쿼리 사용에 대한 자세한 내용은 [카탈로그 서비스 API 안내서](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/)를 참조하세요.
