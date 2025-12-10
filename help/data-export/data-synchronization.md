---
title: SaaS 데이터 내보내기와 데이터 동기화
description: ' [!DNL SaaS Data Export] 이(가) Adobe Commerce 인스턴스와 연결된 SaaS 서비스 간에 데이터를 수집하고 동기화하는 방법에 대해 알아봅니다.'
role: Admin, Developer
exl-id: 2ca7c92a-fb52-4055-ae16-11e99b38d161
source-git-commit: c6725fc524e9d239ccc0f16701e92ad5d2fc7729
workflow-type: tm+mt
source-wordcount: '880'
ht-degree: 0%

---

# SaaS 데이터 내보내기와 데이터 동기화

카탈로그 서비스, 라이브 검색 또는 제품 권장 사항과 같은 데이터 내보내기가 필요한 Commerce 서비스를 설치하면 데이터 수집 및 동기화 프로세스를 관리하기 위해 Saas 데이터 내보내기 모듈 컬렉션이 설치됩니다.

SaaS 데이터 내보내기는 데이터를 최신 상태로 유지하기 위해 제품 데이터를 Adobe Commerce 인스턴스에서 Commerce 서비스 플랫폼으로 지속적으로 이동합니다. 예를 들어 제품 권장 사항에는 현재 카탈로그 정보가 있어야 정확한 이름, 가격 및 가용성의 권장 사항을 정확하게 반환할 수 있습니다. [데이터 관리 대시보드](https://experienceleague.adobe.com/en/docs/commerce/user-guides/data-services/catalog-sync)를 사용하여 동기화 프로세스를 관찰 및 관리하거나 명령줄 인터페이스를 사용하여 동기화를 트리거하고 Commerce 서비스에서 사용할 제품 데이터를 다시 인덱싱할 수 있습니다.

다음 다이어그램은 SaaS 데이터 내보내기 플로우를 보여 줍니다.

Adobe Commerce에 대한 ![SaaS 데이터 내보내기 컬렉션 및 동기화 흐름](assets/data-export-flow.png){width="900" zoomable="yes"}

SaaS 데이터 내보내기 흐름의 주요 구성 요소는 다음과 같습니다.

- Adobe Commerce에서 피드에 대한 데이터를 수집하고, 피드 항목을 조합하고, 업데이트를 수신하고, 피드 상태를 유지하는 SaaS 데이터 내보내기 모듈입니다.
- 데이터를 내보내고, 라우팅을 구성하고, 연결된 서비스에 피드를 게시하는 SaaS 내보내기 모듈.
- Adobe Commerce 서비스는 수신 피드의 유효성을 검사하고 연결된 서비스에 대한 업데이트를 지속하기 위해 데이터 수집 프로세스를 관리합니다.

>[!NOTE]
>
>Adobe 원활한 예약을 보장하고 사이트 운영의 중단을 방지하려면 데이터 피드 동기화를 시작하기 전에 데이터 볼륨과 동기화 시간을 추정하는 것이 좋습니다. 이러한 예측은 초기 동기화 또는 대량 가격 변경과 같은 대규모 카탈로그 업데이트를 계획할 때 중요합니다. 자세한 내용은 [데이터 동기화에 대한 데이터 볼륨 및 전송 시간 예측](estimate-data-volume-sync-time.md)을 참조하세요.

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

### 부분 동기화

부분 동기화를 통해 SaaS 데이터 내보내기는 제품 이름 변경 또는 가격 업데이트와 같은 Commerce 애플리케이션의 업데이트를 연결된 상거래 서비스로 자동으로 전송합니다.

데이터 내보내기 프로세스에서는 다음 cron 작업을 사용하여 부분 동기화 작업을 자동화합니다.

- &quot;index&quot; cron 그룹 작업:
   - `indexer_reindex_all_invalid` 작업이 잘못된 피드를 모두 다시 인덱싱합니다. 표준 Adobe Commerce 크론 작업입니다.
   - `saas_data_exporter` 작업은 레거시 내보내기 피드에 사용됩니다.
   - `sales_data_exporter` 작업은 판매 데이터 내보내기 피드에 따라 다릅니다.

이러한 작업은 매 분마다 실행됩니다.

부분 동기화가 작동하려면 Commerce 애플리케이션에 다음 구성이 필요합니다.

- [cron 작업을 통해 작업 일정을 사용할 수 있습니다](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/next-steps/configuration.html)

- 모든 SaaS 데이터 내보내기 인덱서가 `Update by Schedule` 모드에서 구성되었습니다.

  SaaS 데이터 내보내기 버전 103.1.0 이상에서는 기본적으로 `Update by Schedule` 모드가 활성화되어 있습니다. Commerce CLI 명령 `bin/magento indexer:show-mode | grep -i feed`을(를) 사용하여 서버에서 인덱스 구성을 확인할 수 있습니다.

### 실패한 항목 동기화 다시 시도

실패한 항목 동기화 다시 시도는 별도의 프로세스를 사용하여 동기화 프로세스 중 오류(예: 애플리케이션 오류, 네트워크 중단 또는 SaaS 서비스 오류)로 인해 동기화에 실패한 항목을 다시 보냅니다. 이 동기화에 대한 구현도 cron 작업을 기반으로 합니다.

- `resync_failed_feeds_data_exporter`개의 cron 그룹 작업:
   - `<feed name>_feed_resend_failed_feeds_items` 작업이 동기화에 실패한 항목을 다시 보냅니다(예: `products_feed_resend_failed_items`).

### 동기화 프로세스 보기 및 관리

대부분의 동기화 활동은 애플리케이션 구성에 따라 자동으로 처리됩니다. 그러나 SaaS 데이터 내보내기는 프로세스를 관리하는 도구도 제공합니다.

- 관리자는 동기화 진행 상황을 보고 추적하고 [데이터 관리 대시보드](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard)에서 데이터에 대한 정보를 가져올 수 있습니다.

- Commerce 애플리케이션 서버에 액세스할 수 있는 개발자, 시스템 통합자 또는 관리자는 Adobe Commerce 명령줄 도구(CLI)를 사용하여 동기화 프로세스 및 데이터 피드를 관리할 수 있습니다. [Commerce CLI를 사용하여 동기화 작업 관리](data-export-cli-commands.md)를 참조하십시오.

### Commerce 애플리케이션 구성 확인

Commerce 인스턴스가 올바르게 구성된 경우에만 부분 동기화 및 실패한 항목 동기화 다시 시도 가 작동합니다. 일반적으로 Commerce 서비스를 설정할 때 구성이 완료됩니다. 데이터 내보내기가 제대로 작동하지 않으면 다음 구성을 확인하십시오.

- [cron 작업이 실행 중인지 확인](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-readiness-check-issues).

- 인덱서가 [Admin](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management)에서 실행되거나 Commerce CLI 명령 `bin/magento indexer:info`을(를) 사용하여 실행되고 있는지 확인하십시오.

- 카탈로그 특성, Product, Product Overrides 및 Product Variant 피드의 인덱서가 `Update by Schedule`(으)로 설정되어 있는지 확인하십시오. 관리자의 [인덱스 관리](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management)에서 또는 CLI(`bin/magento indexer:show-mode | grep -i feed`)를 사용하여 인덱서를 확인할 수 있습니다.

### 데이터 전송 로깅을 위한 이벤트 관리자 알림

버전 103.3.4 이상에서는 Commerce 인스턴스에서 Adobe Commerce 서비스로 데이터를 보낼 때 SaaS 데이터 내보내기가 `data_sent_outside` 이벤트를 전달합니다.

```php
$this->eventManager->dispatch(
   "data_sent_outside",
   [
       "timestamp" => time(),
       "type" => $metadata->getFeedName(),
       "data" => $data
   ]
);
```

>[!NOTE]
>
>이벤트 및 이벤트 구독 방법에 대한 자세한 내용은 Adobe Commerce 개발자 설명서에서 [이벤트 및 관찰자](https://developer.adobe.com/commerce/php/development/components/events-and-observers)를 참조하십시오.
