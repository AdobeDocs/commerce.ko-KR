---
title: '[!DNL Retrieve catalog data with GraphQL]'
description: GraphQL 쿼리를 사용하여 카탈로그 데이터를 검색하여 Commerce 환경을 향상시킵니다.
role: Admin, Developer
feature: Services, API Mesh, Catalog Service
exl-id: 49bbdb3b-bbe9-4777-8ea7-3bd25ae53889
TQID: https://experienceleague.adobe.com/ahutwotbB6Dxg7Tc3WMFd7S-WBMALvOYIUTmB5JKmyM
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: d842311424e76b83a131ada7a2db6e3fb868acd8
workflow-type: tm+mt
source-wordcount: 269
ht-degree: 0%

---

# GraphQL으로 카탈로그 데이터 검색 {#graphql-queries}

GraphQL 쿼리를 사용하여 [!DNL Catalog Service] 데이터 공간에서 제품, 가격 및 기타 카탈로그 데이터를 검색하고 기본 제품 쿼리보다 [!DNL Adobe Commerce] 상점 경험을 더 빠르게 렌더링합니다.

{{aco-merchandising-services}}

[!DNL Catalog Service]은(는) 다음 쿼리를 제공합니다.

| 쿼리 | 설명 | 사용 | 제한 |
| --- | --- | --- | --- |
| `categories` | 범주 데이터를 반환합니다. `subtree` 입력 개체가 지정된 경우 쿼리는 하위 범주에 대한 세부 정보를 반환합니다. | 상점 탐색 및 카테고리 페이지를 렌더링하는 데 유용합니다. [예제를 참조하십시오.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/){target="_blank"} | — |
| `products` | 입력으로 지정된 SKU에 대한 세부 정보를 반환합니다. | 주로 제품 세부 사항 및 제품 비교 페이지의 콘텐츠를 렌더링하는 데 사용됩니다. [예제를 참조하십시오.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/){target="_blank"} | 요청당 100SKU |
| `productSearch` | 검색 기준과 일치하는 제품 목록을 반환합니다. | 검색 입력을 기반으로 검색 결과 및 제품 목록 페이지를 렌더링하는 데 유용합니다. [예제를 참조하십시오.](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/){target="_blank"} | 요청당 100SKU |
| `refineProduct` | 복잡한 제품에 대한 `products` 쿼리 결과를 좁혀 제품 변형에 대한 특정 정보를 반환합니다. | 구매자가 제품 옵션을 선택할 때 업데이트된 제품 세부 사항 페이지를 렌더링하는 데 유용합니다. [예제를 참조하십시오.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/refine-product/){target="_blank"} | 요청당 100SKU |
| `variants` | 제품의 모든 변형에 대한 세부 정보를 반환합니다. | 여러 API 요청을 제출하지 않고 제품 세부 사항에 변형 이미지를 표시하거나 페이지를 나열하는 데 유용합니다. [예제를 참조하십시오.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/product-variants/){target="_blank"} | 요청당 100SKU |

{style="table-layout:auto"}

이러한 쿼리 사용에 대한 자세한 내용은 [Storefront Services GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/storefront-services/){target="_blank"}을(를) 참조하십시오.
