---
title: Adobe Commerce 제품 솔루션
description: 핵심 상거래, Adobe Commerce Optimizer, Adobe Commerce as a Cloud Service 및 Commerce 서비스를 포함한 Adobe Commerce 제품 포트폴리오에 대해 알아봅니다.
role: Admin, Developer, Leader, User
feature: Storefront, Integration, Configuration
recommendations: noCatalog
autotag-review: '2026-10-20T01:12:06.064Z'
TQID: 'https://experienceleague.adobe.com/R3Cp6MuHJDY-7Dv6DbML0qvVutxrwyQe66I-I9FGgQ4'
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
  - id: 00451af3-7b97-5414-9992-3a6c269e413f
    internal-label: Paas
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
  - id: 4273989f-0bf2-5361-a17a-6909488d18ab
    internal-label: Catalog Service
  - id: 4820f335-ec9f-5611-8fe3-f5b7e3e56967
    internal-label: Orders
  - id: 4ca54350-01cb-5b22-8966-5f2873dc6d90
    internal-label: Media
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: 591c578b-908e-5b79-a9d3-931dfe60c24c
    internal-label: Invoices
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: 6388cf7b-8a81-5248-a1e4-7bb57bbe250f
    internal-label: Install
  - id: 72863f3c-9d27-5dda-afe1-d9f934b1fba0
    internal-label: Extensibility
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
  - id: adedf70c-c1e1-5734-acdc-c5c43b114964
    internal-label: Release Notes
  - id: bcd8874c-7b93-5596-bdaa-22660e84df14
    internal-label: Deploy
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: cc250cf1-34eb-4863-80d0-d170d45ea067
    internal-label: Developer tools
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
subfeature_v2:
  - id: a1d22079-48b9-5e69-9ee6-eb236068ef34
    internal-label: Search
  - id: a743e5dc-8f37-4b5d-a848-03c32ca30598
    internal-label: App Builder
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
    internal-label: Customer experience
source-git-commit: 4c3c267873a68560a885c6376cd1137a7503710a
workflow-type: tm+mt
source-wordcount: '1130'
ht-degree: 0%
---

# Adobe Commerce 플랫폼 및 서비스 살펴보기

완전한 상거래 플랫폼이 필요하든, 호스팅과 운영 방법을 선택하든, 기존 상거래 백엔드와 함께 상점 및 카탈로그 기능을 원하든 관계없이 Adobe Commerce은 사용자의 요구 사항에 맞는 옵션을 제공합니다. 사람이 주도하고 무제한 쇼핑 여정 전반에서 Adobe Commerce은 AI 기반 제품 검색, 번개처럼 빠른 상점 전면, 한 번의 클릭으로 체크아웃을 수행함으로써 브랜드가 전환율과 평균 주문 가치를 높일 수 있도록 지원합니다. 이 개요에서는 핵심 오퍼링을 비교하고 이를 확장하는 서비스 및 개발자 도구를 소개하여 시작점을 식별하고 구현에 적합한 기능을 확인하는 데 도움이 됩니다.

각 서비스마다 제공되는 서비스는 다양합니다. 구현을 계획할 때 특정 제품 및 배포 모델에 대한 설명서를 검토하십시오.

## Commerce 제공

### B2C 및 B2B 상거래

Adobe Commerce은 단일 Commerce 인스턴스의 두 모델을 모두 포함하여 B2C 및 B2B 비즈니스 모델을 모두 지원합니다. [Adobe Commerce B2B 소개](https://experienceleague.adobe.com/ko/docs/commerce-admin/b2b/introduction)

B2B 기능은 제공에 따라 다릅니다. Adobe Commerce 온 클라우드 인프라 및 온프레미스의 경우 Adobe Commerce B2B는 별도의 라이선스와 설치가 필요한 확장 프로그램입니다. Adobe Commerce as a Cloud Service에는 기본적으로 회사 관리 및 견적 처리와 같은 핵심 B2B 기능이 포함되어 있습니다. [Adobe Commerce B2B](https://experienceleague.adobe.com/ko/docs/commerce-admin/start/resources/extensions)을(를) 참조하십시오.

### Adobe Commerce as a Cloud Service

Adobe Commerce as a Cloud Service은 완전히 관리되는 클라우드 기반의 SaaS(Software as a Service) 서비스입니다. Adobe은 핵심 Commerce 애플리케이션, 인프라 및 업데이트를 관리합니다. 구성 요소에는 Commerce Foundation, Edge Delivery Services에서 제공하는 Commerce Storefront, 머천다이징 서비스, 제품 시각화 및 개발자 도구가 포함됩니다.

[Adobe Commerce as a Cloud Service 개요](https://experienceleague.adobe.com/ko/docs/commerce/cloud-service/overview)를 참조하세요.

### Adobe Commerce Optimizer

Adobe Commerce Optimizer은 상점, 카탈로그, 제품 검색 및 머천다이징 경험을 개선하기 위한 SaaS 솔루션입니다. 기존 Adobe Commerce 또는 서드파티 상거래 백엔드와 함께 작동하므로 조직은 트랜잭션을 관리하는 시스템을 교체하지 않고도 고객 경험을 현대화할 수 있습니다.

Adobe Commerce Optimizer은 서드파티 소스에서 카탈로그 데이터를 수집할 수 있습니다. 서드파티 시스템과의 장바구니 및 체크아웃 통합은 API Mesh 및 App Builder과 같은 통합 도구를 사용합니다.

[Adobe Commerce Optimizer이란?](https://experienceleague.adobe.com/ko/docs/commerce/optimizer/overview)을(를) 참조하십시오.

>[!NOTE]
>
>Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer은 현재 서로 통합되지 않습니다. 구현을 계획할 때 이를 별도의 아키텍처 옵션으로 처리합니다.

### Adobe Commerce 온-프레미스

Adobe Commerce 온프레미스는 판매자 또는 호스팅 공급자가 호스팅합니다. 판매자 또는 제공자는 호스팅 환경, 인프라 및 플랫폼 서비스를 관리한다.

[온-프레미스 설치 개요](https://experienceleague.adobe.com/ko/docs/commerce-operations/installation-guide/overview)를 참조하세요.

### 클라우드 인프라의 Adobe Commerce

클라우드 인프라의 Adobe Commerce은 PaaS(Platform as a Service) 배포입니다. Adobe은 호스팅된 플랫폼을 관리하는 반면, 판매자는 애플리케이션 수준 유지 관리, 사용자 지정 코드, 구성 및 기타 공유 책임 작업에 대한 책임을 유지합니다.

[클라우드 인프라의 Commerce](https://experienceleague.adobe.com/ko/docs/commerce-on-cloud/user-guide/overview) 및 [Adobe Commerce as a Cloud Service으로 마이그레이션](https://experienceleague.adobe.com/ko/docs/commerce/cloud-service/migration/overview)을 참조하십시오.

## Commerce을 확장하는 서비스

### 상점 및 머천다이징 서비스

storefront 및 제품 경험을 위한 Adobe Commerce 서비스는 다음과 같습니다.

- **[Edge Delivery Services에서 제공하는 Commerce Storefront](https://experienceleague.adobe.com/en/tools/commerce-storefront/merchants/quick-start/create-content/)**—고객 응대 상거래 경험을 구축하기 위한 Storefront 옵션입니다.
- **[Storefront Services](/help/landing/home.md)**—최적화된 카탈로그 액세스, AI 기반 검색 및 제품 추천, 결제 처리를 위한 Storefront API 및 서비스를 지원하는 Adobe Commerce용 클라우드 제공 SaaS 기능([!DNL Adobe Commerce on cloud infrastructure] 및 [!DNL Adobe Commerce as a Cloud Service] 포함)을 통해 판매자가 쇼핑 경험, 성능 및 전환을 개선할 수 있도록 지원합니다
  - 카탈로그 서비스 - 최적화된 제품 카탈로그 경험과 상점 성능을 지원합니다.
  - 라이브 검색 - AI 기반 제품 검색을 제공합니다.
  - 제품 권장 사항 - 구매자 동작, 트렌드 및 제품 유사성을 기반으로 권장 사항을 제공합니다.
- **[Commerce Optimizer 머천다이징 서비스](/help/optimizer/overview.md)** - 최적화된 카탈로그 액세스, 관련 검색 결과 및 개인화된 제품 권장 사항을 통해 카탈로그 데이터와 AI를 사용하여 제품 검색을 개선하는 Cloud on Cloud 및 Adobe Commerce as a Cloud Service의 클라우드 제공 API 우선 기능으로, 쇼핑객이 제품을 찾고 더 나은 상점 성능과 전환을 지원하는 데 도움이 됩니다.
  - **제품 시각화** - Adobe Experience Manager Assets 통합을 통해 제품 이미지 및 미디어를 지원합니다.

### 결제

**결제 서비스**&#x200B;에서는 결제 방법 및 결제 처리, 주문 및 송장에 대한 보기를 제공합니다. 사용 가능 여부는 Commerce 제품 및 배포에 따라 다릅니다.

[결제 서비스](https://experienceleague.adobe.com/ko/docs/commerce/payment-services/guide-overview)를 참조하세요.

### 데이터 및 통합 서비스

Commerce에는 플랫폼 연결 및 데이터 동기화를 위한 서비스 및 도구가 포함되어 있습니다.

- **[Commerce 서비스 커넥터](/help/landing/saas.md)** - Adobe Commerce on cloud, 온-프레미스 또는 Magento Open Source을 지원되는 Commerce SaaS 서비스에 연결합니다.
- **[SaaS 데이터 내보내기](/help/data-export/overview.md)** - 연결된 서비스를 위한 Commerce 데이터의 이동 및 동기화를 지원합니다.
- **[데이터 연결](/help/data-connection/overview.md)** - Commerce 데이터를 Adobe Experience Platform에 연결합니다.
- **[Adobe Commerce Optimizer 커넥터](/help/aco-connector/overview.md)** - 지원되는 Adobe Commerce 배포의 카탈로그 및 가격 데이터를 Adobe Commerce Optimizer에 동기화합니다.
- **[플랫폼별 커넥터](/help/optimizer/integrations/integrations-overview.md#commerce-salesforce-connector)** - 지원되는 특정 서드파티 상거래 플랫폼과 Adobe Commerce Optimizer을 연결합니다.

### 개발자 도구 및 확장성

개발자 기능에는 **Adobe Developer App Builder**, **API Mesh**, **이벤트**, **웹후크** 및 **관리 UI SDK**&#x200B;가 포함됩니다. 이러한 도구는 사용자 정의 애플리케이션, 통합 및 확장을 지원합니다. 사용 가능 여부는 Commerce 오퍼링에 따라 다릅니다.

[Adobe Commerce 개발자 설명서](https://developer.adobe.com/commerce/docs/)를 참조하세요.

### 서비스 가용성

이 비교를 사용하여 Commerce 제품에 대한 서비스 경로를 식별합니다. 지원되는 버전, 라이선스 및 설정 요구 사항에 대해서는 [Adobe Commerce 기능 비교](https://experienceleague.adobe.com/ko/docs/commerce/cloud-service/feature-comparison) 및 각 서비스 안내서를 검토하십시오.

| 서비스 또는 기능 | 가용성 |
| --- | --- |
| [[!DNL Catalog Service]](/help/catalog-service/overview.md) | Adobe Commerce on cloud infrastructure 또는 온프레미스 및 Adobe Commerce as a Cloud Service |
| [[!DNL Live Search]](/help/live-search/overview.md) | Adobe Commerce on cloud infrastructure 또는 온프레미스 및 Adobe Commerce as a Cloud Service |
| [[!DNL Product Recommendations]](/help/product-recommendations/overview.md) | Adobe Commerce on cloud infrastructure 또는 온프레미스 및 Adobe Commerce as a Cloud Service |
| [자산 관리](../aem-assets/aem-assets-integration.md) | Adobe Commerce 온클라우드 인프라 또는 Commerce용 AEM Assets 통합을 통한 온프레미스. AEM Assets에서 제공하는 제품 비주얼을 통해 Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer. |
| [기본 검색 및 머천다이징](/help/optimizer/merchandising/overview.md) | Adobe Commerce Optimizer은 독립 실행형이거나 Optimizer 커넥터를 통해 Adobe Commerce에 연결됩니다. 이러한 기능은 별도의 Catalog Service, Live Search 및 Product Recommendations 확장을 대체합니다. |
| [[!DNL Payment Services]](/help/payment-services/guide-overview.md) | Adobe Commerce as a Cloud Service, 클라우드 인프라 또는 온프레미스에서 Adobe Commerce의 지원되는 버전 및 Magento Open Source |


>[!NOTE]
>
>Adobe Commerce as a Cloud Service에는 카탈로그 서비스, 라이브 검색 및 제품 권장 사항이 자동으로 설치되고 구성됩니다. 클라우드 인프라 또는 온프레미스의 Adobe Commerce에서 구성하기 전에 각 확장을 설치합니다. 역할 및 플랫폼별 설정 경로에 대해서는 [역할별 시작](../get-started/get-started-by-role.md)을 참조하십시오.

## 사용할 Commerce 제공 결정

[Commerce 옵션을 선택](choose-commerce-option.md)하여 배포 모델, 거래 소유권 및 머천다이징 기능을 비교하여 요구 사항에 맞는 아키텍처를 확인하십시오.
