---
title: SaaS 데이터 내보내기 모듈
description: ' [!DNL SaaS Data Export] 에 포함된 Magento 모듈 패키지와 데이터 수집, 변환 및 Adobe SaaS 서비스 제출에 대한 역할에 대해 알아봅니다.'
autotag-review: '2026-06-17T15:08:59.000Z'
role: Developer
feature: Services
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: cc250cf1-34eb-4863-80d0-d170d45ea067
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 111
ht-degree: 0%

---


# SaaS 데이터 내보내기 모듈

[!DNL SaaS Data Export]은(는) 데이터 수집 및 인덱싱을 위한 첫 번째 모듈 그룹과 HTTP 전송 및 제출을 위한 두 번째 모듈 그룹으로 구성됩니다.

이러한 모듈은 엔티티 변경 감지, 피드 색인화, 데이터 추출 및 스키마 정의를 처리합니다.
다음 표에서는 프레임워크 수준 모듈만 제공합니다. 사용 가능한 모듈의 전체 목록은 설치된 패키지에 따라 다릅니다.

| 모듈 | 목적 | 주요 클래스 |
| --- | --- |--- |
| `DataExporter` | 코어 프레임워크: 인덱서, 피드 테이블, 해시, 다시 시도, 잠금 | `FeedIndexer`, `FeedIndexMetadata`, `FeedMetadataPool`, `FeedLockManager` |
| `QueryXml` | 데이터 수집을 위한 XML 기반 쿼리 DSL | `QueryFactory`, `QueryProcessor`, `SelectBuilder` |
| `SaaSCommon` | 공유 HTTP 전송, 다시 시도, CLI(`saas:resync`), 오케스트레이션 재동기화 | `ExportFeed`, `SubmitFeed`, `ResyncManager`, `ResyncManagerPool`, `ProgressBarManager` |

동기화 중에 이러한 모듈을 함께 사용하는 방법에 대해 알아보려면 [SaaS 데이터 내보내기 파이프라인](../sync-overview.md)을 참조하세요.

>[!MORELIKETHIS]
>
>- [동기화 작동 방식](../sync-overview.md)
>- [피드 테이블 스키마](feed-table-reference.md)
>- [SaaS 데이터 내보내기 확장 관리](../manage-extension.md)
