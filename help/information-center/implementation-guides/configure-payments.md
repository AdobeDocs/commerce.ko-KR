---
title: 결제 구성
description: Adobe Commerce용 결제 서비스를 구성하여 여러 결제 방법을 지원하고 결제, 주문 및 송장에 대한 통합 대시보드를 지원하는 방법에 대해 알아봅니다.
role: Admin, Developer
feature: Configuration
recommendations: noCatalog
autotag-review: '2026-10-20T11:00:28.278Z'
TQID: 'https://experienceleague.adobe.com/egM9HoywqOQgL27ykw5SBdvoMHsmagYNoDMtNSLPds0'
product_v2:
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
  - id: 4820f335-ec9f-5611-8fe3-f5b7e3e56967
    internal-label: Orders
  - id: 591c578b-908e-5b79-a9d3-931dfe60c24c
    internal-label: Invoices
  - id: 6388cf7b-8a81-5248-a1e4-7bb57bbe250f
    internal-label: Install
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: ca6bb3543583c865c42b8f4d84f01e27a04f9223
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%
---

# 결제 구성

[!DNL Payment Services]에서는 고객에게 무이자 할부를 비롯한 여러 결제 방법을 제공하고 가맹점에게 결제, 주문 및 송장 관리를 위한 통합 대시보드를 제공합니다.

>[!NOTE]
>
>이 안내서는 Adobe Commerce(클라우드 또는 온프레미스), Adobe Commerce as a Cloud Service 또는 Magento Open Source이 트랜잭션을 처리하는 경우에 적용됩니다. Adobe Commerce Optimizer 프로젝트의 경우 트랜잭션 백엔드가 이러한 지원되는 플랫폼 중 하나인 경우에만 이 흐름을 따르십시오. 서드파티 백엔드가 트랜잭션을 처리하는 경우 대신 해당 백엔드의 결제 설정을 사용하십시오.

## 시작

1. [결제 서비스 호환성](https://experienceleague.adobe.com/ko/docs/commerce/payment-services/compatibility)에서 제품 버전 및 국가 가용성을 확인하세요.

1. [온보딩 결제 서비스 흐름](/help/payment-services/onboard.md)을 따르십시오.

1. Commerce on Cloud 또는 온-프레미스 인스턴스가 Commerce 서비스에 연결되어 있지 않은 경우 먼저 [Commerce 서비스를 설정](set-up-commerce-services.md)하세요.

## 관련 지침

- [결제 서비스 안내서 개요](/help/payment-services/guide-overview.md)
- [Commerce 서비스 설정](set-up-commerce-services.md)
