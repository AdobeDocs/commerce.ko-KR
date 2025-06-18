---
title: 사용자 지정 자동 일치
description: 사용자 지정 자동 일치가 복잡한 일치 논리를 사용하는 판매자나 제품 시각적 메타데이터를 AEM Assets에 채울 수 없는 서드파티 시스템에 의존하는 판매자에게 특히 유용한 방법에 대해 알아봅니다.
feature: CMS, Media, Integration
source-git-commit: 3ecc429003490235211a812af064d1b10d053e38
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---


# 사용자 지정 자동 일치

기본 자동 일치 전략(**OOTB 자동 일치**)이 특정 비즈니스 요구 사항과 일치하지 않는 경우 사용자 지정 일치 옵션을 선택하십시오. 이 옵션은 [Adobe Developer App Builder](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder)을(를) 사용하여 복잡한 일치 논리를 처리하는 사용자 지정 일치 응용 프로그램 또는 제품 시각적 메타데이터를 AEM Assets에 채울 수 없는 서드파티 시스템에서 제공되는 에셋을 개발할 수 있도록 지원합니다.

## 사용자 지정 자동 일치 구성

1. Commerce 관리자에서 **[!UICONTROL Store]** > 구성 > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**(으)로 이동합니다.

1. **[!UICONTROL Custom Matcher]**&#x200B;을(를) 일치 규칙으로 선택합니다.

1. 이 일치 규칙을 선택하면 관리자가 사용자 지정 일치 논리에 필요한 **인증 매개 변수** 및 **끝점**&#x200B;을 구성하기 위한 추가 필드를 표시합니다.

## 사용자 지정 선택기 API 엔드포인트

[App Builder](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder){target=_blank}을(를) 사용하여 사용자 지정 선택기 응용 프로그램을 빌드할 때 응용 프로그램은 다음 끝점을 노출해야 합니다.

* 제품 URL에 대한 **App Builder 자산** 끝점
* 자산 URL에 대한 **App Builder 제품** 끝점

### 제품 URL 엔드포인트에 대한 App Builder 에셋

이 끝점은 지정된 자산과 연결된 SKU 목록을 검색합니다.

#### 사용 예

```bash
const { Core } = require('@adobe/aio-sdk')
 
async function main (params) {
    // return the products that map to the assetId
    return {
        statusCode: 200,
        body: {
          asset_id: "urn:aaid:aem:1aa1d4a0-18b8-40a7-a228-e0ab588deee1",
          product_matches: [
            {
              product_sku: "SKU1",
              asset_roles: ["thumbnail"],
              asset_position: [1]
            }
          ]
        }
   }
}
 
exports.main = main
```

**요청**

```bash
GET https://your-app-builder-url/api/v1/web/app-builder-external-rule/asset-to-product
```

| 매개 변수 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `assetId` | 문자열 | 업데이트된 자산 ID를 나타냅니다. |

**응답**

```bash
{
  "asset_id": "{ASSET_ID}",
  "product_matches": [
    {
      "product_sku": "{PRODUCT_SKU_1}",
      "asset_roles": ["thumbnail","image"]
    },
    {
      "product_sku": "{PRODUCT_SKU_2}",
      "asset_roles": ["thumbnail"]
    }
  ]
}
```

### App Builder 제품-에셋 URL 끝점

이 끝점은 지정된 SKU와 연결된 자산 목록을 검색합니다.

#### 사용 예

```bash
const { Core } = require('@adobe/aio-sdk')
 
async function main (params) {
    // return asset matches for a product
    return {
        statusCode: 200,
        body: {
          product_sku: params.productSku, //SKU-1
          asset_matches: [
            {
              asset_id: "urn:aaid:aem:1aa1d4a0-18b8-40a7-a228-e0ab588deee1",
              asset_roles: ["thumbnail","image"]
            }
          ]
        }
      }
}
 
exports.main = main
```

**요청**

```bash
GET https://your-app-builder-url/api/v1/web/app-builder-external-rule/product-to-asset
```

| 매개 변수 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `productSKU` | 문자열 | 업데이트된 제품 SKU를 나타냅니다. |

**응답**

```bash
{
  "product_sku": "{PRODUCT_SKU}",
  "asset_matches": [
    {
      "asset_id": "{ASSET_ID_1}",
      "asset_roles": ["thumbnail","image"]
    },
    {
      "asset_id": "{ASSET_ID_2}",
      "asset_roles": ["thumbnail"]
    }
  ]
}
```

>[!TIP]
>
> `asset_roles` 키에서 `thumbnail`, `image`, `small_image` 및 `swatch_image`과(와) 같이 지원되는 [Commerce 자산 역할](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/digital-assets/product-image#image-roles)을(를) 사용합니다.
