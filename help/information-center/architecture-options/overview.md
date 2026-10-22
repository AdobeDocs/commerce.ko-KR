---
title: Commerce 아키텍처 개요
description: Adobe Commerce 제품 모델 및 자세한 아키텍처 옵션, 상점 및 API 지침을 찾을 수 있는 위치에 대해 알아봅니다.
role: Developer, Leader
feature: Storefront, Integration
recommendations: noCatalog
autotag-review: '2026-10-20T10:11:03.706Z'
TQID: 'https://experienceleague.adobe.com/V9Zp0eS8b45xYEay4EK91tPVnKhRdkWGDj4Vv7hB79U'
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
  - id: 4273989f-0bf2-5361-a17a-6909488d18ab
    internal-label: Catalog Service
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dec06508-d41f-555a-87e8-29e8bcdfa95a
    internal-label: Recommendations
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: da3860b0-d637-47df-bef0-273751180266
    internal-label: Digital asset management
source-git-commit: ca6bb3543583c865c42b8f4d84f01e27a04f9223
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%
---

# Commerce 아키텍처 개요

Adobe Commerce 아키텍처는 일반적으로 상거래 백엔드([!DNL Adobe Commerce] 또는 [!DNL Adobe Commerce Optimizer]), 상점 및 연결된 서비스 및 통합 세트의 세 계층을 결합합니다. 이 섹션에서는 제품 모델을 소개하고 각 전용 페이지에서 유지 관리되는 자세한 비교, 다이어그램 및 API 참조를 안내합니다.

## 시작

| 섹션 | 사용 대상 |
| ------- | --------- |
| [플랫폼 및 서비스](../portfolio/platform-and-services.md) | Adobe Commerce, Commerce Foundation, Adobe Commerce Optimizer 및 Adobe Commerce as a Cloud Service 등 각 Commerce 제품이 무엇인지 이해합니다. |
| [Commerce 옵션 선택](../portfolio/choose-commerce-option.md) | 거래 소유권, 배포 모델 및 머천다이징 요구 사항을 기반으로 Commerce 옵션을 비교합니다. |
| [아키텍처 옵션](../architecture-options/implementation-architectures.md) | 시스템 다이어그램 및 참조 링크를 포함하여 지원되는 네 가지 아키텍처를 모두 자세히 비교합니다. |
| [상점](../storefronts/overview.md) | 상점 옵션 및 각 아키텍처에 연결하는 방법을 이해합니다. |
| [API](../apis/commerce-apis.md) | Commerce Foundation, Storefront Services 및 Commerce Optimizer에서 사용되는 API 제품군을 비교합니다. |
| [Commerce용 AEM Assets 통합](../aem-assets/aem-assets-integration.md) | 모든 Commerce 또는 Optimizer 아키텍처에 중앙 집중식 디지털 에셋 관리를 추가합니다. |
| [마이그레이션 및 채택](../migration-adoption/overview.md) | 아키텍처 간 이동 또는 Adobe Commerce Optimizer의 단계적 채택을 계획합니다. |

## 용어 빠른 참조

| 기본 용어 | 의미 | 를 현재 아키텍처 레이블로 사용하지 않음 |
| --- | --- | --- |
| **Commerce Foundation** | 기본 상거래 및 트랜잭션 기능 | 코어 Commerce 및 PHP 기본 레이어 |
| **상점 서비스** | 카탈로그 서비스, 라이브 검색 및 제품 추천을 위한 상점 지향 API | 레이블은 하나의 Commerce 플랫폼으로만 제한됨 |
| **Commerce Optimizer 머천다이징 서비스** | 카탈로그 검색 및 머천다이징 경험을 위한 Optimizer API | Commerce Foundation API |
| **Edge Delivery Services에서 제공하는 Commerce 상점** | 고객용 Storefront 구현 | API 제품군 |

## 관련 지침

- [구현 아키텍처](implementation-architectures.md)
- [참조 아키텍처](reference-architectures.md)
- [새 상점 만들기](../implementation-guides/build-new-storefront.md)
