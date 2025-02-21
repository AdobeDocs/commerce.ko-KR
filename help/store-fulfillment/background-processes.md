---
title: 백그라운드 프로세스 구성
description: 데이터를 이행 서비스와 동기화하는 데 사용되는  [!DNL Store Fulfillment] 백그라운드 프로세스에 대한 일정을 구성합니다.
role: Admin, Developer
level: Intermediate
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---


# 백그라운드 프로세스 구성

Store Fulfillment 통합에서는 최적의 성능과 확장을 위해 백그라운드 프로세스와 메시지 대기열을 사용합니다. [메시지 큐 실행자](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/message-queues/message-queue-framework)를 자동으로 시작하는 [배포 변수](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-deploy#cron_consumers_runner)을(를) 사용하여 Adobe Commerce 스토어에 대한 환경을 빌드합니다.

백그라운드 프로세스는 표준 Adobe Commerce [예약된 작업](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/cron) 기능을 사용하여 관리됩니다. 이러한 프로세스는 주문 및 가맹점 구성 데이터를 매장 이행 웹 서비스와 동기화하는 역할을 합니다.

## 스토어 이행 예약 작업 관리

관리자의 **[!UICONTROL Stores > Configuration > Advanced > System > Cron (Scheduled Tasks) > Cron configuration options for group:store_fulfillment]**(으)로 이동합니다.

스토어 이행 서비스에 대한 기본 구성을 검토하십시오. 주문 처리 볼륨 및 리소스 가용성에 따라 이러한 설정을 사용자 지정할 수 있습니다.
