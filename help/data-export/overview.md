---
title: '[!DNL SaaS Data Export Guide]'
description: Adobe Commerce과 연결된 Adobe Commerce 서비스 간에 데이터를 동기화하는 Commerce SaaS 서비스용  [!DNL data export] 확장 사용에 대해 알아봅니다.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
exl-id: 8a0067ba-90a4-48a6-8276-208d09abe6fc
TQID: https://experienceleague.adobe.com/OHE1GBUEd8hHFPwFlO9fJa3Y0wK2xZ0HOYnwUn0-DSk
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: b974b164-8a4e-43b8-a9e2-8e67ec131677id: cdf0c6dd-1717-4e20-9530-a24eee57088bid: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2: id: c1256247-af4b-46d8-9dca-0c654ecfa157id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 402
ht-degree: 0%

---

# [!DNL SaaS Data Export] 안내서

[!DNL SaaS data export]은(는) Adobe Commerce 인스턴스와 연결된 Commerce 서비스 간에 데이터를 동기화합니다. Live Search, 제품 추천, 카탈로그 서비스 또는 [!DNL Adobe Commerce Optimizer Connector]을(를) Adobe Commerce 설치에 추가하면 [!DNL Data Export] 확장이 자동으로 설치됩니다.

>[!NOTE]
>
>[!DNL Adobe Commerce Optimizer Connector]을(를) 설치하는 경우 동일한 [!DNL Data Export] 확장은 [!DNL Adobe Commerce]에서 카탈로그 및 가격 피드를 수집합니다. 그런 다음 커넥터가 CCDM(Composable Catalog Data Model)을 사용하여 해당 피드를 매핑하고 [!DNL Adobe Commerce Optimizer]에 제출합니다. 설정 및 아키텍처는 [[!DNL Adobe Commerce Optimizer Connector] 개요](../aco-connector/overview.md)를, 내보내기 후 동기화 동작은 [커넥터 동기화 파이프라인](../aco-connector/connector-sync-pipeline.md)을 참조하십시오.

SaaS 데이터 내보내기는 특정 유형의 정보를 집계하는 _피드_&#x200B;라고 하는 다양한 유형의 데이터를 수집하고 내보냅니다. 설치된 Commerce 서비스에 따라 SaaS 데이터 내보내기 피드는 다음과 같습니다.

- **카탈로그 엔터티 피드** 집계 제품 데이터입니다. 데이터에는 제품, 제품 속성, 제품 가격, 제품 변형, 카테고리, 카테고리 권한 및 제품 권한이 포함됩니다.
- **범위 피드**&#x200B;는 고객 그룹, 웹 사이트, 스토어 및 스토어 보기에 대한 데이터를 집계합니다.
- **판매 주문 피드**&#x200B;는 송장, 배송, 대변 메모 등과 같은 관련 엔터티를 포함하는 주문 데이터를 집계합니다.
- **다중 Source 인벤토리 피드**&#x200B;는 인벤토리 재고 상태 항목에 대한 데이터를 집계합니다.

SaaS 데이터 내보내기는 자동화된 동기화와 수동 동기화를 모두 지원하는 PHP 확장으로 제공됩니다.

- **자동 동기화** - Commerce 서비스에 연결할 때 초기 전체 동기화 후 cron 작업은 부분 동기화 및 실패한 항목의 자동 재시도를 사용하여 연결된 서비스를 최신 상태로 유지하며, 관리 사용자 또는 시스템 통합자의 작업이 필요하지 않습니다.

- **수동 동기화**—Commerce 관리자 또는 [Commerce CLI](data-export-cli-commands.md)에서 선택한 피드를 전체 다시 동기화하거나 다시 동기화합니다.

- **모니터링** - Commerce 관리자의 [!UICONTROL Data Feed Sync Status] 페이지 및 데이터 관리 대시보드에서 피드 상태, 상태 및 게재를 추적합니다. 확인 및 다시 동기화 단계는 [동기화 관리](data-sync-manage.md)를 참조하십시오.

동기화 동작, 모드 및 내보내기 흐름 다이어그램에 대해서는 [동기화 작동 방식](sync-overview.md)을 참조하십시오.

또한 SaaS 데이터 내보내기는 동기화 프로세스를 계획하고 해결하는 도구를 제공합니다.

- **예약 및 성능** - 동기화 시간을 예측하여 처리 일정을 예약하고 사이트 중단을 방지하며, 내보내기 처리를 사용자 지정하여 성능을 개선합니다. [데이터 볼륨 및 전송 시간 예측](estimate-data-volume-sync-time.md) 및 [데이터 내보내기 성능 향상](customize-export-processing.md)을 참조하십시오.

- **추적 및 문제 해결** - 데이터 내보내기 및 saas 내보내기 로그를 사용하여 동기화 상태 및 피드 페이로드를 검토하십시오. [로그 검토 및 문제 해결](troubleshooting/logging.md)을 참조하세요.

>[!MORELIKETHIS]
>
> - [SaaS 데이터 내보내기 피드 확장 및 사용자 지정](extensibility-and-customizations.md) - 피드 데이터를 추가하거나 수정합니다.
> - [시나리오 문제 해결](troubleshooting/troubleshooting-scenarios.md) - 잘못된 구성과 예기치 않은 동기화 결과를 진단합니다.
> - [릴리스 정보](release-notes.md) — 확장 업데이트 및 알려진 문제입니다.
