---
title: GraphQL
description: ' [!DNL Live Search] GraphQL 작업 영역을 사용하면 라이브 데이터로 쿼리를 작성할 수 있습니다.'
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '39'
ht-degree: 0%

---

# GraphQL

*GraphQL* 작업 영역을 통해 관리자는 자신의 데이터를 사용하여 GraphQL 쿼리를 빌드하고 테스트할 수 있습니다.

이 작업 영역은 [`productSearch`](https://developer.adobe.com/commerce/services/graphql/live-search/product-search/) 및 [`attributeMetadata`](https://developer.adobe.com/commerce/services/graphql/live-search/attribute-metadata/) 쿼리를 지원합니다.

![GraphQL 작업 공간](assets/graphql.png)

```graphql
query productSearch {
  productSearch(phrase: "a306") {
    total_count
    items {
      product {
        sku
		name
      }
    }
    facets {
      title
    }
  }
}
```

변수:

```json
{
  "Magento-Environment-Id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
  "Magento-Website-Code": "base",
  "Magento-Store-Code": "base",
  "Magento-Store-View-Code": "default",
  "X-Api-Key": "search_gql"
}
```

