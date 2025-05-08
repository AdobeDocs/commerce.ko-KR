---
title: 신용 카드 보관
description: 구매자는 향후 구매를 위해 신용 카드 세부 정보를 저장(저장)할 수 있습니다.
exl-id: b4060307-ffcd-41cb-9b9d-a2fef02f23bd
feature: Payments, Checkout, Paas, Saas
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---

# 신용 카드 보관

신용 카드 소산을 통해 일회성 쇼핑객을 단골 고객으로 전환합니다. 로그인한 고객은 동일한 머천트 계정 내에서 나중에 동일한 또는 다른 머천트 계정의 구매에 사용할 신용 카드 자격 증명을 저장(또는 &quot;자격 증명 모음&quot;)할 수 있습니다.

## 보관 사용

가맹점은 [!DNL Payment Services] [설정](settings.md#card-vaulting)에서 가맹점에 대해 신용 카드 보관 기능을 사용할 수 있습니다.

1. _관리자_ 사이드바에서 **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**(으)로 이동합니다.

1. **[!UICONTROL Settings]**&#x200B;을(를) 클릭합니다.

1. **[!UICONTROL Vault enabled]** 선택기를 전환합니다. 자세한 내용은 [사용 [!DNL Payment Services]](settings.md#enable-payment-services)을 참조하세요.

## 구매 없이 보관

로그인한 고객은 **내 계정** 대시보드에서 다음 방법으로 결제 방법을 저장할 수 있습니다.

1. 상점 첫 화면에서 **내 계정**&#x200B;에 로그인하는 중입니다.

1. 저장된 결제 방법을 모두 보려면 왼쪽 탐색에서 **[!UICONTROL Stored Payment Methods]**(으)로 이동합니다.

   자세한 내용은 [저장된 결제 방법](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/payments/stored-payment-methods)을 참조하세요.

1. 고객이 **[!UICONTROL Add New Card]**&#x200B;을(를) 클릭하여 새 카드를 저장합니다.

   ![새 카드 추가](assets/add-new-card.png){width="400" zoomable="yes"}

   고객은 결제 방법을 보관하기 위해 카드 및 청구 정보 등 필요한 모든 세부 정보를 제공해야 합니다.
보관된 모든 결제 방법은 구매자의 PayPal 계정에 있는 카드를 보관하는 동안 청구 주소 세트를 사용합니다. 고객에게 Commerce에 표시된 청구 주소와 다른 청구 주소가 표시될 수 있습니다.

1. **[!UICONTROL Save New Card]** 클릭

   ![내 계정에 저장된 결제 방법](assets/stored-payment-methods.png){width="400" zoomable="yes"}

저장된 카드는 주문 시 사용할 수 있습니다.

![나중에 구입할 수 있도록 저장된 자격 증명 사용](assets/use-stored-card.png){width="400" zoomable="yes"}

### 저장된 결제 방법 삭제

고객은 특정 카드에 대해 **삭제**&#x200B;를 클릭하여 **내 계정**&#x200B;의 **저장된 결제 방법**&#x200B;에서 저장된 신용 카드를 쉽게 삭제할 수 있습니다.

## 체크아웃 중 결제 방법 저장

로그인한 고객은 체크아웃 중에 신용 카드를 보관하여 동일한 가맹점 계정 내의 현재 스토어 또는 다른 스토어에서 나중에 구매할 수 있습니다.

![나중에 사용할 수 있도록 신용 카드 저장](assets/save-card-for-later.png){width="400" zoomable="yes"}

Commerce은 고객이 저장된 신용 카드 정보를 가져와서 향후 체크아웃을 완료할 수 있도록 도와주는 토큰을 저장합니다. 고객 계정에서 또는 체크아웃 중에 카드를 보관하면 다른 결제 토큰이 생성됩니다.

>[!WARNING]
>
> PayPal은 현재 최대 5개의 저장된 카드를 저장할 수 있습니다.

## 관리자에서 보관 사용

고객이 이전에 저장된 신용 카드를 보유하고 있는 경우, 판매자는 관리자가 이러한 저장된 결제 방법을 사용하여 해당 고객에 대한 후속 주문을 생성할 수 있습니다.

고객이 기존 계정과 이전에 완료된 결제 후 시스템에 저장된 유효한 토큰이 모두 있는 경우에만 관리자의 저장된 카드를 사용할 수 있습니다.

저장된 신용 카드를 사용하는 고객을 위해 관리자에서 주문을 생성하려면:

1. [주문을 만들고 제품을 추가](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/point-of-purchase/assist/customer-account-create-order.html)합니다.
1. _[!UICONTROL Payment & Shipping Information]_에서&#x200B;**[!UICONTROL Stored Cards]**을(를) 결제 방법으로 선택합니다.
1. 원하는 저장된 신용 카드 결제 방법을 선택합니다.
1. 주문에 필요한 다른 단계를 완료한 후 [제출하세요](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/point-of-purchase/assist/customer-account-create-order.html?lang=en#step-3%3A-submit-the-order).

   ![고객을 위해 관리자의 저장된 신용 카드 사용](assets/admin-vaultedcard.png){width="600" zoomable="yes"}

## 보안

최소 신용 카드 정보는 쇼핑객과 공유됩니다. 쇼핑객은 저장한 신용 카드의 마지막 네 자리, 만료일 및 브랜드만 볼 수 있습니다. 신용 카드 정보는 [PCI](security.md#PCI-compliance) 준수 표준을 충족하도록 결제 공급자와 함께 저장됩니다.
