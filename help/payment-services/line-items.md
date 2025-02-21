---
title: ' [!DNL Payment Services]에 대한 라인 항목'
description: ' [!DNL Payment Services] 의 라인 항목 및 판매자 대시보드에서 라인 항목을 보는 방법에 대해 알아봅니다.'
feature: Payments
role: User
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 0%

---

# [!DNL Payment Services]에 대한 라인 항목

[!DNL Payment Services]에 대한 라인 항목은 주문에 포함된 항목입니다. 이러한 라인 항목은 다음과 같은 정보를 제공합니다.

* 제품 세부 사항
* 수량
* 가격(세금, 할인 및 기타 관련 정보 포함)

이 정보는 고객 서비스, 주문 관리 및 적절한 청구에 유용합니다.

이 기능은 [!DNL Payment Services]에 대해 기본적으로 활성화되어 있습니다. 라인 품목을 조회하려면

1. [PayPal 판매자 대시보드로 이동](https://www.paypal.com/merchant/){target=_blank}.

1. **활동** > **모든 트랜잭션**&#x200B;을 클릭합니다.

1. 원하는 주문을 선택하고 라인 항목을 조회합니다.

   > 쇼퍼 대시보드 보기의 라인 항목 예

   ![라인 항목 보기](assets/paypal-shopper-dashboard-line-items-view.png){width="500" zoomable="yes"}

## 라인 항목 속성

주문이 Adobe Commerce을 통해 배치되고 정보가 PayPal로 전송될 때 다음 속성을 사용하여 라인 항목이 생성됩니다.

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `name` | 문자열! | 항목 이름입니다. 품목이 복수 수량 또는 세금 반올림 문제로 인해 둘 이상의 라인을 가질 경우, 품목명은 모든 라인에 대해 동일하게 유지되지만 표시된 가격은 반올림으로 인해 약간 달라질 수 있습니다. |
| `unit_amount` | 개체! | 단위당 품목 가격 또는 비율. `currency_code` 및 `value` 특성을 포함합니다. |
| `tax` | 오브젝트 | 각 단위에 대한 품목 세금. `currency_code` 및 `value` 특성을 포함합니다. |
| `quantity` | 문자열! | 품목 수량. 정수가 됩니다. |
| `description` | 문자열 | 자세한 항목 설명. |
| `sku` | 문자열 | 항목에 대한 재고 유지 장치(또는 SKU). |
| `url` | 문자열 | 구매 중인 항목에 대한 `URL`입니다. 구매자에게 표시되고 구매자 경험에 사용됩니다. |
| `upc` | 오브젝트 | 항목의 범용 제품 코드(또는 UPC). |
| `category` | 문자열 | 항목 범주 유형. |

### `unit_amount` 특성

`unit_amount` 개체에 다음 특성이 포함되어 있습니다.

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `currency_code` | 문자열! | 통화를 식별하는 [3자리 ISO-4217 통화 코드](https://developer.paypal.com/api/rest/reference/currency-codes/). |
| `value` | 문자열! | 항목의 값을 나타냅니다. `currency_code`은(는) 필요한 소수 자릿수를 결정합니다. |

### `tax` 특성

`tax` 개체에 다음 특성이 포함되어 있습니다.

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `currency_code` | 문자열! | 통화를 식별하는 [3자리 ISO-4217 통화 코드](https://developer.paypal.com/api/rest/reference/currency-codes/). |
| `value` | 문자열! | 항목의 값을 나타냅니다. 필요한 소수 자릿수에 대해 각 `currency_code`에 따라 다릅니다. |

### `upc` 특성

`upc` 개체에 다음 특성이 포함되어 있습니다.

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `type` | string! | UPC 유형. |
| `code` | string! | 항목의 UPC 제품 코드입니다. |

+++라인 항목 예

```json
{
    "name": "Crown Summit Backpack - 1",
    "unit_amount": {
        "currency_code": "USD",
        "value": "38.50"
    },
    "tax": {
        "currency_code": "USD"
        "value": "3.13"
    },
    "quantity": "1",
    "description": "The Crown Summit Backpack is equally at home in a gym locker, study cube or a pup tent, so be sure yours is packed with books,",
    "sku": "24-MB03",
    "url": "https://magento.test/crown-summit-backpack.html",
    "upc": {
        "type": "UPC-A",
        "code": "000003"
    },
    "category": "PHYSICAL_GOODS"
},
{
    "name": "Crown Summit Backpack - 2",
    "unit_amount": {
        "currency_code": "USD",
        "value": "38.50"
    },
    "tax": {
        "currency_code": "USD",
        "value": "3.14"
    },
    "quantity": "1",
    "description": "The Crown Summit Backpack is equally at home in a gym locker, study cube or a pup tent, so be sure yours is packed with books,",
    "sku": "24-MB03",
    "url": "https://magento.test/crown-summit-backpack.html",
    "upc": {
        "type": "UPC-A",
        "code": "000003"
    },
    "category": "PHYSICAL_GOODS"
}
```

+++

이러한 필드 및 제한 사항에 대한 자세한 내용은 [라인 항목에 대한 PayPal 개발자 설명서](https://developer.paypal.com/docs/api/orders/v2/#definition-line_item){target=_blank}를 참조하십시오.

## 라인 항목 관리

Adobe Commerce [각 행의 총액을 기반으로 세금을 계산합니다](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/taxes/taxes#warning-messages){target=_blank}. 동일한 항목의 여러 수량을 주문하거나 세금 포함 가격이 카탈로그에 표시되는 경우 반올림 문제가 발생할 수 있습니다. 이 경우, 총 수량은 두 줄로 나눌 수 있지만, 수량은 주문한 총 품목과 같습니다.

> 판매자 대시보드 뷰에 반올림 문제가 있는 라인 항목의 예

![라인 항목 보기](assets/line-items-example.png){width="600" zoomable="yes"}

+++Adobe Commerce이 라인 항목에서 반올림 문제를 계산하는 방법

[!DNL Payment Services]에 대한 라인 항목은 `unit_amount` 또는 `unit_tax` 값이 주문의 총 금액과 일치하도록 이 반올림 문제의 균형을 유지합니다. 이 반올림 문제를 해결하기 위해 품목을 두 줄로 분할할 수 있습니다.

* `unit_amount`에 반올림 문제가 나타나면 판매자는 이 추가 라인에 대한 가격 차이를 확인해야 합니다.
* `unit_tax`에 반올림 문제가 표시되면 `tax`이(가) 그리드에 표시되지 않고 맨 아래의 합계로만 표시되기 때문에 개별 라인 항목에는 차이가 표시되지 않습니다.

+++
