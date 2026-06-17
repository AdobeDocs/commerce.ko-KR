---
title: ' [!DNL Adobe Commerce Optimizer Connector] 피드에 대한 필드 매핑'
description: 모든 피드에 대한  [!DNL Adobe Commerce] 카탈로그 데이터에서  [!DNL Adobe Commerce Optimizer] 수집 API 형식으로의  [!DNL Adobe Commerce Optimizer Connector] 필드 매핑에 대해 알아봅니다.
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="PaaS만" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce 온 클라우드 프로젝트(Adobe 관리 PaaS 인프라) 및 온프레미스 프로젝트에만 적용됩니다."
autotag-review: '2026-06-09T15:49:03.934Z'
TQID: 'https://experienceleague.adobe.com/SOWOnguudhqzX-r66nGUqc-WKet5qq6GRV11ADx0Me4'
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: b974b164-8a4e-43b8-a9e2-8e67ec131677id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: e7dae43f-215c-4cdf-90d3-c5a461a6e669id: c32adafa-ed01-4b31-997e-2413013911b0
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: e0eb8757-182f-49f3-94a4-1587d16f5094id: b23e006f-0a29-4f1d-8fd0-77aa56f3d12b
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 665
ht-degree: 0%

---


# 커넥터 피드에 대한 필드 매핑

이 페이지에서는 [!DNL Adobe Commerce Optimizer Connector]이(가) [!DNL Adobe Commerce] 카탈로그 필드를 [!DNL Commerce Optimizer] [!DNL Catalog Data Ingestion API]에 필요한 형식으로 변환하는 방법을 설명합니다. 지원되는 피드 및 해당 API 끝점에 대한 목록은 [커넥터 참조](connector-reference.md#supported-feeds)를 참조하십시오.

## 제품

`products` 피드가 [제품 끝점](https://developer.adobe.com/commerce/services/reference/rest/#tag/Products){target="_blank"}에 데이터를 보냅니다.

| [!DNL Adobe Commerce] 필드 | [!DNL Commerce Optimizer] API 필드 | 메모 |
| ----------------------------------------------- | -------------- | ------- |
| `sku` | `sku` | |
| `storeViewCode` | `source/locale` | |
| `name` | `name` | |
| `urlKey` | `slug` | |
| `productId` | `externalIds[0].id` | `origin`이(가) `"AdobeCommerce"`(으)로 수정됨 |
| `status` | `status` | 상위 항목입니다. 하위 항목이 할당되지 않은 복합 제품에 대해 `DISABLED`(으)로 설정합니다. |
| `description` | `description` | |
| `shortDescription` | `shortDescription` | |
| `visibility` | `visibleIn` | 쉼표로 구분된 값 분할 및 매핑됨: `Catalog`→`CATALOG`, `Search`→`SEARCH`; 매핑되지 않은 값이 삭제됨 |
| `metaTitle` | `metaTags/title` | |
| `metaDescription` | `metaTags/description` | |
| `metaKeyword` | `metaTags/keywords` | 줄바꿈으로 구분된 문자열을 배열로 분할 |
| `inStock`, `lowStock`, `weight`, `weightUnit` | `attributes[].code = "aco_ac_attributes"` | JSON 인코딩 개체 `{inStock, lowStock, weight, weightType}`; 항상 첫 번째 특성 항목으로 표시 |
| `attributes[]` | `attributes[]` | `{code, values[], variantReferenceId}`; `inStock`, `lowStock`, `weight`, `weightType`에 매핑된 각 항목이 제외됩니다(`aco_ac_attributes`(으)로 이동). |
| `images[]` | `images[]` | `url`, `label`; 매핑된 표준 역할: `image`→`BASE`, `small_image`→`SMALL`, `thumbnail`→`THUMBNAIL`, `swatch_image`→`SWATCH`; 비표준 역할은 `customRoles[]`(으)로 이동 |
| `categoryData[].categoryPath` | `routes[].path` | |
| `categoryData[].productPosition` | `routes[].position` | |
| `links[].type` + `links[].sku` | `links[]` | `type`이(가) 우선함, `sku`이(가) 없는 항목이 삭제됨 |
| `parents[].productType` + `parents[].sku` | `links[]` | 매핑된 형식: `configurable`→`VARIANT_OF`, `bundle`/`bundle_fixed`→`IN_BUNDLE` |
| `configurable options` | `configurations[]` | `id`→`attributeCode`, `label`; `swatchType`이(가) 설정된 경우 옵션 유형 `SWATCH`, 기타 `CONFIGURABLE`; `isDefault`의 기본 변형; 값: `variantReferenceId`, `label`, `colorHex`, `imageUrl` |
| `bundle options` | `bundles[]` | `label`→`group`; `required`; `renderType` `checkbox`/`multi`→`multiSelect: true`; `isDefault`의 기본 SKU; 항목에 `sku`, `qty`, `userDefinedQty`(`qtyMutability`) 포함 |

## 제품 특성 메타데이터

`productAttributes` 피드가 [메타데이터 끝점](https://developer.adobe.com/commerce/services/reference/rest/#tag/Metadata){target="_blank"}에 데이터를 보냅니다.


| [!DNL Adobe Commerce] 필드 | [!DNL Commerce Optimizer] API 필드 | 메모 |
| --------------- | -------------- | ------- |
| `attributeCode` | `code` | |
| `storeViewCode` | `source/locale` | |
| `label` | `label` | |
| `dataType` + `frontendInput` | `dataType` | 아래의 전환 표를 참조하십시오. |
| `visible` | `visibleIn: "PRODUCT_DETAIL"` | `true`할 때 배열에 추가됨 |
| `visibleInSearch` | `visibleIn: "SEARCH_RESULTS"` | `true`할 때 배열에 추가됨 |
| `visibleInListing` | `visibleIn: "PRODUCT_LISTING"` | `true`할 때 배열에 추가됨 |
| `visibleInCompareList` | `visibleIn: "PRODUCT_COMPARE"` | `true`할 때 배열에 추가됨 |
| `filterable` | `filterable` | |
| `sortable` | `sortable` | |
| `searchable` | `searchable` | |
| `searchWeight` | `searchWeight` | |
| `searchTypes` | `searchTypes` | |

### 데이터 유형 전환

커넥터가 위의 매핑 테이블에 있는 Commerce `dataType` 및 `frontendInput` 필드에서 API `dataType`을(를) 파생합니다. 다음 표는 커넥터가 적용되는 전환 규칙을 보여 줍니다.

| [!DNL Adobe Commerce] `dataType` | [!DNL Adobe Commerce] `frontendInput` | [!DNL Commerce Optimizer] API `dataType` |
| -------------------- | -------------------------- | ------------------- |
| `int` | `boolean` | `BOOLEAN` |
| `int` | `text` 또는 `select` | `TEXT` |
| `int` | 기타 | `INTEGER` |
| `decimal` | - | `DECIMAL` |
| `text`, `varchar`, `static`, `datetime` | - | `TEXT` |
| `OBJECT` | - | `OBJECT` |
| 기타 | - | `TEXT` |

>[!NOTE]
>
>특성에 대한 `dataType`이(가) `OBJECT`(으)로 설정되어 있으면 [제품 API](https://developer.adobe.com/commerce/services/reference/graphql/#products){target="_blank"}은(는) 특성 값을 일반 문자열이 아닌 구조화된 개체로 취급합니다. 쿼리 시간에 API는 저장된 값을 JSON으로 구문 분석하려고 합니다. 구문 분석이 성공하면 결과가 응답에서 중첩 객체로 반환됩니다. **이 동작은 사용자 지정 특성을 동적으로 제공할 때(예: 스칼라 값으로 표현할 수 없는 구조화된 또는 다중 필드 데이터를 전달할 때) 특히 유용합니다**. 자세한 지침은 [제품 특성을 동적으로 추가](../../data-export/add-attribute-dynamically.md)를 참조하십시오.

## 가격 장부

`priceBooks` 피드가 [가격 장부 끝점](https://developer.adobe.com/commerce/services/reference/rest/#tag/Price-Books){target="_blank"}에 데이터를 보냅니다.

다른 커넥터 피드와 달리 `priceBooks` 피드는 [!DNL Adobe Commerce]의 [!DNL SaaS Data Export] 인덱서에서 수집되지 않습니다. 커넥터는 관리자의 웹 사이트 및 고객 그룹 구성에서 이 피드를 생성합니다.

웹 사이트당 하나의 **기본 가격 책**&#x200B;이 만들어지고 웹 사이트-고객 그룹 쌍당 하나의 **하위 가격 책**&#x200B;이 만들어집니다.

**가격 장부 ID 수식:**

- **기본**(정가): `priceBookId = websiteCode`
- **자식**(고객 그룹 또는 공유 카탈로그): `priceBookId = websiteCode::sha1(customerGroupId)`. 여기서 `sha1(customerGroupId)`은(는) 고객 그룹의 정수 ID에 대한 SHA-1 16진수 다이제스트입니다.

가격 피드는 가격 입력이 속한 가격 장부를 해결할 때 동일한 공식을 사용합니다. Storefront가 고객 세션에 대한 `priceBookId`을(를) 해결하는 방법은 [Headless storefront 통합](../headless-storefront.md#graphql-commerceoptimizer-query)을(를) 참조하십시오.

| 생성된 필드 | [!DNL Commerce Optimizer] API 필드 | 메모 |
| ---------------- | -------------- | ------- |
| `websiteCode`, `customerGroupId` | `priceBookId` | |
| 웹 사이트 이름 | `name` | 기본 가격 장부: 웹 사이트 이름. 자식: `"Group Name (Website Name)"` |
| `websiteCode` | `parentId` | 아동 가격 장부에만 표시, 기본 가격 장부를 가리킵니다. |
| 웹 사이트 기본 통화 | `currency` | 기본 가격 장부로만 제공, 자녀에게 상속 |

## 가격

`prices` 피드가 [가격 끝점](https://developer.adobe.com/commerce/services/reference/rest/#tag/Prices){target="_blank"}에 데이터를 보냅니다.

| [!DNL Adobe Commerce] 필드 | [!DNL Commerce Optimizer] API 필드 | 메모 |
| --------------- | -------------- | ------------------------------------------------------------------------------- |
| `sku` | `sku` | |
| `websiteCode`, `customerGroupId` | `priceBookId` | |
| `regular` | `regular` | |
| `discounts[]` | `discounts[]` | 할인의 예: 특별 가격, 카탈로그 규칙 가격, 공유 카탈로그 가격 |
| `tierPrices[]` | `tierPrices[]` | |

## 카테고리

`categories` 피드가 [Categories 끝점](https://developer.adobe.com/commerce/services/reference/rest/#tag/Categories){target="_blank"}으로 데이터를 보냅니다.

빈 `urlPath`(논리 루트 범주)이 있는 항목은 건너뛰고 제출되지 않습니다.

| [!DNL Adobe Commerce] 필드 | [!DNL Commerce Optimizer] API 필드 | 메모 |
| --------------- | -------------- | ------- |
| `storeViewCode` | `source/locale` | |
| `name` | `name` | |
| `urlPath` | `slug` | |
| `description` | `description` | |
| `metaTitle` | `metaTags/title` | |
| `metaDescription` | `metaTags/description` | |
| `metaKeywords` | `metaTags/keywords` | 줄바꿈으로 구분된 문자열을 배열로 분할 |
| `image` | `images[].url` | 단일 요소 배열; `roles: ["BASE"]` |
| `isActive` + `includeInMenu` | `families` | `true`과(와) 그렇지 않은 경우 `["top_menu"]`, 그렇지 않은 경우 `[]` |

>[!MORELIKETHIS]
>
> - [데이터 수집 API를 사용하여 제품 및 가격 데이터 수집](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/){target="_blank"} - 메타데이터, 제품, 카테고리, 가격 장부 및 가격에 대한 카탈로그 데이터 모델을 알아봅니다.
> - [카탈로그 데이터 수집 REST API 참조](https://developer.adobe.com/commerce/services/reference/rest/){target="_blank"} - 각 피드 끝점에 대한 요청 및 응답 스키마 검토
> - [다음을 사용하는 방법 [!DNL Commerce Optimizer Connector] 방법 [!DNL Adobe Commerce]](../overview.md#how-the-connector-works-with-adobe-commerce) - 스토어 조회수, 웹 사이트 및 고객 그룹이 카탈로그 소스 및 가격 장부에 매핑되는 방법을 알아봅니다.
> - [가격 장부 위치 [!DNL Commerce Optimizer]](/help/optimizer/setup/pricebooks.md) — 커넥터 내보내기로 생성된 가격 장부를 관리합니다.
> - [헤드리스 상점 통합](../headless-storefront.md#graphql-commerceoptimizer-query) — 고객 세션에 대한 `priceBookId` 해결
