---
title: 테스트 및 유효성 검사
description: 테스트와 유효성 검사를 통해  [!DNL Payment Services] 함수가 예상대로 작동하는지 확인하고 고객에게 최상의 결제 옵션을 제공합니다
feature: Payments, Checkout
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---

# 테스트 및 유효성 검사

[!DNL Adobe Commerce] 및 [!DNL Magento Open Source]에 대한 [!DNL Payment Services]을(를) 쇼핑객에게 노출하기 전에 프로덕션의 샌드박스 환경 _및_&#x200B;에서 테스트하는 것이 좋습니다. 테스트 및 유효성 검사를 통해 [!DNL Payment Services] 기능이 예상대로 작동하는지 확인하고 매장 및 고객에게 최상의 결제 옵션을 제공합니다.

## 샌드박스 환경에서 테스트

샌드박스 환경에서 [!DNL Payment Services]을(를) 테스트하는 것은 중요한 유효성 검사 단계입니다. 실제 은행과 판매자가 아니라 PayPal 샌드박스에만 연결된 시뮬레이션된 환경입니다.

1. [신용 카드 필드](payments-options.md#credit-card-fields) 또는 [PayPal 결제 단추](payments-options.md#paypal-smart-buttons)를 사용하여 스토어에서 성공적으로 체크아웃하세요. 테스트를 위해 가짜 신용 카드를 사용하는 방법에 대한 자세한 내용은 [자격 증명 테스트](#testing-credentials)를 참조하십시오.
1. 결제 액션이 [을(를) `Authorize and Capture`](onboard.md#set-payment-services-as-payment-method)(으)로 설정한 경우, [환불](refunds.md) 또는 [무효](voids.md)를 방금 완료된 주문을 캡처합니다. 결제 작업이 `Authorize and Capture` 대신 `Authorize`(으)로 설정된 경우 주문에 대해 [송장을 만들기](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/invoices#create-an-invoice){target="_blank"}할 수도 있습니다.
1. 24~48시간 내에 [지급 보고서](payouts.md)에서 거래 및 기타 정보를 봅니다.
1. [주문 결제 상태 보고서](order-payment-status.md)에서 주문 세부 사항을 확인하세요.

### 자격 증명 테스트

샌드박스를 테스트하고 확인할 때 기존 신용카드 계정에 실제 요금을 부과하지 않도록 가짜 신용카드 번호를 사용해야 합니다.

PayPal의 신용 카드 생성기를 사용하여 테스트를 위해 [무작위 신용 카드 정보를 생성](https://www.paypal.com/us/smarthelp/article/where-can-i-find-test-credit-card-numbers-ts2157)하세요.

샌드박스 모드에서 Apple Pay를 테스트하려면 다음을 수행하십시오.

* 가짜 신용 카드와 청구 정보를 사용하여 [Apple 샌드박스 테스터 계정](https://developer.apple.com/apple-pay/sandbox-testing/#create-a-sandbox-tester-account)을 만듭니다.
* [샌드박스 도메인을 등록](https://developer.paypal.com/docs/checkout/apm/apple-pay/#link-registeryoursandboxdomains)합니다.

>[!NOTE]
>
>PayPal의 샌드박스 결제 처리가 느려지고 서비스가 가끔 다운될 수 있습니다. 이러한 상황은 실시간 상품 결제 처리의 신속성과 효율성을 나타내는 것이 아니다.

## 프로덕션에서 테스트

쇼핑객에게 이 기능을 노출하기 전에 실제 신용 카드와 은행으로 프로덕션에서 [!DNL Payment Services]을(를) 테스트하는 것이 좋습니다. 샌드박스에서 [!DNL Payment Services]을(를) 테스트하는 것이 중요하지만 프로덕션에서 테스트하는 것은 [!DNL Payment Services]이(가) 예상대로 작동하는지 확인하기 위한 가장 어리석은 방법입니다.

다음 두 가지 방법 중 하나로 프로덕션에서 [!DNL Payment Services]을(를) 테스트할 수 있습니다.

* 구매자가 주문을 하지 않을 때를 선택합니다.
* 일시적으로 쇼핑객에게 액세스할 수 없지만 테스트를 위해 액세스할 수 있는 웹 스토어를 사용하십시오.

실제 신용 카드 및 PayPal 계정으로 프로덕션 테스트를 완료하고 캡처 및 환불을 포함한 전체 결제 라이프사이클을 테스트합니다. 테스트 중에 전체 체크아웃 및 결제 흐름을 완료하면 라이브 구매자가 [!DNL Payment Services] 기능을 사용할 때 작동하는 방식을 가장 명확하게 파악할 수 있습니다.

또한 생산 테스트에 사용하는 결제 방법에 대한 은행 거래 명세서에 표시되는 정보가 정확하고 예상되는지 확인해야 합니다(비즈니스 설명 포함).

프로덕션 모드에서 Apple 페이를 테스트하려면 [프로덕션 도메인을 등록](https://developer.paypal.com/docs/checkout/apm/apple-pay/#register-your-live-domain)해야 합니다.
