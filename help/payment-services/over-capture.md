---
title: 오버캡처
description: 결제 서비스 확장에 대한 오버캡처 요구 사항 및 구성에 대해 알아봅니다.
role: Admin, User
level: Intermediate
feature: Payments, Paas
source-git-commit: d2bcc58f34af50f26d4a4f082e5b3fc30089ab58
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 0%
---
# 오버캡처

오버캡처를 사용하면 PayPal 오버캡처 계약을 보유한 적격 가맹점은 주문 송장 발행 시 원래 승인된 금액보다 더 많은 금액을 캡처할 수 있습니다. 예를 들어, 승인 및 이행 간의 중량 기반 조정이나 자재 비용의 변경으로 인해 최종 금액이 증가할 수 있습니다.

PayPal은 각 판매자 계정에 대한 초과 캡처 한도를 결정합니다. [!DNL Payment Services]에서 오버캡처를 사용하도록 설정하면 PayPal에서 승인한 계약이 설정되거나 제한이 증가하지 않습니다.

>[!NOTE]
>
>이 항목에서는 [!DNL Payment Services] 확장의 오버캡처를 설명합니다. [!DNL Adobe Commerce as a Cloud Service]의 경우 [사용자 지정 캡처 양](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/invoices#custom-capture-amounts)을 참조하여 별도의 사용 가능 여부 및 사용 요구 사항을 확인하십시오.

## 사전 요구 사항

오버캡처를 활성화하기 전에:

* [!DNL Payment Services] 2.17.0 이상에서만 오버캡처를 사용할 수 있습니다.
* Overcapture는 미국 내 기업에서만 사용할 수 있습니다. PayPal의 [오버캡처 요구 사항(PSD2)](https://www.paypal.com/us/cshelp/article/overcapture-requirements-psd2-help954)은 유럽 경제 지역(EEA)의 PayPal 구매자에게 판매하는 미국 기반 판매자에게도 적용됩니다.
* 대체 결제 방법(APM)에는 오버캡처를 사용할 수 없습니다.
* PayPal과 오버캡처 계약을 체결하고 PayPal 계정 관리자에게 판매자 계정에 대해 승인된 한도를 확인합니다.
* 결제 방법 **[!UICONTROL Payment Action]**&#x200B;을(를) `Authorize`(으)로 설정합니다. 오버캡처는 `Authorize and Capture`(으)로 자동 캡처된 주문이 아니라 나중에 송장 발행 중에 캡처된 승인된 주문에 적용됩니다. [결제 방법으로 설정 [!DNL Payment Services] 을 참조하십시오](production.md#set-payment-services-as-payment-method).

## 오버캡처 활성화

1. _관리자_ 사이드바에서 **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**(으)로 이동합니다.
1. 왼쪽 패널에서 **[!UICONTROL Sales]**&#x200B;을(를) 확장하고 **[!UICONTROL Payment Methods]**&#x200B;을(를) 선택합니다.
1. 스토어 범위 선택기를 사용하여 구성할 웹 사이트를 선택합니다.
1. _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_섹션을 확장합니다.
1. _[!UICONTROL Payment Services]_섹션에서_[!UICONTROL General Configuration]_ 섹션을 확장합니다.
1. **[!UICONTROL Over Capture Enabled]**&#x200B;을(를) `Yes`(으)로 설정합니다.
1. 변경 내용을 저장하려면 **[!UICONTROL Save Config]**&#x200B;을(를) 클릭합니다.
1. **[!UICONTROL System]** > **[!UICONTROL Cache Management]**(으)로 이동한 다음 **[!UICONTROL Flush Cache]**&#x200B;을(를) 클릭하여 모든 잘못된 캐시를 새로 고칩니다.

## 승인된 결제 캡처

초과 캡처는 관리자에서 송장을 발행하는 동안 발생합니다. 요청된 캡처 금액은 PayPal에서 판매자 계정에 대해 승인한 한도 내에 있어야 합니다. 표준 송장 발행 워크플로우에 대해서는 [송장 만들기](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/invoices#create-an-invoice)를 참조하십시오.

1. _관리자_ 사이드바에서 **[!UICONTROL Sales]** > **[!UICONTROL Orders]**(으)로 이동합니다.
1. 아직 캡처되지 않은 승인된 지급으로 주문을 엽니다.
1. **[!UICONTROL Invoice]**&#x200B;을(를) 클릭합니다.
1. 사용자 정의 캡처 양 필드에 캡처할 총 양을 입력합니다. 예를 들어, 승인된 금액이 USD 100이고 최종 요금이 USD 110인 경우 `10`이(가) 아닌 `110`을(를) 입력하십시오. 요청한 금액은 PayPal 승인 한도 내에 있어야 합니다.
1. 송장의 온라인 캡처를 선택하여 지급 공급자를 통해 지급을 요청합니다.
1. 송장을 검토하고 **[!UICONTROL Submit Invoice]**&#x200B;을(를) 클릭합니다.

### 송장 API를 사용하여 캡처

표준 [송장 만들기](https://developer.adobe.com/commerce/webapi/rest/tutorials/orders/order-create-invoice) 끝점을 사용합니다.

```http
POST /rest/<store_code>/V1/order/<orderId>/invoice
```

주문에 대한 스토어 코드 및 주문의 내부 ID를 사용합니다. 인증된 관리자 또는 통합 토큰으로 인증하고 `Content-Type: application/json`을(를) 설정합니다.

다음 예제 페이로드는 상인의 PayPal 계약이 해당 금액을 허용하는 경우 USD 100에 대해 승인된 주문에 대해 USD 110의 온라인 캡처와 함께 전체 송장을 요청합니다.

```json
{
  "capture": true,
  "notify": false,
  "arguments": {
    "extension_attributes": {
      "custom_capture_amount": 110
    }
  }
}
```

이 예제에서는

1. `capture`개의 온라인 캡처를 요청합니다.
1. `notify`은(는) Commerce에서 송장 알림 이메일을 전송하는지 여부를 제어합니다.
1. `custom_capture_amount`은(는) 인증된 양에 대한 증가가 아니라 캡처할 최종 양입니다.

## 거부된 캡처 문제 해결

PayPal이 오버캡처 요청을 거부하는 경우:

* 결제에 사용된 PayPal 판매자 계정에 대해 오버캡처 계약이 활성화되어 있는지 확인합니다.
* 요청한 금액이 승인된 한도 내에 있는지 확인합니다. 한도를 초과하는 경우 더 낮은 금액을 요청하거나 PayPal 계정 관리자에게 문의하여 증액에 대해 논의하십시오.
