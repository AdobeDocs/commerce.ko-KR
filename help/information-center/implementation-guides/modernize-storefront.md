---
title: 기존 Storefront 현대화
description: 기존 Adobe Commerce 상점 첫 화면에서 Edge Delivery Services 및 드롭인 구성 요소를 기반으로 구축된 상점 첫 화면으로의 증분 마이그레이션을 계획하는 방법을 알아봅니다.
role: Developer, Leader
feature: Storefront
recommendations: noCatalog
autotag-review: '2026-10-20T11:09:14.812Z'
TQID: 'https://experienceleague.adobe.com/1OR7uwncjLw-NpwMMuwKjDjpASdh74sfu6s5rNClqxg'
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
  - id: 4273989f-0bf2-5361-a17a-6909488d18ab
    internal-label: Catalog Service
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
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
source-git-commit: ca6bb3543583c865c42b8f4d84f01e27a04f9223
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%
---

# 기존 상점 현대화

한 번에 모든 스토어를 다시 빌드하는 대신 레거시 스토어를 Edge Delivery Services 및 Commerce 드롭인 구성 요소로 점진적으로 마이그레이션할 수 있습니다.

>[!NOTE]
>
>이 안내서는 Adobe Commerce as a Cloud Service, Adobe Commerce on cloud infrastructure 또는 Storefront Services 또는 Adobe Commerce Optimizer Connector를 사용하는 온프레미스 배포에 적용됩니다. 기존 또는 타사 백엔드가 있는 독립형 Adobe Commerce Optimizer에도 적용됩니다. 프로젝트에 적용되는 옵션을 확인하려면 [구현 아키텍처 옵션](../architecture-options/implementation-architectures.md)을 참조하세요.

## 시작

1. Edge Delivery Services에 구축된 Storefront가 현재 구현과 어떻게 다른지 이해하려면 [Adobe Commerce Storefront 개요](https://experienceleague.adobe.com/en/tools/commerce-storefront/)를 검토하십시오.

1. [Storefront 개발자 안내서](https://experienceleague.adobe.com/en/tools/commerce-storefront/get-started/)를 사용하여 먼저 마이그레이션할 페이지 또는 흐름의 범위를 지정하십시오.

1. Adobe Commerce as a Cloud Service의 경우 기존 Commerce 서비스 연결([!DNL Catalog Service], [!DNL Live Search], [!DNL Product Recommendations], [!DNL Payment Services])을 그대로 유지합니다. [Commerce 서비스 설정](set-up-commerce-services.md)을 참조하십시오.

## 관련 지침

- [새 상점 만들기](build-new-storefront.md)
- [아키텍처 옵션](../architecture-options/overview.md)
