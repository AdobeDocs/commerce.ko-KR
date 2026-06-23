---
title: 피드 테이블 스키마 참조
description: ' [!DNL Adobe Commerce Optimizer Connector] 이(가) 피드 항목 상태, 내보내기 상태 및 오류 세부 사항을 추적하는 데 사용하는 피드 테이블 스키마에 대해 알아봅니다.'
autotag-review: '2026-06-23T00:00:00.000Z'
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="PaaS만" type="Informative" url="https://experienceleague.adobe.com/ko/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce 온 클라우드 프로젝트(Adobe 관리 PaaS 인프라) 및 온프레미스 프로젝트에만 적용됩니다."
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: cc250cf1-34eb-4863-80d0-d170d45ea067
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: 19de20caafd45e3a00896d0d4b29b7e96dfe94e1
workflow-type: tm+mt
source-wordcount: 324
ht-degree: 0%

---


# 피드 테이블 스키마 참조

모든 피드에는 [!DNL Adobe Commerce] 데이터베이스에 전용 MySQL 테이블이 있습니다. 모든 피드 테이블은 동일한 열 구조를 공유합니다.

## 지원되는 피드

API 끝점, 일괄 처리 제한, 인덱서 이름 및 피드 테이블 이름을 사용하는 지원되는 피드의 전체 목록에 대해서는 [커넥터 모듈 및 피드 끝점](connector-reference.md#supported-feeds)을 참조하십시오.

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
| `status` | INT | 마지막 내보내기 시도에 따른 제출 상태 코드. [피드 제출 및 오류 처리](../connector-sync-pipeline.md#feed-submission-and-error-handling)를 참조하십시오. |
| `errors` | 텍스트 | 이 항목에 대해 [!DNL Commerce Optimizer] API에서 반환된 JSON 인코딩 오류 세부 정보 |
| `metadata` | JSON | 내보내기 프레임워크에서 사용하는 내부 동기화 플래그 및 메타데이터 잠금 정보 |

## 일반적인 진단 쿼리

다음 SQL 쿼리를 사용하여 피드 테이블 상태를 직접 검사하십시오. `feed_data` 열은 [!DNL Adobe Commerce Optimizer] API 형식으로 데이터를 저장합니다. `<SKU>`, `<ATTRIBUTE_CODE>`, `<SLUG>` 및 `<PRICE_BOOK_ID>` 등의 자리 표시자 값을 환경의 실제 값으로 바꾸십시오.

**제품 피드 - SKU별:**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.sku') AS 'SKU',
       JSON_EXTRACT(f.feed_data, '$.source.locale') AS 'locale',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_products_feed f
WHERE JSON_EXTRACT(f.feed_data, '$.sku') IN ('<SKU>');
```

**제품 특성 피드 - 특성 코드별:**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.code') AS 'code',
       JSON_EXTRACT(f.feed_data, '$.source.locale') AS 'locale',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_product_attributes_feed f
WHERE JSON_EXTRACT(f.feed_data, '$.code') IN ('<ATTRIBUTE CODE>');
```

**범주 피드 - URL 경로별:**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.slug') AS 'slug',
    JSON_EXTRACT(f.feed_data, '$.source.locale') AS 'locale',
    f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_categories_feed f
WHERE JSON_EXTRACT(f.feed_data, '$.slug') IN ('<SLUG>');
```

**가격 피드 - SKU 기준:**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.sku') AS 'SKU',
       JSON_EXTRACT(f.feed_data, '$.priceBookId') AS 'price book ID',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_product_prices_feed f
WHERE JSON_EXTRACT(f.feed_data, '$.sku') IN ('<SKU>');
```

**가격 장부 피드 - 가격 장부 ID별:**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.priceBookId') AS 'price book ID',
    JSON_EXTRACT(f.feed_data, '$.name') AS 'name',
    JSON_EXTRACT(f.feed_data, '$.parentId') AS 'parent price book ID',
    JSON_EXTRACT(f.feed_data, '$.currency') AS 'currency',
    f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_price_books_feed f
WHERE JSON_UNQUOTE(JSON_EXTRACT(f.feed_data, '$.priceBookId'))  IN ('<PRICE_BOOK_ID>');
```

>[!MORELIKETHIS]
>
>- [커넥터 모듈 및 피드 끝점](connector-reference.md)
>- [커넥터 동기화 파이프라인](../connector-sync-pipeline.md)
>- [동기화 관리](../data-sync-manage.md)
>- [커넥터 피드에 대한 필드 매핑](field-mapping.md)
