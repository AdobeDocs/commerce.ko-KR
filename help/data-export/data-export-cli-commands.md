---
title: SaaS 데이터 내보내기 명령줄 인터페이스
description: 명령줄 인터페이스 명령을 사용하여  [!DNL data export extension] for Adobe Commerce SaaS 서비스에 대한 피드 및 프로세스를 관리하는 방법을 알아봅니다.
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 0%

---

# SaaS 데이터 내보내기 명령줄 인터페이스 참조

개발자와 시스템 관리자는 [Adobe Commerce 명령줄 도구](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/config-cli)&#x200B;(CLI)를 사용하여 SaaS 데이터 내보내기를 위한 동기화 작업을 관리할 수 있습니다. `saas:resync` 명령이 `magento/saas-export` 패키지에 포함되어 있습니다.

Adobe에서는 `saas:resync` 명령을 정기적으로 사용하지 않는 것이 좋습니다. 명령 사용에 대한 일반적인 시나리오는 다음과 같습니다.

- 초기 동기화
- [SaaS 데이터 공간 ID](https://experienceleague.adobe.com/en/docs/commerce-admin/config/services/saas)이(가) 변경되었으며 데이터를 새 데이터 공간과 동기화해야 합니다.
- 문제 해결

## 초기 동기화

>[!NOTE]
>라이브 검색 또는 제품 추천을 사용하는 경우 초기 동기화를 실행할 필요가 없습니다. 이 프로세스는 서비스를 Commerce 인스턴스에 연결한 후 자동으로 시작됩니다.

명령줄에서 `saas:resync`을(를) 트리거할 때 카탈로그 크기에 따라 데이터를 업데이트하는 데 몇 분에서 몇 시간이 걸릴 수 있습니다.

초기 동기화의 경우 Adobe에서는 다음 순서로 명령을 실행하는 것이 좋습니다.

```bash
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

## 명령 예

`saas:resync` 명령을 사용하기 전에 [옵션 설명](#command-options)을 검토하십시오.

- 엔티티 피드에 대해 전체 재동기화를 수행합니다.

  ```
  bin/magento saas:resync --feed='<FEED_NAME>' 1
  ```

  이미 내보내기에 성공한 피드는 다시 동기화되지 않습니다.

- 지정된 피드 및 정리 데이터를 완전히 다시 동기화합니다.

  ```
  bin/magento saas:resync --feed='FEED_NAME' --cleanup-feed
  ```

  [!DNL Data Space ID Cleanup] 작업을 수행한 후에만 사용합니다.

- 즉시 피드를 내보내려면 피드 테이블에서 인덱스 데이터를 자르지 않고 연결된 Commerce 서비스에 모든 데이터를 다시 전송하십시오

  ```
   bin/magento saas:resync --feed='FEED_NAME' --no-reindex
  ```

- 사용 가능한 명령 및 옵션을 설명과 함께 나열합니다.

  ```
  bin/magento saas:resync --help
  ```

## 명령 옵션

`saas:resync` 작업을 관리하는 데 다음 옵션을 사용할 수 있습니다.

>[!NOTE]
>
>`saas:resync` 명령은 또한 일괄 처리 크기를 늘리고 다중 스레드 처리를 추가하여 데이터 내보내기 명령을 개선하는 고급 옵션을 지원합니다. [내보내기 처리 사용자 지정](customize-export-processing.md)을 참조하세요.

### `feed`

이 필수 옵션은 `products`과(와) 같이 다시 동기화할 피드 엔터티를 지정합니다.

`feed` 옵션 값에는 사용 가능한 엔터티 피드가 포함될 수 있습니다.

- `products`: 제품 데이터 피드
- `productAttributes`: 제품 특성 데이터 피드
- `categories`: 범주 데이터 피드
- `variants`: 구성 가능한 제품 변형 데이터 피드
- `prices`: 제품 가격 데이터 피드
- `categoryPermissions`: 범주 권한 데이터 피드
- `productOverrides`: 제품 권한 데이터 피드
- `inventoryStockStatus`: 재고 재고 상태 데이터 피드
- `scopesWebsite`: 스토어 및 스토어 보기 데이터 피드가 있는 웹 사이트
- `scopesCustomerGroup`: 고객 그룹 데이터 피드
- `orders`: 판매 주문 데이터 피드

설치된 [Commerce 서비스](../landing/saas.md)에 따라 `saas:resync` 명령에 사용할 수 있는 다른 피드 집합이 있을 수 있습니다.

### `no-reindex`

이 옵션은 다시 인덱싱하지 않고 기존 카탈로그 데이터를 [!DNL Commerce Services]에 다시 제출합니다. 이 옵션을 지정하지 않으면 명령은 데이터를 동기화하기 전에 전체 색인 재지정을 실행합니다.

이 옵션의 동작은 [레거시 또는 즉시 내보내기 모드](data-synchronization.md#synchronization-modes)에서 피드를 내보내는지에 따라 다릅니다

- 기존 내보내기 피드의 경우 동기화 프로세스는 피드 테이블에서 인덱싱된 데이터를 잘라내지 않습니다. 대신 모든 데이터를 Adobe Commerce 서비스로 다시 보냅니다.
- 즉시 내보내기 피드의 경우, 이 옵션이 지정된 경우 무시됩니다. 이러한 피드의 경우 재동기화 프로세스는 인덱스를 자르지 않고 이전에 실패한 업데이트 또는 항목만 재동기화합니다.

### `cleanup`

이 옵션은 동기화 전에 피드 인덱서 테이블을 정리합니다. 지정하면 SaaS 데이터 내보내기가 지정된 피드에 대해 전체 재동기화를 실행하고 피드 테이블의 기존 데이터를 모두 정리합니다.

Adobe에서는 [!DNL Data Space ID Cleanup] 작업을 수행한 후에만 이 명령을 사용하는 것이 좋습니다.

>[!WARNING]
>
>**이 옵션을 정기적으로 사용하지 마십시오**. 이로 인해 Adobe Commerce 서비스에서 데이터 동기화 문제가 발생할 수 있습니다. 예를 들어 `cleanup` 옵션을 사용하는 경우 `delete product event`이(가) Adobe Commerce 서비스로 전파되지 않을 수 있습니다.

## 문제 해결

연결된 Commerce 서비스에 예상 데이터가 표시되지 않으면 데이터 내보내기 오류 로그를 확인하고 환경 변수와 함께 `saas:resync` 명령을 사용하여 페이로드 및 프로파일러 데이터를 검토하여 문제를 해결하십시오. [로그 검토 및 문제 해결](troubleshooting-logging.md)을 참조하세요.
