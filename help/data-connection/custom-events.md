---
title: 사용자 지정 이벤트 만들기
description: Adobe Commerce 데이터를 다른 Adobe DX 제품에 연결하기 위한 사용자 지정 이벤트를 만드는 방법을 알아봅니다.
role: Admin, Developer
feature: Personalization, Integration, Eventing
exl-id: db782c0a-8f13-4076-9b17-4c5bf98e9d01
source-git-commit: 81fbcde11da6f5d086c2b94daeffeec60a9fdbcc
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 1%

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

표준 이벤트에 대한 속성 재정의는 Experience Platform에 대해서만 지원됩니다. 사용자 지정 데이터는 Commerce 대시보드 및 지표 추적기로 전달되지 않습니다.

`customContext`이(가) 있는 모든 이벤트에 대해 수집기는 관련 컨텍스트에 설정된 필드를 `customContext`의 필드와 조인합니다. 재정의에 대한 사용 사례는 개발자가 이미 지원되는 이벤트에서 페이지의 다른 부분에 의해 설정된 컨텍스트를 재사용하고 확장하려는 경우입니다.

### 예

Adobe Commerce Events SDK을 통해 재정의가 게시된 제품 보기:

```javascript
mse.publish.productPageView({
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

Experience Platform Edge에서:

```javascript
{
  xdm: {
    eventType: 'commerce.productViews',
    identityMap: {
      ECID: [
        {
          id: 'ecid1234',
          primary: true,
        }
      ]
    },
    commerce: {
      productViews: {
        value : 1,
      }
    },
    productListItems: [{
        SKU: "1234",
        name: "leora summer pants",
        productCategories: [{
            categoryID: "cat_15",
            categoryName: "summer pants",
            categoryPath: "pants/mens/summer",
        }],
    }],
  }
}
```

Luma 기반 스토어:

Luma 기반 스토어에서 게시 이벤트는 기본적으로 구현됩니다. 따라서 `customContext`을(를) 확장하여 사용자 지정 데이터를 설정할 수 있습니다.

For example:

```javascript
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
```

사용자 지정 데이터 처리에 대한 자세한 내용은 [사용자 지정 이벤트 재정의](https://github.com/adobe/commerce-events/blob/main/examples/events/custom-event-override.md)를 참조하십시오.

>[!NOTE]
>
> 사용자 지정 속성으로 이벤트를 재정의하는 경우 기본 Adobe Analytics 보고서에 영향을 줄 수 있습니다.
