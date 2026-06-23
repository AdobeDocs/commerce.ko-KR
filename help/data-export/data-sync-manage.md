---
title: 동기화 프로세스 보기 및 관리
description: 데이터 관리 대시보드 및 데이터 피드 동기화 상태 페이지를 사용하여  [!DNL SaaS Data Export] 동기화 프로세스를 보고 관리하는 방법을 알아봅니다.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 98d604a71c2062a44070b207fc43b9d9b1c434fd
workflow-type: tm+mt
source-wordcount: 557
ht-degree: 0%

---

# 동기화 프로세스 보기 및 관리

대부분의 동기화 활동은 전체 동기화, 부분 동기화 또는 실패한 항목 동기화를 다시 시도하여 자동으로 처리됩니다. 각 유형이 실행되는 시기에 대한 자세한 내용은 [동기화 유형](sync-overview.md#synchronization-types)을 참조하십시오. [!DNL SaaS Data Export]은(는) 프로세스를 모니터링, 관리 및 문제를 해결하는 도구도 제공합니다. 배포용 대시보드를 사용하여 동기화 상태를 보고 데이터 동기화 프로세스를 관리할 수 있습니다.

>[!BEGINTABS]

>[!TAB Adobe Commerce]

Adobe Commerce on cloud, 온-프레미스 또는 Adobe Commerce as a Cloud Service 배포의 경우 다음 Commerce 관리 리소스에서 동기화 프로세스를 보고 관리합니다.

- **[데이터 피드 동기화 상태 페이지](https://experienceleague.adobe.com/ko/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status)**—[!DNL Live Search], [!DNL Product Recommendations] 또는 [!DNL Catalog Service]에 연결된 배포에 대한 피드 내보내기 상태를 확인하십시오. 이 대시보드는 발생한 오류를 포함하여 각 피드에 대한 피드 내보내기 상태를 표시합니다. 세부 사항 보기에는 개별 피드 항목에 대한 피드 내보내기 상태가 표시됩니다.

- **[데이터 관리 대시보드](https://experienceleague.adobe.com/ko/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard)**—관리자는 연결된 Commerce 서비스에 성공적으로 내보내지고 동기화된 데이터를 보고 추적할 수 있습니다. 이 대시보드에는 Commerce 서비스에 동기화된 제품 데이터가 표시됩니다.

>[!NOTE]
>
>데이터 관리 대시보드 및 데이터 피드 동기화 상태 페이지는 [!DNL Live Search], [!DNL Product Recommendations] 또는 [!DNL Catalog Service]이(가) 설치된 경우에만 사용할 수 있습니다.

>[!TAB Commerce Optimizer이 포함된 Adobe Commerce]

[!DNL Commerce Optimizer]과(와) 통합된 Commerce 온 클라우드 또는 온-프레미스 배포의 경우 다음 리소스를 사용하여 동기화 프로세스를 보고 관리합니다.

- **[데이터 피드 동기화 상태 페이지](https://experienceleague.adobe.com/ko/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status)**—Commerce 관리자의 커넥터 피드 내보내기 상태를 모니터링합니다. 이 페이지에서는 피드별 및 항목별 오류 세부 정보를 포함하여 [!DNL Adobe Commerce]에서 카탈로그 데이터를 내보냈는지 여부를 표시합니다.

- **[데이터 동기화 페이지](../optimizer/setup/data-sync.md)**—데이터 동기화 페이지에서 업스트림 카탈로그 원본에서 [!DNL Commerce Optimizer]&#x200B;(으)로 들어오는 제품 데이터의 동기화 상태에 대한 개요를 제공합니다.

이러한 대시보드를 사용하여 데이터 동기화가 작동하는지 확인하고 수동으로 데이터를 다시 동기화하는 방법에 대한 자세한 내용은 _Adobe Commerce Optimizer Connector 안내서_&#x200B;에서 [동기화 관리](../aco-connector/data-sync-manage.md)를 참조하십시오.

>[!ENDTABS]

## 데이터 동기화가 작동하는지 확인 {#verify-that-the-data-sync-is-working}


{{$include /help/_includes/data-export/verify-commerce-service-data-sync.md}}

## 수동으로 데이터 재동기화

부분 동기화 및 자동 재시도로 동기화 문제가 해결되지 않으면 Commerce 관리에서 또는 Commerce CLI 명령을 사용하여 데이터를 수동으로 재동기화할 수 있습니다. 사용 가능한 옵션은 배포에 따라 다릅니다.

### 사용 가능한 수동 재동기화 옵션 {#manual-resync-options-commerce}

피드 데이터를 수동으로 다시 동기화하려면 다음 옵션을 사용하십시오.

| 작업 | 옵션 | 메모 |
| --- | --- | --- |
| 선택한 피드 항목 재동기화 실패 또는 문제 발생 | **[!UICONTROL Data Feed Sync Status]페이지** | Commerce 관리자에서 선택한 피드 항목을 모니터링하고 다시 동기화합니다. [데이터 동기화가 작동하는지 확인](#verify-that-the-data-sync-is-working)을 참조하십시오. |
| 모든 피드의 전체 재동기화 | **[!UICONTROL Data Management Dashboard]** | Commerce 관리자의 모든 피드를 전체 재동기화합니다. Adobe은 주로 Commerce 서비스에 처음 연결할 때 이 작업을 권장합니다. 마지막 내보내기 이후 콘텐츠 해시가 변경되지 않은 항목은 건너뜁니다. [데이터 동기화가 작동하는지 확인](#verify-that-the-data-sync-is-working)을 참조하십시오. |
| 운영 제어를 사용하여 타겟팅된 피드 재동기화 | **Commerce CLI** | 대상 피드를 다시 동기화하려면 `saas:resync` 명령을 사용하십시오. [Commerce CLI를 사용하여 피드 동기화](data-export-cli-commands.md)를 참조하십시오. |

>[!MORELIKETHIS]
>
> - [동기화 작동 방식](sync-overview.md) - 동기화 모드, 전체 동기화, 부분 동기화 및 실패한 항목 다시 시도에 대해 알아봅니다.
> - [Commerce CLI를 사용하여 피드 동기화](data-export-cli-commands.md) — `saas:resync` 명령을 사용하여 대상 피드를 다시 동기화합니다.
> - [로그 검토 및 문제 해결](troubleshooting/logging.md) - 데이터 내보내기 및 SaaS 내보내기 오류를 진단합니다.
> - [동기화 관리 [!DNL Commerce Optimizer]](../aco-connector/data-sync-manage.md) - 카탈로그 데이터 동기화를 확인하고 커넥터 피드를 수동으로 다시 동기화합니다.
