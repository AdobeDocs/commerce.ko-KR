---
title: '[!DNL SaaS Data Export Guide]'
description: Adobe Commerce과 연결된 Adobe Commerce 서비스 간에 데이터를 동기화하는 Commerce SaaS 서비스용  [!DNL data export] 확장 사용에 대해 알아봅니다.
role: Admin, Developer
exl-id: 8a0067ba-90a4-48a6-8276-208d09abe6fc
TQID: https://experienceleague.adobe.com/OHE1GBUEd8hHFPwFlO9fJa3Y0wK2xZ0HOYnwUn0-DSk
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 2a09ef51939649a12b72c45cbb8b0dc0d0a4c8ad
workflow-type: tm+mt
source-wordcount: 571
ht-degree: 0%

---

# [!DNL SaaS Data Export] 안내서

[!DNL SaaS data export]은(는) Adobe Commerce 인스턴스와 연결된 Commerce 서비스 간에 데이터를 동기화합니다. Live Search, 제품 추천, 카탈로그 서비스 또는 [!DNL Adobe Commerce Optimizer Connector]을(를) Adobe Commerce 설치에 추가하면 [!DNL Data export] 확장이 자동으로 설치됩니다.

>[!NOTE]
>
>[!DNL Adobe Commerce Optimizer Connector]을(를) 설치하는 경우 동일한 [!DNL Data Export] 확장은 [!DNL Adobe Commerce]에서 카탈로그 및 가격 피드를 수집합니다. 그런 다음 커넥터가 CCDM(Composable Catalog Data Model)을 사용하여 해당 피드를 매핑하고 [!DNL Adobe Commerce Optimizer]에 제출합니다. 설정 및 아키텍처는 [[!DNL Adobe Commerce Optimizer Connector] 개요](../aco-connector/overview.md)를, 내보내기 후 동기화 동작은 [커넥터 동기화 파이프라인](../aco-connector/connector-sync-pipeline.md)을 참조하십시오.

SaaS 데이터 내보내기는 특정 유형의 정보를 집계하는 _피드_&#x200B;라고 하는 다양한 유형의 데이터를 수집하고 내보냅니다. 설치된 Commerce 서비스에 따라 SaaS 데이터 내보내기 피드는 다음과 같습니다.

- **카탈로그 엔터티 피드** 집계 제품 데이터입니다. 데이터에는 제품, 제품 속성, 제품 가격, 제품 변형, 카테고리, 카테고리 권한 및 제품 권한이 포함됩니다.
- **범위 피드**&#x200B;는 고객 그룹, 웹 사이트, 스토어 및 스토어 보기에 대한 데이터를 집계합니다.
- **판매 주문 피드**&#x200B;는 송장, 배송, 대변 메모 등과 같은 관련 엔터티를 포함하는 주문 데이터를 집계합니다.
- **다중 Source 인벤토리 피드**&#x200B;는 인벤토리 재고 상태 항목에 대한 데이터를 집계합니다.

SaaS 데이터 내보내기는 PHP 확장으로 제공됩니다. 데이터 동기화 프로세스를 시작하고 관리하는 여러 방법을 지원합니다.

- **관리자 또는 명령줄에서 수동 동기화**

   - Commerce 관리자의 [데이터 관리 대시보드](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard)에서는 제품 데이터가 상거래 서비스에 성공적으로 동기화되었음을 보여 주는 동기화 상태를 그래픽으로 볼 수 있습니다. 대시보드를 사용하여 모든 피드의 전체 다시 동기화(_전체 동기화_)를 수행할 수 있습니다. 그러나 Adobe은 Adobe Commerce을 Commerce 서비스에 처음 연결할 때만 전체 동기화를 수행하는 것이 좋습니다. [동기화 프로세스](data-synchronization.md)를 참조하십시오.

     {{aco-data-sync-verification}}

   - [데이터 피드 동기화 상태](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status) 페이지에서는 제품 및 카테고리 데이터를 Commerce에서 제품 추천, 라이브 검색 및 카탈로그 서비스와 같은 외부 서비스나 Adobe Commerce Optimizer으로 전송하는 데이터 내보내기 피드의 상태와 성능에 대한 실시간 통찰력을 제공합니다.

   - [Adobe Commerce 명령줄 도구](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/config-cli)&#x200B;(CLI)는 특정 피드를 동기화하는 명령을 제공하며 피드 처리를 사용자 지정하는 추가 옵션을 포함합니다.

- **cron 작업과 자동 동기화**

   - [부분 데이터 동기화](data-synchronization.md#partial-sync) - Commerce 관리 사용자가 엔터티를 업데이트할 때 Cron 작업이 부분 데이터 동기화를 트리거합니다. 데이터 내보내기 프로세스는 연결된 Commerce 서비스에 이러한 업데이트만 전송합니다. 부분 동기화 프로세스는 MView 메커니즘을 기반으로 하며 관리자 사용자 또는 시스템 통합자의 작업이 필요하지 않습니다.

   - [동기화 오류에 대한 자동 다시 시도](data-synchronization.md#retry-failed-items-sync) - 데이터 동기화 프로세스 중에 오류가 발생하면 Cron 작업이 동기화 프로세스의 자동 다시 시도를 트리거합니다.

- **일정 및 성능 내보내기**

   - 개발자와 시스템 통합자는 Adobe Commerce과 연결된 서비스 간에 데이터를 동기화하기 위해 SaaS 데이터 내보내기에 필요한 시간을 예측할 수 있습니다. 이러한 추정은 사이트 중단을 방지하기 위해 데이터 내보내기 처리를 예약하는 데 도움이 될 수 있습니다. [데이터 볼륨 및 전송 시간 예상](estimate-data-volume-sync-time.md)을 참조하세요.

   - 동기화가 보다 신속하게 수행되어야 하는 경우 SaaS 데이터 내보내기는 내보내기 처리 성능을 개선하기 위한 사용자 지정 옵션을 제공합니다. [데이터 내보내기 성능 개선](customize-export-processing.md)을 참조하세요.

- **데이터 내보내기 작업 추적 및 문제 해결**—데이터 내보내기 및 saas-export 로그를 사용하여 동기화 및 인덱싱 프로세스 중에 동기화 상태와 피드 페이로드를 검토하십시오. [로깅 및 문제 해결](troubleshooting-logging.md)을 참조하십시오.
