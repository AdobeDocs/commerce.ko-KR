---
source-git-commit: 1b8a6de3a35a626f211089955029207f8a88414c
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 0%

---
# MDEE 로그 코드 참조

로그 코드 형식: `CDE<group_id>-<log_id>`(예: `CDE01-02`)

소스: `commerce-data-export`, `commerce-data-export-ee`, `saas-export`

코드는 `error`, `warning` 및 `critical` 수준 로그 메시지에만 할당됩니다. `info`, `notice` 및 `debug` 수준 메시지가 제외됩니다.

## 그룹 01 - 데이터 수집 단계

일반적으로 데이터 공급자 내에서 소스 엔티티에서 데이터를 수집하는 동안 발생하는 오류 또는 경고와 관련된 코드를 기록합니다.
- 영향을 받는 엔티티는 부분 데이터로 처리되거나 오류가 발생하면 완전히 건너뛸 수 있습니다. 자세한 내용은 로그 메시지를 참조하십시오.
- 경고는 서드파티 모듈에서 데이터 내보내기 확장과 잘못 통합되었음을 나타낼 수 있지만 동기화 작업은 일반적으로 계속됩니다.

| 로그 코드 | 레벨 | 메시지 |
|----------|---------|------------------------------------------------------------------------------------------------------------------------------------|
| CDE01-01 | 오류 | `CDE01-01 Failed to add stock info to "ac_inventory" attribute for ids "{ids}". Error: {exception_message}` |
| CDE01-02 | 경고 | `CDE01-02 Field "{field}" is missing in row {row_data}` |
| CDE01-03 | 경고 | `CDE01-03 Invalid field "{field}" requested from inventory config {config_data}` |
| CDE01-04 | 오류 | `CDE01-04 Was not able to add data to "ac_attribute_set" attribute for ids "{ids}". Error: {exception_message}` |
| CDE01-05 | 오류 | `CDE01-05 Unable to sync feed "{feed}" for ids "{ids}". Affected data provider: "{provider}". Error: {exception_message}` |
| CDE01-06 | 오류 | `CDE01-06 Unable to sync feed "{feed}" for ids "{ids}". Error: {exception_message}` |
| CDE01-07 | 오류 | `CDE01-07 Source entity id is null. Item sync was skip for feed "{feed}". field: "{field}", item: {item}` |
| CDE01-08 | 오류 | `CDE01-08 Cannot collect "inStock" for products "{product_ids}": no sales channel data for stores "{store_view_codes}"` |
| CDE01-09 | 오류 | `CDE01-09 Cannot get status attribute. Product variants ignore stock status. Error: {exception_message}` |
| CDE01-10 | 오류 | `CDE01-10 Unable to retrieve gift card product options for products "{values}". Error: {exception_message}` |
| CDE01-11 | 오류 | `CDE01-11 Unable to retrieve gift card shopper input options for products "{values}". Error: {exception_message}` |
| CDE01-12 | 경고 | `CDE01-12 Catalog Permissions: Global Configuration path was not found for path {path}. {config_dump}` |
| CDE01-13 | 오류 | `CDE01-13 Catalog Permissions: wrong state in global config. item: {item}, config: {config}` |
| CDE01-14 | 오류 | `CDE01-14 Failed to assign UUIDs for type: {type}, ids: {ids}` |
| CDE01-15 | 오류 | `CDE01-15 Failed to assign UUIDs for type: {type}, ids: {ids}. duplicates: {duplicates}` |
| CDE01-16 | 오류 | `CDE01-16 "{feed_name}" feed sync error: cannot build identifier for "{field}". Item skipped: {item}` |
| CDE01-17 | 경고 | `CDE01-17 Failed to create attribute "{attribute_code}". Will be retried on next sync. Error: {message}` |
| CDE01-18 | 경고 | `CDE01-18 Error on getting datetime for catalog price rule fetch. Using system time. website: "{website_id}", store: "{store_id}"` |
| CDE01-19 | 경고 | `CDE01-19 GiftCard {sku} does not have shopper input options` |
| CDE01-20 | 경고 | `CDE01-20 GiftCard {sku} doesn't have valid options: {options}` |
| CDE01-21 | 오류 | `CDE01-21 Unable to resolve url_path for category {id} with path "{path}", url_key "{urk_key}", store "{store}"` |
| CDE01-22 | 오류 | `CDE01-22 Unable to resolve url_path for category{id} with path "{path}" for store view "{store}"` |

## 그룹 02 - SaaS 단계로 데이터 전송

피드 데이터를 SaaS 엔드포인트에 전송하는 동안 발생하는 오류 또는 경고와 관련된 코드를 기록합니다.
- 오류는 일반적으로 HTTP 요청, 응답 처리 또는 데이터 유효성 검사 중 데이터가 허용되지 않는 오류를 나타냅니다.
- 경고는 일반적으로 요청이 자동으로 재시도되는 일시적인 조건(예: 속도 제한 또는 서버 오류)을 나타냅니다.

| 로그 코드 | 레벨 | 메시지 |
|-----------|---------|---------|
| CDE02-01 | 오류 | `CDE02-01 Application error on sending data to SaaS for feed "{feed_name}". Error: {error_message}` |
| CDE02-02 | 오류 | `CDE02-02 Unexpected error on sending data to SaaS for feed "{feed_name}". Error: {error_message}` |
| CDE02-03 | 경고 | `CDE02-03 Cannot parse the API response because the request was not successful.` |
| CDE02-04 | 오류 | `CDE02-04 Cannot obtain feed metadata for feed name "{feed_name}". Sync terminated. Error: {error_message}` |
| CDE02-05 | 오류 | `CDE02-05 Failed to submit feed batch for feed {feed_name}. Error: {error_message}` |
| CDE02-06 | 오류 | `CDE02-06 Failed to retry feed items submission for feed {feed_name}. Error: {error_message}` |
| CDE02-07 | 경고 | `CDE02-07 Feed "{feed_name}" sync error: too many requests (HTTP 429). Request will be retried.` |
| CDE02-08 | 경고 | `CDE02-08 Feed "{feed_name}" sync error: Server error (HTTP {http_status_code}). Request will be retried.` |
| CDE02-09 | 오류 | `CDE02-09 Feed "{feed_name}" sync error: data validation failed. Check logs. Request will not be retried.` |
| CDE02-10 | 경고 | `CDE02-10 Feed "{feed_name}" sync error: Client error (HTTP {http_status_code}). Request will be retried.` |
| CDE02-11 | 경고 | `CDE02-11 Feed "{feed_name}" sync error: application-level error. Request will be retried.` |
| CDE02-12 | 오류 | `CDE02-12 Feed "{feed_name}" sync error API request was not successful (status code: {status_code}).` |
| CDE02-13 | 경고 | `CDE02-13 The zlib-ext is not loaded. Request body can't be compressed and will proceed with regular json` |

## 그룹 03 - 엔티티 업데이트 시 동기화 예약

엔티티 변경에 대한 응답으로 동기화를 예약하거나 트리거할 때 발생하는 오류 또는 경고와 관련된 로그 코드.
- 오류로 인해 증분 동기화를 예약하지 못할 수 있으며 복구하려면 전체 또는 부분 재동기화가 필요한 경우가 많습니다.
- 경고는 지원되지 않는 입력, 누락된 식별자 또는 구성 문제로 인해 동기화 작업을 건너뛰거나 지연했음을 나타냅니다.

| 로그 코드 | 레벨 | 메시지 |
|----------|----------|----------------------------------------------------------------------------------------------------------------------------------|
| CDE03-01 | 오류 | `CDE03-01 Cannot schedule resync for feeds` |
| CDE03-02 | 경고 | `CDE03-02 Skipping product feed update scheduling. Category path "{category_path}" is wrongly formatted` |
| CDE03-03 | 오류 | `CDE03-03 Categories sync error on category "{category_id}" save. Run resync. Error: {error_message}` |
| CDE03-04 | 오류 | `CDE03-04 Product sync scheduling error on url key change ({old_url_key} -> {new_url_key}). Run resync. Error: {error_message}` |
| CDE03-05 | 오류 | `CDE03-05 Product sync scheduling error on category path change ({old_path} -> {new_path}). Run resync. Error: {error_message}` |
| CDE03-06 | 오류 | `CDE03-06 Product sync scheduling error on attribute "{attribute_code}" deletion. Run full resync. Error: {error_message}` |
| CDE03-07 | 경고 | `CDE03-07 Product sync scheduling error on inventory source save for SKUs: {product_skus}. Error: {error_message}` |
| CDE03-08 | 오류 | `CDE03-08 Product variants sync scheduling error on product "{sku_or_id}" save. Run resync. Error: {error_message}` |
| CDE03-09 | 경고 | `CDE03-09 The '{feed_name}' feed does not support partial resync by IDs, or an unsupported identifier type was specified.` |
| CDE03-10 | 경고 | `CDE03-10 There are no {id_field}s found to reindex for provided identifiers list: {identifiers}` |
| CDE03-11 | 오류 | `CDE03-11 Categories Permissions feed sync scheduling error on category "{category_id_and_name}" delete. Error: {error_message}` |
| CDE03-12 | 경고 | `CDE03-12 Product Overrides sync failed. Marked indexer as invalid. Error: {error_message}` |
| CDE03-13 | 오류 | `CDE03-13 Cannot invalidate indexers "{indexer_ids}" for event "{event_name}". Error: {error_message}` |
| CDE03-14 | 오류 | `CDE03-14 Failed to read config values. Indexer invalidation skipped. Error: {error_message}` |
| CDE03-15 | 오류 | `CDE03-15 Categories Permissions feed sync scheduling error on config save: {error_message}` |
| CDE03-16 | 오류 | `CDE03-16 Failed to reindex category permissions global configuration after full reindex: {error_message}` |
| CDE03-17 | 중요 | `CDE03-17 Failed to recreate product override view subscriptions on customer group save: {error_message}` |
| CDE03-18 | 중요 | `CDE03-18 Failed to recreate product override view subscriptions on customer group delete: {error_message}` |
| CDE03-19 | 오류 | `CDE03-19 Failed to remove product override view subscriptions during table maintenance: {error_message}` |
| CDE03-20 | 오류 | `CDE03-20 Failed to recreate product override view subscriptions after table maintenance: {error_message}` |
| CDE03-21 | 오류 | `CDE03-21 Product sync scheduling error on attribute {%s} option change. Run resync. Error: %s` |
| CDE03-22 | 경고 | `CDE03-22 StagedCategoryUrlKeyChangeDetector: no active row at version {version_id} for entity_id(s) [{entity_ids}]; skipping.` |
| CDE03-23 | 오류 | `CDE03-23 StagedCategoryUrlKeyChangeDetector: catalog_category url_key attribute not found; failing open.` |
| CDE03-24 | 오류 | `CDE03-24 InvalidateProductFeedOnCategoryUrlKeyChange: scheduler failed for path "{path}": {error_message}` |
| CDE03-25 | 오류 | `CDE03-25 InvalidateProductFeedOnCategoryUrlKeyChange: gate query failed: {error_message}` |
| CDE03-26 | 오류 | `CDE03-26 InvalidateProductFeedOnCategoryUrlKeyChange: unable to expand staged url_key category reindex scope: {error_message}` |
| CDE03-27 | 오류 | `CDE03-27 Failed to invalidate indexers after config "{config_section}" change. Error: {error_message}` |
| CDE03-28 | 경고 | `CDE03-28 StagedCategoryUrlKeyChangeDetector: catalog category staging schema is not present; skipping staged url_key change detection.` |

## 그룹 04 - 인덱스 또는 구성과 관련된 일반 오류

색인 지정 프로세스 중 또는 잘못된 구성으로 인한 오류와 관련된 로그 코드.

| 로그 코드 | 레벨 | 메시지 |
|-----------|---------|---------|
| CDE04-02 | 오류 | `CDE04-02 Cannot set indexer to Update On Schedule mode for indexer {indexer_id}. Error: {message}` |
| CDE04-03 | 경고 | `CDE04-03 Partial sync failed for changelog "{changelog_name}". Should be retried. Error: {message}` |
| CDE04-04 | 오류 | `CDE04-04 Feed metadata does not contain indexer name. Check di.xml config` |
| CDE04-05 | 오류 | `CDE04-05 Cannot load feed indexer for feed` |
| CDE04-06 | 오류 | `CDE04-06 Failed to reset MView triggers for "{affected_views}" on index table switch. Run reindex. Error: {message}` |
| CDE04-07 | 오류 | `CDE04-07 Error on partial resync for feed "{feed_name}". Error: {message}` |
| CDE04-08 | 오류 | `CDE04-08 Error retrying failed items sync for feed "{feed_name}". Error: {message}` |
| CDE04-09 | 오류 | `CDE04-09 Error on full resync for feed "{feed_name}". Error: {message}` |
| CDE04-10 | 오류 | `CDE04-10 Error during full sync. Message: "{message}". The following IDs were skipped: [{ids}]` |
| CDE04-11 | 경고 | `CDE04-11 Feed "{feed_name}" sync failed. Resync will be run on next cron run. Error: {message}` |
| CDE04-12 | 경고 | `CDE04-12 Partial sync failed for feed "{feed_name}". Retry has been scheduled. Error: {message}` |
| CDE04-13 | 오류 | `CDE04-13 Sync completed, but failed to persist status to feed table for "{feed_name}" feed. Error: {message}` |
| CDE04-14 | 오류 | `CDE04-14 Cannot delete feed items for feed "{feed_name}" for ids: "{ids}". Error: {message}` |
| CDE04-15 | 경고 | `CDE04-15 Failed to serialize metadata after sync. Error: {message}` |
| CDE04-16 | 경고 | `CDE04-16 Batch table insert query "{query}" returned unexpected result. Expected: {expected_class}, Actual: {actual_type}` |
| CDE04-17 | 경고 | `CDE04-17 Failed to check indexer type when setting schedule mode: {message}` |
| CDE04-18 | 경고 | `CDE04-18 Fixture generator: failed to filter indexer changelog tables from fixture SQL: {message}` |
| CDE04-19 | 경고 | `CDE04-19 The identifier for a feed item is empty. Sync is skipped for the entity.` |
| CDE04-20 | 경고 | `CDE04-20 Unexpected call: feed "{feed_name}" is not locked, trace: {stack_trace}` |
| CDE04-21 | 오류 | `CDE04-21 Failed to clean up deleted feed items for feed "{feed_name}". Error: {error_message}` |
