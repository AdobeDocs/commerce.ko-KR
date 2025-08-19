---
title: 보안 및 규정 준수
description: 사이트에 대한 보안 및 규정 준수 요구 사항을 검토합니다.
exl-id: 083c5a12-1d78-48b5-b9e3-612b104ce7e0
feature: Payments, Checkout, Compliance
redirect_from: https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/security.html?lang=ko
source-git-commit: 870c2497a2d6dcfc4066c07f20169fc9040ae81a
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 0%

---

# 보안 및 규정 준수

보안은 [!DNL Payment Services]에서 가장 중요한 사항이며 개인 또는 PCI(결제 카드 산업) 규제 정보가 [!DNL Payment Services]에 전달되지 않습니다.

## Commerce 보안

[!DNL Adobe Commerce] 및 [!DNL Magento Open Source]은(는) 여러 보안 기능을 지원합니다.

보안 모범 사례를 검토하고 관리 세션 및 자격 증명을 관리하고 CAPTCHA를 구현하며 웹 사이트 제한을 관리하는 방법에 대해 알아보려면 핵심 사용 안내서의 [보안](https://experienceleague.adobe.com/ko/docs/commerce-admin/systems/security/security){target="_blank"}을 참조하십시오.

## PCI 준수

PCI(Payment Card Industry)는 인터넷을 통해 신용 카드로 결제를 받는 사업자를 위한 일련의 요구 사항을 수립했습니다. 고객 신용카드 정보를 취급하는 가맹점은 안전한 환경 유지와 더불어 몇 가지 표준 가이드라인을 준수할 책임이 있다.

자세한 내용은 [PCI 준수 지침](https://experienceleague.adobe.com/ko/docs/commerce-admin/start/compliance/payments/compliance-pci){target="_blank"}을 참조하십시오.

가맹점은 카드 소지자 데이터에 대한 보안을 평가하는 자체 유효성 검사 도구인 [SAQ(자체 평가 설문)](https://www.pcisecuritystandards.org/pci_security/completing_self_assessment){target="_blank"}을(를) 완료할 수 있습니다.

### 신용 카드 필드

신용 카드 필드를 사용하면 PCI 규제 데이터가 서비스에 전달되지 않습니다. 이러한 데이터를 저장하거나 유지 관리할 필요가 없으므로 PCI 규정 준수에 대한 우려가 크게 줄어듭니다.

### 3DS

PCI 3D Secure(3DS)는 온라인 신용 카드 구매 시 신용 카드 발급자와 구매자 인증을 가능하게 합니다. 이러한 추가 보안 계층은 온라인 사기 행위를 방지하는 데 도움이 되며 유럽 연합(EU) 규정 준수 규칙의 일부로 필요합니다.

[!UICONTROL Payment Services]은(는) 가맹점이 EU 규정을 준수할 수 있도록 하고 고객 및 가맹점의 사기 행위로부터 고객을 보호할 수 있는 3DS 기능을 제공합니다.

EU 또는 영국 내에서 3DS 준수가 필요한 판매자인 경우 `Off`구성 관리자[에서 수동으로 3DS(기본적으로 ](configure-admin.md#credit-card-fields)임)를 켜야 합니다.

>[!IMPORTANT]
>
>3DS 요건은 회사 및 카드 소유자의 은행이 [유럽 경제 지역](https://www.efta.int/eea)&#x200B;(EEA) 및 영국에 있는 거래에 적용됩니다. 미국 상인은 3DS를 필요로 하지 않지만, 원할 경우 거래에 사용할 수 있습니다.

판매자/점포 직원이 구매자를 위해 발주한 주문은 3DS 준수 조치로 구성되지 않는다.

>[!MORELIKETHIS]
>
> * 자세한 내용은 [ 설정의 ](configure-admin.md#3ds)3DS를 참조하십시오.
> * 3DS 테스트를 위한 특정 신용 카드에 대한 자세한 내용은 PayPal 개발자 설명서에서 [테스트 카드](https://developer.paypal.com/docs/checkout/advanced/customize/3d-secure/test/)를 참조하십시오.

### 카드 보관

구매자가 매장에서 나중에 구매할 수 있도록 구매자의 신용 카드 정보를 [보관 또는 &quot;저장&quot;하면](vaulting.md) 구매자와 최소한의 신용 카드 정보(마지막 네 자리, 카드 만료일 및 카드 브랜드)가 공유됩니다. 신용 카드 정보는 결제 제공자와 함께 저장됩니다. 카드가 만료되거나 더 이상 정보를 저장할 필요가 없을 때, 결제 공급자가 정보를 더 이상 저장하지 않도록 해당 토큰을 삭제할 수 있습니다.

자세한 내용은 [신용 카드 보관](vaulting.md)을 참조하세요.

### PayPal 결제 단추

PayPal 결제 버튼을 사용하면 PCI 규제 데이터가 서비스에 전달되지 않습니다. 이러한 데이터를 저장하거나 유지 관리할 필요가 없으므로 PCI 규정 준수에 대한 우려가 크게 줄어듭니다.

보안상의 이유로 PayPal은 체크아웃 시 청구 주소를 전달하지 않습니다(국가, 이메일 및 이름 만이 사용되는 청구 정보임). PayPal에 연락하고 검사 프로세스를 완료하여 사이트의 PayPal 체크아웃이 전체 청구 주소를 반환하도록 선택적으로 활성화할 수 있습니다.

또한 PayPal은 머신 러닝을 사용하여 사기 행위를 방지하는 통합된 사기 방지 기능을 제공합니다. 자세한 내용은 PayPal의 [판매자 보호 설명서](https://www.paypal.com/us/webapps/mpp/security/seller-protection)를 참조하십시오.

## 사기 방지

[Signifyd 확장](https://commercemarketplace.adobe.com/signifyd-module-connect.html)을(를) 사용하여 결제 서비스에 대해 자동 사기 방지 기능을 사용할 수 있습니다. 자세한 내용은 [Signifyd 사기 방지](fraud-protection.md)를 참조하십시오.

PayPal은 개발자 설명서에서 [사기 방지](https://www.paypal.com/us/cshelp/article/what-is-fraud-protection-help1014){target=_blank}를 위한 다른 옵션을 제공합니다.

* 자세한 내용은 [사기 방지 고급](https://www.paypal.com/us/enterprise/fraud-protection-advanced#fraud-protection-advanced){target=_blank}을 참조하십시오.
* 자세한 내용은 [비용 산출 보호](https://www.paypal.com/us/cshelp/article/what-is-chargeback-protection-help608){target=_blank}를 참조하십시오.
