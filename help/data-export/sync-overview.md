---
title: SaaS 데이터 내보내기와 데이터 동기화
description: ' [!DNL SaaS Data Export] 이(가) Adobe Commerce 인스턴스와 연결된 Commerce 서비스 간에 데이터를 수집하고 동기화하는 방법에 대해 알아봅니다.'
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
exl-id: 2ca7c92a-fb52-4055-ae16-11e99b38d161
TQID: https://experienceleague.adobe.com/wM71qxvduDr77EW6Y8mSNfBXlqkloC-PGOOBOl-mZQM
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: b974b164-8a4e-43b8-a9e2-8e67ec131677id: cdf0c6dd-1717-4e20-9530-a24eee57088bid: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c1579802-ddd4-4214-8a91-97b2066abe11id: d3cdead0-685a-4489-9250-4bb709942f66id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 879
ht-degree: 0%

---

# SaaS 데이터 내보내기와 데이터 동기화

카탈로그 서비스, 라이브 검색 또는 제품 권장 사항과 같은 데이터 내보내기가 필요한 [!DNL Adobe Commerce] 서비스를 설치하면 데이터 수집 및 동기화 프로세스를 관리하기 위해 SaaS 데이터 내보내기 모듈 컬렉션이 설치됩니다.

SaaS 데이터 내보내기는 데이터를 최신 상태로 유지하기 위해 제품 데이터를 Adobe Commerce 인스턴스에서 Commerce 서비스 플랫폼으로 지속적으로 이동합니다. 예를 들어 제품 권장 사항에는 현재 카탈로그 정보가 있어야 정확한 이름, 가격 및 가용성의 권장 사항을 정확하게 반환할 수 있습니다. 동기화 프로세스 모니터링에 대한 자세한 내용은 [동기화 프로세스 보기 및 관리](data-sync-manage.md)를 참조하십시오.

다음 다이어그램은 SaaS 데이터 내보내기 플로우를 보여 줍니다.

Adobe Commerce에 대한 ![SaaS 데이터 내보내기 컬렉션 및 동기화 흐름](assets/data-export-flow.png){width="900" zoomable="yes"}

[!DNL Adobe Commerce]에서 카탈로그 데이터가 변경되면 이러한 단계를 통해 동기화가 이동합니다.

1. **엔티티 변경 감지** - Magento의 Mview 시스템이 구독한 데이터베이스 테이블(예: `catalog_product_entity`)의 행 변경 내용을 감지하고 변경 로그 테이블에 항목을 씁니다.
1. **피드 색인화** - 피드 색인화기가 변경 로그를 읽고 원본 테이블에서 엔터티 데이터를 로드하고 피드 항목을 어셈블합니다.
1. **데이터 수집 및 변환** - 피드 스키마 [`et_schema.xml`](extensibility-and-customizations.md#feed-schema-overview)에 등록된 공급자가 필드 데이터를 수집합니다.
1. **해시 중복 제거** - 콘텐츠 해시는 각 피드 항목에 대해 계산됩니다. 마지막 내보내기 이후 해시가 변경되지 않은 항목은 건너뛰므로 수정된 데이터만 전송됩니다.
1. **HTTP 제출** - 피드 항목이 인증된 HTTP POST 배치로 Adobe SaaS 피드 수집 서비스로 전송됩니다.
1. **상태 지속** - API 응답 상태가 각 항목의 [피드 테이블](reference/feed-table-reference.md)에 다시 기록됩니다.
1. **실패 다시 시도** - 내보내기에 실패한 항목은 예약된 cron 작업에 의해 자동으로 다시 시도됩니다.

>[!NOTE]
>
>[!DNL Adobe Commerce Optimizer Connector] 배포의 경우 [!DNL SaaS Data Export]이(가) 엔터티 변경 검색 및 피드 어셈블리를 처리합니다. 그러면 커넥터가 피드를 [!DNL Catalog Data Ingestion API] 형식으로 매핑하여 [!DNL Adobe Commerce Optimizer]에 제출합니다. 범위 제어, 제출 및 오류 처리에 대해서는 [커넥터 동기화 파이프라인](../aco-connector/connector-sync-pipeline.md)을 참조하십시오.

>[!NOTE]
>
>원활한 예약을 보장하고 사이트 운영의 중단을 방지하려면 데이터 피드 동기화를 시작하기 전에 데이터 볼륨과 동기화 시간을 추정하는 것이 좋습니다. 이러한 예측은 초기 동기화 또는 대량 가격 변경과 같은 대규모 카탈로그 업데이트를 계획할 때 중요합니다. 자세한 내용은 [데이터 동기화에 대한 데이터 볼륨 및 전송 시간 예측](estimate-data-volume-sync-time.md)을 참조하세요.

## 동기화 모드

SaaS 데이터 내보내기에는 엔티티 피드를 처리하는 두 가지 모드가 있습니다.

- **즉시 내보내기 모드**—이 모드에서는 데이터가 수집되어 단일 반복으로 Commerce 서비스로 즉시 전송됩니다. 이 모드는 Commerce 서비스에 대한 엔티티 업데이트 전달 속도를 높이고 피드 테이블의 저장소 크기를 줄입니다.

- **기존 내보내기 모드**—이 모드에서는 데이터가 단일 프로세스로 수집됩니다. 그런 다음 cron 작업은 연결된 상거래 서비스로 수집된 데이터를 전송합니다. 데이터 내보내기 로그 항목에서 레거시 모드를 사용하는 피드의 레이블은 `(legacy)`입니다.

## 동기화 유형

SaaS 데이터 내보내기는 세 가지 동기화 유형(전체 동기화, 부분 동기화 및 실패한 항목 동기화 다시 시도)을 지원합니다.

### 전체 동기화

Adobe Commerce 인스턴스를 Commerce 서비스에 연결한 후 전체 동기화를 수행하여 Adobe Commerce에서 연결된 서비스로 엔티티 피드 데이터를 보냅니다.

>[!NOTE]
>
>전체 동기화는 주로 온보딩 단계에 해당합니다. 데이터베이스 오버로드를 방지하기 위해 정기적으로 사용하지 마십시오. 초기 동기화 후 진행 중인 변경 사항은 부분 동기화를 사용하여 자동으로 동기화됩니다.

### 부분 동기화 {#partial-sync}

부분 동기화를 통해 SaaS 데이터 내보내기는 제품 이름 변경 또는 가격 업데이트와 같은 Commerce 애플리케이션의 업데이트를 연결된 상거래 서비스로 자동으로 전송합니다.
부분 동기화가 작동하려면 Commerce 애플리케이션에 다음 구성이 필요합니다.

- [작업 예약이 cron job을 통해 활성화됨](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/next-steps/configuration.html)
- 모든 SaaS 데이터 내보내기 인덱서가 `Update by Schedule` 모드에서 구성되었습니다.

### 실패한 항목 동기화 다시 시도 {#retry-failed-items-sync}

실패한 항목 동기화 다시 시도는 별도의 프로세스를 사용하여 동기화 프로세스 중 오류(예: 애플리케이션 오류, 네트워크 중단 또는 SaaS 서비스 오류)로 인해 동기화에 실패한 항목을 다시 보냅니다. `resync_failed_feeds_data_exporter` 그룹의 `*_resend_failed_items` cron 작업이 5분마다 자동으로 처리됩니다.

## 예약된 cron 작업

다음 cron 그룹은 고정된 일정에 따라 파이프라인을 자동화합니다.

| 크론 군 | 크론 작업 | 목적 | 일정 |
|---|---|---|---|
| `index` | `indexer_update_all_views` | Mview 변경 로그를 처리하고 부분 피드 업데이트를 트리거합니다. | 1분마다 |
| `index` | `indexer_reindex_all_invalid` | &quot;색인 재지정 필요&quot;로 표시된 피드 색인에 대해 전체 재동기화를 수행합니다. | 1분마다 |
| `resync_failed_feeds_data_exporter` | `*_resend_failed_items` | 실패한 피드 항목을 감지하고 다시 제출합니다. | 5분마다 |
| `commerce_data_export` | `saas_data_exporter` | 레거시 모드 피드(주문, 범위)에 대한 데이터 제출 | 5분마다 |
| `commerce_data_export` | `cleanup_deleted_feed_items` | 보존 기간(7일)이 지난 동기화된 삭제된 피드 항목을 정리합니다 | 매일 오전 2:00시 |

## 피드 제출 및 HTTP 오류 처리 {#feed-submission-and-http-error-handling}

피드 항목은 HTTP POST를 통해 인증된 gzip 압축 JSON 배치로 제출됩니다. 다음 표는 HTTP 응답 코드가 내보내기 상태 및 다시 시도 동작에 매핑되는 방법을 보여 줍니다.

| 상태 코드 | 다시 시도하시겠습니까? | 의미 |
|-------------|--------|---------------------------------------------------------------------------------------------------------------------|
| 200 | 아니요 | 수락됨 |
| 400 | 아니요 | 잘못된 데이터 또는 유효성 검사 실패 - 수동 조사가 필요합니다. 자세한 내용은 `var/log/saas-export-errors.log`을(를) 확인하세요. |
| 429 | 예 | 속도 제한 히트 - [처리 설정 내보내기](customize-export-processing.md)에서 `thread_count` 감소 |
| 5xx | 예 | SaaS측 오류 - 자동 다시 시도 |
| 2 | 예 | 항목이 다시 시도되도록 예약되었습니다. |

HTTP 수준 오류 외에도 로컬 처리 오류나 네트워크 중단과 같은 응용 프로그램 수준 오류도 `*_resend_failed_items` cron 작업에 의해 자동으로 다시 시도되도록 예약됩니다.

Commerce 관리자의 [[!UICONTROL Data Feed Sync Status]](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status) 페이지에서 피드당 상태를 모니터링합니다.

>[!MORELIKETHIS]
>
> - [동기화 관리](data-sync-manage.md) — 동기화 상태를 확인하고 피드를 수동으로 다시 동기화합니다.
> - [피드 테이블 스키마](reference/feed-table-reference.md) — 항목 수준 상태 및 오류 세부 정보를 검사합니다.
> - [데이터 내보내기 성능 향상](customize-export-processing.md) — 일괄 처리 크기 및 스레드 수를 조정합니다.
