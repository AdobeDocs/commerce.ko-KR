---
title: 사용자 지정 자동 일치
description: 사용자 지정 자동 일치가 복잡한 일치 논리를 사용하는 판매자나 메타데이터를 AEM Assets에 채울 수 없는 서드파티 시스템에 의존하는 판매자에게 특히 유용한 방법에 대해 알아봅니다.
feature: CMS, Media, Integration
exl-id: e7d5fec0-7ec3-45d1-8be3-1beede86c87d
source-git-commit: ee1dd902a883e5653a9fb8764fac708975c37091
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 1%

---

# 사용자 지정 자동 일치

기본 자동 일치 전략(**OOTB 자동 일치**)이 특정 비즈니스 요구 사항과 일치하지 않는 경우 사용자 지정 일치 옵션을 선택하십시오. 이 옵션은 [Adobe Developer App Builder](https://experienceleague.adobe.com/ko/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder)을(를) 사용하여 복잡한 일치 논리를 처리하는 사용자 지정 일치 응용 프로그램 또는 메타데이터를 AEM Assets에 채울 수 없는 서드파티 시스템에서 오는 에셋을 개발할 수 있도록 지원합니다.

## 사용자 지정 자동 일치 구성

1. Commerce 관리자에서 **[!UICONTROL Store]** > 구성 > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**(으)로 이동합니다.

1. **[!UICONTROL Custom Matcher]**&#x200B;을(를) 일치 규칙으로 선택합니다.

1. 이 일치 규칙을 선택하면 관리자가 사용자 지정 일치 논리에 필요한 **인증 매개 변수** 및 **끝점**&#x200B;을 구성하기 위한 추가 필드를 표시합니다.

## 사용자 지정 선택기 API 엔드포인트

[App Builder](https://experienceleague.adobe.com/ko/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder){target=_blank}을(를) 사용하여 사용자 지정 선택기 응용 프로그램을 빌드할 때 응용 프로그램은 다음 끝점을 노출해야 합니다.

* 제품 URL에 대한 **App Builder 자산** 끝점
* 자산 URL에 대한 **App Builder 제품** 끝점

### 제품 URL 엔드포인트에 대한 App Builder 에셋

이 끝점은 지정된 자산과 연결된 SKU 목록을 검색합니다.

#### 사용 예

```bash
const { Core } = require('@adobe/aio-sdk')

async function main(params) {

    // Build your own matching logic here to return the products that map to the assetId
    // var productMatches = [];
    // params.assetId
    // params.eventData.assetMetadata['commerce:isCommerce']
    // params.eventData.assetMetadata['commerce:skus'][i]
    // params.eventData.assetMetadata['commerce:roles']
    // params.eventData.assetMetadata['commerce:positions'][i]
    // ...
    // End of your matching logic

    return {
        statusCode: 500,
        body: {
            asset_id: params.assetId,
            product_matches: [
                {
                    product_sku: "<YOUR-SKU-HERE>",
                    asset_roles: ["thumbnail", "image", "swatch_image", "small_image"],
                    asset_position: 1
                }
            ]
        }
    };
}

exports.main = main;
```

**요청**

```bash
POST https://your-app-builder-url/api/v1/web/app-builder-external-rule/asset-to-product
```

| 매개 변수 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `assetId` | 문자열 | 업데이트된 자산 ID를 나타냅니다. |
| `eventData` | 문자열 | 자산 ID와 연결된 데이터 페이로드를 반환합니다. |

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

async function main(params) {
    // return asset matches for a product
    // Build your own matching logic here to return the assets that map to the productSku
    // var assetMatches = [];
    // params.productSku
    // ...
    // End of your matching logic

    return {
        statusCode: 500,
        body: {
            product_sku: params.productSku,
            asset_matches: [
                {
                    asset_id: "<YOUR-ASSET-ID-HERE>", // urn:aaid:aem:1aa1d5i2-17h8-40a7-a228-e3ur588deee1
                    asset_roles: ["thumbnail", "image", "swatch_image", "small_image"],
                    asset_format: "image", // can be "image" or "video"
                    asset_position: 1
                }
            ]
        }
    };
}

exports.main = main;
```

**요청**

```bash
POST https://your-app-builder-url/api/v1/web/app-builder-external-rule/product-to-asset
```

| 매개 변수 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `productSKU` | 문자열 | 업데이트된 제품 SKU를 나타냅니다. |
| `eventData` | 문자열 | 제품 SKU와 연결된 데이터 페이로드를 반환합니다. |

**응답**

```bash
{
  "product_sku": "{PRODUCT_SKU}",
  "asset_matches": [
    {
      "asset_id": "{ASSET_ID_1}",
      "asset_roles": ["thumbnail","image"],
      "asset_position": 1,
      "asset_format": image
    },
    {
      "asset_id": "{ASSET_ID_2}",
      "asset_roles": ["thumbnail"]
      "asset_position": 2,
      "asset_format": image     
    }
  ]
}
```

| 매개 변수 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `productSKU` | 문자열 | 업데이트된 제품 SKU를 나타냅니다. |
| `asset_matches` | 문자열 | 특정 제품 SKU와 연결된 모든 자산을 반환합니다. |

`asset_matches` 매개 변수에는 다음 특성이 포함되어 있습니다.

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `asset_id` | 문자열 | 업데이트된 자산 ID를 나타냅니다. |
| `asset_roles` | 문자열 | 사용 가능한 모든 자산 역할을 반환합니다. [, ](https://experienceleague.adobe.com/ko/docs/commerce-admin/catalog/products/digital-assets/product-image#image-roles), `thumbnail` 및 `image`과(와) 같이 지원되는 `small_image`Commerce 자산 역할`swatch_image`을(를) 사용합니다. |
| `asset_format` | 문자열 | 에셋에 사용할 수 있는 형식을 제공합니다. 가능한 값은 `image` 및 `video`입니다. |
| `asset_position` | 문자열 | 자산의 위치를 표시합니다. |
