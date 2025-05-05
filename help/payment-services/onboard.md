---
title: 온보드 [!DNL Payment Services]
description: 몇 가지 온보딩 단계를 완료하여 인스턴스를  [!DNL Payment Services] 기능과 연결하십시오.
role: User
level: Intermediate
feature: Payments, Checkout, Integration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---

# [!DNL Payment Services] 온보드

[!DNL Adobe Commerce] 및 [!DNL Magento Open Source]에 대해 [!DNL Payment Services]을(를) 사용하려면 인스턴스를 결제 기능과 연결하는 몇 가지 온보딩 단계를 완료해야 합니다.

## 온보딩 플로우

이 흐름 다이어그램은 [!DNL Payment Services] 온보딩에 대한 일반 프로세스를 보여 줍니다.

![온보딩 흐름](assets/onboarding-diagram.svg){width="600" zoomable="yes"}

>[!NOTE]
>
> Adobe Commerce 버전 2.4.7 이상의 경우 [!DNL Payment Services]을(를) 즉시 사용할 수 있으므로 Marketplace 확장 단계를 건너뛸 수 있습니다.

샌드박스 또는 라이브 결제에 대한 온보딩을 완료한 후 관리자의 [!DNL Payment Services]에서 재무 보고에 액세스할 수 있습니다.

샌드박스 및 라이브 결제가 모두 온보딩되고 활성화된 경우 [!DNL Payment Services] 홈에서 이러한 모드 간에 쉽게 전환할 수 있습니다.

## 전제 조건

[!DNL Payment Services]을(를) 사용하려면 모든 종속 모듈이 활성화되어 있어야 하며 인스턴스에 대해 다음 항목을 사용할 수 있어야 합니다.

* 서비스 커넥터 모듈
* 서비스 ID 모듈
* API 키

서비스 커넥터 및 서비스 ID 모듈은 [설치 [!DNL Payment Services]](install.md) 중에 자동으로 설치됩니다.

설치가 완료되면 **[!UICONTROL Services]**—**[!UICONTROL Commerce Services Connector]**&#x200B;을(를) 확장하면 구성 설정(**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**)에 새 섹션이 표시됩니다.

API 키를 만들거나 액세스하는 방법에 대한 자세한 내용은 [API 자격 증명](#obtain-api-credentials)을 참조하세요.

## 온보딩 단계

1. [확장 설치 [!DNL Payment Services] 2&rbrace;.](install.md#get-payment-services)
1. [API 자격 증명 가져오기](connect.md#obtain-api-credentials).
1. Commerce 서비스에 [인스턴스 연결](connect.md#configure-commerce-services). 이 연결은 Commerce 인스턴스당 한 번만 완료되어야 합니다.
1. [PayPal 결제 처리 계정을 사용하여 샌드박스 서비스를 설정](sandbox.md#enable-sandbox-testing)(또는 다른 환경에서 기능을 테스트한 경우 [실시간 결제 활성화](sandbox.md#enable-live-payments))합니다.
1. 샌드박스 모드에서 테스트 결제 처리를 시작하려면 [결제 방법으로  [!DNL Payment Services] 설정](production.md#set-payment-services-as-payment-method)합니다.
1. [결제 권한을 요청](production.md#request-payments-entitlement-from-adobe)하여 실시간 온보딩을 사용하도록 설정하십시오.
1. [판매자 온보딩 완료](production.md#complete-merchant-onboarding)를 통해 Commerce 웹 사이트에 대한 실시간 결제를 사용할 수 있습니다.
1. [판매자 ID를  [!DNL Payment Services] 받은 후](production.md#configure-pricing-tier)영업팀에 제출하여 올바른 가격 책정 계층을 구성하세요.
1. [실시간 결제 처리를 시작하려면 [!DNL Payment Services] 실시간 모드에서 사용](production.md#enable-live-payments)하세요.
1. [샌드박스](sandbox.md#test-in-sandbox-environment) 및 [프로덕션](production.md#test-in-production) 환경 모두에서 결제를 테스트합니다.

>[!NOTE]
>
>관리자(3단계)에서 Commerce 서비스를 구성하지 않으면 샌드박스 또는 라이브 결제를 설정할 수 없습니다.

## 문제 해결

* [문제 해결 [!DNL Payment Services] 설치](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-install.html?lang=ko)
* [PayPal 샌드박스 계정이 확인되지 않음](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-paypal-acct.html?lang=ko)
* [지연 [!DNL Payment Services] 보고서 데이터](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-report-info-delayed.html?lang=ko)
* [샌드박스 환경에서 결제를 처리할 때 PayPal로 신용 카드 테스트 실패](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-cc-sandbox-failure.html?lang=ko)
