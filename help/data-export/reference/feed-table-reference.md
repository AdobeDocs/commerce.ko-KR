---
title: 피드 테이블 스키마 참조
description: ' [!DNL SaaS Data Export] 이(가) 피드 항목 상태, 내보내기 상태 및 오류 세부 사항을 추적하는 데 사용하는 피드 테이블 스키마에 대해 알아봅니다.'
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
feature: Services
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: b974b164-8a4e-43b8-a9e2-8e67ec131677id: cdf0c6dd-1717-4e20-9530-a24eee57088bid: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: cc250cf1-34eb-4863-80d0-d170d45ea067
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: c70c1643afbf8e9633df89a613d6798416c8eb44
workflow-type: tm+mt
source-wordcount: 429
ht-degree: 0%

---


# 피드 테이블 스키마 참조

모든 피드에는 [!DNL Adobe Commerce] 데이터베이스에 전용 MySQL 테이블이 있습니다. 모든 피드 테이블은 동일한 열 구조를 공유합니다. 아래 표에는 각 피드가 CLI 피드 이름, 인덱서 ID 및 피드 테이블 이름과 함께 나열되어 있습니다.

## 지원되는 피드

실제 피드 목록은 설치된 [!DNL SaaS Data Export] 패키지에 따라 다릅니다.


| 피드(`--feed`) | 목적 | 인덱서 ID | 피드 테이블 | 내보내기 모드 |
| --- | ------------------------------------------------------------------- | --- | --- | --- |
| `products` | 제품 카탈로그(속성, 카테고리, 이미지 등) | `catalog_data_exporter_products` | `cde_products_feed` | 즉시 |
| `productAttributes` | 속성 정의 및 메타데이터. 검색 스키마를 정의하는 데 사용됩니다. | `catalog_data_exporter_product_attributes` | `cde_product_attributes_feed` | 즉시 |
| `categories` | 카테고리 데이터 | `catalog_data_exporter_categories` | `cde_categories_feed` | 즉시 |
| `prices` | 고객 그룹 가격 및 계층 가격이 포함된 제품 가격 | `catalog_data_exporter_product_prices` | `cde_product_prices_feed` | 즉시 |
| `variants` | 구성 가능한 제품 변형 | `catalog_data_exporter_product_variants` | `cde_product_variants_feed` | 즉시 |
| `scopesWebsite` | 스토어 보기 코드가 있는 웹 사이트 | `scopes_website_data_exporter` | `scopes_website_data_exporter` | 레거시 |
| `scopesCustomerGroup` | 고객 그룹 정의 | `scopes_customergroup_data_exporter` | `scopes_customergroup_data_exporter` | 레거시 |
| `productOverrides` | 계산된 제품 권한 | `catalog_data_exporter_product_overrides` | `cde_product_overrides_feed` | 즉시 |
| `categoryPermissions` *(EE)* | 원시 범주 권한 데이터 | `catalog_data_exporter_category_permissions` | `cde_category_permissions_feed` | 즉시 |
| `orders` | 판매 주문 상태 | `sales_order_data_exporter_v2` | `sales_data_exporter_orders_v2` | 레거시 |

**내보내기 모드** 열은 각 피드가 데이터를 수집하고 제출하는 방법을 나타냅니다.

- **즉시 모드 피드** - 데이터를 수집하고, 콘텐츠 해시를 사용하여 변경되지 않은 항목을 건너뛰고(해시 중복 제거), 같은 인덱서 실행에서 업데이트를 제출합니다.
- **레거시 모드 피드**(`scopesWebsite`, `scopesCustomerGroup`, `orders`) — 먼저 어셈블된 데이터를 피드 테이블에 저장하고 별도의 cron 작업을 통해 제출합니다.

[동기화 모드](../sync-overview.md#synchronization-modes)를 참조하십시오.

## 스키마

| 열 | 유형 | 설명 |
| --- | --- | ---------------- |
| `id` | INT(PK) | 기본 키 자동 증가 |
| `source_entity_id` | INT | Commerce 소스 테이블의 엔터티 ID(예: `catalog_product_entity.entity_id`) |
| `feed_id` | VARCHAR | 피드 항목에 대한 고유 식별자입니다. 자동 증가 값이 아닌 항목의 ID 필드(예: `sku + storeViewCode`)의 해시로 계산됩니다. |
| `feed_data` | JSON | 이 항목에 대한 피드 페이로드. 엔티티 식별자 및 범위로서 최소한의 정보만 채워집니다. `PERSIST_EXPORTED_FEED=1`이(가) 설정되면 전체 페이로드가 저장됩니다. |
| `feed_hash` | VARCHAR | 변경 내용 검색에 사용되는 컨텐츠 해시입니다. 페이로드에서 계산되며, 타임스탬프(`modifiedAt`, `updatedAt`)는 제외됩니다. 해시가 이전 내보내기와 일치하는 경우 항목이 다시 제출되지 않습니다. |
| `is_deleted` | TINYINT | 일시 삭제 마커. Commerce에서 엔터티가 삭제되면 `1`(으)로 설정합니다. |
| `modified_at` | 타임스탬프 | 이 피드 항목이 마지막으로 수정된 시간 |
| `status` | INT | 마지막 내보내기 시도에 따른 제출 상태 코드. [피드 제출 및 HTTP 오류 처리](../sync-overview.md#feed-submission-and-http-error-handling)를 참조하십시오. |
| `errors` | 텍스트 | 이 항목에 대해 SaaS 서비스에서 반환한 JSON 인코딩 오류 세부 정보 |
| `metadata` | JSON | 내보내기 프레임워크에서 사용하는 내부 동기화 플래그 및 메타데이터 잠금 정보 |

## 일반적인 진단 쿼리

다음 SQL 쿼리를 사용하여 피드 테이블 상태를 직접 검사하십시오. `<SKU>`, `<ATTRIBUTE_CODE>` 및 `<CATEGORY_ID>` 등의 자리 표시자 값을 환경의 실제 값으로 바꾸십시오. 테이블 이름의 전체 목록은 [지원되는 피드](#supported-feeds)를 참조하십시오.

**제품 피드 — SKU별:**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.sku') AS 'SKU',
       JSON_EXTRACT(f.feed_data, '$.storeViewCode') AS 'store view code',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_products_feed f
WHERE JSON_EXTRACT(f.feed_data, '$.sku') IN ('<SKU>');
```

**제품 특성 피드 — 특성 코드별:**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.attributeCode') AS 'code',
       JSON_EXTRACT(f.feed_data, '$.storeViewCode') AS 'store view code',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_product_attributes_feed f
WHERE JSON_EXTRACT(f.feed_data, '$.attributeCode') IN ('<ATTRIBUTE_CODE>');
```

**가격 피드 — SKU 기준:**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.sku') AS 'SKU',
       JSON_EXTRACT(f.feed_data, '$.websiteCode') AS 'website code',
       JSON_EXTRACT(f.feed_data, '$.customerGroupCode') AS 'customer group code',
       IFNULL(cg.customer_group_code, '-- (base price)') AS 'AC customer group',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_product_prices_feed f
LEFT JOIN customer_group cg
       ON sha1(cg.customer_group_id) = JSON_EXTRACT(f.feed_data, '$.customerGroupCode')
WHERE JSON_EXTRACT(f.feed_data, '$.sku') IN ('<SKU>');
```

**SKU별 제품 재정의 피드 —**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.sku') AS 'SKU',
       JSON_EXTRACT(f.feed_data, '$.websiteCode') AS 'website code',
       JSON_EXTRACT(f.feed_data, '$.customerGroupCode') AS 'customer group code',
       IFNULL(cg.customer_group_code, 'NA (deleted)') AS 'AC customer group',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_product_overrides_feed f
LEFT JOIN customer_group cg
       ON sha1(cg.customer_group_id) = JSON_EXTRACT(f.feed_data, '$.customerGroupCode')
WHERE JSON_EXTRACT(f.feed_data, '$.sku') IN ('<SKU>');
```

**범주 피드 — 범주 ID별:**

```sql
SELECT JSON_EXTRACT(feed_data, '$.categoryId') AS 'Category ID',
       JSON_EXTRACT(f.feed_data, '$.storeViewCode') AS 'store view code',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_categories_feed f
WHERE JSON_EXTRACT(feed_data, '$.categoryId') IN (<CATEGORY_ID>);
```

**Variants 피드 — 구성 가능한 제품 SKU별:**

```sql
SELECT JSON_EXTRACT(feed_data, '$.parentSku') AS 'configurable SKU',
       JSON_EXTRACT(feed_data, '$.productSku') AS 'Variant SKU',
       JSON_EXTRACT(f.feed_data, '$.optionValues') AS 'options',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_product_variants_feed f
WHERE JSON_EXTRACT(feed_data, '$.parentSku') = '<SKU>';
```


>[!MORELIKETHIS]
>
>- [데이터를 SaaS 데이터 내보내기와 동기화](../sync-overview.md)
>- [동기화 보기 및 관리](../data-sync-manage.md)
>- [Commerce CLI를 사용하여 피드 동기화](../data-export-cli-commands.md)
