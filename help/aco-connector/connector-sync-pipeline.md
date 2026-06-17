---
title: 카탈로그 동기화 파이프라인
description: 피드 변환, cron 일정, 범위 제어 및 오류 처리를 포함하여  [!DNL Adobe Commerce Optimizer Connector] 동기화 파이프라인이 작동하는 방식에 대해 알아봅니다.
feature: Integration, Configuration
badgePaas: label="PaaS만" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce 온 클라우드 프로젝트(Adobe 관리 PaaS 인프라) 및 온프레미스 프로젝트에만 적용됩니다."
autotag-review: '2026-06-09T16:21:52.214Z'
TQID: 'https://experienceleague.adobe.com/EXUQzAd0I6Hnq4twzhaBZZnv0jLjeGBuTx-QgQz-5MA'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2:
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: cc250cf1-34eb-4863-80d0-d170d45ea067
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: addc3a3a-2b1c-4fdf-aea4-4b1eb2931ba6
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 662
ht-degree: 1%

---

# 커넥터 동기화 파이프라인

[[!DNL SaaS Data Export]](https://experienceleague.adobe.com/en/docs/commerce/saas-data-export/overview)을(를) 기반으로 빌드된 **[!DNL Adobe Commerce Optimizer Connector]**&#x200B;은(는) [!DNL SaaS Data Export] 인덱서가 수집한 데이터를 [!DNL Adobe Commerce Optimizer] [!DNL Catalog Data Ingestion API]에 필요한 형식으로 매핑하고 인증, 일괄 처리된 제출 및 범위 기반 동기화 제어를 처리합니다. 아래 섹션에서는 이러한 동기화가 작동하는 방식을 설명합니다.

관련 컨텍스트:

- [[!DNL Commerce Optimizer Connector] 개요](overview.md) 항목에서 통합의 비즈니스 가치, 주요 기능 및 아키텍처에 대해 알아봅니다.

- 모듈 패키지 이름, 피드 API 끝점 및 구성 키 경로에 대해서는 [커넥터 참조](reference/connector-reference.md)를 참조하십시오.

## 동기화 작동 방식

다음 다이어그램은 [!DNL Adobe I/O Gateway]을(를) 통해 [!DNL Adobe Commerce]에서 [!DNL Commerce Optimizer]로의 데이터 동기화를 보여 줍니다.

![Commerce Optimizer 커넥터 높은 수준의 동기화 다이어그램](assets/aco-connector-sync-high-level-diagram.png){width="800" zoomable="yes"}

[!DNL Adobe Commerce]에서 카탈로그 데이터가 변경되면 이러한 단계를 통해 동기화가 이동합니다.

1. **엔티티 변경 감지** —(1분마다) cron 작업(`indexer_reindex_all_invalid`)이 [!DNL Adobe Commerce]개의 엔티티 변경을 감지하고 피드 항목을 결합하는 [!DNL SaaS Data Export]을(를) 트리거합니다.
1. **변환** — [!DNL Commerce Optimizer Connector]은(는) 어셈블된 피드를 선택하고 [!DNL Adobe Commerce] 엔터티 및 범위를 [!DNL Commerce Optimizer] API에 필요한 형식에 매핑하며 전송할 페이로드를 준비합니다.
1. **전송** — 변환된 데이터는 HTTP POST(`/v1/catalog/<feed name>`)를 통해 [!DNL Adobe I/O Gateway]을(를) 통해 [!DNL Commerce Optimizer]&#x200B;(으)로 전송되며, 받는 피드의 유효성을 검사하고 지속됩니다.
1. **결과 유지** — [피드 테이블](reference/connector-reference.md#supported-feeds)에 API 응답 상태를 유지합니다.
1. **실패 다시 시도**(5분마다) — 별도의 cron 작업(`*_resend_failed_items`)이 실패한 피드 항목을 감지하여 동일한 파이프라인을 통해 다시 제출합니다.

### 예약된 cron 작업

다음 cron 작업은 고정된 일정에 따라 파이프라인을 자동화합니다.

| 크론 군 | 크론 작업 | 목적 | 일정 |
|-------------------------------------|-------------------------------|------------------------------------------------------------------------------|----------------|
| `index` | `indexer_update_all_views` | 엔티티 업데이트를 수신하고 피드 항목을 어셈블하며 피드 상태를 유지합니다. | 1분마다 |
| `index` | `indexer_reindex_all_invalid` | &quot;색인 재지정 필요&quot;로 표시된 피드 색인에 대해 전체 재동기화 수행 | 1분마다 |
| `resync_failed_feeds_data_exporter` | `*_resend_failed_items` | 실패한 피드 항목을 확인하고 [!DNL Commerce Optimizer]에 다시 제출합니다. | 5분마다 |
| `commerce_data_export` | `cleanup_deleted_feed_items` | 보존 기간(7일)이 지난 동기화된 삭제된 피드 항목을 정리합니다 | 매일 오전 2:00시 |

**[!DNL SaaS Data Export]** 확장은 피드 컬렉션 및 상태 추적을 처리합니다. 커넥터 레이어는 엔터티 및 범위를 [!DNL Commerce Optimizer] API에 필요한 형식에 매핑하고 `POST /v1/catalog/<feed name>`을(를) 통해 제출합니다.

#### 요구 사항

- [Commerce cron이 실행 중이어야 합니다](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-readiness-check-issues){target="_blank"}.
- 피드 인덱서는 **[!UICONTROL Update by Schedule]** 모드를 사용해야 합니다. [부분 동기화](../data-export/sync-overview.md#partial-sync){target="_blank"}를 참조하십시오.

## 범위 기반 동기화 제어

`CommerceOptimizerScopeMapper` 모듈은 웹 사이트 및 스토어 보기 내보내기 설정을 읽고 피드 수집 및 제출 중에 이를 적용합니다.

- **사용 가능한 범위** 정상적인 델타 일정에서 데이터를 내보냅니다.
- **비활성화된 범위**&#x200B;이(가) 파이프라인에서 제외됩니다.
이전에 동기화된 엔터티는 다음 cron 실행 시 [!DNL Commerce Optimizer]에서 제거됩니다.

동기화 문제가 하나의 카탈로그 원본 또는 가격책에만 영향을 주는 경우 [데이터가 동기화되지 않음](troubleshooting.md#data-not-syncing)을 참조하세요.

동기화 범위 사용자 지정에 대한 자세한 내용은 [Commerce 범위 내보내기 구성 사용자 지정](get-started.md#customize-the-commerce-scopes-export-configuration)을 참조하십시오.

## 타이밍 및 모니터링

| 시나리오 | 일반적인 시간 |
| -------- | -------------- |
| 정기 카탈로그 업데이트 | 델타 동기화 주기 1~2회(색인화 시~1~2분, 제출) |
| 일시적 실패 | 5분마다 재시도됨 |
| 전체 동기화 또는 큰 카탈로그 | 분 ~ 시간 |

Commerce 관리자의 [[!UICONTROL Data Feed Sync Status]](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status) 페이지에서 피드당 상태를 모니터링합니다. [데이터 동기화가 작동하는지 확인](./data-sync-manage.md#verify-that-the-data-sync-is-working)을 참조하십시오.

## 피드 제출 및 오류 처리

`FeedSubmitter` 프로세스가 [!DNL Catalog Data Ingestion API] 호출을 처리합니다.

1. 업데이트 항목을 삭제 항목(다양한 API 엔드포인트)과 구분합니다.
1. 는 끝점을 독립적으로 업데이트하고 삭제합니다.
1. 항목별 상태 결과를 단일 응답으로 다시 병합합니다.

### HTTP 상태 코드 병합

업데이트 및 삭제 호출이 서로 다른 상태 코드를 반환하는 경우 `FeedSubmitter`은(는) 다음과 같이 결과를 결합합니다.

| 업데이트 결과 | 결과 삭제 | 최종 결과 |
| --------------- | --------------- | ------------- |
| 200 | 200개 또는 없음 | 200 성공 |
| 200 | 400 | 삭제 오류가 있는 200 |
| 400 | 400 | 병합된 오류 400개 |
| 기타 | 기타 | 재시도 가능해 |

| 오류 유형 | 비헤이비어 |
| ---------- | -------- |
| **400** | 응답 `errors` 필드에 나열된 항목은 관리자에 표시되며 주의가 필요합니다. 배치의 다른 항목을 재시도합니다. |
| **5xx** | `resync_failed_feeds_data_exporter` 그룹의 피드별 `*_feed_resend_failed_items` cron 작업에서 재시도되었습니다. |

>[!MORELIKETHIS]
>
> - [커넥터 개요](overview.md) - 비즈니스 컨텍스트 및 범위 매핑에 대해 알아보기
> - [커넥터 참조](reference/connector-reference.md) - 모듈, API 끝점 및 구성 키 검토
> - [Commerce 범위 내보내기 구성 사용자 지정](./get-started.md#customize-the-commerce-scopes-export-configuration) - 범위 수준별 피드 구성, 동작 활성화 및 비활성화, 관리 단계
> - [문제 해결](troubleshooting.md) — 동기화 오류 진단
