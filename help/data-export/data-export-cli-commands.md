---
title: Commerce CLI를 사용하여 피드 동기화
description: 명령줄 인터페이스 명령을 사용하여  [!DNL data export extension] for Adobe Commerce SaaS 서비스에 대한 피드 및 프로세스를 관리하는 방법을 알아봅니다.
exl-id: 1ebee09e-e647-4205-b90c-d0f9d2cac963
source-git-commit: 086a571b69e8ad76a912c339895409b0037642b9
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 0%

---

# Commerce CLI를 사용하여 피드 동기화

`magento/saas-export` 패키지의 `saas:resync` 명령을 사용하면 Adobe Commerce SaaS 서비스에 대한 데이터 동기화를 관리할 수 있습니다.

Adobe에서는 `saas:resync` 명령을 정기적으로 사용하지 않는 것이 좋습니다. 명령 사용에 대한 일반적인 시나리오는 다음과 같습니다.

- 초기 동기화
- [SaaS 데이터 공간 ID를 변경한 후 데이터를 새 데이터 공간에 동기화](https://experienceleague.adobe.com/en/docs/commerce-admin/config/services/saas)
- 문제 해결

`var/log/saas-export.log` 파일에서 동기화 작업을 모니터링합니다.

## 초기 동기화

>[!NOTE]
>
>라이브 검색 또는 제품 권장 사항이 활성화되면 초기 동기화가 자동으로 실행됩니다. 수동 명령은 필요하지 않습니다.

명령줄에서 `saas:resync`을(를) 트리거할 때 카탈로그 크기에 따라 데이터를 업데이트하는 데 몇 분에서 몇 시간이 걸릴 수 있습니다.

초기 동기화의 경우 Adobe에서는 다음 순서로 명령을 실행하는 것이 좋습니다.

```shell
bin/magento saas:resync --feed productattributes
bin/magento saas:resync --feed products
bin/magento saas:resync --feed scopesCustomerGroup
bin/magento saas:resync --feed scopesWebsite
bin/magento saas:resync --feed prices
bin/magento saas:resync --feed productoverrides
bin/magento saas:resync --feed variants
bin/magento saas:resync --feed categories
bin/magento saas:resync --feed categoryPermissions
```

## CLI 명령을 사용하여 동기화

`saas:resync` 명령은 다양한 동기화 작업을 지원합니다.

- SKU별 부분 동기화
- 중단된 동기화 다시 시작
- 동기화하지 않고 데이터 유효성 검사

사용 가능한 모든 옵션 보기:

```shell
bin/magento saas:resync --help
```

예가 포함된 옵션 설명은 다음 섹션을 참조하십시오.


>[!NOTE]
>
>내보내기 처리를 관리하는 고급 옵션에 대해서는 [내보내기 처리 사용자 지정](customize-export-processing.md)을 참조하십시오.

## `--by-ids`

특정 엔티티를 해당 ID별로 부분적으로 다시 동기화합니다. `products`, `productAttributes` 및 `productOverrides` 피드를 지원합니다.

기본적으로 엔티티는 제품 SKU로 지정됩니다. 대신 제품 ID를 사용하려면 `--id-type=ProductID`을(를) 사용하십시오.

**예:**

```shell
bin/magento saas:resync --feed='<FEED_NAME>' --by-ids='<SKU-1>,<SKU-2>,<SKU-3>'

bin/magento saas:resync --feed='<FEED_NAME>' --by-ids='<ID-1>,<ID-2>,<ID-3>' --id-type='productId'
```

## `--cleanup-feed`

데이터를 다시 인덱싱하여 SaaS로 보내기 전에 피드 인덱서 테이블을 정리합니다. `products`, `productOverrides` 및 `prices` 피드에서만 지원됩니다.

>[!IMPORTANT]
>
>환경 정리 후에만 사용합니다. Commerce 서비스에서 데이터 동기화 문제를 일으킬 수 있습니다.

**예:**

```shell
bin/magento saas:resync --feed='<FEED_NAME>' --cleanup-feed
```

## `--continue-resync`

중단된 재동기화 작업을 다시 시작합니다. `products`, `productAttributes` 및 `productOverrides` 피드에서만 지원됩니다.

**예:**

```shell
bin/magento saas:resync --feed='<FEED_NAME>' --continue-resync
```

## `--dry-run`

SaaS에 제출하거나 피드 테이블에 저장하지 않고 피드 색인 재지정 프로세스를 실행합니다. 를 사용하여 데이터의 유효성을 검사합니다.

페이로드를 `var/log/saas-export.log`에 저장하려면 `EXPORTER_EXTENDED_LOG=1` 환경 변수를 추가하십시오.

**예:**

```shell
EXPORTER_EXTENDED_LOG=1 bin/magento saas:resync --feed='<FEED_NAME>' --dry-run
```

## `--feed`

필수. 다시 동기화할 피드 엔티티를 지정합니다.

사용 가능한 피드:

- `categories`
- `categoryPermissions`
- `inventoryStockStatus`
- `orders`
- `prices`
- `products`
- `productAttributes`
- `productOverrides`
- `scopesWebsite`
- `scopesCustomerGroup`
- `variants`

**예:**

```shell
bin/magento saas:resync --feed='<FEED_NAME>'
```

## `--no-reindex`

리인덱싱하지 않고 기존 카탈로그 데이터를 [!DNL Commerce Services]에 다시 제출합니다. 제품 관련 피드에 대해서는 지원되지 않습니다.

동작은 [내보내기 모드](data-synchronization.md#synchronization-modes)마다 다릅니다.

- 레거시 모드: 자르지 않고 모든 데이터를 다시 제출합니다.
- 즉시 모드: 옵션은 무시되며 업데이트/실패만 동기화합니다.

**예:**

```shell
bin/magento saas:resync --feed='<FEED_NAME>' --no-reindex
```

## 문제 해결

연결된 Commerce 서비스에 예상 데이터가 표시되지 않으면 데이터 내보내기 오류 로그를 확인하고 환경 변수와 함께 `saas:resync` 명령을 사용하여 페이로드 및 프로파일러 데이터를 검토하여 문제를 해결하십시오. [로그 검토 및 문제 해결](troubleshooting-logging.md)을 참조하세요.
