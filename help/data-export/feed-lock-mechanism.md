---
title: SaaS 데이터 내보내기를 위한 피드 잠금 메커니즘
description: ' [!DNL SaaS Data Export] 피드 잠금을 사용하여 동기화 작업 충돌을 막고 동시 피드 업데이트 중 데이터 무결성을 보호하는 방법을 알아봅니다.'
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
feature: Services
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: b974b164-8a4e-43b8-a9e2-8e67ec131677id: cdf0c6dd-1717-4e20-9530-a24eee57088bid: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 355
ht-degree: 0%

---


# SaaS 데이터 내보내기를 위한 피드 잠금 메커니즘

[!DNL SaaS Data Export] 확장은 여러 프로세스가 동일한 피드를 동시에 동기화하려고 시도할 때 경합 조건을 방지하기 위해 피드 잠금 메커니즘을 사용합니다. 예를 들어 cron에서 트리거된 재동기화가 수동 `saas:resync` CLI 호출과 겹치는 경우 이 문제가 발생할 수 있습니다.

## 피드 잠금 작동 방식

cron 작업 또는 수동 `saas:resync` CLI 호출에 의해 트리거된 각 피드 동기화 작업은 동일한 시퀀스를 따릅니다.

1. 프로세스에서 피드 잠금을 획득하려고 합니다. 잠금 시도는 비차단이며 다른 프로세스가 이미 잠금을 보유하고 있는 경우 즉시 반환됩니다.
1. 잠금이 **사용할 수 없음**&#x200B;인 경우 작업을 건너뛰고 기록됩니다.

   데이터가 손실되지 않습니다. 다음 cron run은 현재 프로세스가 완료된 후 보류 중인 변경 사항을 선택합니다.
1. 잠금이 **획득됨**&#x200B;인 경우 프로세스는 진단 목적으로 이름과 PID를 기록한 다음 동기화를 실행합니다.
1. 동기화가 완료되거나 실패하면 잠금이 무조건 해제되어 다음에 예약된 cron 작업이 정상적으로 진행될 수 있습니다.

cron 또는 CLI로 시작되었는지에 관계없이 한 번에 하나의 동기화 작업만 피드 잠금을 유지할 수 있습니다. 피드 잠금은 [!DNL Adobe Commerce]의 `LockManagerInterface`을(를) 통해 구현됩니다. 기본 백엔드는 `GET_LOCK` 및 `RELEASE_LOCK` 함수를 사용하는 MySQL입니다. 다른 잠금 공급자를 구성하려면 [잠금 공급자 구성](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/lock-provider){target="_blank"}을 참조하십시오.

## 예상 로그 메시지

`commerce-data-export.log`의 다음 메시지는 정상이며 문제를 나타내지 않습니다.

```json
{"feed":"products","operation":"partial sync","status":"operation skipped - process locked by \"full sync(1234)\"", ...}
```

이 메시지는 전체 색인 재지정 또는 `saas:resync`이(가) 이미 진행 중인 동안 크론 트리거된 부분 동기화를 실행하려고 할 때 표시됩니다. 건너뛴 작업은 손실되지 않습니다. 실행 중인 프로세스가 완료되고 잠금이 해제되면 다음 cron 실행에서 보류 중인 모든 변경 사항을 선택하고 동기화합니다.

>[!NOTE]
>
>`commerce-data-export.log`에 기록된 로그 형식 및 작업 유형에 대한 일반 정보는 [로그 검토 및 문제 해결](troubleshooting/logging.md)을 참조하십시오.

>[!MORELIKETHIS]
>
> - [데이터를 SaaS 데이터 내보내기와 동기화](sync-overview.md)
> - [Commerce CLI를 사용하여 피드 동기화](data-export-cli-commands.md)
> - [커넥터 동기화 파이프라인](../aco-connector/connector-sync-pipeline.md)
> - [잠금 공급자 구성](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/lock-provider){target="_blank"}
