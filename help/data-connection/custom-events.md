---
title: 사용자 지정 이벤트 만들기
description: Adobe Commerce 데이터를 다른 Adobe DX 제품에 연결하기 위한 사용자 지정 이벤트를 만드는 방법을 알아봅니다.
role: Admin, Developer
feature: Personalization, Integration, Eventing
exl-id: db782c0a-8f13-4076-9b17-4c5bf98e9d01
source-git-commit: 25d796da49406216f26d12e3b1be01902dfe9302
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# 사용자 지정 이벤트 만들기

고유한 업계 데이터를 수집하기 위해 고유한 상점 이벤트를 만들어 [이벤트 플랫폼](events.md)을 확장할 수 있습니다. 사용자 지정 이벤트를 만들고 구성하면 [Adobe Commerce 이벤트 수집기](https://github.com/adobe/commerce-events/tree/main/packages/storefront-events-collector)로 전송됩니다.

## 사용자 지정 이벤트 처리

사용자 지정 이벤트는 Adobe Experience Platform에 대해서만 지원됩니다. 사용자 지정 데이터는 Adobe Commerce 대시보드 및 지표 추적기로 전달되지 않습니다.

`custom` 이벤트의 경우 수집기는

- `identityMap`을(를) 기본 ID로 사용하는 `ECID` 추가
- 이벤트에 보조 ID `email`if`identityMap` _이(가) 설정되었으므로_&#x200B;의 `personalEmail.address`을(를) 포함합니다.
- Edge으로 전달하기 전에 `xdm` 개체 내에 전체 이벤트를 래핑합니다.

예:

Adobe Commerce 이벤트 SDK을 통해 게시된 사용자 지정 이벤트:

```javascript
mse.publish.custom({
    commerce: {
        saveForLaters: {
            value: 1,
        },
    },
});
```

Experience Platform Edge에서:

```javascript
{
  xdm: {
    identityMap: {
      ECID: [
        {
          id: 'ecid1234',
          primary: true
        }
      ],
      email: [
        {
          id: "runs@safari.ke",
          primary: false
        }
      ]
    },
    commerce: {
        saveForLaters: {
            value: 1
        }
    }
  }
}
```

>[!NOTE]
>
> 사용자 지정 이벤트를 사용하면 기본 Adobe Analytics 보고서에 영향을 줄 수 있습니다.

## 이벤트 재정의 처리(사용자 지정 속성)

`customContext`이(가) 있는 모든 이벤트 집합의 경우 수집기는 이벤트 페이로드의 필드를 `custom context`의 필드에서 재정의하거나 확장합니다. 재정의에 대한 사용 사례는 개발자가 이미 지원되는 이벤트에서 페이지의 다른 부분에 의해 설정된 컨텍스트를 재사용하고 확장하려는 경우입니다.

이벤트 재정의는 Experience Platform으로 전달할 때만 적용됩니다. Adobe Commerce 및 Sensei 분석 이벤트에는 적용되지 않습니다. Adobe Commerce 이벤트 수집기 [README](https://github.com/adobe/commerce-events/blob/e34bcfc0deca8d5ac1f9310fc1ee4c1becf4ffbb/packages/storefront-events-collector/README.md)에서 추가 정보를 제공합니다.

>[!NOTE]
>
>Experience Platform 이벤트 페이로드에서 사용자 지정 속성으로 `productListItems`을(를) 보강할 때 SKU를 사용하여 제품을 일치시키십시오. 이 요구 사항은 `product-page-view`개 이벤트에는 적용되지 않습니다.

### 사용

```javascript
const mse = window.magentoStorefrontEvents;

mse.publish.productPageView(customCtx);
```

### 예제 1 - `productCategories` 추가

```javascript
magentoStorefrontEvents.publish.productPageView({
    productListItems: [
        {
            productCategories: [
                {
                    categoryID: "cat_15",
                    categoryName: "summer pants",
                    categoryPath: "pants/mens/summer",
                },
            ],
        },
    ],
});
```

### 예제 2 - 이벤트를 게시하기 전에 사용자 지정 컨텍스트 추가

```javascript
const mse = window.magentoStorefrontEvents;

mse.context.setCustom({
  productListItems: [
    {
      productCategories: [
        {
          categoryID: "cat_15",
          categoryName: "summer pants",
          categoryPath: "pants/mens/summer",
        },
      ],
    },
  ],
});

mse.publish.productPageView();
```

### 예제 3 - 게시자의 사용자 지정 컨텍스트 세트는 Adobe 클라이언트 데이터 레이어에 이전에 설정된 사용자 지정 컨텍스트를 덮어씁니다.

이 예제에서 `pageView` 이벤트는 **필드에**&#x200B;사용자 지정 페이지 이름 2`web.webPageDetails.name`을 갖게 됩니다.

```javascript
const mse = window.magentoStorefrontEvents;

mse.context.setCustom({
  web: {
    webPageDetails: {
      name: 'Custom Page Name 1'
    },
  },
});

mse.publish.pageView({
  web: {
    webPageDetails: {
      name: 'Custom Page Name 2'
    },
  },
});
```

### 예제 4 - 여러 제품이 있는 이벤트가 있는 `productListItems`에 사용자 지정 컨텍스트 추가

```javascript
const mse = window.magentoStorefrontEvents;

mse.context.setCustom({
  productListItems: [
    {
      SKU: "24-WB01", //Match SKU to override correct product in event payload
      productCategory: "Hand Bag", //Custom attribute added to event payload
      name: "Strive Handbag (CustomName)" //Override existing attribute with custom value in event payload
    },
    {
      SKU: "24-MB04",
      productCategory: "Backpack Bag",
      name: "Strive Backpack (CustomName)"
    },
  ],
});

mse.publish.shoppingCartView();
```

>[!NOTE]
>
> 사용자 지정 속성으로 이벤트를 재정의하는 경우 기본 Adobe Analytics 보고서에 영향을 줄 수 있습니다.
