---
title: Commerce CLI를 사용하여 피드 동기화
description: Commerce CLI 명령을 사용하여  [!DNL data export extension] 의 Adobe Commerce SaaS 서비스에 대한 피드를 관리하고 프로세스를 동기화하는 방법에 대해 알아봅니다.
autotag-review: '2026-06-17T15:08:59.000Z'
exl-id: 1ebee09e-e647-4205-b90c-d0f9d2cac963
TQID: 'https://experienceleague.adobe.com/Vi8hMKOBjTPkSQp0t8DCkjZsJ8s3Q5GSbSXyX2gmWRo'
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
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: ef1a9efc579d8d21c145e6981235489a2e4ea203
workflow-type: tm+mt
source-wordcount: 728
ht-degree: 0%

---

# Commerce CLI를 사용하여 피드 동기화

`magento/saas-export` 패키지의 `saas:resync` 명령을 사용하면 [!DNL Adobe Commerce] SaaS 서비스에 대한 데이터 동기화를 관리할 수 있습니다.

>[!NOTE]
>
>`saas:resync` 명령은 `products`, `categories` 및 `priceBooks`과(와) 같은 [!DNL Adobe Commerce Optimizer Connector] 피드에도 적용됩니다. 커넥터 피드 및 인덱서 이름의 전체 목록은 [지원되는 피드](../aco-connector/reference/connector-reference.md#supported-feeds)를 참조하십시오.

Adobe에서는 `saas:resync` 명령을 정기적으로 사용하지 않는 것이 좋습니다. 명령 사용에 대한 일반적인 시나리오는 다음과 같습니다.

- 초기 동기화
- [SaaS 데이터 공간 ID를 변경한 후 데이터를 새 데이터 공간에 동기화](https://experienceleague.adobe.com/ko/docs/commerce-admin/config/services/saas)
- 문제 해결

`var/log/saas-export.log` 파일에서 동기화 작업을 모니터링합니다.

## 초기 동기화

>[!NOTE]
>
>라이브 검색 또는 제품 권장 사항이 활성화되면 초기 동기화가 자동으로 실행됩니다. 수동 명령은 필요하지 않습니다.
>
>[!DNL Adobe Commerce Optimizer Connector] 배포의 경우 `aco:config:init` 명령은 모든 커넥터 피드 인덱서를 무효화하여 초기 전체 동기화를 예약합니다. [통합 사용](../aco-connector/get-started.md#enable-the-adobe-commerce-optimizer-integration) 및 [동기화 관리 [!DNL Commerce Optimizer]](../aco-connector/data-sync-manage.md)를 참조하십시오. [!DNL Commerce Optimizer] 

명령줄에서 `saas:resync`을(를) 트리거할 때 카탈로그 크기에 따라 데이터를 업데이트하는 데 몇 분에서 몇 시간이 걸릴 수 있습니다.

피드 동기화는 임의의 순서로 실행할 수 있으며, 피드 동기화 사이에는 엄격한 종속성이 없습니다. 다음 시퀀스는 먼저 범위 데이터로 시작됩니다. 범위 데이터는 다른 피드가 참조하는 저장소 보기를 정의하므로 논리적 시작점입니다.

```shell
bin/magento saas:resync --feed scopesWebsite
bin/magento saas:resync --feed scopesCustomerGroup
bin/magento saas:resync --feed productAttributes
bin/magento saas:resync --feed categories
bin/magento saas:resync --feed products
bin/magento saas:resync --feed prices
bin/magento saas:resync --feed variants
bin/magento saas:resync --feed productoverrides
```

>[!NOTE]
>
>환경에 이 시퀀스의 모든 피드가 포함되지 않을 수 있습니다. 전체 피드 목록, CLI 피드 이름 및 모듈 요구 사항에 대해서는 [지원되는 피드](reference/feed-table-reference.md#supported-feeds)를 참조하십시오.

## 명령 옵션

`saas:resync` 명령은 다양한 동기화 작업을 지원합니다.

- SKU별 부분 동기화
- 중단된 동기화 다시 시작
- 동기화하지 않고 데이터 유효성 검사

모든 명령 옵션 및 플래그 보기:

```shell
bin/magento saas:resync --help
```

예가 포함된 옵션 설명은 다음 섹션을 참조하십시오.

>[!NOTE]
>
>내보내기 처리를 관리하는 고급 옵션에 대해서는 [내보내기 처리 사용자 지정](customize-export-processing.md)을 참조하십시오.

## `--feed`

필수 여부. 다시 동기화할 피드 엔티티를 지정합니다.

`bin/magento saas:resync --help`개의 문서 명령 옵션 및 플래그. 환경에서 사용할 수 있는 모든 피드가 나열되지 않습니다. CLI 피드 이름, 인덱서 ID 및 피드 테이블을 포함한 전체 피드 목록은 [지원되는 피드](reference/feed-table-reference.md#supported-feeds)를 참조하십시오.

>[!NOTE]
>
>설치된 모듈은 재동기화할 수 있는 피드를 결정합니다. 예를 들어 `productOverrides`에는 클라우드, 온-프레미스 또는 Commerce as a Cloud Service에 [!DNL Adobe Commerce]이(가) 필요하며 `orders`에는 판매 주문 모듈이 필요합니다.

>[!NOTE]
>
>`saas:resync` 명령은 새 항목, 업데이트된 항목 및 이전에 내보내지 못한 항목만 전송합니다. 마지막 내보내기 이후 콘텐츠 해시가 변경되지 않은 항목은 건너뜁니다.

**예:**

```shell
bin/magento saas:resync --feed products
```

## `--by-ids`

특정 엔티티를 해당 ID별로 부분적으로 다시 동기화합니다. `products`, `productAttributes`, `productOverrides`, `inventoryStockStatus`, `prices`, `variants` 및 `categoryPermissions` 피드를 지원합니다.

기본적으로 `--by-ids` 옵션을 사용하는 경우 제품 SKU 값을 사용하여 값을 지정합니다. 대신 제품 ID를 사용하려면 `--id-type=productId` 옵션을 추가하십시오.

>[!NOTE]
>
>표준 재동기화와 달리 `--by-ids`은(는) 해시 확인을 무시하고 마지막 내보내기 이후 콘텐츠가 변경되었는지 여부에 관계없이 지정된 엔터티를 연결된 Commerce 서비스에 강제로 제출합니다.

**예:**

```shell
bin/magento saas:resync --feed products --by-ids='ADB102,ADB111,ADB112'

bin/magento saas:resync --feed products --by-ids='1,2,3' --id-type='productId'
```

## `--cleanup-feed`

데이터를 리인덱싱하여 SaaS로 보내기 전에 피드 인덱서 테이블을 정리합니다. `products`, `productAttributes`, `productOverrides`, `inventoryStockStatus`, `prices`, `variants` 및 `categoryPermissions`에 대해서만 지원됩니다.

`--dry-run` 옵션과 함께 사용하는 경우 작업은 모든 항목에 대해 시험 실행 다시 동기화 작업을 수행합니다.

>[!WARNING]
>
>`cleanup-feed` 옵션과 함께 resync 명령을 사용하면 로컬 피드 내보내기 상태가 지워지고 동기화되지 않을 수 있습니다. 예를 들어 [!DNL Adobe Commerce]의 엔티티 삭제는 연결된 Commerce 서비스에 반영되지 않거나 [!DNL Adobe Commerce]에서 삭제되거나 업데이트되었더라도 오래된 엔티티가 원격 Commerce 서비스 인덱스에 남아 있을 수 있습니다. 이 옵션은 SaaS 데이터 공간 정리 후와 같이 전체 환경 재빌드에만 사용합니다.

**예:**

```shell
bin/magento saas:resync --feed products --cleanup-feed
```

## `--continue-resync`

중단된 재동기화 작업을 다시 시작합니다. `products`, `productAttributes` 및 `productOverrides` 피드에서만 지원됩니다.

**예:**

```shell
bin/magento saas:resync --feed productAttributes --continue-resync
```

## `--dry-run`

SaaS에 피드를 제출하지 않고 피드 테이블에 저장하지 않고 피드 색인 재지정 프로세스를 실행합니다. 이 옵션은 데이터 세트와 관련된 문제를 식별하는 데 유용합니다.

페이로드를 `var/log/saas-export.log`에 저장하려면 `EXPORTER_EXTENDED_LOG=1` 환경 변수를 추가하십시오.

**예:**

```shell
EXPORTER_EXTENDED_LOG=1 bin/magento saas:resync --feed products --dry-run
```

### 특정 피드 항목 테스트

확장된 로그 컬렉션과 함께 `--by-ids` 옵션을 추가하여 특정 피드 항목을 테스트하여 `var/log/saas-export.log` 파일에서 생성된 페이로드를 확인합니다.

**예:**

```shell
EXPORTER_EXTENDED_LOG=1 bin/magento saas:resync --feed products --dry-run --by-ids='ADB102,ADB111,ADB112'
```

### 모든 피드 항목 테스트

기본적으로 `resync --dry-run` 작업 중에 제출된 피드에는 새 항목이나 이전에 내보내지 못한 항목만 포함됩니다. 처리할 피드에 모든 항목을 포함하려면 `--cleanup-feed` 옵션을 사용하십시오.

**예:**

```shell
bin/magento saas:resync --feed products --dry-run --cleanup-feed
```

## `--no-reindex`

리인덱싱하지 않고 기존 카탈로그 데이터를 [!DNL Commerce Services]에 다시 제출합니다. 제품 관련 피드에 대해서는 지원되지 않습니다.

동작은 [내보내기 모드](sync-overview.md#synchronization-modes)마다 다릅니다.

- 레거시 모드: 자르지 않고 모든 데이터를 다시 제출합니다.
- 즉시 모드: 옵션은 무시되며 업데이트/실패만 동기화합니다.

**예:**

```shell
bin/magento saas:resync --feed productAttributes --no-reindex
```

>[!MORELIKETHIS]
>
> - [로그 검토 및 문제 해결](troubleshooting/logging.md) - 데이터 내보내기 및 SaaS 내보내기 오류를 진단합니다.
> - [시나리오 문제 해결](troubleshooting/troubleshooting-scenarios.md) - 잘못된 구성과 예기치 않은 동기화 결과를 해결합니다.
> - [동기화 작동 방식](sync-overview.md) - 동기화 모드 및 다시 시도 동작에 대해 알아봅니다.
