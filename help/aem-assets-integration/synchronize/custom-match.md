---
title: 사용자 지정 자동 일치
description: 사용자 지정 자동 일치가 복잡한 일치 논리를 사용하는 판매자나 메타데이터를 AEM Assets에 채울 수 없는 서드파티 시스템에 의존하는 판매자에게 특히 유용한 방법에 대해 알아봅니다.
feature: CMS, Media, Integration
exl-id: e7d5fec0-7ec3-45d1-8be3-1beede86c87d
source-git-commit: 6e8d266aeaec4d47b82b0779dfc3786ccaa7d83a
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 0%

---

# 사용자 지정 자동 일치

기본 자동 일치 전략(**OOTB 자동 일치**)이 특정 비즈니스 요구 사항과 일치하지 않는 경우 사용자 지정 일치 옵션을 선택하십시오. 이 옵션은 [Adobe Developer App Builder](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder)을(를) 사용하여 복잡한 일치 논리를 처리하는 사용자 지정 일치 응용 프로그램 또는 메타데이터를 AEM Assets에 채울 수 없는 서드파티 시스템에서 오는 에셋을 개발할 수 있도록 지원합니다.

## 사용자 지정 자동 일치 구성

1. Commerce 관리자에서 **[!UICONTROL Store]** > 구성 > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**(으)로 이동합니다.

1. **[!UICONTROL Custom Matcher]**&#x200B;을(를) 일치 규칙으로 선택합니다.

1. 이 일치 규칙을 선택하면 관리자가 사용자 지정 일치 논리에 필요한 **인증 매개 변수** 및 **끝점**&#x200B;을 구성하기 위한 추가 필드를 표시합니다.

### workspace.json

**[!UICONTROL Adobe I/O Workspace Configuration]** 필드를 사용하면 App Builder `workspace.json` 구성 파일을 가져와서 사용자 지정 Matcher를 간소화할 수 있습니다.

`workspace.json`Adobe Developer Console[에서 ](https://developer.adobe.com/console) 파일을 다운로드할 수 있습니다. 파일에는 App Builder 작업 공간에 대한 모든 자격 증명과 구성 세부 정보가 포함되어 있습니다.

+++예 `workspace.json`

```json
{
  "project": {
    "id": "project_id",
    "name": "project_name",
    "title": "title_name",
    "org": {
      "id": "id",
      "name": "Organization_name",
      "ims_org_id": "ims_id"
    },
    "workspace": {
      "id": "workspace_id",
      "name": "workspace_name_id",
      "title": "workspace_title_id",
      "action_url": "https://action_url.net",
      "app_url": "https://app_url.net",
      "details": {
        "credentials": [
          {
            "id": "credential_id",
            "name": "credential_name_id",
            "integration_type": "oauth_server_to_server",
            "oauth_server_to_server": {
              "client_id": "client_id",
              "client_secrets": ["secret"],
              "technical_account_email": "xx@technical_account_email.com",
              "technical_account_id": "technical_account_id",
              "scopes": [
                "AdobeID",
                "openid",
                "read_organizations",
                "additional_info.projectedProductContext",
                "additional_info.roles",
                "adobeio_api",
                "read_client_secret",
                "manage_client_secrets"
              ]
            }
          }
        ],
        "services": [
          {
            "code": "AdobeIOManagementAPISDK",
            "name": "I/O Management API"
          }
        ],
        "runtime": {
          "namespaces": [
            {
              "name": "namespace_name",
              "auth": "example_auth"
            }
          ]
        },
        "events": {
          "registrations": []
        },
        "mesh": {}
      }
    }
  }
}
```

+++

1. App Builder 프로젝트의 `workspace.json` 파일을 **[!UICONTROL Adobe I/O Workspace Configuration]** 필드로 끌어서 놓습니다. 또는 를 클릭하여 파일을 찾아 선택할 수 있습니다.

![Workspace 구성](../assets/workspace-configuration.png){width="600" zoomable="yes"}

1. 시스템은 자동으로 다음을 수행합니다.

   * JSON 구조의 유효성을 검사합니다
   * OAuth 자격 증명 추출 및 채우기
   * 작업 공간에 대해 사용 가능한 런타임 작업을 가져옵니다.
   * **[!UICONTROL Product to Asset URL]** 및 **[!UICONTROL Asset to Product URL]** 필드에 드롭다운 옵션을 채웁니다.

1. 드롭다운 메뉴에서 각 플로우에 대한 적절한 런타임 작업을 선택합니다.

1. **[!UICONTROL Save Config]**&#x200B;을(를) 클릭합니다.

## 사용자 지정 선택기 API 엔드포인트

[App Builder](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder){target=_blank}을(를) 사용하여 사용자 지정 선택기 응용 프로그램을 빌드할 때 응용 프로그램은 다음 끝점을 노출해야 합니다.

* 제품 URL에 대한 **App Builder 자산** 끝점
* 자산 URL에 대한 **App Builder 제품** 끝점

### 제품 URL 엔드포인트에 대한 App Builder 에셋

이 끝점은 지정된 자산과 연결된 SKU 목록을 검색합니다.

#### 사용 예

```javascript
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

    // Set skip to true if the mapping hasn't changed
    const skipSync = false;

    return {
        statusCode: 200,
        body: {
            asset_id: params.assetId,
            product_matches: [
                {
                    product_sku: "<YOUR-SKU-HERE>",
                    asset_roles: ["thumbnail", "image", "swatch_image", "small_image"],
                    asset_position: 1
                }
            ],
            skip: skipSync
        }
    };
}

exports.main = main;
```

**요청**

```text
POST https://your-app-builder-url/api/v1/web/app-builder-external-rule/asset-to-product
```

| 매개 변수 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `assetId` | 문자열 | 업데이트된 자산 ID를 나타냅니다. |
| `eventData` | 문자열 | 자산 ID와 연결된 데이터 페이로드를 반환합니다. |

**응답**

```json
{
  "asset_id": "{ASSET_ID}",
  "product_matches": [
    {
      "product_sku": "{PRODUCT_SKU_1}",
      "asset_roles": ["thumbnail", "image"]
    },
    {
      "product_sku": "{PRODUCT_SKU_2}",
      "asset_roles": ["thumbnail"]
    }
  ],
  "skip": false
}
```

| 매개 변수 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `asset_id` | 문자열 | 일치하는 자산 ID입니다. |
| `product_matches` | 배열 | 자산과 연결된 제품 목록입니다. |
| `skip` | 부울 | (선택 사항) `true`일 때 규칙 엔진은 이 자산에 대한 동기화를 건너뜁니다(제품 매핑 업데이트 없음). `false`을(를) 생략하면 일반 처리가 실행됩니다. [동기화 처리 건너뛰기](#skip-sync-processing)를 참조하십시오. |

### App Builder 제품-에셋 URL 끝점

이 끝점은 지정된 SKU와 연결된 자산 목록을 검색합니다.

#### 사용 예

```javascript
const { Core } = require('@adobe/aio-sdk')

async function main(params) {
    // return asset matches for a product
    // Build your own matching logic here to return the assets that map to the productSku
    // var assetMatches = [];
    // params.productSku
    // ...
    // End of your matching logic

    // Set skip to true if the mapping hasn't changed
    const skipSync = false;

    return {
        statusCode: 200,
        body: {
            product_sku: params.productSku,
            asset_matches: [
                {
                    asset_id: "<YOUR-ASSET-ID-HERE>", // urn:aaid:aem:1aa1d5i2-17h8-40a7-a228-e3ur588deee1
                    asset_roles: ["thumbnail", "image", "swatch_image", "small_image"],
                    asset_format: "image", // can be "image" or "video"
                    asset_position: 1
                }
            ],
            skip: skipSync
        }
    };
}

exports.main = main;
```

**요청**

```text
POST https://your-app-builder-url/api/v1/web/app-builder-external-rule/product-to-asset
```

| 매개 변수 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `productSKU` | 문자열 | 업데이트된 제품 SKU를 나타냅니다. |
| `eventData` | 문자열 | 제품 SKU와 연결된 데이터 페이로드를 반환합니다. |

**응답**

```json
{
  "product_sku": "{PRODUCT_SKU}",
  "asset_matches": [
    {
      "asset_id": "{ASSET_ID_1}",
      "asset_roles": ["thumbnail", "image"],
      "asset_position": 1,
      "asset_format": "image"
    },
    {
      "asset_id": "{ASSET_ID_2}",
      "asset_roles": ["thumbnail"],
      "asset_position": 2,
      "asset_format": "image"
    }
  ],
  "skip": false
}
```

| 매개 변수 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `product_sku` | 문자열 | 일치하는 제품 SKU입니다. |
| `asset_matches` | 배열 | 제품과 연계된 자산 목록. |
| `skip` | 부울 | (선택 사항) `true`일 때 규칙 엔진은 이 제품에 대한 동기화를 건너뜁니다(자산 매핑 업데이트 없음). `false`을(를) 생략하면 일반 처리가 실행됩니다. [동기화 처리 건너뛰기](#skip-sync-processing)를 참조하십시오. |

`asset_matches` 매개 변수에는 다음 특성이 포함되어 있습니다.

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `asset_id` | 문자열 | 에셋 ID입니다. |
| `asset_roles` | 배열 | 자산 역할. [, ](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/digital-assets/product-image#image-roles), `thumbnail` 및 `image`과(와) 같이 지원되는 `small_image`Commerce 자산 역할`swatch_image`을(를) 사용합니다. |
| `asset_format` | 문자열 | 에셋 포맷. 가능한 값은 `image` 및 `video`입니다. |
| `asset_position` | 숫자 | 제품 갤러리에서 에셋의 위치입니다. |

## 동기화 처리 건너뛰기

`skip` 매개 변수를 사용하면 사용자 지정 선택기가 특정 에셋 또는 제품에 대한 동기화 처리를 우회할 수 있습니다.

App Builder 응용 프로그램이 응답에서 `"skip": true`을(를) 반환하면 규칙 엔진은 해당 에셋 또는 제품에 대한 Commerce에 업데이트 또는 제거 API 요청을 보내지 않습니다. 이 최적화는 불필요한 API 호출을 줄이고 성능을 향상시킵니다.
