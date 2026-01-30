---
title: 테스트 및 유효성 검사
description: 테스트와 유효성 검사를 통해  [!DNL Payment Services] 함수가 예상대로 작동하는지 확인하고 고객에게 최상의 결제 옵션을 제공합니다
exl-id: 95b4615e-73b0-41e8-83e2-e65a0b22f10f
feature: Payments, Checkout, Paas, Saas
source-git-commit: 91a4b8fa7228fb91c8ee0bf0a1623d104f061894
workflow-type: tm+mt
source-wordcount: '729'
ht-degree: 0%

---

# 테스트 및 유효성 검사

[!DNL Payment Services] 및 [!DNL Adobe Commerce]에 대한 [!DNL Magento Open Source]을(를) 쇼핑객에게 노출하기 전에 프로덕션의 샌드박스 환경 _및_&#x200B;에서 테스트하는 것이 좋습니다. 테스트 및 유효성 검사를 통해 [!DNL Payment Services] 기능이 예상대로 작동하는지 확인하고 매장 및 고객에게 최상의 결제 옵션을 제공합니다.

## 샌드박스 환경에서 테스트

샌드박스 환경에서 [!DNL Payment Services]을(를) 테스트하는 것은 중요한 유효성 검사 단계입니다. 실제 은행과 판매자가 아니라 PayPal 샌드박스에만 연결된 시뮬레이션된 환경입니다.

1. [신용 카드 필드](payments-options.md#credit-card-fields) 또는 [PayPal 결제 단추](payments-options.md#paypal-smart-buttons)를 사용하여 스토어에서 성공적으로 체크아웃하세요. 테스트를 위해 가짜 신용 카드를 사용하는 방법에 대한 자세한 내용은 [자격 증명 테스트](#testing-credentials)를 참조하십시오.
1. 결제 액션이 [을(를) `Authorize and Capture`](onboard.md#set-payment-services-as-payment-method)(으)로 설정한 경우, [환불](refunds.md) 또는 [무효](voids.md)를 방금 완료된 주문을 캡처합니다. 결제 작업이 [&#x200B; 대신 &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/invoices#create-an-invoice){target="_blank"}(으)로 설정된 경우 주문에 대해 `Authorize`송장을 만들기`Authorize and Capture`할 수도 있습니다.
1. 24~48시간 내에 [지급 보고서](payouts.md)에서 거래 및 기타 정보를 봅니다.
1. [주문 결제 상태 보고서](order-payment-status.md)에서 주문 세부 사항을 확인하세요.

### 로컬 개발 환경에서 테스트

로컬 개발 환경에서 PayPal, PayLater 및 Venmo 결제 방법을 테스트하려면 인터넷에서 환경에 액세스해야 합니다. 이러한 결제 방법은 PayPal이 Commerce 인스턴스와 통신하여 배송 옵션을 검색하고 합계를 계산해야 하는 [서버측 배송 콜백](https://developer.paypal.com/docs/multiparty/checkout/standard/customize/shipping-module/)을 사용합니다.

>[!INFO]
>
>인터넷에 액세스할 수 있는 URL이 없으면 배송 콜백이 작동하지 않아 프로덕션과 다른 체크아웃 흐름이 발생합니다. 정확한 결과를 얻으려면 항상 액세스 가능한 URL로 테스트하십시오.

로컬 환경을 노출하려면 다음을 수행하십시오.

1. [ngrok](https://ngrok.com/)과(와) 같은 터널링 서비스를 사용하여 로컬 환경에 대해 공개적으로 액세스할 수 있는 URL을 만드십시오.

1. Ngrok URL과 일치하도록 Commerce 기본 URL 구성 업데이트:

   ```bash
   bin/magento config:set web/unsecure/base_url https://your-ngrok-url.ngrok.io/
   bin/magento config:set web/secure/base_url https://your-ngrok-url.ngrok.io/
   bin/magento cache:flush
   ```

1. PayPal, PayLater 또는 Venmo 결제 방법으로 테스트를 완료하십시오.

1. 테스트가 완료되면 원래 기본 URL 구성을 복원합니다.

끝점의 응답 시간이 5초 미만인 경우 PayPal은 팝업에 오류 메시지를 표시합니다.

#### Apple Pay 로컬 개발

Apple Pay는 로컬 개발을 위해 추가 구성이 필요합니다. Apple Pay는 도메인 등록을 사용하여 사이트에서 Apple Pay 결제를 수락할 수 있는 권한이 있는지 확인합니다. 즉, Apple이 `/.well-known/apple-developer-merchantid-domain-association`에서 도메인 확인 파일의 유효성을 검사하려면 도메인에 연결할 수 있어야 합니다.

로컬 개발을 위해 환경은 다음 요구 사항을 충족해야 합니다.

* **공개적으로 액세스할 수 있음**, Apple이 인터넷에서 도메인에 연결할 수 있어야 합니다.
* **HTTPS 프로토콜**, Apple Pay는 보안 연결에서만 작동합니다.

[ngrok](https://ngrok.com/)과(와) 같은 터널링 서비스를 사용하면 두 요구 사항을 모두 충족할 수 있습니다. 위에서 설명한 대로 ngrok를 설정한 후 [ngrok](https://developer.paypal.com/docs/checkout/apm/apple-pay/#link-registeryoursandboxdomains) URL을 사용하여 PayPal에 **샌드박스 도메인을 등록**&#x200B;합니다.

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

### 프로덕션에서 Apple Pay 테스트

프로덕션 모드에서 Apple 페이를 테스트하려면 [프로덕션 도메인을 등록](https://developer.paypal.com/docs/checkout/apm/apple-pay/#register-your-live-domain)해야 합니다.
