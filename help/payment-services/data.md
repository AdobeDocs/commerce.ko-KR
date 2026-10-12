---
title: 사용 가능한 데이터
description: 재무 보고 데이터를 사용하여 Commerce이 아닌 시스템과 보고를 조정합니다.
role: User
level: Intermediate
exl-id: dbf41ce9-01f9-45d0-b651-e4c499e83822
feature: Payments, Checkout, Data Import/Export, Paas, Saas
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: 601e4abe-d9bf-58de-a779-32ed6794dcbe
    internal-label: Data Import/Export
  - id: 00451af3-7b97-5414-9992-3a6c269e413f
    internal-label: Paas
  - id: d3b92bef-63fa-5031-a925-d04d9362d616
    internal-label: Saas
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
source-git-commit: 76e77db86adecdbd3be76040970c0d0899c34cdc
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%
---
# 사용 가능한 데이터

외부 시스템 전반에서 Adobe Commerce 재무 보고를 조정할 수 있도록 일부 주문 및 지급 데이터를 사용할 수 있습니다.

## ERP 시스템과 조정

특정 주문과 연관된 증분 ID를 사용하여 Adobe Commerce financial reporting을 비 Adobe ERP(Enterprise Resource Planning) 시스템과 조정할 수 있습니다.

결제 서비스에서 Commerce 주문을 PayPal로 보내면 증분 ID가 `invoice_id`의 `custom_id` _및_(또한 `increment_id` 뒤에 임의의 문자열 포함)로 포함됩니다.

ID는 지불에 대한 판매자 활동 세부 사항과 PayPal 웹후크에서 모두 쉽게 액세스할 수 있습니다.

`invoice_id` 및 `custom_id`은(는) 지불에 대한 판매자 활동 세부 정보 하단 근처에 표시됩니다.

판매자 활동 세부 정보의 ![`custom_id`](assets/merchant-activity-ids.png){width="600" zoomable="yes"}

PayPal 웹후크의 세부 정보에 있는 `custom_id` 및 `invoice_id`:

```json
   ...
   {
    "id": "4E855005GK253170H",
    "intent": "AUTHORIZE",
    "status": "COMPLETED",
    "payment_source": {
        ...
    },
    "purchase_units": [
        {
            ...
            "custom_id": "000001322",
            "invoice_id": "000001322-c01bd7c3-920f-4542-a900-738082177e92",
            ...
            "payments": {
                "authorizations": [
                    {
                       ...
                        "invoice_id": "000001322-c01bd7c3-920f-4542-a900-738082177e92",
                        "custom_id": "000001322",
                        ...
                    }
                ],
                "captures": [
                    {
                        ...
                        "invoice_id": "000001322-c01bd7c3-920f-4542-a900-738082177e92",
                        "custom_id": "000001322",
                        ...
                    }
                ]
            }
        }
    ],
    "payer": {
        ...
    },
    "create_time": "2022-09-12T14:59:01Z",
    "update_time": "2022-09-12T14:59:45Z",
    "links": [
        ...
    ]
}
   ...
```

자세한 내용은 PayPal의 REST API 설명서 를 참조하십시오.

* [`purchase_unit`, `custom_id` 및 `invoice_id` 위치](https://developer.paypal.com/docs/api/orders/v2/#definition-purchase_unit)
* [주문 세부 사항 표시](https://developer.paypal.com/docs/api/orders/v2/#orders_get)
