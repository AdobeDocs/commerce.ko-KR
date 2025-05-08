---
title: ' [!DNL Payment Services]에 대한 호환성'
description: ' [!DNL Payment Services] 이(가) 해당 국가에서 사용 가능한지, 그리고 해당 버전이 Adobe Commerce 버전과 호환되는지 알아봅니다.'
role: User
level: Intermediate
feature: Payments, Checkout, Paas, Saas
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 0%

---


# [!DNL Payment Services]에 대한 호환성

[!DNL Payment Services]은(는) Adobe Commerce 및 Magento Open Source에서 사용할 수 있습니다. [!DNL Payment Services]은(는) 이제 Adobe Commerce 버전 2.4.x와 호환됩니다.

## 사전 요구 사항

[!DNL Payment Services]을(를) 사용하려면 먼저 Commerce 인스턴스에 연결해야 합니다. **이 연결을 한 번만 설정했습니다**.

1. 인스턴스가 연결되어 있는지 확실하지 않은 경우 **시스템** > 서비스 > **Commerce 서비스 커넥터**(으)로 이동하여 샌드박스 키 및 프로덕션 키 섹션의 공개 및 개인 API 키 값과 SaaS 식별자 섹션의 프로젝트 및 데이터 공간 필드를 확인하십시오. 해당 값이 있으면 인스턴스가 연결됩니다.

1. 인스턴스를 계속 연결해야 하는 경우 [Commerce 서비스 커넥터](../landing/saas.md) 페이지에서 지침을 확인하십시오.

   >[!TIP]
   >
   > 자세한 내용은 [Adobe Commerce 서비스 커넥터](https://experienceleague.adobe.com/ko/docs/commerce-learn/tutorials/admin/adobe-commerce-services/configure-adobe-commerce-services-connector) 튜토리얼 비디오를 참조하십시오.

1. 인스턴스를 이미 연결한 경우 다음 단계를 위해 [온보딩](onboard.md) 페이지로 이동하십시오.

>[!IMPORTANT]
>
> [!DNL Payment Services]의 권한이 있는 모든 판매자는 **하나의 프로덕션 데이터 공간** 및 **두 개의 테스트 데이터 공간**&#x200B;을 사용할 수 있습니다.

## 표준 및 고급 [!DNL Payment Services] 경험 비교

[!DNL Payment Services]은(는) 운영하는 국가에 따라 **표준**(빠른 체크아웃) 및 **고급**(전체 지원) 결제 옵션 및 온보딩 흐름을 제공합니다.

>[!NOTE]
>
> [!DNL Payment Services]은(는) 온보딩 중 [&#128279;](../payment-services/production.md#complete-merchant-onboarding)사용 가능한 다른 국가에 대해 [빠른 체크아웃 기능](../payment-services/payments-options.md)(결제 옵션 하위 집합)을 제공합니다.

### 어떤 [!DNL Payment Services] 옵션이 적합합니까?

>[!VIDEO](https://video.tv.adobe.com/v/3447811)

[!DNL Payment Services] 확장 설정에 대한 자세한 내용은 [연결](connect.md)을 참조하세요.

>[!BEGINTABS]

>[!TAB 표준(빠른 체크아웃)]

![확인](assets/icon-check.png) PayPal 체크아웃

![확인](assets/icon-check.png) PayPal 직불 또는 신용 카드 단추

![확인](assets/icon-check.png) 사용자 지정 체크 아웃 구성

![확인](assets/icon-check.png) 표준 가격

![확인](assets/icon-check.png) **XX 국가에서 사용 가능**

[![자세히 알아보기](assets/learn-more-button.svg)](onboard.md)

>[!TAB 고급(전체 지원)]

직불 카드 ![확인](assets/icon-check.png)

![확인](assets/icon-check.png) PayPal 크레딧

신용 카드 필드 ![확인](assets/icon-check.png)

![확인](assets/icon-check.png) Apple 결제 단추

![확인](assets/icon-check.png) Google 결제 단추

![확인](assets/icon-check.png) PayPal 결제 단추

![확인](assets/icon-check.png) 벤 단추

![확인](assets/icon-check.png) PayPal 직불 또는 신용 카드 단추

![확인](assets/icon-check.png) 나중에 결제 단추

![확인](assets/icon-check.png) 사용자 지정 체크 아웃 구성

![확인](assets/icon-check.png) 사용자 지정 가격

![확인](assets/icon-check.png)(L2/L3 가격 기능 - 미국만 해당)

![확인](assets/icon-check.png) **미국(미국), 캐나다(CA), 호주(호주)에서만 사용 가능. 프랑스(FR), 영국(UK)**

[![자세히 알아보기](assets/learn-more-button.svg)](onboard.md)

>[!ENDTABS]

릴리스 및 버전별 정보는 [라이프사이클 정책](https://experienceleague.adobe.com/docs/commerce-operations/release/planning/lifecycle-policy.html?lang=ko) 및 [[!DNL Payment Services] 릴리스 정보](release-notes.md) 페이지를 참조하세요.

전체 지침을 받고 온보딩 프로세스를 시작하려면 [시작하기 [!DNL Payment Services]](onboard.md)를 참조하세요.

### 허용된 신용 카드 및 통화

[!DNL Payment Services]은(는) [ 사용 가능한 국가의 통화를 수락합니다](#availability). 환율 설정에 대한 자세한 내용은 [통화 구성](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/site-store/currency/currency-configuration.html?lang=ko)을 참조하십시오.

PayPal 제품 및 서비스에서 사용할 수 있는 통화 및 결제 방법에 대한 자세한 내용은 다음 페이지를 참조하십시오.

* [지원되는 통화 설명서](https://developer.paypal.com/docs/reports/reference/paypal-supported-currencies/).

* [결제 방법 설명서](https://developer.paypal.com/docs/checkout/payment-methods/).
