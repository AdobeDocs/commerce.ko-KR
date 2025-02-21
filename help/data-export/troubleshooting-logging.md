---
title: 로그 검토 및 문제 해결
description: 데이터 내보내기 및 saas 내보내기 로그를 사용하여  [!DNL data export] 오류를 해결하는 방법에 대해 알아봅니다.
feature: Services
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '1071'
ht-degree: 0%

---

# 로그 검토 및 문제 해결

[!DNL data export] 확장은 데이터 수집 및 동기화 프로세스를 추적할 로그를 제공합니다.

## 로그

Commerce 응용 프로그램 서버의 `var/log` 디렉터리에서 로그를 사용할 수 있습니다.

| 로그 이름 | 파일 이름 | 설명 |
|-----------------| ----------| -------------|
| SaaS 데이터 내보내기 로그 | `commerce-data-export.log` | 엔터티 이벤트 및 전체 재동기화 트리거와 같은 데이터 내보내기 활동에 대한 정보를 제공합니다.  각 로그 레코드는 특정 구조를 가지며 피드, 작업, 상태, 경과 시간, 프로세스 ID 및 호출자에 대한 정보를 제공합니다. |
| SaaS 데이터 내보내기 오류 로그 | `data-export-errors.log` | 데이터 동기화 프로세스 중에 발생하는 오류에 대한 오류 메시지 및 스택 추적을 제공합니다. |
| SaaS 내보내기 로그 | `saas-export.log` | Commerce SaaS 서비스로 전송된 데이터에 대한 정보를 제공합니다. |
| SaaS 내보내기 오류 로그 | `saas-export-errors.log` | Commerce SaaS 서비스로 데이터를 전송할 때 발생하는 오류에 대한 정보를 제공합니다. |

Adobe Commerce 서비스에 대한 예상 데이터가 표시되지 않으면 데이터 내보내기 확장에 대한 오류 로그를 사용하여 문제가 발생한 위치를 파악하십시오. 또한 추적 및 문제 해결을 위해 추가 데이터로 로그를 확장할 수 있습니다. [확장된 로깅](#extended-logging)을 참조하십시오.

### 로그 형식

각 로그 레코드에는 다음과 같은 구조가 있습니다.

```
[<log record datetime>] report.<log level>:
{
   "feed": "<feed name>",
   "operation": "<executed operation>",
   "status": "<status of operation>",
   "elapsed": "<time elaspsed from script run>",
   "pid": "<proccess id who executed `operation`>",
   "caller": "<who called this `operation`>"
} [] []
```

>[!NOTE]
>
>가독성을 높이기 위해 JSON 기반 문자열이 아름답게 수정되었습니다.

다음 표에서는 로그에 기록할 수 있는 작업 유형을 설명합니다.

| 작업 | 설명 | 발신자 예 |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| 전체 동기화 | 전체 동기화는 주어진 피드에 대해 모든 데이터를 수집하여 SaaS로 전송합니다. | `bin/magento saas:resync --feed=products` |
| 부분 색인 재지정 | 부분 동기화는 지정된 피드에서 업데이트된 엔터티에 대해서만 데이터를 수집하여 SaaS로 보냅니다. 이 로그는 업데이트된 엔티티가 있는 경우에만 표시됩니다. | `bin/magento cron:run --group=index` |
| 실패한 항목 다시 시도 | Commerce 애플리케이션 또는 서버 오류로 인해 이전 동기화 작업이 실패한 경우 지정된 피드에 대한 항목을 SaaS에 다시 보냅니다. 이 로그는 실패한 항목이 있는 경우에만 존재합니다. | `bin/magento cron:run --group=saas_data_exporter`(&quot;*_data_exporter&quot; 크론 그룹) |
| 전체 동기화(이전) | 레거시 내보내기 모드에서 지정된 피드에 대한 전체 동기화. | `bin/magento saas:resync --feed=categories` |
| 부분 색인 재지정(기존) | 레거시 내보내기 모드에서 지정된 피드에 대해 업데이트된 엔티티를 SaaS로 보냅니다. 이 로그는 업데이트된 엔티티가 있는 경우에만 표시됩니다. | `bin/magento cron:run --group=index` |
| 부분 동기화(레거시) | 레거시 내보내기 모드에서 지정된 피드에 대해 업데이트된 엔티티를 SaaS로 보냅니다. 이 로그는 업데이트된 엔티티가 있는 경우에만 표시됩니다. | `bin/magento cron:run --group=saas_data_exporter`(&quot;*_data_exporter&quot; 크론 그룹) |


### 로깅 예

전체 재동기화 중에 진행률은 기본적으로 30초마다 추적되고 기록됩니다. 다음은 로그 항목의 예입니다.

```json
{
   "feed": "prices",
   "operation": "full sync",
   "status": "Progress: 2/5, processed: 200, synced: 100",
   "elapsed": "00:00:00 190 ms",
   "pid": "12824",
   "caller": "bin/magento saas:resync --feed=products"
}
```

이 예제에서 `status` 값은 동기화 작업에 대한 정보를 제공합니다.

- **`"Progress 2/5"`**&#x200B;은(는) 5개 중 2개의 반복이 완료되었음을 나타냅니다. 반복 횟수는 내보낸 엔티티 수에 따라 다릅니다.
- **`"processed: 200"`**&#x200B;은(는) 200개 항목이 처리되었음을 나타냅니다.
- **`"synced: 100"`**&#x200B;은(는) 100개의 항목이 SaaS로 전송되었음을 나타냅니다. `"synced"`은(는) `"processed"`과(와) 같지 않아야 합니다. 예를 들면 다음과 같습니다.
   - **`"synced" < "processed"`**&#x200B;은(는) 피드 테이블이 이전에 동기화된 버전과 비교하여 항목의 변경 사항을 감지하지 못했음을 의미합니다. 이러한 항목은 동기화 작업 중에 무시됩니다.
   - 동일한 엔터티 id(예: `Product ID`)의 **`"synced" > "processed"`**&#x200B;에 다른 범위의 값이 여러 개 있을 수 있습니다. 예를 들어 하나의 제품을 5개의 웹 사이트에 할당할 수 있습니다. 이 경우 &quot;1개의 처리된&quot; 항목과 &quot;5개의 동기화된&quot; 항목이 있을 수 있습니다.

+++ **예: 가격 피드에 대한 전체 재동기화 로그**

```
Price feed full resync:

[2024-03-05T21:00:51.754687+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Initialize","elapsed":"383 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:51.803178+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Creating batch table `catalog_data_exporter_product_prices_index_batches`. Start position: 30515","elapsed":"434 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:51.851878+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Batch table `catalog_data_exporter_product_prices_index_batches` created. Total Items: 500, batches: ~1","elapsed":"482 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:51.852548+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"start processing `500` items in `1` threads with `500` batch size","elapsed":"483 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:52.288369+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Progress 1\/1, processed 500, synced 0","elapsed":"919 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:53.994249+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Progress 1\/1, processed 500, synced 100","elapsed":"00:00:02 625 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:53.995168+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Complete","elapsed":"00:00:02 626 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
```

+++

## New Relic을 사용하여 로그 보기 및 문제 해결

Adobe Commerce 로그를 New Relic에 저장하는 경우 구문 분석 규칙을 추가하여 가독성과 쿼리 경험을 개선할 수 있습니다.

1. New Relic에 로그인.

1. `Logs => Parsing`(으)로 이동합니다.

1. `Create parsing rule`을(를) 클릭합니다.

1. 다음 값을 추가하여 구문 분석 규칙을 구성합니다.

   - **NRQL을 기반으로 로그 필터링**

     `filePath LIKE '%commerce-data-export%.log'`

   - **규칙 구문 분석**

     `\[%{DATA:timestamp}\] report.%{DATA:logLevel} %{GREEDYDATA:feed:json}`

이 예에서는 특정 피드 유형, 작업 등을 기준으로 New Relic 로그를 쿼리할 수 있는 규칙을 추가합니다.

**예제 쿼리 문자열**—`feed.feed:"products" and feed.status:"Complete"`

## 문제 해결

Commerce Services에서 데이터가 누락되었거나 잘못된 경우 로그를 확인하여 Adobe Commerce 인스턴스에서 Commerce 서비스 플랫폼으로 동기화하는 동안 문제가 발생했는지 확인하십시오. 필요한 경우 확장 로깅을 사용하여 문제를 해결하기 위해 로그에 추가 정보를 추가합니다.

- commerce-data-export-errors.log - 수집 단계에서 오류가 발생한 경우
- saas-export-errors.log - 전송 단계 중 오류가 발생한 경우

구성 또는 타사 확장과 관련이 없는 오류가 표시되면 가능한 많은 정보가 포함된 [지원 티켓](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html?lang=en#submit-ticket)을 제출하십시오.

### 카탈로그 동기화 문제 해결 {#resolvesync}

데이터 재동기화를 트리거할 때 데이터를 업데이트하고 라이브 검색 및 추천 단위와 같은 UI 구성 요소에 반영되기까지 최대 1시간이 걸릴 수 있습니다. 여전히 Commerce 상점 첫 화면의 카탈로그와 데이터 사이에 불일치가 있거나 카탈로그 동기화가 실패한 경우 다음을 참조하십시오.

#### 데이터 불일치

1. 검색 결과에 해당 제품에 대한 세부 보기를 표시합니다.
1. JSON 출력을 복사하고 콘텐츠가 [!DNL Commerce] 카탈로그에 있는 것과 일치하는지 확인합니다.
1. 콘텐츠가 일치하지 않으면 공백 또는 마침표 추가와 같이, 카탈로그의 제품에 약간의 변경 작업을 수행합니다.
1. 다시 동기화할 때까지 기다리거나 [수동 다시 동기화를 트리거](#resync)합니다.

#### 동기화가 실행되고 있지 않음

동기화가 일정에 따라 실행되고 있지 않거나 동기화되지 않은 경우 이 [KnowledgeBase](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/troubleshoot-product-recommendations-module-in-magento-commerce.html) 문서를 참조하십시오.

#### 동기화 실패

카탈로그 동기화 상태가 **실패**&#x200B;인 경우 [지원 티켓](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket)을 제출하세요.

## 확장된 로깅

추가 로그 정보의 경우 환경 변수를 사용하여 추적 및 문제 해결을 위한 추가 데이터와 함께 로그를 확장할 수 있습니다.

`var/log/` 디렉터리에 두 개의 로그 파일이 있습니다.

- commerce-data-export-errors.log - 수집 단계에서 오류가 발생한 경우
- saas-export-errors.log - 전송 단계 중 오류가 발생한 경우

환경 변수를 사용하여 추적 및 문제 해결을 위한 추가 데이터와 함께 로그를 확장할 수 있습니다.

### 피드 페이로드 확인

피드를 다시 동기화할 때 `EXPORTER_EXTENDED_LOG=1` 환경 변수를 추가하여 SaaS 내보내기 로그에 피드 페이로드를 포함하십시오.

```shell script
EXPORTER_EXTENDED_LOG=1 bin/magento saas:resync --feed=products
```

작업이 완료되면 SaaS 내보내기 로그(`var/.log/saas-export.log`)에서 피드 페이로드를 검토할 수 있습니다.

### 피드 인덱스 테이블의 페이로드 유지

Commerce SaaS 데이터 내보내기 확장(`magento/module-data-exporter`) 103.3.0 이상의 경우 즉시 내보내기 피드는 인덱스 테이블에서 필요한 최소 데이터만 유지합니다. 피드에는 모든 카탈로그 및 재고 상태 피드가 포함됩니다.

프로덕션 환경에서는 인덱스 테이블의 페이로드 데이터를 보존하지 않는 것이 좋지만 개발자 환경에서는 유용할 수 있습니다. 피드를 다시 동기화할 때 `PERSIST_EXPORTED_FEED=1` 환경 변수를 추가하여 인덱스에 피드 페이로드를 포함하십시오.

```shell script
PERSIST_EXPORTED_FEED=1 bin/magento saas:resync --feed=products
```

### 프로파일러를 실행하여 성능 저하 문제 해결

특정 피드의 색인 재지정 프로세스에 불합리한 시간이 걸리는 경우 프로파일러를 실행하여 지원 팀에 유용할 수 있는 추가 데이터를 수집합니다.

reindex 명령을 실행할 때 `EXPORTER_PROFILER=1` 환경 변수를 추가하여 프로파일러를 실행하십시오.

```
EXPORTER_PROFILER=1 bin/magento indexer:reindex catalog_data_exporter_products
```

프로파일러 데이터는 데이터 내보내기 로그(`var/log/commerce-data-export.log`)에 다음 형식으로 저장됩니다.

```
<Provider class name>, <# of processed entities>, <execution time im ms>, <memory consumption in Mb>
```
