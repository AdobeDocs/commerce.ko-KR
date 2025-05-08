---
title: 명령줄 구성
description: 설치 후 명령줄 인터페이스(CLI)를 사용하여  [!DNL Payment Services] 을(를) 구성할 수 있습니다.
role: Admin, Developer
level: Intermediate
exl-id: 265ab1be-fe52-41f3-85cb-addbc2ddfb17
feature: Payments, Checkout, Configuration, Integration, Paas
badgePaas: label="PaaS만" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce 온 클라우드 프로젝트(Adobe 관리 PaaS 인프라) 및 온프레미스 프로젝트에만 적용됩니다."
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '621'
ht-degree: 0%

---

# 명령줄 구성

[!DNL Payment Services]을(를) 설치한 후 [홈](payments-home.md)에서 또는 명령줄 인터페이스(CLI)를 통해 쉽게 구성할 수 있습니다.

## 데이터 내보내기 구성

[!DNL Payment Services]은(는) [!DNL Magento Open Source] 및 [!DNL Adobe Commerce]에서 내보낸 주문 데이터를 결제 공급자의 집계된 결제 데이터와 결합하여 유용한 보고서를 만듭니다. [!DNL Payment Services] 확장은 인덱서를 사용하여 보고서에 필요한 모든 데이터를 효율적으로 수집합니다.

[!DNL Payment Services] 보고에 사용된 데이터에 대한 자세한 내용은 [결제 상태 보고서 주문](order-payment-status.md#data-used-in-the-report)을 참조하세요.

### [!DNL Magento Open Source]에서 크론 구성

[!DNL Magento Open Source]에서 `BY SCHEDULE` 인덱스 모드를 사용하려면 cron을 구성해야 합니다. [cron 구성 및 실행](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs)을 참조하세요.

### 인덱서 설정

주문 데이터를 내보내고 두 인덱스 모드 중 하나(`ON SAVE`(기본값) 또는 `BY SCHEDULE`(권장))를 사용하여 결제 서비스에서 유지합니다.

[!DNL Payment Services]에 대한 색인은 다음과 같습니다.

| 코드 | 이름 | 설명 |
|    ---    |  ---  |  ---  |
| `sales_order_data_exporter` | 판매 주문 피드 | 주문 데이터의 인덱스를 작성합니다. |
| `sales_order_status_data_exporter` | 판매 주문 상태 피드 | 판매 주문 상태 데이터의 인덱스를 작성합니다. |
| `store_data_exporter` | 피드 저장 | 스토어 데이터의 인덱스를 작성합니다. |

세 개의 모든 인덱서에 대한 인덱스 모드를 변경하려면 다음을 실행합니다.

```bash
bin/magento indexer:set-mode schedule sales_order_data_exporter sales_order_status_data_exporter store_data_exporter
```

>[!TIP]
>
>명령에 인덱서를 지정하지 않으면 모든 인덱서가 동일한 값으로 업데이트됩니다. 특정 인덱서를 변경하려면 해당 인덱서를 명령에 나열해야 합니다.

인덱서의 모드를 수동으로 변경하는 방법에 대한 자세한 내용은 개발자 설명서에서 [인덱서 구성](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/manage-indexers#configure-indexers){target="_blank"}을 참조하십시오. 관리에서 변경하는 방법에 대해 알아보려면 핵심 사용 안내서의 [색인 관리](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management#change-the-index-mode){target="_blank"}를 참조하세요.

### 수동으로 데이터 다시 인덱싱

데이터가 자동으로 발생할 때까지 기다리지 않고 수동으로 데이터를 다시 인덱싱할 수 있습니다. 자세한 내용은 [인덱서 관리](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/manage-indexers){target="_blank"}의 [인덱스 다시 지정](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/manage-indexers#reindex){target="_blank"}을 참조하십시오.

`BY SCHEDULE` 모드가 설정되면 시스템이 변경된 엔터티를 추적하고 cron 작업이 설정된 일정에 따라 해당 엔터티의 인덱스를 업데이트합니다. cron 작업을 사용하여 인덱싱을 수동으로 트리거하는 방법에 대해 알아보려면 [명령줄에서 cron 실행](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs#config-cli-cron-group-run)&#x200B;([cron 구성 및 실행](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs))을 참조하십시오.

### 재인덱싱된 데이터를 결제 서비스로 보내기

데이터가 인덱싱되면 자동으로 [!DNL Payment Services]&#x200B;(으)로 전송됩니다. 다음 명령을 사용하여 인덱싱된 데이터를 전송하는 프로세스를 수동으로 트리거할 수도 있습니다.

```bash
bin/magento saas:resync --feed [feedName]
```

다음 명령 옵션을 사용합니다.

| 명령 | 설명 |
|  ---  |  ---  |
| `bin/magento saas:resync --feed [feedName]` | 지정된 피드의 색인 재지정을 수행하고 해당 서비스로 보냅니다. |
| `bin/magento saas:resync --no-reindex` | 인덱싱을 건너뛰고 인덱스에서 동기화되지 않은 데이터를 보냅니다. |

`--feed` 매개 변수를 사용하면 전송할 피드를 지정할 수 있습니다.

| 피드 | 설명 |
|  ---  |  ---  |
| `paymentServicesOrdersProduction` | 프로덕션 모드의 주문 피드 |
| `paymentServicesOrdersSandbox` | 샌드박스 모드의 주문 피드 |
| `paymentServicesOrderStatusesProduction` | 프로덕션 모드의 주문 상태 |
| `paymentServicesOrderStatusesSandbox` | 샌드박스 모드의 주문 상태 |
| `paymentServicesStoresProduction` | 프로덕션 모드로 저장 |
| `paymentServicesStoresSandbox` | 샌드박스 모드로 저장 |

cron이 구성 및 설치된 경우 보고서에 필요한 모든 데이터가 자동으로 [!DNL Payment Services]&#x200B;(으)로 전송됩니다. cron 데이터를 [!DNL Payment Services]&#x200B;(으)로 전송하는 프로세스를 수동으로 트리거할 수도 있습니다.

```bash
bin/magento cron:run --group payment_services_data_export
```

리인덱싱과 인덱서에 대한 자세한 내용은 개발자 설명서에서 [인덱서 관리](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/manage-indexers) 항목을 참조하십시오.

## CLI를 통해 범위 구성

[!DNL Payment Services]을(를) 통해 판매자는 [여러 PayPal 계정](settings.md#use-multiple-paypal-accounts)을 사용할 수 있습니다. 이제 CLI를 통해 이러한 계정의 범위를 변경할 수 있습니다.

범위를 `website` 수준으로 설정하려면 다음을 실행하십시오.

```bash
bin/magento config:set payment/payment_services/mba_scoping_level website
```

범위를 `store` 수준으로 설정하려면 다음을 사용합니다.

```bash
bin/magento config:set payment/payment_services/mba_scoping_level store
```

>[!TIP]
>
> 범위를 저장소 수준으로 변경하려면 [!DNL Payment Services] 영업 담당자에게 문의하십시오.

범위를 변경하면 변경 사항을 표시하기 위해 캐시를 플러시합니다.

```bash
bin/magento cache:clean:payment_services_merchant_scopes
```

## L2/L3 처리 구성

[!DNL Payment Services]은(는) 카드 결제 거래에서 레벨 2 및 레벨 3 데이터를 처리하여 가맹점에 대한 추가 정보를 제공할 수 있습니다.

>[!WARNING]
>
> PayPal을 사용한 레벨 2 및 레벨 3 처리와 통합은 미국 판매자만 사용할 수 있습니다. 자세한 내용은 PayPal 개발자 설명서에서 [결제 처리](https://developer.paypal.com/docs/checkout/advanced/processing/){target=_blank}를 참조하십시오.

[!DNL Payment Services]에 대한 L2/L3 처리 데이터를 사용하거나 질문이 있는 경우 [!DNL Payment Services] 계정 관리자에게 문의하십시오.

[!DNL Payment Services]에서 사용되는 L2 및 L3 처리에 대한 자세한 내용은 [수준 2 및 수준 3 처리](levels-card-payment-transactions.md)를 참조하십시오.
