---
title: 결제 옵션
description: 스토어 고객이 사용할 수 있는 방법을 사용자 지정하려면 결제 옵션을 설정하십시오.
feature: Payments, Checkout, Configuration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '1174'
ht-degree: 0%

---

# 결제 옵션

[!DNL Adobe Commerce] 및 [!DNL Magento Open Source] [!DNL Payment Services]을(를) 사용하면 여러 결제 옵션을 사용할 수 있습니다.

[홈 설정](payments-home.md) 또는 [스토어 구성](configure-admin.md)에서 이러한 결제 옵션을 구성할 수 있습니다(레거시 결제 옵션 또는 다중 스토어 설정에 권장).

체크아웃 프로세스의 위치에 따라 각 결제 방법마다 다른 동작이 있습니다.

* 제품 페이지 - 항목에 대한 제품 페이지
* 미니 장바구니 - 제품이 장바구니에 추가되었을 때 장바구니 아이콘을 클릭하면 사용할 수 있습니다.
* 장바구니—미니 장바구니에서 _장바구니 보기 및 편집_&#x200B;을 클릭하면 사용할 수 있습니다.
* 체크아웃 보기—미니 장바구니 또는 장바구니에서 _체크아웃 진행_&#x200B;을 클릭하면 사용할 수 있습니다.

>[!IMPORTANT]
>
>결제를 처리하려면 [!DNL Payment Services] 온보딩을 완료해야 합니다.

## 표준 및 고급 결제 경험 비교

[!DNL Payment Services]은(는) 운영하는 국가에 따라 **고급**(전체 지원) 및 **표준**(빠른 체크아웃) 결제 옵션과 온보딩 흐름을 제공합니다.

* **고급** - 현재 [완전히 지원되는 국가](../payment-services/overview.md#availability)에서 사용 가능한 모든 [결제 옵션](../payment-services/payments-options.md)을 사용할 수 있습니다. 실시간 결제를 활성화하려면 온보딩 중에 [고급 온보딩 옵션](../payment-services/production.md#advanced-onboarding)을 선택하세요.
* **표준** - 일부 결제 옵션(빠른 체크아웃)(PayPal 신용 카드 및 직불 카드)은 사용 가능한 다른 지원 국가에서 사용할 수 있습니다. 이 온보딩 옵션에는 [신용 카드 필드](#credit-card-fields) 및 [Apple 결제](#apple-pay-button)를 사용할 수 없습니다. 실시간 결제를 사용하려면 온보딩 중에 [표준 온보딩 옵션](../payment-services/production.md#standard-onboarding)을 선택하세요.

고급 및 표준 온보딩 완료에 대한 자세한 내용은 [프로덕션에 대해  [!DNL Payment Services] 사용](../payment-services/production.md#complete-merchant-onboarding)을 참조하세요.

## [!UICONTROL Credit Card Fields]

[!UICONTROL Credit Card Fields]에서 신용 카드 또는 직불 카드 결제 방법을 간단하고 안전하게 체크아웃할 수 있습니다. 쇼핑객이 신용 카드 필드를 사용하여 체크아웃할 때 구매자의 이름, 청구 주소 및 신용 또는 직불 카드 정보를 입력하여 주문합니다. 고객 정보는 구매 세션 중에 안전하게 사용되어 체크아웃 흐름을 원활하게 안내합니다.

![체크아웃 중인 신용 카드 필드](assets/credit-card-fields.png){width="500" zoomable="yes"}

스토어에 대해 [신용 카드 보관](#vaulting)을 활성화하여 구매자가 나중에 빠른 체크아웃을 위해 신용 카드 정보를 보관(저장)할 수 있도록 합니다.

저장소 구성 또는 [!DNL Payment Services] 홈에서 [!UICONTROL Credit Card Fields]을(를) 구성할 수 있습니다. 자세한 내용은 [설정](settings.md#credit-card-fields)을 참조하세요.

신용 카드 필드의 레이아웃, 너비, 높이 및 외부 스타일을 변경할 수도 있습니다. 자세한 내용은 [PayPal 설명서](https://developer.paypal.com/docs/checkout/advanced/customize/card-field-style/)를 참조하세요.

## [!DNL Apple Pay] 단추

고객은 iOS 또는 macOS 장치에 저장된 신용 및 직불 카드 결제 자격 증명을 사용하는 [[!DNL Apple Pay]](https://www.apple.com/apple-pay/)을(를) 사용하여 구매할 수 있습니다.

[!DNL Apple Pay]은(는) Safari 브라우저에서만 사용할 수 있습니다. 가맹점은 가맹점 계좌당 최대 99개의 도메인을 추가할 수 있다.

미니카트의 ![Apple 결제 단추](assets/applepay-button.png){width="500" zoomable="yes"}

제품 페이지, 미니 장바구니, 장바구니 및 체크아웃 보기에서 [!DNL Apple Pay] 단추를 볼 수 있습니다.

스토어에 [!DNL Apple Pay]을(를) 사용하려면 [자가 등록 [!DNL Apple Pay]](https://developer.paypal.com/docs/checkout/apm/apple-pay/#register-your-live-domain)&#x200B;(_라이브 도메인 등록_ 섹션만 해당)을 완료하고 [스토어에 대해 구성 [!DNL Payment Services]](settings.md#payment-buttons)하세요.

>[!NOTE]
>
> 구매자가 사이트에서 Apple Pay로 결제할 수 있도록 하는 방법을 확인하려면 PayPal 개발자 설명서에서 [고급 체크아웃](https://www.paypal.com/us/cshelp/article/what-is-paypal-advanced-checkout-and-how-do-i-get-started-help953){target=_blank}을 참조하십시오.

저장소 구성 또는 결제 서비스 홈에서 [!UICONTROL Apple Pay]을(를) 구성할 수 있습니다. 자세한 내용은 [설정](settings.md#apple-pay)을 참조하세요.

## [!DNL Google Pay] 단추

고객은 원활한 체크아웃 환경을 위해 안전하게 저장되는 Google 계정에 결제 세부 정보를 추가하여 [[!DNL Google Pay]](https://pay.google.com/about/)을(를) 사용할 수 있습니다.

[!DNL Google Pay]은(는) 특정 국가 또는 지역 및 특정 장치에서만 사용할 수 있습니다. 자세한 내용은 [[!DNL Google Pay] 설명서](https://developer.paypal.com/docs/checkout/apm/google-pay/#link-googlepayintegration)를 참조하세요.

![체크아웃의 Google 결제 단추](assets/google-pay-button.png){width="500" zoomable="yes"}

제품 페이지, 미니 장바구니, 장바구니 및 체크아웃 보기에서 [!DNL Google Pay] 단추를 볼 수 있습니다.

저장소 구성 또는 결제 서비스 홈에서 [!UICONTROL Google Pay]을(를) 구성할 수 있습니다. 자세한 내용은 [설정](configure-admin.md)을 참조하세요.

>[!NOTE]
>
> [!DNL Google Pay] API는 보안 컨텍스트의 웹 사이트에서만 사용할 수 있습니다. 자세한 내용은 [문제 해결](https://developers.google.com/pay/api/web/support/troubleshooting) 설명서를 참조하십시오.

## [!DNL PayPal Payment Buttons]

[!DNL PayPal payment buttons]: PayPal을 사용하여 구매를 완료하고 나중에 사용할 수 있도록 구매자의 배송 주소, 청구 주소 및 결제 세부 정보를 저장합니다. 쇼핑객은 PayPal에서 이전에 저장하거나 제공하는 결제 방법을 사용할 수 있습니다.

![PayPal 단추](assets/paypal-button.png){width="350" zoomable="yes"}

저장소 구성 또는 [!DNL Payment Services] 홈에서 [!UICONTROL PayPal payment buttons]을(를) 구성할 수 있습니다. 자세한 내용은 [설정](settings.md#payment-buttons)을 참조하세요.

PayPal의 [결제 방법 설명서](https://developer.paypal.com/docs/checkout/payment-methods/)에서 국가별 결제 방법의 사용 가능 여부에 대해 알아보세요.

### [!DNL PayPal] 단추

고객은 PayPal 버튼을 사용하여 쉽고 안전하게 체크아웃할 수 있습니다.

제품 페이지, 미니 장바구니, 장바구니 및 체크아웃 보기에서 [!DNL PayPal] 단추를 볼 수 있습니다.

### [!DNL Venmo] 단추

고객은 [Venmo](https://venmo.com/) 버튼을 사용하여 체크아웃할 수 있습니다.

제품 페이지, 미니 장바구니, 장바구니 및 체크아웃 보기에서 [!DNL Venmo] 단추를 볼 수 있습니다.

### PayPal 직불 또는 신용카드 단추

고객은 PayPal 직불 또는 신용카드 버튼을 사용하여 체크아웃할 수 있습니다.

PayPal 직불 또는 신용 카드 버튼은 체크아웃 페이지에서 볼 수 있습니다.

이 옵션은 신용카드 통합에 대한 대안으로 PayPal 호스팅 버튼을 사용하여 구매자에게 직불 또는 신용카드 결제 옵션을 제공하는 데 사용할 수 있습니다.

### [!DNL Pay Later] 단추

고객에게 단기, 무이자 결제 및 기타 금융 옵션을 제공하여 지금 구입하고 나중에 [!DNL Pay Later] 버튼을 사용하여 결제할 수 있도록 하십시오.

제품 페이지, 미니 장바구니, 장바구니 및 체크아웃 보기에서 [!DNL Pay Later] 단추를 볼 수 있습니다.

[PayPal의 나중에 결제 방법 설명서](https://developer.paypal.com/docs/checkout/pay-later/us/)에서 나중에 결제 방법에 대한 정보를 확인하세요. **국가 또는 지역** 드롭다운을 사용하여 관심 지역을 선택하십시오.

[설정](settings.md#payment-buttons) 구성을 업데이트하여 [!DNL Pay Later] 메시지를 사용하지 않도록 설정하거나 사용하도록 설정하는 방법에 대해 알아봅니다.

## PayPal 결제 버튼만 사용

스토어를 프로덕션 모드로 빠르게 전환하려면 _only_ PayPal 결제 버튼(Venmo, PayPal 등)을 구성할 수 있습니다.—PayPal 신용카드 결제 옵션을 사용하지 않습니다.

이를 통해 다음을 수행할 수 있습니다.

* Venmo 및 PayPal 결제 버튼을 포함하여 고객을 위한 다양한 결제 옵션을 제공하고, PayPal 호스팅 카드 필드를 끄고 기존 신용카드 제공업체를 사용할 수 있는 옵션을 제공합니다.
* PayPal의 기타 결제 옵션을 사용하면서 신용 카드 결제를 위해 기존 신용카드 제공업체를 이용하십시오.
* PayPal이 신용 카드를 지원하지 않는 지역의 PayPal 결제 버튼을 결제 옵션으로 사용합니다.

**PayPal 결제 버튼(_PayPal 신용카드 결제 옵션 없음_)을 사용하여 _전용_으로 결제 캡처**:

1. 스토어가 [프로덕션 모드](settings.md#enable-payment-services)에 있는지 확인하십시오.
1. 설정에서 [원하는 PayPal 결제 단추를 구성하십시오](settings.md#payment-buttons).
1. _[!UICONTROL Payment buttons]_&#x200B;섹션에서&#x200B;**[[!UICONTROL Show PayPal Credit and Debit card button]](settings.md#payment-buttons)**&#x200B;옵션을_&#x200B;끄기&#x200B;_합니다.

**기존 신용 카드 공급자 _및_ PayPal 결제 단추**&#x200B;로 결제를 캡처하려면:

1. 스토어가 [프로덕션 모드](settings.md#enable-payment-services)에 있는지 확인하십시오.
1. [원하는 PayPal 결제 단추를 구성하십시오](settings.md#payment-buttons).
1. _[!UICONTROL Payment buttons]_&#x200B;섹션에서&#x200B;**[[!UICONTROL PayPal Show Credit and Debit card button]](settings.md#payment-buttons)**&#x200B;옵션을_&#x200B;끄기&#x200B;_합니다.
1. _[!UICONTROL Credit card fields]_&#x200B;섹션에서&#x200B;**[[!UICONTROL Show on checkout page]](settings.md#credit-card-fields)**&#x200B;옵션을_&#x200B;해제&#x200B;_하고 [기존 신용 카드 공급자 계정](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/payments/payments.html?lang=ko#payments)을 사용하세요.

## 주문 다시 계산

고객이 미니 장바구니, 장바구니 또는 제품 페이지에서 체크아웃 플로우를 입력하면 PayPal 팝업 창에서 선택한 배송 주소를 볼 수 있는 주문 검토 페이지로 이동합니다. 고객이 배송 방법을 선택한 후 주문 금액이 적절하게 재계산되어 배송비와 세금을 볼 수 있습니다.

고객이 체크아웃 페이지에서 체크아웃 플로우를 입력하면 시스템에서 배송 주소와 최종 계산된 금액을 이미 알고 있으며 합계가 적절히 표시됩니다.

납세의무자, 운송비, 판매세는 장소마다 매우 다양할 수 있다. [!DNL Payment Services]이(가) 배송 주소와 요금을 받은 후 적용 가능한 모든 비용을 빠르게 다시 계산하고 마지막 체크아웃 단계에서 적절하게 표시합니다.

## 신용 카드 보관

구매자는 웹 사이트 수준(동일한 가맹점 계정 내 모든 매장)에서 향후 구매를 위해 신용 카드 정보를 저장(저장)할 수 있습니다.

자세한 내용은 [신용 카드 보관](vaulting.md)을 참조하세요.

## 보안

자세한 내용은 [PCI 규정 준수](security.md#pci-compliance)를 참조하십시오.
