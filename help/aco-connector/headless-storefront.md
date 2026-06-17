---
title: '[!DNL Adobe Commerce Optimizer Connector] Headless Storefront 통합'
description: Headless 상점 전면을  [!DNL Adobe Commerce Optimizer Connector] GraphQL API, 가격 장부 ID 및 번들 추가 장바구니 인코딩과 통합하는 방법을 알아봅니다.
feature: Storefront, Integration, GraphQL
badgePaas: label="PaaS만" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce 온 클라우드 프로젝트(Adobe 관리 PaaS 인프라) 및 온프레미스 프로젝트에만 적용됩니다."
autotag-review: '2026-06-09T16:27:30.102Z'
TQID: 'https://experienceleague.adobe.com/Orif1rROglTQ-3ZkRj5LMF90Y-AdpfTnOgPmJXQjYgc'
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: b974b164-8a4e-43b8-a9e2-8e67ec131677id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: c32adafa-ed01-4b31-997e-2413013911b0
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: d378ca77-2da1-4f39-ad92-1917fe974a38
topic_v2: id: e0eb8757-182f-49f3-94a4-1587d16f5094id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 237
ht-degree: 0%

---

# Headless 상점 첫 화면 통합

`CommerceAdapter` 모듈이 [!DNL Adobe Commerce]을(를) 확장하여 헤드리스 상점 앞과 [!DNL Adobe Commerce Optimizer] 사이의 간격을 메웁니다. 고객 가격 장부 컨텍스트를 해결하기 위한 GraphQL 쿼리를 제공하고 [!DNL Adobe Commerce Optimizer] GraphQL API에 필요한 번들 제품 인코딩을 적용합니다.

높은 수준의 상점 설치 지침은 [!DNL Adobe Commerce Optimizer Connector] 개요에서 [머천다이징 및 상점 구성](./overview.md#merchandising-storefronts)을 참조하십시오.

## GraphQL: `commerceOptimizer` 쿼리 {#graphql-commerceoptimizer-query}

Headless storefront는 `commerceOptimizer` GraphQL 쿼리를 호출하여 현재 고객 세션에 대한 `priceBookId`을(를) 검색합니다. 가격을 가져올 때 이 값을 [[!DNL Adobe Commerce Optimizer] GraphQL API](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/using-the-api){target="_blank"}에 전달하십시오.

```graphql
{
  commerceOptimizer {
    priceBookId
  }
}
```

응답 예:

```json
{
  "data": {
    "commerceOptimizer": {
      "priceBookId": "base::a94a8fe5ccb19ba61c4c0873d391e987982fbbd3"
    }
  }
}
```

`priceBookId`을(를) 해결하는 방법:

| 세션 상태 | `priceBookId` |
|-----------------------|---------------------------------------------------------------------|
| 게스트(로그인되지 않음) | `websiteCode::sha1(0)`. 여기서 `0`은(는) 게스트 고객 그룹 ID입니다. |
| 로그인한 고객 | `websiteCode::sha1(customerGroupId)` |

`Store` 요청 헤더가 웹 사이트 범위를 결정하므로 `websiteCode` 구성 요소가 결정됩니다. `sha1(customerGroupId)` 구성 요소는 데이터 동기화 중에 사용된 가격 장부 ID 수식과 일치합니다. [가격 장부](reference/field-mapping.md#price-books)를 참조하세요.

## 번들 제품: 장바구니에 추가 형식 {#bundle-products-add-to-cart-format}

쇼핑객이 선택한 각 번들 옵션에 대해 `SKU` 및 `qty`만 사용하여 Headless 상점 앞에서 장바구니에 번들 제품을 추가할 수 있도록 허용합니다.

선택하거나 입력한 각 옵션 값은 다음 형식으로 base64로 인코딩되어야 합니다.

```text
base64("bundle_item/" + JSON.stringify({"sku": "<child_sku>", "qty": "<qty>"}))
```

모든 옵션에서 동일한 하위 SKU가 한 번만 표시될 수 있습니다.

예([!DNL JavaScript]):

```javascript
const encodedOption = btoa(
  'bundle_item/' + JSON.stringify({ sku: 'child-product-sku', qty: '1' })
);
```
