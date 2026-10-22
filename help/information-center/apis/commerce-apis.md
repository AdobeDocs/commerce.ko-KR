---
title: COMMERCE API
description: Adobe Commerce Foundation, Storefront Services, Commerce Optimizer 머천다이징 서비스, 데이터 수집을 비롯한 Commerce API 제품군을 비교합니다.
role: Developer, Leader
feature: Storefront, Integration
recommendations: noCatalog
autotag-review: '2026-10-20T01:36:11.529Z'
TQID: 'https://experienceleague.adobe.com/JBpnpCy9QITdcYtKnL2btd9grmgIk1prYaCNasgWkok'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
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
  - id: 72863f3c-9d27-5dda-afe1-d9f934b1fba0
    internal-label: Extensibility
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dec06508-d41f-555a-87e8-29e8bcdfa95a
    internal-label: Recommendations
  - id: c4f010fa-1478-4300-a88d-706fbc036a7a
    internal-label: APIs and SDKs
subfeature_v2:
  - id: e396cff5-f586-484c-89f0-7f1da3308f92
    internal-label: GraphQL
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: da3860b0-d637-47df-bef0-273751180266
    internal-label: Digital asset management
source-git-commit: ca6bb3543583c865c42b8f4d84f01e27a04f9223
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%
---

# API

| API 제품군 | 주요 목적 | 사용한 사람 |
| --- | --- | --- |
| **Commerce Foundation GraphQL API** | 카탈로그 작업, 장바구니, 체크아웃, 고객 및 주문과 같은 핵심 상거래 및 트랜잭션 기능 | 클라우드에 [!DNL Adobe Commerce]개, 온프레미스에 [!DNL Adobe Commerce]개, 그리고 [!DNL Adobe Commerce as a Cloud Service]개 |
| **Storefront Services GraphQL API** | [!DNL Catalog Service], [!DNL Live Search] 및 [!DNL Product Recommendations]을(를) 통한 상점 지향 카탈로그, 검색 및 권장 사항 경험 | [!DNL Adobe Commerce] 클라우드 또는 구성된 서비스를 사용하는 온-프레미스에서 및 [!DNL Adobe Commerce as a Cloud Service] |
| **Commerce Optimizer 머천다이징 서비스 GraphQL API** | Optimizer 관리 카탈로그, 카탈로그 보기, 가격 컨텍스트, 검색, 권장 사항 및 머천다이징 결과 검색 | [!DNL Adobe Commerce] 클라우드 또는 Optimizer 커넥터가 있는 온프레미스에서 및 독립 실행형 [!DNL Adobe Commerce Optimizer] |
| **Commerce Optimizer 데이터 수집 REST API** | 독립 실행형 [!DNL Adobe Commerce Optimizer] 구현에 카탈로그 및 가격 데이터 추가 | 외부 데이터 원본에 연결된 독립 실행형 [!DNL Adobe Commerce Optimizer] |

## Commerce Foundation GraphQL API

카탈로그, 장바구니, 체크아웃, 고객 및 주문을 포함한 핵심 상거래 기능. 클라우드의 [!DNL Adobe Commerce], 온프레미스의 [!DNL Adobe Commerce] 및 [!DNL Adobe Commerce as a Cloud Service]에서 사용됩니다. [Commerce GraphQL API](https://developer.adobe.com/commerce/webapi/graphql/)를 참조하세요.

## Storefront Services GraphQL API

[!DNL Catalog Service], [!DNL Live Search] 및 [!DNL Product Recommendations]을(를) 통한 상점 지향 카탈로그, 검색 및 추천 경험입니다. 클라우드, 온-프레미스 및 [!DNL Adobe Commerce as a Cloud Service]의 [!DNL Adobe Commerce]에서 사용합니다. [Storefront Services GraphQL 스키마](https://developer.adobe.com/commerce/webapi/graphql/schema/storefront-services/)를 참조하세요.

## Commerce Optimizer 머천다이징 서비스 GraphQL API

Optimizer 관리 카탈로그, 카탈로그 보기, 가격 컨텍스트, 검색, 권장 사항 및 머천다이징 결과를 검색합니다. 클라우드, [!DNL Adobe Commerce Optimizer Connector]을(를) 사용하는 온-프레미스 및 독립 실행형 [!DNL Adobe Commerce Optimizer]에서 사용하는 [!DNL Adobe Commerce]입니다. [Commerce Optimizer 머천다이징 서비스](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/)를 참조하십시오.

## Commerce Optimizer 데이터 수집 REST API

외부 데이터 원본에서 독립 실행형 [!DNL Adobe Commerce Optimizer] 구현에 카탈로그 및 가격 데이터를 추가합니다. [Commerce Optimizer 데이터 수집](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/)을 참조하세요.

## Commerce Optimizer 통합

[!DNL Adobe Commerce Optimizer]은(는) [!DNL Adobe Commerce] 또는 타사 백엔드와 연결되는지 여부에 따라 여러 통합 경로를 통해 다른 시스템에 연결합니다.

### Adobe Commerce Optimizer 커넥터

Optimizer에서 검색 및 머천다이징을 제공하는 동안 [!DNL Adobe Commerce]을(를) 트랜잭션 시스템으로 유지하면서 클라우드 또는 온프레미스의 [!DNL Adobe Commerce]에서 [!DNL Adobe Commerce Optimizer]&#x200B;(으)로 카탈로그 및 가격 데이터를 동기화합니다. [Commerce Optimizer 통합](/help/optimizer/integrations/integrations-overview.md)을 참조하세요.

### 서드파티 상거래 통합

데이터 수집 REST API를 통해 타사 상거래 플랫폼, PIM, ERP 또는 기타 소스의 카탈로그 및 가격 데이터를 독립 실행형 [!DNL Adobe Commerce Optimizer]&#x200B;(으)로 수집하는 반면 타사 플랫폼은 트랜잭션 레코드 시스템으로 유지됩니다.

### API Mesh 및 App Builder

API Mesh를 사용하여 Adobe Commerce API를 개인 또는 서드파티 API로 오케스트레이션합니다. Adobe Developer App Builder을 사용하여 사용자 정의 애플리케이션 및 통합을 빌드합니다. 관련된 Commerce 확장성 지침을 보려면 [API Mesh](https://developer.adobe.com/graphql-mesh-gateway/) 및 [Adobe Commerce 확장성](https://developer.adobe.com/commerce/extensibility/)을 참조하십시오.

특히 이벤트 기반 통합에 대해서는 [Adobe Commerce용 Adobe I/O Events](https://experienceleague.adobe.com/ko/docs/commerce-learn/tutorials/extensibility/adobe-developer-app-builder/io-events/getting-started-io-events)을 참조하십시오.


### 장바구니 및 체크아웃 전달

외부 백엔드가 있는 독립형 [!DNL Adobe Commerce Optimizer]의 경우 상점은 제품 경험을 위해 머천다이징 서비스 GraphQL API를 사용한 다음 API Mesh, App Builder 또는 직접 통합을 통해 장바구니, 체크아웃, 고객, 주문, 결제, 세금, 배송 및 주문 처리를 백엔드로 전달합니다.

### AEM Assets

AEM Assets은 선택적인 교차 디지털 에셋 관리 통합으로, 자체 별도의 통합 경로가 아닌 모든 Commerce 또는 Optimizer 아키텍처에 추가할 수 있습니다. [Commerce용 AEM Assets 통합](../aem-assets/aem-assets-integration.md)을 참조하세요.

## 관련 지침

- [아키텍처 개요](../architecture-options/overview.md)
- [상점 전선](../storefronts/overview.md)
- [Commerce용 AEM Assets 통합](../aem-assets/aem-assets-integration.md)
