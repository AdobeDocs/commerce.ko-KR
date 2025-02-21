---
title: 상당한 사기 방지
description: Signifyd를 사용하여  [!DNL Payment Services] 에 대한 자동 사기 방지 기능을 활성화합니다.
role: Admin, User
level: Intermediate
feature: Payments, Checkout, Configuration, Security
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---

# 상당한 사기 방지

[Signifyd 확장](https://commercemarketplace.adobe.com/signifyd-module-connect.html)을(를) 사용하여 [!DNL Payment Services]에 대해 자동 사기 방지 기능을 활성화할 수 있습니다.

Adobe Commerce은 Signifyd 버전 5.4.0 이상을 지원합니다. [!DNL Payment Services]은(는) 사전 인증 및 사후 인증 Signifyd 흐름을 지원합니다.

Signifyd/[!DNL Payment Services] 통합은 신용 카드, 직불 카드, 저장된 카드, 관리자를 통한 체크아웃, PayPal 및 Apple Pay 결제 방법에 대한 적용 범위를 제공합니다. 일부 거래 세부 사항이 결제 서비스와 Signifyd 간에 공유되지 않는 반면 Signifyd는 모든 결제 방법에 대해 포괄적인 위험 범위를 제공하여 최대한 보호를 보장합니다.

확장 설치 및 구성에 대한 자세한 내용은 [Signifyd 설명서](https://community.signifyd.com/support/s/article/magento-2-extension-install-guide?language=en_US#downloadandinstallingmagento2extension)를 참조하십시오.

## 온보딩

[!DNL Payment Services]과(와) 함께 사용하기 위해 확장을 온보딩하려면 Signifyd와 직접 통신해야 합니다. [!DNL Payment Services] 구성이 필요하지 않습니다. 설치 후 관리자에서 Signifyd 확장을 구성할 수 있습니다. 이 확장과 관련된 모든 지원은 Signifyd에서 관리합니다.

Signifyd로 온보딩할 때 다음을 수행해야 합니다.

1. 새 계정을 설정하려면 Signifyd에 문의하십시오.
1. 기본적으로 Signifyd는 현재 지원하지 않는 다른 결제 옵션에 대해 트리거되지 않도록 [허용 목록에추가된](https://github.com/signifyd/magento2/blob/main/docs/RESTRICT-PAYMENTS.md)입니다. 특정 지불 방법을 금지하려면 변경해야 합니다.
1. Paypal이 Paypal에서 승인할 수 있는 상인의 사기 방지 설정을 통해 Signifyd에 의해 주문을 거부하지 않을 것인지 확인하십시오.
1. [!DNL Payment Services]과(와) 호환되도록 Signifyd 확장을 활성화하십시오.
   * _Live_ 모드에서 [!DNL Payment Services]을(를) 사용하는 경우 Signifyd는 프로덕션 모드여야 합니다.
   * _샌드박스_ 모드에서 [!DNL Payment Services]을(를) 사용하는 경우 Signifyd는 테스트 모드여야 합니다.

## 구성

Signifyd는 주문에 대해 일부 조치를 취하므로 [!DNL Payment Services]에 대해 설정한 결제 조치를 기반으로 적절하게 작동하도록 확장을 구성해야 합니다.

이러한 구성 옵션은 결제 서비스 및 Signifyd 통합과 호환되지 않습니다.

* [!DNL Payment Services]이(가) `Authorize` 결제 작업 _과(와)_(으)로 구성된 경우 _[!UICONTROL Decline Guarantees]_옵션이&#x200B;**신용 메모 만들기**(으)로 설정된 Signifyd는 `PostAuth` 모드에 있습니다.

  이유: [!DNL Payment Services]에서 Signify가 환불을 시도하는 인증 트랜잭션을 만듭니다.


* [!DNL Payment Services]이(가) `Authorize and Capture` 결제 동작 _을(를) 사용하여 구성되었습니다._ Signifyd는 `PostAuth` 모드에 있습니다. _[!UICONTROL Decline Guarantees]_옵션은&#x200B;**주문 취소**(으)로 설정되어 있습니다.

  이유: [!DNL Payment Services]은(는) Signifyd가 무효화하려고 시도하는 캡처 트랜잭션을 만듭니다.


[확장 구성](https://community.signifyd.com/support/s/article/magento-2-extension-install-guide?language=en_US#configuringmagento2extension)에 대한 자세한 내용은 Signifyd 설명서를 참조하십시오.

[주문 워크플로우에 대해 자세히 알아보기](https://community.signifyd.com/support/s/article/magento-2-extension-install-guide?language=en_US#howmagento2works)하려면 Signifyd 설명서를 참조하십시오.
