---
title: 상점 전선
description: Edge Delivery Services에서 제공하는 Adobe Commerce Storefront 및 사용자 지정 Headless 구현을 포함한 Commerce Storefront 옵션에 대해 알아봅니다.
role: Developer, Leader
feature: Storefront, Integration
recommendations: noCatalog
autotag-review: '2026-10-20T01:12:22.967Z'
TQID: 'https://experienceleague.adobe.com/1mQm2s3UGzr7S4j9RMZAaRoUVtzu93N1IFbOypR8vkA'
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
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
subfeature_v2:
  - id: e396cff5-f586-484c-89f0-7f1da3308f92
    internal-label: GraphQL
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
source-git-commit: ca6bb3543583c865c42b8f4d84f01e27a04f9223
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%
---

# 상점 전선

상점 첫 화면은 Commerce 백엔드 및 API 레이어와 별개입니다. 선택한 아키텍처에 따라 Storefront는 API Mesh, App Builder 또는 기타 통합 메커니즘을 통해 Commerce Foundation API, Storefront Services API, [!DNL Adobe Commerce Optimizer] 머천다이징 서비스 API 또는 연결된 시스템에서 데이터를 검색할 수 있습니다. 각 상점 및 Commerce 백엔드의 연결 방법은 [아키텍처 옵션](../architecture-options/overview.md)을 참조하세요.

## Edge Delivery Services 기반 Commerce Storefront

[!DNL Edge Delivery Services]에서 제공하는 Commerce Storefront는 드롭인 구성 요소와 콘텐츠 블록을 사용하여 Adobe Commerce 보일러판에 빌드된 고객 대면 상점 옵션입니다. 백엔드에 따라 Commerce Foundation, Storefront Services 또는 [!DNL Adobe Commerce Optimizer] 머천다이징 서비스에 연결하는 [아키텍처 개요](../architecture-options/overview.md)와(과) 호환됩니다. [Adobe Commerce 상점 개요](https://experienceleague.adobe.com/en/tools/commerce-storefront/)를 참조하세요.

## Storefront Services

[!DNL Storefront Services]은(는) [!DNL Adobe Commerce]에서 사용되는 상점 지향 서비스입니다. 서비스 API는 다음과 같은 기능에 대한 최적화된 액세스를 제공합니다.

- [!DNL Catalog Service]
- [!DNL Live Search]
- [!DNL Product Recommendations]

[!DNL Adobe Commerce] 온 클라우드 또는 온-프레미스(구성된 경우)와 [!DNL Adobe Commerce as a Cloud Service] 모두 Storefront 서비스를 사용합니다. 이 레이블은 [!DNL Adobe Commerce as a Cloud Service]에만 사용할 수 있으며 두 [!DNL Adobe Commerce] 플랫폼 옵션 간의 구분 레이블로 사용해서는 안 됩니다. [Storefront Services GraphQL 스키마](https://developer.adobe.com/commerce/webapi/graphql/schema/storefront-services/)를 참조하세요.

## 사용자 정의 헤드리스 상점

[!DNL Edge Delivery Services]에서 제공하는 Commerce Storefront 이외의 Storefront 옵션에는 플랫폼 지원 및 구현 요구 사항에 따라 [!DNL Luma], [!DNL PWA Studio] 또는 사용자 지정 Headless Storefront가 포함됩니다. 사용자 지정 Headless Storefront는 선택한 [아키텍처 옵션](../architecture-options/overview.md)을(를) 기반으로 다른 Storefront 옵션(Commerce Foundation, Storefront Services 또는 Commerce Optimizer 머천다이징 서비스)과 동일한 API 제품군에 연결합니다.

## 장바구니와 체크아웃 통합

장바구니 및 체크아웃 트랜잭션이 처리되는 위치는 상점 기술이 아닌 Commerce 백엔드에 따라 다릅니다.

- [!DNL Adobe Commerce] Commerce Foundation이 백엔드인 경우 스토어프론트는 구성된 결제, 세금, 배송 및 이행 통합과 함께 장바구니, 체크아웃, 고객 및 주문 운영을 위해 Commerce Foundation API를 사용합니다.
- 독립 실행형 [!DNL Adobe Commerce Optimizer]과(와) 같이 서드파티 상거래 플랫폼이 백엔드인 경우 상점은 API Mesh, App Builder 또는 직접 통합을 통해 해당 플랫폼의 장바구니, 체크아웃, 고객, 주문, 결제, 세금, 배송 및 이행 서비스에 연결합니다.

## 관련 지침

- [아키텍처 개요](../architecture-options/overview.md)
- [API](../apis/commerce-apis.md)
