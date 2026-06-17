---
title: ' [!DNL Adobe Commerce Optimizer Connector] 동기화 관리'
description: ' [!DNL Adobe Commerce] 에서 [!DNL Adobe Commerce Optimizer] 사이의 카탈로그 데이터 동기화를 확인하고 커넥터 피드를 수동으로 다시 동기화하는 방법에 대해 알아봅니다.'
autotag-review: '2026-06-17T15:08:59.000Z'
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
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
subfeature_v2:
  - id: a40ebd6b-b542-4432-a730-1803ef74518d
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 287
ht-degree: 0%

---

# [!DNL Commerce Optimizer]에 대한 동기화 관리

[!DNL Adobe Commerce Optimizer Connector]을(를) 설정한 후에는 대부분의 카탈로그 업데이트가 예약된 cron 작업을 통해 자동으로 동기화됩니다. 자동 동기화 작동 방식에 대한 자세한 내용은 [커넥터 동기화 파이프라인](connector-sync-pipeline.md)을 참조하십시오. 이 항목의 도구를 사용하여 데이터가 [!DNL Adobe Commerce Optimizer]에 도달하는지 확인하고 필요한 경우 피드를 수동으로 다시 동기화하십시오.

## 데이터 동기화가 작동하는지 확인 {#verify-that-the-data-sync-is-working}

{{$include /help/_includes/aco-connector/verify-optimizer-data-sync.md}}

## 수동으로 데이터 재동기화 {#manually-resync-data}

부분 동기화 및 자동 재시도로 동기화 문제가 해결되지 않으면 카탈로그 데이터를 수동으로 재동기화할 수 있습니다. 선택하는 옵션은 문제가 발생하는 위치와 필요한 제어 양에 따라 다릅니다.

| 작업 | 옵션 | 메모 |
| --- | --- | --- |
| 제품이 누락된 경우 동기화 상태를 확인하고 업스트림 시스템에서 다시 동기화 | **업스트림 시스템 재동기화** | [!DNL Commerce Optimizer]에서 **[!UICONTROL Data Sync]**&#x200B;을(를) 선택하고 필요한 카탈로그 원본, 제품, 가격 및 특성이 표시되는지 확인하십시오. 제품이 누락된 경우 **[!UICONTROL Data Feed Sync Status]** 페이지 또는 Commerce CLI를 사용하여 업스트림 [!DNL Adobe Commerce] 인스턴스에서 다시 동기화합니다(다음 행 참조). |
| 선택한 커넥터 피드 항목 재동기화 실패 또는 문제 발생 | Commerce 관리자의 **[!UICONTROL Data Feed Sync Status]페이지** | Commerce 관리자에서 내보내기 상태를 모니터링하고 선택한 커넥터 피드 항목을 다시 동기화합니다. [데이터 동기화가 작동하는지 확인](#verify-that-the-data-sync-is-working)을 참조하십시오. |
| 작동 제어를 사용하여 타깃팅된 커넥터 피드 재동기화 | **Commerce CLI** | 커넥터 피드에 대해 Adobe Commerce 인스턴스에서 `saas:resync`을(를) 실행합니다. [Commerce CLI를 사용하여 피드 동기화](../data-export/data-export-cli-commands.md) 및 [지원되는 피드](reference/connector-reference.md#supported-feeds)를 참조하십시오. |

>[!MORELIKETHIS]
>
> - [커넥터 동기화 파이프라인](connector-sync-pipeline.md) - 동기화, cron 일정 및 오류 처리 작업을 자동화하는 방법에 대해 알아봅니다.
> - [데이터 볼륨 및 동기화 시간 예상](reference/estimate-data-volume-sync-time.md) — 예상 동기화 기간 계산
> - [문제 해결](troubleshooting.md) — 자격 증명, 동기화 및 범위 내보내기 문제 진단
> - [커넥터 모듈 및 피드 끝점](reference/connector-reference.md) - 모듈, API 끝점 및 지원되는 피드를 검토합니다.
