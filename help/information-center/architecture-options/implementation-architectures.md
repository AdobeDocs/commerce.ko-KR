---
title: 구현 아키텍처 옵션
description: Commerce Foundation, Adobe Commerce as a Cloud Service, Optimizer 커넥터 및 독립형 Optimizer를 비롯한 Adobe Commerce 아키텍처를 비교합니다.
role: Developer, Leader
feature: Storefront, Integration
recommendations: noCatalog
autotag-review: '2026-10-20T01:39:51.406Z'
TQID: 'https://experienceleague.adobe.com/tYkxRAfJWOY7C0OEqYxEb4onwvnnL9wEofEG2e6qnKA'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: ef0c45ae-6bee-4821-a65e-e1e118e8a01c
    internal-label: Commerce Optimizer
feature_v2:
  - id: 22bad240-8308-569b-a9d5-578f1ff890ca
    internal-label: Customers
  - id: 4273989f-0bf2-5361-a17a-6909488d18ab
    internal-label: Catalog Service
  - id: 4820f335-ec9f-5611-8fe3-f5b7e3e56967
    internal-label: Orders
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
  - id: 8dc0e58b-adf0-51bb-8db5-bb36e3e656fb
    internal-label: Inventory
  - id: bcd8874c-7b93-5596-bdaa-22660e84df14
    internal-label: Deploy
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: d3b92bef-63fa-5031-a925-d04d9362d616
    internal-label: Saas
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dec06508-d41f-555a-87e8-29e8bcdfa95a
    internal-label: Recommendations
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
subfeature_v2:
  - id: e396cff5-f586-484c-89f0-7f1da3308f92
    internal-label: GraphQL
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
source-git-commit: 4c3c267873a68560a885c6376cd1137a7503710a
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 0%
---

# 구현 아키텍처 옵션

Adobe Commerce 구현 아키텍처는 상거래 백엔드([!DNL Adobe Commerce] 또는 [!DNL Adobe Commerce Optimizer]), 상점 및 연결된 서비스 및 통합 세트의 세 계층을 결합합니다. 다음 옵션을 비교하여 각 아키텍처에서 카탈로그, 가격 책정, 장바구니, 체크아웃, 주문 및 고객 트랜잭션을 소유한 시스템을 식별합니다.

## 아키텍처 옵션 요약

거래 소유권별 및 상점 경험별로 옵션을 비교합니다.

### Commerce 플랫폼 및 트랜잭션

| 옵션 | 기록 시스템 | 트랜잭션 경로 | 최적 |
| --- | --- | --- | --- |
| Commerce Foundation이 있는 **[!DNL Adobe Commerce as a Cloud Service]** | Adobe 관리 Commerce Foundation | 관리 Commerce Foundation 및 연결된 Commerce 서비스 | 인프라 소유권이 감소된 Adobe 관리 SaaS(Software as a Service) Commerce을 원하는 고객 |
| [!DNL Adobe Commerce Optimizer Connector]&#x200B;**을(를) 사용하여 클라우드 또는 온프레미스에서**&#x200B;[!DNL Adobe Commerce] | 기존 Commerce Foundation, Commerce 데이터 및 트랜잭션 | 기존 Commerce Foundation API 및 연결된 트랜잭션 서비스 | 기존 [!DNL Adobe Commerce] 배포에 Optimizer 검색 및 머천다이징 기능을 추가하려는 고객 |
| 외부 상거래 백엔드가 있는 **독립 실행형 [!DNL Adobe Commerce Optimizer]** | 기존 또는 타사 상거래 플랫폼. 카탈로그 및 가격 데이터가 외부 소스에서 Optimizer에 추가됩니다. | API Mesh, App Builder 또는 직접 통합은 상점 전면을 서드파티 장바구니, 체크아웃, 고객, 주문, 결제, 세금, 배송 및 주문 처리 서비스에 연결합니다 | 기존 또는 서드파티 트랜잭션 상거래 플랫폼을 유지하면서 Optimizer 기능을 원하는 고객 |
| **[!DNL Adobe Commerce]클라우드 또는 Commerce Foundation을 사용하는 온-프레미스** | Commerce 재단 | Commerce Foundation API 및 구성된 결제, 세금, 배송, 재고 및 이행 통합 | 클라우드 또는 온-프레미스 인프라에 대한 배포 제어와 함께 전체 [!DNL Adobe Commerce] 플랫폼이 필요한 고객 |

### Storefront 경험

Storefront는 Commerce Foundation API, Storefront 서비스([!DNL Catalog Service], [!DNL Live Search] 및 [!DNL Product Recommendations]) 또는 [!DNL Adobe Commerce Optimizer] 머천다이징 서비스에 연결합니다.

| 옵션 | Storefront 경험 | Storefront 데이터 경로 |
| --- | --- | --- |
| Commerce Foundation이 있는 **[!DNL Adobe Commerce as a Cloud Service]** | Edge Delivery Services 또는 기타 지원되는 Headless 환경에서 제공하는 Commerce Storefront | Storefront Services 및 핵심 플랫폼 데이터용 Commerce Foundation API |
| [!DNL Adobe Commerce Optimizer Connector]&#x200B;**을(를) 사용하여 클라우드 또는 온프레미스에서**&#x200B;[!DNL Adobe Commerce] | Optimizer 경험을 사용한 Edge Delivery Services 또는 사용자 지정 헤드리스 상점 | Optimizer 관리 카탈로그 및 머천다이징 데이터를 위한 Commerce Optimizer 머천다이징 서비스 GraphQL API |
| 외부 상거래 백엔드가 있는 **독립 실행형 [!DNL Adobe Commerce Optimizer]** | Edge Delivery Services 또는 사용자 지정 헤드리스 상점 기반의 Commerce 상점 | 카탈로그 및 머천다이징 데이터용 Commerce Optimizer 머천다이징 서비스 GraphQL API |
| **[!DNL Adobe Commerce]클라우드 또는 Commerce Foundation을 사용하는 온-프레미스** | Edge Delivery Services, Luma, PWA 또는 사용자 지정 헤드리스 상점 | Commerce Foundation API 및 구성 시 Storefront 서비스 |

## Adobe Commerce as a Cloud Service

![Commerce Storefront를 제공하는 Managed Commerce Foundation 및 Storefront Services가 있는 Adobe Commerce as a Cloud Service의 아키텍처 다이어그램](../assets/architecture/commerce-cloud-service-storefront-services-arch.drawio.png){width="600" zoomable="yes"}

**키 경계** - Adobe에서 Commerce Foundation 플랫폼을 관리합니다. 아키텍처는 상점 경험을 위해 [!DNL Catalog Service], [!DNL Live Search] 및 [!DNL Product Recommendations]을(를) 포함한 상점 서비스를 사용합니다. AEM Assets에서 제공하는 [!DNL Product Visuals]은(는) 선택적 SaaS 통합입니다. [Commerce용 AEM Assets 통합](../aem-assets/aem-assets-integration.md)을 참조하세요.

**참조:**

- [[!DNL Adobe Commerce as a Cloud Service] 개요](/help/cloud-service/overview.md)
- [Commerce 상점 첫 화면](https://experienceleague.adobe.com/en/tools/commerce-storefront/)
- [Storefront Services GraphQL 스키마](https://developer.adobe.com/commerce/webapi/graphql/schema/storefront-services/)

## Commerce Foundation을 사용한 Adobe Commerce

![Commerce Storefront를 제공하는 Storefront Services 및 Commerce Foundation API를 통한 Cloud 또는 온프레미스의 Adobe Commerce 아키텍처 다이어그램](../assets/architecture/commerce-paas-storefront-services-arch.drawio.png){width="600" zoomable="yes"}

**키 경계** - Commerce Foundation은 Commerce 플랫폼 및 트랜잭션 흐름을 소유합니다. [!DNL Catalog Service], [!DNL Live Search] 및 [!DNL Product Recommendations]은(는) 구성 시 카탈로그, 검색 및 권장 사항에 대한 최적화된 Storefront 액세스를 제공합니다. AEM Assets 통합은 선택 사항입니다. [Commerce용 AEM Assets 통합](../aem-assets/aem-assets-integration.md)을 참조하세요.

**참조:**

- [Commerce 상점 첫 화면](https://experienceleague.adobe.com/en/tools/commerce-storefront/)
- [COMMERCE GRAPHQL API](https://developer.adobe.com/commerce/webapi/graphql/)
- [Storefront Services GraphQL 스키마](https://developer.adobe.com/commerce/webapi/graphql/schema/storefront-services/)


## Optimizer 커넥터가 있는 Adobe Commerce

![카탈로그 및 가격 데이터를 Adobe Commerce에서 Adobe Commerce Optimizer으로 동기화하는 Adobe Commerce Optimizer 커넥터의 아키텍처 다이어그램으로, 머천다이징 서비스 API를 통해 Commerce 상점 제공](../assets/architecture/adobe-commerce-optimizer-architecture.drawio.png){width="600" zoomable="yes"}

**키 경계** - 커넥터가 카탈로그 및 가격 데이터를 [!DNL Adobe Commerce]에서 [!DNL Adobe Commerce Optimizer]&#x200B;(으)로 동기화합니다. [!DNL Adobe Commerce]은(는) 트랜잭션 시스템으로 남지만 Optimizer는 머천다이징 서비스 API를 통해 검색 및 머천다이징 경험을 제공합니다.

**참조:**

- [Commerce Optimizer 통합](/help/optimizer/integrations/integrations-overview.md)
- [Commerce Optimizer 머천다이징 서비스](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/)
- [COMMERCE GRAPHQL API](https://developer.adobe.com/commerce/webapi/graphql/)
- [Commerce 상점 첫 화면](https://experienceleague.adobe.com/en/tools/commerce-storefront/)

## 서드파티 백엔드가 포함된 독립형 Commerce Optimizer

![데이터 수집을 통해 카탈로그 및 가격 데이터를 독립 실행형 Adobe Commerce Optimizer에 전송하여 타사 상거래 백엔드에 연결된 Commerce Storefront를 제공하는 고객 소유 소스 시스템의 아키텍처 다이어그램](../assets/architecture/adobe-commerce-optimizer-standalone-detailed.drawio.png){width="800" zoomable="yes"}

**키 경계**—독립 실행형 [!DNL Adobe Commerce Optimizer]이(가) 카탈로그 검색 및 머천다이징 경험을 소유하지만 트랜잭션 Commerce 백엔드는 소유하지 않습니다. 카탈로그 및 가격 데이터는 데이터 수집 REST API를 통해 입력합니다. Edge Delivery Services 상점은 제품 경험을 위해 머천다이징 서비스 GraphQL API를 사용하고 장바구니 및 체크아웃을 위해 서드파티 백엔드에 연결합니다.

**참조:**

- [Adobe Commerce Optimizer란?](/help/optimizer/overview.md)
- [Commerce Optimizer 데이터 수집](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/)
- [Commerce Optimizer 머천다이징 서비스](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/)
- [Commerce 상점 첫 화면](https://experienceleague.adobe.com/en/tools/commerce-storefront/)

## 용어 빠른 참조

| 기본 용어 | 의미 | 를 현재 아키텍처 레이블로 사용하지 않음 |
| --- | --- | --- |
| **Commerce Foundation** | 기본 상거래 및 트랜잭션 기능 | 코어 Commerce, PHP 기본 레이어 |
| **상점 서비스** | 카탈로그 서비스, 라이브 검색 및 제품 추천을 위한 상점 지향 API | 레이블은 하나의 Commerce 플랫폼으로만 제한됨 |
| **Commerce Optimizer 머천다이징 서비스** | 카탈로그 검색 및 머천다이징 경험을 위한 Optimizer API | Commerce Foundation API |
| **Edge Delivery Services에서 제공하는 Commerce 상점** | 고객용 Storefront 구현 | API 제품군 |

## 관련 지침

- [참조 아키텍처](reference-architectures.md)
- [Commerce 옵션 선택](../portfolio/choose-commerce-option.md)
- [상점 전선](../storefronts/overview.md)
- [API](../apis/commerce-apis.md)
