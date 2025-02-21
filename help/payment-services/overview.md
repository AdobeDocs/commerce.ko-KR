---
title: ' [!DNL Payment Services] 소개'
description: ' [!DNL Adobe Commerce] 및 [!DNL Magento Open Source]  웹 사이트를 위한 턴키로서  [!DNL Payment Services] 강력하고 안전한 결제 처리 솔루션을 설치하고 사용하는 방법에 대해 알아봅니다.'
role: User
level: Intermediate
feature: Payments, Checkout
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---

# [!DNL Payment Services] 소개

[!DNL Adobe Commerce] 및 [!DNL Magento Open Source]의 [!DNL Payment Services]은(는) Commerce 웹 사이트에 강력하고 안전한 결제 처리를 제공하기 위한 샌드박스 테스트 및 간단한 설정을 포함한 턴키 셀프 서비스 솔루션입니다.

중소기업, 미드마켓 경쟁사, 대기업 등 어디에 있든 이 결제 솔루션을 사용하면 운영 비용을 절감하고 수익을 증대할 수 있을 뿐만 아니라 전체 구매자 경험을 향상시킬 수 있는 유용한 도구를 제공할 수 있습니다.

[!DNL Payment Services]:

* 간편한 설치 및 유지 관리
* 귀사의 수익을 극대화하도록 설계
* 안전하고 안전하
* 모든 결제 요구 사항을 충족하도록 설계
* 관리자 내에 자체 포함

## 기능

>[!NOTE]
>
>여기에 언급된 기능 중 일부는 GA(General Availability) 릴리스에서 아직 제공되지 않을 수 있습니다.

[!DNL Payment Services]은(는) 온라인 체크아웃(결제 및 환불부터 결제까지)을 위한 원스톱 샵입니다. 구매자에게 최상의 경험을 제공하기 위해 필요한 통찰력과 컨트롤을 제공하는 강력한 도구를 제공합니다.

* [**온보딩**](onboard.md) - 이 프로세스는 상업 등록, 기술 구성, 권한, 샌드박스 환경 구성 및 라이브 결제 활성화를 안내합니다.
* [**결제 옵션**](payments-options.md)—스토어(또는 여러 스토어) 고객이 사용할 수 있는 방법을 사용자 지정하려면 결제 옵션을 설정합니다.
* **현금 흐름 관리 재무 보고** - [결제 세부 정보](order-payment-status.md)를 주문과 동기화하여 처리된 거래량, 결제 잔액, [결제](payouts.md) 및 세부 [거래 수준 보고](transactions.md)를 통해 재무 조정 및 거래 가시성을 최대한 확보합니다.
* **투명한 가격 책정**—가격은 명확하고 선결적입니다. 현재 표시되는 값은 다음과 같습니다.
* **효율적인 체크아웃 환경** - [카드 보관](vaulting.md) 및 [즉시 구매](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/point-of-purchase/checkout-instant-purchase.html)&#x200B;(Adobe Commerce의 경우 기본적으로 활성화됨) 기능을 사용하여 빠르고 간단한 체크아웃에 대한 장벽을 제거하고 단골 고객을 만드십시오.

## 가용성

[!DNL Payment Services]은(는) [!DNL Adobe Commerce] 및 [!DNL Magento Open Source]에 사용할 수 있습니다. [!DNL Payment Services] 확장은 [!DNL Adobe Commerce] 버전 2.4.4 - 2.4.7-p3과 호환됩니다.

현재 [!DNL Payment Services]은(는) 다음 국가의 모든 결제 옵션에 대한 전체 지원([고급 온보딩](../payment-services/production.md#advanced-onboarding)을 통해)을 제공합니다.

* 미국 (US)
* 캐나다 (CA)
* 오스트레일리아(호주)
* 프랑스 (FR)
* 영국 (UK)

결제 서비스는 온보딩 중 [사용 가능한 다른 국가에 대해 [빠른 체크아웃 기능](../payment-services/payments-options.md)(결제 옵션 하위 집합)을 제공합니다](../payment-services/production.md#complete-merchant-onboarding).

릴리스 및 버전별 정보는 [라이프사이클 정책](https://experienceleague.adobe.com/docs/commerce-operations/release/planning/lifecycle-policy.html) 및 [[!DNL Payment Services] 릴리스 정보](release-notes.md) 페이지를 참조하십시오.

### 허용된 신용 카드 및 통화

[!DNL Payment Services]은(는) [ 사용 가능한 국가의 통화를 수락합니다](#availability). 자세한 내용은 [통화 구성](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/site-store/currency/currency-configuration.html)을 참조하세요.

PayPal이 지원하는 통화를 확인하려면 [지원되는 통화 설명서](https://developer.paypal.com/docs/reports/reference/paypal-supported-currencies/)를 참조하세요.

PayPal이 지원하는 결제 방법을 보려면 해당 [결제 방법 설명서](https://developer.paypal.com/docs/checkout/payment-methods/)를 참조하세요.

## 시작하기

[!DNL Payment Services] 온보딩 및 설정이 몇 단계만 거치면 완료됩니다.

1. [[!DNL Payment Services] 확장](install.md)을 가져옵니다.
1. Commerce 인스턴스를 Commerce 서비스에 연결합니다.
1. 샌드박스 서비스를 온보딩하고 설정합니다.
1. 결제 방법으로 [!DNL Payment Services]을(를) 사용하도록 설정하고 테스트 결제 처리를 시작합니다.
1. 판매자 온보딩을 완료하여 웹 사이트에 대한 실시간 결제를 활성화하십시오.
1. [!DNL Payment Services]을(를) 실시간 결제 모드로 활성화하여 실시간 결제 처리를 시작합니다.

전체 지침을 받고 온보딩 프로세스를 시작하려면 [온보딩 [!DNL Payment Services]](onboard.md)을 참조하세요.

## [!DNL Payment Services] 데모

[!DNL Payment Services]에 대해 알아보려면 이 비디오 보기:

>[!VIDEO](https://video.tv.adobe.com/v/343990?quality=12)
