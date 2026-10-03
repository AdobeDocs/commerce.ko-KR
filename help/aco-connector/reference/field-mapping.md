---
title: '[!DNL Adobe Commerce Optimizer Connector]개 피드에 대한 필드 매핑'
description: '[!DNL Adobe Commerce] 카탈로그 데이터에서 모든 피드의 [!DNL Adobe Commerce Optimizer] 수집 API 형식으로의 [!DNL Adobe Commerce Optimizer Connector] 필드 매핑에 대해 알아봅니다.'
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="PaaS만" type="Informative" url="https://experienceleague.adobe.com/ko/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce 온 클라우드 프로젝트(Adobe 관리 PaaS 인프라) 및 온프레미스 프로젝트에만 적용됩니다."
autotag-review: '2026-06-09T15:49:03.934Z'
TQID: 'https://experienceleague.adobe.com/SOWOnguudhqzX-r66nGUqc-WKet5qq6GRV11ADx0Me4'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
    internal-label: Admin tools and workspace
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
  - id: b23e006f-0a29-4f1d-8fd0-77aa56f3d12b
    internal-label: Data modeling
source-git-commit: 1e34df4f07f9043675104fce55c58e0617463b33
workflow-type: tm+mt
source-wordcount: '1023'
ht-degree: 2%
---

# 커넥터 피드에 대한 필드 매핑

이 페이지에서는 [!DNL Adobe Commerce Optimizer Connector]이(가) [!DNL Adobe Commerce] 카탈로그 필드를 [!DNL Commerce Optimizer] [!DNL Catalog Data Ingestion API]에 필요한 형식으로 변환하는 방법을 설명합니다. 지원되는 피드 및 해당 API 끝점에 대한 목록은 [커넥터 참조](connector-reference.md#supported-feeds)를 참조하십시오.

## 제품

`products` 피드가 [제품 끝점](https://developer.adobe.com/commerce/services/reference/rest/#tag/Products){target="_blank"}에 데이터를 보냅니다.

| [!DNL Adobe Commerce] 필드 | [!DNL Commerce Optimizer] API 필드 | 매핑 세부 정보 |
| ----------------------------------------------- | -------------- | ------- |
| `sku` | `sku` | |
| `storeViewCode` | `source/locale` | |
| `name` | `name` | |
| `urlKey` | `slug` | |
| `productId` | `externalIds[0].id` | `origin`을(를) `"AdobeCommerce"`(으)로 설정 |
| `status` | `status` | 상태를 대문자로 변환합니다. 상태가 누락되었거나 구성 가능한 또는 번들 제품에 옵션 값이 없는 경우 `DISABLED`을(를) 사용합니다. |
| `description` | `description` | 설명이 누락된 경우 빈 문자열을 사용합니다. |
| `shortDescription` | `shortDescription` | 짧은 설명이 누락된 경우 빈 문자열을 사용합니다. |
| `visibility` | `visibleIn` | 쉼표로 구분된 값을 분할하고 `Catalog`을(를) `CATALOG`에, `Search`을(를) `SEARCH`에 매핑합니다. 다른 값을 삭제합니다. |
| `metaTitle` | `metaTags/title` | |
| `metaDescription` | `metaTags/description` | |
| `metaKeyword` | `metaTags/keywords` | 줄바꿈으로 구분된 키워드를 배열로 분할하고 공백을 트리밍합니다. |
| `inStock`, `lowStock`, `weight`, `weightUnit` | `attributes[].code = "aco_ac_attributes"` | `aco_ac_attributes` 항목을 항상 첫 번째 특성으로 추가합니다. 해당 JSON 값에는 문자열로 `inStock` 및 `lowStock`이(가) 포함되어 있습니다. 해당 값을 사용할 수 있는 경우 `weight` 및 `weightType`이(가) 포함됩니다. |
| `attributes[]` | `attributes[]` | 사용 가능한 경우 각 항목을 해당 특성 코드, 문자열 값 및 일치하는 변형 참조 ID에 매핑합니다. `inStock`, `lowStock`, `categories`, `weight` 및 `weightType`을(를) 건너뜁니다. 인벤토리 관련 값이 `aco_ac_attributes`에 포함되어 있습니다. 범주는 경로로 내보내집니다. |
| `images[]` | `images[]` | URL 없이 이미지를 건너뜁니다.<br>`url`, `label`(누락된 경우 비어 있음), `sortOrder`(정수, 기본값: `0`)을 내보냅니다.<br>이미지를 `sortOrder`별로 오름차순으로 정렬합니다.<br>표준 역할 `image`을(를) `BASE`에, `small_image`을(를) `SMALL`에, `thumbnail`을(를) `THUMBNAIL`에, `swatch_image`을(를) `SWATCH`에 매핑합니다. 다른 역할을 `customRoles[]`(으)로 내보냅니다. |
| `categoryData[].categoryPath` | `routes[].path` | 빈 범주 경로가 있는 항목을 건너뜁니다. |
| `categoryData[].productPosition` | `routes[].position` | 제품 위치가 누락된 경우 `0`을(를) 사용합니다. |
| `links[].type` + `links[].sku` | `links[]` | `type`이(가) 우선함, `sku`이(가) 없는 항목이 삭제됨 |
| `parents[].productType` + `parents[].sku` | `links[]` | `configurable`을(를) `VARIANT_OF`에 매핑하고 `bundle` 또는 `bundle_fixed`을(를) `IN_BUNDLE`에 매핑합니다. 다른 제품 유형을 대문자로 변환합니다. SKU 없이 상위 항목을 건너뜁니다. |
| `configurable options` | `configurations[]` | ID와 하나 이상의 값이 있는 옵션을 내보냅니다.<br>`id`을(를) `attributeCode`에 매핑합니다. `swatchType`이(가) 있는 경우 `type`을(를) `SWATCH`(으)로 설정하고, 그렇지 않은 경우 `CONFIGURABLE`(으)로 설정합니다.<br>기본 값의 ID를 `defaultVariantReferenceId`(으)로 사용합니다.<br>각 값을 `variantReferenceId`, `label`, `colorHex` 및 `imageUrl`에 매핑합니다. |
| `bundle options` | `bundles[]` | 하나 이상의 항목이 포함된 옵션을 내보냅니다.<br>옵션 레이블을 `group`(으)로 사용하거나 레이블이 비어 있는 경우 `Bundle group`(으)로 사용합니다. `required`을(를) 출력으로 복사합니다.<br>렌더링 형식 `checkbox` 및 `multi`에 대해 `multiSelect`을(를) `true`(으)로 설정합니다.<br>`defaultItemSkus`에 기본 SKU를 나열합니다. 각 항목에는 `sku`, `qty`(기본값: `0`) 및 `userDefinedQty`(기본값: `qtyMutability`, 기본값: `false`)이(가) 포함됩니다. |

## 제품 특성 메타데이터

`productAttributes` 피드가 [메타데이터 끝점](https://developer.adobe.com/commerce/services/reference/rest/#tag/Metadata){target="_blank"}에 데이터를 보냅니다.

| [!DNL Adobe Commerce] 필드 | [!DNL Commerce Optimizer] API 필드 | 매핑 세부 정보 |
| --------------- | -------------- | ------- |
| `attributeCode` | `code` | |
| `storeViewCode` | `source/locale` | |
| `label` | `label` | |
| `dataType` + `frontendInput` | `dataType` | 아래의 전환 표를 참조하십시오. |
| `dataType` 및 `frontendInput` | `dataType` | 아래의 전환 규칙을 사용합니다. |
| `visible`, `visibleInSearch`, `visibleInListing`, `visibleInCompareList` | `visibleIn[]` | 플래그가 `true`이면 해당 값 <br>`visible` → `PRODUCT_DETAIL`<br>`visibleInSearch` → `SEARCH_RESULTS`<br>`visibleInListing` → `PRODUCT_LISTING`<br>`visibleInCompareList` → `PRODUCT_COMPARE`을(를) 추가합니다. |
| `filterable` | `filterable` | |
| `sortable` | `sortable` | |
| `searchable` | `searchable` | |
| `searchWeight` | `searchWeight` | |
| `searchTypes` | `searchTypes` | |

### 데이터 유형 전환

`dataType`이(가) `int`이면 커넥터가 `frontendInput`을(를) 확인합니다. 다른 데이터 형식의 경우 `frontendInput`은(는) 변환에 영향을 주지 않습니다.

| `dataType` 입력 | `frontendInput` 입력 | 출력 `dataType` |
| ---------------- | --------------------- | ----------------- |
| `int` | `boolean` | `BOOLEAN` |
| `int` | `text` 또는 `select` | `TEXT` |
| `int` | 누락된 값을 포함한 기타 모든 값 | `INTEGER` |
| `decimal` | 사용되지 않음 | `DECIMAL` |
| `text`, `varchar`, `static`, `datetime` | 사용되지 않음 | `TEXT` |
| `OBJECT` | 사용되지 않음 | `OBJECT` |
| 기타 값 | 사용되지 않음 | `TEXT` |

>[!NOTE]
>
>특성이 `OBJECT` 데이터 형식을 사용하는 경우 [Products API](https://developer.adobe.com/commerce/services/reference/graphql/#products){target="_blank"}에서 저장된 값을 JSON으로 구문 분석하려고 합니다. 구문 분석이 성공하면 API는 값을 중첩 객체로 반환합니다. 단일 값으로 표현할 수 없는 구조화된 특성 데이터에 `OBJECT`을(를) 사용하십시오. 자세한 지침은 [제품 특성을 동적으로 추가](../../data-export/add-attribute-dynamically.md)를 참조하십시오.

## 가격 장부

`priceBooks` 피드가 [가격 장부 끝점](https://developer.adobe.com/commerce/services/reference/rest/#tag/Price-Books){target="_blank"}에 데이터를 보냅니다.

다른 커넥터 피드와 달리 `priceBooks` 피드는 [!DNL Adobe Commerce]의 [!DNL SaaS Data Export] 인덱서에서 수집되지 않습니다. 커넥터는 관리자의 웹 사이트 및 고객 그룹 구성에서 이 피드를 생성합니다.

각 웹 사이트에 대해 커넥터는 각 고객 그룹에 대해 하나의 기본 가격 장부와 하나의 하위 가격 장부를 만듭니다.

`priceBookId`에 대해 다음 수식 사용:

- 정가에 대한 기본 가격 장부: `priceBookId = websiteCode`.
- 고객 그룹에 대한 하위 가격 장부: `priceBookId = websiteCode::sha1(customerGroupId)`. 여기서 `sha1(customerGroupId)`은(는) 고객 그룹의 정수 ID에 대한 SHA-1 16진수 다이제스트입니다.

가격 피드는 동일한 공식을 사용하여 가격 장부에 각 가격 입력을 지정합니다. Storefront가 고객 세션에 대해 `priceBookId`을(를) 해결하는 방법에 대한 자세한 내용은 [Headless storefront 통합](../headless-storefront.md#graphql-commerceoptimizer-query)을(를) 참조하십시오.


| Source 필드 또는 값 | [!DNL Commerce Optimizer] API 필드 | 매핑 세부 정보 |
| ---------------- | -------------- | ------- |
| `websiteCode` | `parentId` | 하위 가격표에 이 필드를 추가합니다. 이 값은 기본 가격 장부를 식별합니다. |
| 웹 사이트 이름 | `name` | 기본 가격 장부에 웹 사이트 이름을 사용합니다. 하위 가격표에 `Customer group name (Website name)`을(를) 사용합니다. |
| `websiteCode` | `parentId` | 아동 가격 장부에만 표시, 기본 가격 장부를 가리킵니다. |
| 웹 사이트 기본 통화 | `currency` | 기본 가격 장부에만 이 필드를 포함합니다. 아동용 가격 책에는 그것이 빠져 있다. |

## 가격

`prices` 피드가 [!DNL Adobe Commerce] 데이터를 [가격 끝점](https://developer.adobe.com/commerce/services/reference/rest/#tag/Prices){target="_blank"}에 보냅니다.

| 피드 입력 필드 | [!DNL Commerce Optimizer] API 필드 | 매핑 세부 정보 |
| --------------- | -------------- | ------------------------------------------------------------------------------- |
| `sku` | `sku` | SKU를 변경되지 않은 상태로 전달합니다. |
| `websiteCode`, `customerGroupCode` | `priceBookId` | `customerGroupCode`에서 `websiteCode`을(를) 고객 그룹 ID의 SHA-1 해시와 결합합니다. `customerGroupCode`이(가) `0`인 경우 `websiteCode`만 사용합니다. |
| `regular` | `regular` | 변경되지 않은 상태로 일반 가격을 전달합니다. |
| `discounts[]` | `discounts[]` | 원본 값이 `null`인 경우 빈 배열을 내보냅니다.<br>값이 `0`에서 `100` 사이인 경우 `code`이(가) `special_price` 및 `percentage`(으)로 설정된 항목의 경우 `percentage`을(를) `100 - percentage`(으)로 설정합니다. 해당 범위 또는 외부에서 `0`(으)로 설정합니다.<br>가격 기반 특별 가격을 포함한 다른 항목을 변경되지 않은 상태로 전달합니다. |
| `tierPrices[]` | `tierPrices[]` | 원본 값이 없거나 `null`인 경우 빈 배열을 사용합니다. |

## 카테고리

`categories` 피드가 [Categories 끝점](https://developer.adobe.com/commerce/services/reference/rest/#tag/Categories){target="_blank"}에 [!DNL Adobe Commerce] 데이터를 보냅니다.

빈 `urlPath`(논리 루트 범주)이 있는 항목은 건너뛰고 제출되지 않습니다.

| [!DNL Adobe Commerce] 필드 | [!DNL Commerce Optimizer] API 필드 | 매핑 세부 정보 |
| --------------- | -------------- | ------- |
| `storeViewCode` | `source/locale` | |
| `name` | `name` | |
| `urlPath` | `slug` | |
| `description` | `description` | |
| `position` | `position` | 존재하는 경우 카테고리 위치를 내보냅니다. 누락된 경우 필드를 생략합니다. |
| `metaTitle` | `metaTags/title` | |
| `metaDescription` | `metaTags/description` | |
| `metaKeywords` | `metaTags/keywords` | 줄바꿈으로 구분된 문자열을 배열로 분할 |
| `image` | `images[].url` | 단일 요소 배열; `roles: ["BASE"]` |
| `isActive` + `includeInMenu` | `families` | `true`과(와) 그렇지 않은 경우 `["top_menu"]`, 그렇지 않은 경우 `[]` |

| `metaKeywords` | `metaTags/keywords` | 줄바꿈으로 구분된 키워드를 배열로 분할하고 공백을 트리밍합니다. |
| `image` | `images[].url` | `image`이(가) 있으면 `BASE` 역할이 있는 하나의 이미지를 내보냅니다. 이미지가 비어 있거나 누락된 경우 빈 배열을 내보냅니다. |
| `isActive` + `includeInMenu` | `families` | 두 값이 모두 `true`인 경우에만 `top_menu`을(를) 추가합니다. 그렇지 않으면 빈 배열을 내보냅니다. |
| `attributes[]` | `attributes[]` | 비어 있지 않은 `attributeCode`의 항목을 `{code, values[]}`(으)로 내보냅니다. 값을 문자열로 변환합니다. 적격한 항목이 없으면 `attributes`을(를) 생략합니다. |

>[!MORELIKETHIS]
>
> - [데이터 수집 API를 사용하여 제품 및 가격 데이터 수집](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/){target="_blank"} - 메타데이터, 제품, 카테고리, 가격 장부 및 가격에 대한 카탈로그 데이터 모델을 알아봅니다.
> - [카탈로그 데이터 수집 REST API 참조](https://developer.adobe.com/commerce/services/reference/rest/){target="_blank"} - 각 피드 끝점에 대한 요청 및 응답 스키마 검토
> - [다음을 사용하는 방법 [!DNL Commerce Optimizer Connector] 방법 [!DNL Adobe Commerce]](../overview.md#how-the-connector-works-with-adobe-commerce) - 스토어 조회수, 웹 사이트 및 고객 그룹이 카탈로그 소스 및 가격 장부에 매핑되는 방법을 알아봅니다.
> - [가격 장부 위치 [!DNL Commerce Optimizer]](/help/optimizer/setup/pricebooks.md) — 커넥터 내보내기로 생성된 가격 장부를 관리합니다.
> - [헤드리스 상점 통합](../headless-storefront.md#graphql-commerceoptimizer-query) — 고객 세션에 대한 `priceBookId` 해결
