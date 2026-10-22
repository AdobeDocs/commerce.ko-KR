---
title: 마이그레이션 및 채택
description: Adobe Commerce Optimizer을 도입하거나, 기존 스토어프런트를 현대화하거나, Adobe Commerce as a Cloud Service으로 완전히 마이그레이션하는 경로에 대해 알아봅니다.
role: Admin, Developer, Leader
feature: Storefront, Integration, Configuration
recommendations: noCatalog
TQID: 'https://experienceleague.adobe.com/2iEJ6fA-wLr18bi9C8l-w3srx1AWlAtiGt1cG9RPv0Q'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
feature_v2:
  - id: 1783ae9f-7157-5aeb-a915-91e260301e46
    internal-label: Routes
  - id: 22bad240-8308-569b-a9d5-578f1ff890ca
    internal-label: Customers
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
  - id: 4067ab89-2e97-5de1-8d98-de8318461a8d
    internal-label: Products
  - id: 4820f335-ec9f-5611-8fe3-f5b7e3e56967
    internal-label: Orders
  - id: 4ca54350-01cb-5b22-8966-5f2873dc6d90
    internal-label: Media
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: 72863f3c-9d27-5dda-afe1-d9f934b1fba0
    internal-label: Extensibility
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
  - id: bcd8874c-7b93-5596-bdaa-22660e84df14
    internal-label: Deploy
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: d3b92bef-63fa-5031-a925-d04d9362d616
    internal-label: Saas
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: dec06508-d41f-555a-87e8-29e8bcdfa95a
    internal-label: Recommendations
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
source-git-commit: 4c3c267873a68560a885c6376cd1137a7503710a
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%
---

# 마이그레이션 및 채택

채택 시 한 번에 모든 플랫폼을 변경할 필요가 없습니다. 즉각적인 목표가 상점 현대화, 머천다이징 개선, 백엔드 현대화 또는 SaaS(Managed Software as a Service)로의 완전한 이동인지에 따라 경로를 선택합니다.

## 채택 경로

### 기존 Adobe Commerce 배포 현대화

- 기존 Commerce Foundation을 트랜잭션 백엔드로 유지합니다.
- [!DNL Edge Delivery Services]에서 제공하는 Commerce Storefront를 채택하십시오.
- Storefront Services, App Builder, API Mesh 및 선택적 AEM Assets 통합을 사용하십시오.

### Commerce Optimizer을 브리지로 사용

- [!DNL Adobe Commerce Optimizer Connector]을(를) 사용하여 [!DNL Adobe Commerce] 클라우드 또는 온-프레미스에 연결합니다.
- 머천다이징 서비스, 검색, 권장 사항 및 Edge Delivery Services 스토어를 채택하십시오.
- [!DNL Adobe Commerce]을(를) 제품, 가격, 카탈로그 구조, 장바구니, 체크아웃, 고객 및 주문에 대한 기본 기록 시스템으로 유지합니다.
- 이 아키텍처를 [!DNL Adobe Commerce as a Cloud Service]&#x200B;(으)로 전환할 수 있습니다.

### Adobe Commerce as a Cloud Service으로 완전히 마이그레이션

- 현재 애플리케이션, 사용자 정의, 통합, 상점 및 데이터를 평가합니다.
- SaaS 호환 확장성 패턴을 사용하여 맞춤화를 현대화합니다.
- 상점 및 통합을 재구축하거나 조정할 수 있습니다.
- 카탈로그, 고객, 주문, 구성 및 지원되는 사용자 지정 데이터를 마이그레이션하고 검증합니다.
- 새로운 SaaS 환경을 테스트, 컷오버 및 운영합니다.

### 독립형 Adobe Commerce Optimizer 채택

- 타사 Commerce 플랫폼, PIM, ERP 또는 기타 소스에서 카탈로그 및 가격 데이터를 수집합니다.
- 카탈로그 검색, 검색, 권장 사항 및 머천다이징에 [!DNL Adobe Commerce Optimizer] 머천다이징 서비스를 사용하십시오.
- [!DNL Edge Delivery Services]에서 제공하는 Commerce Storefront를 사용하십시오.
- 연결된 타사 시스템에서 장바구니, 체크아웃, 고객, 주문, 결제, 세금, 배송 및 이행 상태를 유지합니다.

## 권장 시퀀스

1. 현재 상태를 평가하고 시스템 소유권을 정의합니다.
1. API 우선 통합 경계를 설정합니다.
1. 상점 및 경험 레이어를 현대화합니다.
1. 머천다이징 서비스와 AEM Assets을 동시에 채택합니다.
1. 필요한 경우 Commerce Foundation을 마이그레이션합니다.
1. 유효성 검사, 잘라내기, 모니터링 및 최적화

## 관련 지침

- [Commerce 옵션 선택](../portfolio/choose-commerce-option.md)
- [아키텍처 옵션](../architecture-options/overview.md)
- [기존 상점 현대화](../implementation-guides/modernize-storefront.md)
- [Adobe Commerce Optimizer 활성화](../implementation-guides/enable-aco.md)
