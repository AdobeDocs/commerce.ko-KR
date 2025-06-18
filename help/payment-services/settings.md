---
title: 결제 서비스 설정
description: 설치 후 홈에서  [!DNL Payment Services] 을(를) 구성할 수 있습니다.
role: Admin, User
level: Intermediate
exl-id: 108f2b24-39c1-4c87-8deb-d82ee1c24d55
feature: Payments, Checkout, Configuration, Paas, Saas
source-git-commit: 9e7eb509aa19f3382d36221ac0c7dcf2130e8d8d
workflow-type: tm+mt
source-wordcount: '2420'
ht-degree: 0%

---

# 설정

[!DNL Payment Services] 홈에서 유용한 설정을 사용하여 필요에 맞게 [!DNL Payment Services]을(를) 사용자 지정할 수 있습니다.

[!DNL Adobe Commerce] 및 [!DNL Magento Open Source]에 대해 [!DNL Payment Services]을(를) 구성하려면 **[!UICONTROL Settings]**&#x200B;을(를) 클릭하십시오. 이러한 구성 옵션은 [_일반_ 구성 옵션](#configure-general-settings)의 _[!UICONTROL Payment mode]_필드에 설정된 환경에만 적용됩니다.

다중 스토어 또는 레거시 구성에 대해서는 [관리에서 구성](configure-admin.md)을 참조하십시오.

## 일반 설정 구성

[!UICONTROL General] 설정은 결제 방법으로 결제 서비스를 사용하거나 사용하지 않도록 설정하고 고객 거래에 정보를 추가하여 웹 사이트 또는 스토어 보기를 사용자 지정 정보로 표시하거나 접두하는 기능을 제공합니다.

### 결제 서비스 활성화

웹 사이트에 대해 [!DNL Payment Services]을(를) 사용하도록 설정하고 샌드박스 테스트 또는 라이브 결제를 사용하도록 설정할 수 있습니다.

1. _관리자_ 사이드바에서 **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**(으)로 이동합니다.

1. **[!UICONTROL Settings]**&#x200B;을(를) 클릭합니다. 자세한 내용은 [소개 [!DNL Payment Services] 홈](payments-home.md)을 참조하세요.

   ![React 설정 보기](assets/react-settings-view.png){width="500" zoomable="yes"}

   _[!UICONTROL General]_섹션에는 [!DNL Payment Services]을(를) 결제 방법으로 활성화하는 데 사용되는 설정이 포함되어 있습니다.

1. 스토어의 결제 방법으로 [!DNL Payment Services]을(를) 사용하려면 _[!UICONTROL General]_섹션에서&#x200B;**[!UICONTROL Enable Payment Services as payment method]**을(를) `Yes`(으)로 전환합니다.

1. 스토어에 대해 [!DNL Payment Services]을(를) 계속 테스트하는 경우 **결제 모드**&#x200B;를 `Sandbox`(으)로 설정하십시오. 실시간 결제를 사용할 준비가 되었으면 `Production`(으)로 설정하십시오.

1. [Commerce 서비스 커넥터](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/user-guides/integration-services/saas){target=_blank}를 설정하고 [!DNL Payment Services] 대시보드를 처음 방문하면 **[!UICONTROL Payment Services Sandbox ID]** 및 **[!UICONTROL Payment Services Production ID]** 값이 자동으로 채워집니다. 이렇게 하여 샌드박스 및/또는 프로덕션 환경에 대한 온보딩을 완료합니다. 이 값은 SaaS ID를 [!DNL Payment Services]에 연결합니다.

   >[!WARNING]
   >
   > [!DNL Payment Services] ID를 재설정하는 경우 다시 온보딩해야 합니다.

1. **[!UICONTROL Save]**&#x200B;을(를) 클릭합니다.

   변경 내용을 저장하지 않고 이 보기에서 나가려고 하면 변경 내용을 취소하거나, 편집을 유지하거나, 변경 내용을 저장하라는 모달이 나타납니다.

1. 잘못된 모든 캐시를 새로 고치려면 **[!UICONTROL System]** > **[!UICONTROL Cache Management]**(으)로 이동하고 **[!UICONTROL Flush Cache]**&#x200B;을(를) 클릭합니다.

이제 [결제 옵션](#configure-payment-options) 기능 및 상점 표시에 대한 기본 설정을 계속 변경할 수 있습니다.

### 소프트 설명자 추가

웹 사이트 또는 개별 스토어 보기에 [!UICONTROL Soft Descriptor]을(를) 추가할 수 있습니다. 고객 거래 은행 거래 명세서에 소프트 설명자가 표시됩니다. 예를 들어 여러 상점/브랜드/카탈로그가 있는 경우 [!UICONTROL Soft Descriptor] 필드에 사용자 지정 텍스트를 추가하여 이러한 상점/브랜드/카탈로그를 쉽게 구분할 수 있습니다.

1. _관리자_ 사이드바에서 **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**(으)로 이동합니다.
1. **[!UICONTROL Settings]**&#x200B;을(를) 클릭합니다. 자세한 내용은 [소개 [!DNL Payment Services] 홈](payments-home.md)을 참조하세요.
1. **[!UICONTROL Scope]** 드롭다운 메뉴에서 소프트 설명자를 만들 웹 사이트 또는 스토어 보기를 선택합니다. 초기 설정의 경우 기본값을 설정하려면 이 항목을 **[!UICONTROL Default]**(으)로 둡니다.
1. 텍스트 필드에 사용자 지정 텍스트(최대 22자)를 추가하여 `Soft descriptor`을(를) 바꿉니다.
1. **[!UICONTROL Save]**&#x200B;을(를) 클릭합니다.
1. 웹 사이트 또는 스토어 보기에 대해 구성된 기본값 이외의 소프트 설명자를 만들려면 다음 작업을 수행하십시오.
   1. **[!UICONTROL Scope]** 드롭다운 메뉴에서 소프트 설명자를 만들 웹 사이트 또는 스토어 보기를 선택합니다.
   1. _끄기_ **[!UICONTROL Use website]**(또는 선택한 범위에 따라 **[!UICONTROL Use default]**)를 전환합니다.
   1. 텍스트 필드에 사용자 정의 텍스트를 추가합니다.
   1. **[!UICONTROL Save]**&#x200B;을(를) 클릭합니다.
1. 웹 사이트 또는 스토어에 대해 활성화하려면 상위 웹 사이트에 사용되는 기본 소프트 설명자 _또는_&#x200B;을(를) 봅니다.
   1. **[!UICONTROL Scope]** 드롭다운 메뉴에서 기존 소프트 설명자를 활성화할 웹 사이트 또는 스토어 보기를 선택합니다.
   1. _on_ **[!UICONTROL Use website]**(또는 선택한 범위에 따라 **[!UICONTROL Use default]**)을(를) 전환합니다.
   1. **[!UICONTROL Save]**&#x200B;을(를) 클릭합니다.

   변경 내용을 저장하지 않고 이 보기에서 나가려고 하면 변경 내용을 취소하거나, 편집을 유지하거나, 변경 내용을 저장하라는 모달이 나타납니다.

### 구성 옵션

| 필드 | 범위 | 설명 |
|---|---|---|
| [!UICONTROL Enable] | 웹 사이트 | 웹 사이트에 대해 [!DNL Payment Services]을(를) 활성화하거나 비활성화합니다. 옵션: [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Payment mode] | 스토어 뷰 | 스토어에 대한 메서드 또는 환경을 설정합니다. 옵션: [!UICONTROL Sandbox] / [!UICONTROL Production] |
| [!UICONTROL Payment Services Sandbox ID] | 스토어 뷰 | 샌드박스 온보딩 중 자동으로 생성되는 샌드박스 판매자 ID입니다. |
| [!UICONTROL Payment Services Production ID] | 스토어 뷰 | 프로덕션(라이브) 온보딩 중에 자동으로 생성되는 프로덕션 판매자 ID입니다. |
| [!UICONTROL Soft Descriptor] | 웹 사이트 또는 스토어 보기 | 웹 사이트 및 스토어 보기에 부드러운 설명자를 추가하여 브랜드, 스토어 또는 제품 라인을 설명하는 고객 거래에 정보를 추가합니다. [!UICONTROL Use website] 전환은 웹 사이트 수준에서 추가된 모든 소프트 설명자를 적용합니다. [!UICONTROL Use default] 전환은 기본값으로 추가된 모든 소프트 설명자를 적용합니다. |

## 결제 옵션 구성

웹 사이트에 대해 [!UICONTROL Payment Services]을(를) 활성화했으므로 이제 결제 기능 및 상점 표시에 대한 기본 설정을 변경할 수 있습니다.

1. _관리자_ 사이드바에서 **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**(으)로 이동합니다.
1. **[!UICONTROL Settings]**&#x200B;을(를) 클릭합니다. 자세한 내용은 [소개 [!DNL Payment Services] 홈](payments-home.md)을 참조하세요.
1. 다음 섹션에 따라 [신용 카드](#credit-card-fields), [결제 단추](#payment-buttons) 및 [단추 스타일](#button-style)에 대한 결제 옵션을 구성하십시오.

### 신용 카드 필드

_[!UICONTROL Credit Card Fields]_설정은 신용 카드 또는 직불 카드 결제 방법을 위한 간단하고 안전한 체크아웃 옵션을 제공합니다.

자세한 내용은 [결제 옵션](payments-options.md#credit-card-fields)을 참조하세요.

1. _관리자_ 사이드바에서 **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**(으)로 이동합니다.
1. **[!UICONTROL Scope]** 드롭다운 메뉴에서 결제 방법을 사용할 스토어 보기를 선택합니다.
1. **[!UICONTROL Credit card fields]** 섹션에서 **[!UICONTROL Checkout title]** 필드의 값을 편집하여 체크아웃 중에 표시되는 결제 방법 이름을 변경합니다.
1. [결제 작업을 설정](production.md#set-payment-services-as-payment-method)하려면 **[!UICONTROL Payment action]**&#x200B;을(를) `Authorize` 또는 `Authorize and Capture`(으)로 전환하십시오.
1. 체크아웃 페이지에서 결제 방법의 우선 순위를 지정하려면 **[!UICONTROL Sort order]** 필드에 `Numeric Only` 값을 입력하십시오.
1. [3DS 보안 인증을 사용하려면](security.md#3ds)(`Off`(기본값) **[!UICONTROL 3DS Secure authentication]** 선택기를 `Always` 또는 `When required`(으)로 전환합니다.
1. 체크아웃 페이지에서 신용 카드 필드를 활성화하거나 비활성화하려면 **[!UICONTROL Show on checkout page]** 선택기를 전환하십시오.
1. [카드 보관](#card-vaulting)을 활성화하거나 비활성화하려면 **[!UICONTROL Vault enabled]** 선택기를 전환하십시오.
1. [관리자](#card-vaulting)에서 보관된 결제 방법을 사용하거나 사용하지 않도록 설정하려면(가맹점이 보관된 결제 방법을 사용하여 관리자 고객에 대한 주문을 완료할 수 있도록) **[!UICONTROL Show vaulted methods in Admin]** 선택기를 전환하십시오.
1. 디버그 모드를 활성화하거나 비활성화하려면 **[!UICONTROL Debug Mode]** 선택기를 전환합니다.
1. **[!UICONTROL Save]**&#x200B;을(를) 클릭합니다.

   변경 내용을 저장하지 않고 이 보기에서 나가려고 하면 변경 내용을 취소하거나, 편집을 유지하거나, 변경 내용을 저장하라는 모달이 나타납니다.

1. [캐시를 플러시합니다](#flush-the-cache).

#### 구성 옵션

| 필드 | 범위 | 설명 |
|---|---|---|
| [!UICONTROL Title] | 스토어 뷰 | 체크아웃 중에 결제 방법 보기에서 이 결제 방법의 제목으로 표시할 텍스트를 추가합니다. 옵션: [!UICONTROL text field] |
| [!UICONTROL Payment Action] | 웹 사이트 | 지정한 결제 방법에 대한 [결제 작업](https://experienceleague.adobe.com/en/docs/commerce-admin/config/sales/payment-methods/payment-methods#payment-actions){target="_blank"}. 옵션: [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Sort order] | 스토어 뷰 | 체크아웃 페이지에서 지정된 결제 방법에 대한 정렬 순서. `Numeric Only` 값 |
| [!UICONTROL 3DS Secure authentication] | 웹 사이트 | [3DS 보안 인증을 사용하거나 사용하지 않도록 설정](security.md#3ds). 옵션: [!UICONTROL Always] / [!UICONTROL When Required] / [!UICONTROL Off] |
| [!UICONTROL Show on checkout page] | 웹 사이트 | 신용 카드 필드가 체크아웃 페이지에 표시되도록 활성화하거나 비활성화합니다. 옵션: [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Vault enabled] | 스토어 뷰 | [신용 카드 보관](vaulting.md)을 활성화하거나 비활성화합니다. 옵션: [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show vaulted payment methods in Admin] | 스토어 뷰 | 판매자가 관리자 [저장된 결제 방법을 사용하여](vaulting.md)에서 고객에 대한 주문을 완료할 수 있는 기능을 활성화하거나 비활성화합니다. 옵션: [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Debug Mode] | 웹 사이트 | 디버그 모드를 활성화하거나 비활성화합니다. 옵션: [!UICONTROL Off] / [!UICONTROL On] |

### Apple 페이

[!UICONTROL Apple Pay] 버튼 결제 옵션을 사용하면 Safari 브라우저에서 매장 체크아웃에 [!UICONTROL Apple Pay] 결제 버튼을 제공할 수 있습니다(가맹점 계정당 최대 99개 도메인).

Paypal을 통해 [Apple Pay 자체 등록을 완료](https://developer.paypal.com/docs/checkout/apm/apple-pay/#register-your-live-domain)한 다음 스토어에 대해 [Apple Pay 구성](settings.md/#payment-buttons)한 경우에만 Apple Pay를 사용할 수 있습니다.

자세한 내용은 [결제 옵션](payments-options.md#apple-pay-button)을 참조하세요.

[!UICONTROL Apple Pay] 단추 결제 옵션을 활성화하고 구성할 수 있습니다.

1. _관리자_ 사이드바에서 **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**(으)로 이동합니다.
1. **[!UICONTROL Scope]** 드롭다운 메뉴에서 결제 방법을 사용할 스토어 보기를 선택합니다.
1. **[!UICONTROL Apple Pay]** 섹션에서 _[!UICONTROL Checkout title]_필드의 값을 편집하여 체크아웃 중에 표시되는 결제 방법 이름을 변경합니다.
1. [결제 작업을 설정](production.md#set-payment-services-as-payment-method)하려면 **[!UICONTROL Payment action]**&#x200B;을(를) `Authorize` 또는 `Authorize and Capture`(으)로 전환하십시오.
1. 체크아웃 페이지에서 Apple Pay를 활성화하거나 비활성화하려면 **[!UICONTROL Show Apple Pay on checkout page]** 선택기를 전환하십시오.
1. 제품 세부 사항 페이지에서 Apple Pay를 활성화하거나 비활성화하려면 **[!UICONTROL Show Apple Pay on product detail page]** 선택기를 전환하십시오.
1. 미니 장바구니 미리 보기에서 Apple Pay를 활성화하거나 비활성화하려면 **[!UICONTROL Show Apple Pay on the mini cart preview]** 선택기를 전환합니다.
1. 장바구니 페이지에서 Apple Pay를 활성화하거나 비활성화하려면 **[!UICONTROL Show Apple Pay on cart page]** 선택기를 전환하십시오.
1. 디버그 모드를 활성화하거나 비활성화하려면 **[!UICONTROL Debug Mode]** 선택기를 전환합니다.
1. **[!UICONTROL Save]**&#x200B;을(를) 클릭합니다.

   변경 내용을 저장하지 않고 이 보기에서 나가려고 하면 변경 내용을 취소하거나, 편집을 유지하거나, 변경 내용을 저장하라는 모달이 나타납니다.

1. [캐시를 플러시합니다](#flush-the-cache).

#### 구성 옵션

| 필드 | 범위 | 설명 |
|---|---|---|
| [!UICONTROL Checkout title] | 스토어 뷰 | 체크아웃 중에 결제 방법 보기에서 이 결제 방법의 제목으로 표시할 텍스트를 추가합니다. 옵션: [!UICONTROL text field] |
| [!UICONTROL Payment Action] | 웹 사이트 | 지정한 결제 방법에 대한 [결제 작업](https://experienceleague.adobe.com/en/docs/commerce-admin/config/sales/payment-methods/payment-methods#payment-actions). 옵션: [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Show on checkout page] | 웹 사이트 | 체크아웃 페이지에 표시할 Apple 결제 버튼을 활성화하거나 비활성화합니다. 옵션: [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show on checkout page] | 웹 사이트 | 제품 세부 사항 페이지에 표시할 Apple 결제 버튼을 활성화하거나 비활성화합니다. 옵션: [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show on mini cart preview] | 웹 사이트 | 미니 장바구니 미리 보기에 표시할 Apple 결제 버튼을 활성화하거나 비활성화합니다. 옵션: [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show on cart page] | 웹 사이트 | Apple 결제 버튼이 장바구니 페이지에 표시되도록 활성화하거나 비활성화합니다. 옵션: [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Debug Mode] | 웹 사이트 | 디버그 모드를 활성화하거나 비활성화합니다. 옵션: [!UICONTROL Off] / [!UICONTROL On] |

### 결제 버튼

[!DNL PayPal payment buttons] 결제 옵션은 고객에게 간단하고 빠르고 안전한 체크아웃 프로세스를 제공합니다. 자세한 내용은 [결제 옵션](payments-options.md#paypal-smart-buttons)을 참조하세요.

PayPal 결제 버튼 결제 옵션을 활성화하고 구성할 수 있습니다.

1. **[!UICONTROL Scope]** 드롭다운 메뉴에서 결제 방법을 사용할 스토어 보기를 선택합니다.
1. 결제 방법 이름을 변경하려면 **[!UICONTROL Checkout Title]** 필드에서 값을 편집합니다.
1. [결제 작업을 설정](production.md#set-payment-services-as-payment-method)하려면 **[!UICONTROL Payment action]**&#x200B;을(를) `Authorize` 또는 `Authorize and Capture`(으)로 전환하십시오.
1. 체크아웃 페이지에서 결제 방법의 우선 순위를 지정하려면 **[!UICONTROL Sort order]** 필드에 `Numeric Only` 값을 입력하십시오.
1. 전환 선택기를 사용하여 [!DNL PayPal smart button] 표시 기능을 활성화하거나 비활성화하십시오.

   - **[!UICONTROL Show PayPal buttons on product checkout page]**
   - **[!UICONTROL Show PayPal buttons on product detail page]**
   - **[!UICONTROL Show PayPal buttons in mini-cart preview]**
   - **[!UICONTROL Show PayPal buttons on cart page]**
   - **[!UICONTROL Show PayPal Pay Later button]**
   - **[!UICONTROL Show PayPal Pay Later message]**
   - **[!UICONTROL Show Venmo button]**
   - **[!UICONTROL Show Apple Pay button]**
   - **[!UICONTROL Show PayPal Credit and Debit Card button]**

     >[!NOTE]
     >
     > Apple Pay를 사용하려면 [Apple 샌드박스 테스터 계정](https://developer.apple.com/apple-pay/sandbox-testing/#create-a-sandbox-tester-account)이 있어야 합니다(가짜 신용 카드 및 청구 정보와 함께 완료). 샌드박스 _또는_ 프로덕션 모드에서 Apple Pay를 사용할 준비가 되면 [테스트 및 유효성 검사](test-validate.md#test-in-sandbox-environment)를 완료한 후 [다음  [!DNL Apple Pay]](https://developer.paypal.com/docs/checkout/apm/apple-pay/#register-your-live-domain)&#x200B;(으)로 자가 등록&#x200B;_라이브 도메인 등록_ 섹션만 해당)을 완료하고 [다음 저장소에 맞게 구성합니다 [!DNL Payment Services]](settings.md#payment-buttons).

     가시성을 결제 버튼 또는 PayPal 나중에 결제 메시지로 전환하면 설정 페이지 하단에 해당 구성의 시각적 미리보기가 표시됩니다.

1. 디버그 모드를 사용하려면 **[!UICONTROL Debug Mode]** 선택기를 전환합니다.
1. **[!UICONTROL Save]**&#x200B;을(를) 클릭합니다.

   변경 내용을 저장하지 않고 이 보기에서 나가려고 하면 변경 내용을 취소하거나, 편집을 유지하거나, 변경 내용을 저장하라는 모달이 나타납니다.

1. [캐시를 플러시합니다](#flush-the-cache).

#### 구성 옵션

| 필드 | 범위 | 설명 |
|---|---|---|
| [!UICONTROL Title] | 스토어 뷰 | 체크아웃 중에 결제 방법 보기에서 이 결제 방법의 제목으로 표시할 텍스트를 추가합니다. 옵션: 텍스트 필드 |
| [!UICONTROL Payment Action] | 웹 사이트 | 지정한 결제 방법에 대한 [결제 작업](https://experienceleague.adobe.com/en/docs/commerce-admin/config/sales/payment-methods/payment-methods#payment-actions){target="_blank"}. 옵션: [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Sort order] | 스토어 뷰 | 체크아웃 페이지에서 지정된 결제 방법에 대한 정렬 순서. `Numeric Only` 값 |
| [!UICONTROL Show PayPal buttons on checkout page] | 스토어 뷰 | 체크아웃 페이지에서 [!DNL PayPal payment buttons]을(를) 활성화하거나 비활성화합니다. 옵션: [!UICONTROL  Yes] / [!UICONTROL No] |
| [!UICONTROL Show PayPal buttons on product detail page] | 스토어 뷰 | 제품 세부 정보 페이지에서 [!DNL PayPal payment buttons]을(를) 활성화하거나 비활성화합니다. 옵션: [!UICONTROL  Yes] / [!UICONTROL No] |
| [!UICONTROL Show PayPal buttons in mini-cart preview] | 스토어 뷰 | 미니 장바구니 미리 보기에서 [!DNL PayPal payment buttons]을(를) 활성화하거나 비활성화합니다. 옵션: [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show PayPal buttons on cart page] | 스토어 뷰 | 장바구니 페이지에서 [!DNL PayPal payment buttons]을(를) 사용하거나 사용하지 않도록 설정합니다. 옵션: [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show PayPal Pay Later button] | 스토어 뷰 | 지급 버튼이 표시되는 나중에 지급 옵션 표시를 활성화하거나 비활성화합니다. 옵션: [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show PayPal Pay Later Message] | 웹 사이트 | 장바구니, 제품 페이지, 미니 장바구니에서, 그리고 체크아웃 흐름 동안 나중에 결제 메시지를 활성화하거나 비활성화합니다. 옵션: [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show Venmo button] | 스토어 뷰 | 결제 버튼이 표시되는 Venmo 결제 옵션을 활성화하거나 비활성화합니다. 옵션: [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show Apple Pay button] | 스토어 뷰 | 결제 버튼이 표시되는 Apple 결제 옵션을 활성화하거나 비활성화합니다. 옵션: [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show PayPal Credit and Debit card button] | 스토어 뷰 | 결제 버튼이 표시되는 신용 및 직불 카드 결제 옵션을 활성화하거나 비활성화합니다. 옵션: [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Debug Mode] | 웹 사이트 | 디버그 모드를 활성화하거나 비활성화합니다. 옵션: [!UICONTROL Off] / [!UICONTROL On] |

### 단추 스타일

결제 버튼의 _[!UICONTROL Button style]_옵션을 구성할 수도 있습니다.

1. **[!UICONTROL Layout]**&#x200B;을(를) 변경하려면 `Vertical` 또는 `Horizontal`을(를) 선택하십시오.

   >[!NOTE]
   >
   > 단추 스타일이 `Horizontal`(으)로 구성되어 있고 매장이 여러 결제 단추를 표시하도록 구성된 경우 제품 페이지, 체크아웃 페이지 및 미니 카트에 단추 두 개와 장바구니에 단추 한 개만 표시될 수 있습니다.

1. 가로 레이아웃에서 태그 라인을 활성화하려면 **[!UICONTROL Show tagline]** 선택기를 전환합니다.
1. **[!UICONTROL Color]**&#x200B;을(를) 수정하려면 원하는 색상 옵션을 선택합니다.
1. **[!UICONTROL Shape]**&#x200B;을(를) 수정하려면 `Pill` 또는 `Rectangle`을(를) 선택하십시오.
1. 단추 높이 선택기를 사용하려면 **[!UICONTROL Responsive button height]** 선택기를 전환합니다.
1. **[!UICONTROL Label]**&#x200B;을(를) 수정하려면 원하는 레이블 옵션을 선택합니다.

   레이아웃, 색상, 모양, 높이 및 레이블에 대한 구성 옵션을 변경하면 설정 페이지 하단에 해당 구성의 시각적 미리보기가 표시됩니다. 아래 이미지에서 **[!UICONTROL Shape]**&#x200B;은(는) _Rectangle_(으)로 설정되고 **[!UICONTROL Label]**&#x200B;은(는) _PayPal(권장)_(으)로 설정됩니다.

   ![[!DNL PayPal payment buttons]개 옵션](assets/payment-buttons.png){width="400" zoomable="yes"}

1. **[!UICONTROL Save]**&#x200B;을(를) 클릭합니다.

   변경 내용을 저장하지 않고 이 보기에서 나가려고 하면 변경 내용을 취소하거나, 편집을 유지하거나, 변경 내용을 저장하라는 모달이 나타납니다.

1. [캐시를 플러시합니다](#flush-the-cache).

관리자](configure-admin.md#configure-paypal-smart-buttons) 또는 여기 [!DNL Payment Services Home]의 레거시 구성에서 결제 단추 스타일 [을(를) 구성할 수 있습니다. PayPal 결제 단추 스타일에 대한 자세한 내용은 [PayPal의 단추 스타일 가이드](https://developer.paypal.com/docs/checkout/standard/customize/buttons-style-guide/)를 참조하세요.

#### 구성 옵션

| 필드 | 범위 | 설명 |
|--- |--- |--- |
| [!UICONTROL Layout] | 스토어 뷰 | 결제 버튼에 대한 레이아웃 스타일을 정의합니다. 옵션: [!UICONTROL Vertical] / [!UICONTROL Horizontal] |
| [!UICONTROL Tagline] | 스토어 뷰 | 태그 라인 활성화/비활성화. 옵션: [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Color] | 스토어 뷰 | 결제 버튼의 색상을 정의합니다. 옵션: [!UICONTROL Blue] / [!UICONTROL Gold] / [!UICONTROL Silver] / [!UICONTROL White] / [!UICONTROL Black] |
| [!UICONTROL Shape] | 스토어 뷰 | 결제 버튼의 모양을 정의합니다. 옵션: [!UICONTROL Rectangular] / [!UICONTROL Pill] |
| [!UICONTROL Responsive Button Height] | 스토어 뷰 | 결제 단추에서 기본 높이를 사용하는지 여부를 정의합니다. 옵션: [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Height] | 스토어 뷰 | 결제 버튼의 높이를 정의합니다. 기본값: 없음 |
| [!UICONTROL Label] | 스토어 뷰 | 결제 버튼에 표시되는 레이블을 정의합니다. 옵션: [!UICONTROL PayPal] / [!UICONTROL Checkout] / [!UICONTROL Buynow] / [!UICONTROL Pay] / [!UICONTROL Installment] |

## 역할 구성

관리자 사용자가 Commerce 관리에서 주문을 만들고 관리할 수 있도록 하려면 사용자 역할에 [!DNL Payment Services]별 리소스를 사용하도록 설정하십시오.

역할을 관리하는 방법은 [사용자 역할](https://experienceleague.adobe.com/docs/commerce-admin/systems/user-accounts/permissions-user-roles.html)을 참조하세요.

역할에 리소스를 할당할 때 다음을 선택해야 합니다.

- **결제 방법:[!DNL Payment Services]**—이 리소스는 관리자에서 주문을 만들 때 결제 방법으로 [!DNL Payment Services]개의 신용 카드를 사용할 수 있도록 합니다. **Actions** 상위 리소스를 선택하면 이 리소스도 선택됩니다.
- **[!DNL Payment Services]**—이 리소스에는 **대시보드** 및 **SaaS 서비스 프록시** 리소스가 포함되어 있으며, 이 리소스도 선택해야 합니다. [!DNL Payment Services]이(가) _판매_ 메뉴에 나타나는지 확인합니다.

  ![결제 서비스 리소스](assets/roles-payments.png){width="400" zoomable="yes"}

## 캐시 초기화

Apple Pay, Venmo 또는 PayPal PayLater 단추를 전환하는 등 _설정_&#x200B;에서 구성을 변경하는 경우 저장소에 최신 구성이 표시되도록 캐시를 수동으로 플러시하십시오.

1. _관리자_ 사이드바에서 **[!UICONTROL System]** > **[!UICONTROL Cache Management]**(으)로 이동합니다.
1. 잘못된 모든 캐시를 새로 고치려면 **[!UICONTROL Flush Cache]**&#x200B;을(를) 클릭합니다.

캐시 관리 테이블의 캐시 유형이 `INVALIDATED` 상태인 경우 저장소에 해당 항목에 대한 최신 구성이 표시되지 않을 수 있습니다. 최신 구성을 표시하도록 저장소를 업데이트하려면 캐시를 플러시하십시오.

저장소에 올바른 구성이 표시되는지 확인하려면 주기적으로 [캐시를 플러시](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/cache-management)합니다.

## 카드 보관

고객이 향후 구매를 위해 사용할 신용 카드 정보를 내 계정에 저장(저장)할 수 있는 기능을 활성화할 수 있습니다.

또한 관리자의 카드 보관을 사용하여 기존 고객에 대한 후속 주문을 완료할 수 있습니다.

[신용 카드 필드 설정](#credit-card-fields)에서 카드 보관을 활성화하거나 비활성화합니다.

자세한 내용은 [신용 카드 보관](vaulting.md)을 참조하세요.

## 3DS

3DS는 고객 및 상인의 매장 내 사기 행위를 방지하고 유럽 연합(EU) 표준을 준수할 수 있도록 해줍니다.

[신용 카드 필드 설정](#credit-card-fields)에서 3DS를 활성화하거나 비활성화합니다.

자세한 내용은 [보안의 3DS](security.md#3ds)를 참조하십시오.

## 여러 PayPal 계정 사용

[!UICONTROL Payment Services]에서 웹 사이트 수준의 **one** 판매자 계정 내에서 여러 PayPal 계정을 사용할 수 있습니다. 예를 들어, 여러 국가([다양한 통화](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/currency/currency) 사용)에서 스토어를 운영하거나 비즈니스의 일부에 Adobe Commerce을 사용하려고 하지만 _모두_&#x200B;는 사용하지 않으려는 경우, 판매자 계정을 설정하여 여러 PayPal 계정을 사용할 수 있습니다.

웹 사이트, 스토어 및 스토어 보기의 계층 구조에 대한 자세한 내용은 [사이트, 스토어 및 보기 범위](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html)를 참조하십시오.

CLI를 통해 여러 PayPal 계정에 대한 범위를 구성하는 방법에 대한 자세한 내용은 [명령줄 구성](configure-cli.md#configure-scope-via-cli)을 참조하십시오.

영업 사원은 판매자 계정에 대한 새 [scope](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html#scope-settings)을(를) 만들고 PayPal로 추가 사이트를 온보딩하여 표시되는 PayPal 단추가 사이트에 표시되도록 할 수 있습니다. 웹 사이트에서 여러 PayPal 계정을 사용하는 데 도움이 필요하면 영업 담당자에게 문의하십시오.
