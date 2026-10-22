---
title: Commerce 옵션 선택
description: 거래 소유권, 배포 모델 및 머천다이징 요구 사항을 기반으로 Adobe Commerce 아키텍처를 비교합니다.
role: Admin, Developer, Leader, User
feature: Storefront, Integration, Configuration
recommendations: noCatalog
TQID: 'https://experienceleague.adobe.com/5y0IU5nji50eqfFNQHbVDV-R81Mx0I8v5Y0a6nccL-w'
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
  - id: 22bad240-8308-569b-a9d5-578f1ff890ca
    internal-label: Customers
  - id: 4820f335-ec9f-5611-8fe3-f5b7e3e56967
    internal-label: Orders
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: 6388cf7b-8a81-5248-a1e4-7bb57bbe250f
    internal-label: Install
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
  - id: bcd8874c-7b93-5596-bdaa-22660e84df14
    internal-label: Deploy
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
    internal-label: Accounts
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
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
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
source-git-commit: 4c3c267873a68560a885c6376cd1137a7503710a
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%
---

# Commerce 옵션 선택

장바구니, 체크아웃, 주문 및 기타 트랜잭션을 소유한 시스템을 식별하여 시작합니다. 그런 다음 해당 백엔드에 맞는 머천다이징 경로를 선택합니다.

## 결정을 안내하는 질문

다음 질문을 사용하여 평가할 옵션을 식별합니다. 기존 상거래 백엔드, 유지할 인프라 책임의 크기, 제품 검색 및 머천다이징 개선 필요 여부를 고려합니다. Adobe Commerce Optimizer은 검색 및 머천다이징 기능을 제공합니다. 트랜잭션을 처리하는 백엔드는 대체하지 않습니다.

1. **Adobe에서 SaaS(Software as a Service)로 Commerce 플랫폼을 관리하시겠습니까?**
   - 예: Adobe Commerce as a Cloud Service을 평가합니다.
   - 아니요: Adobe Commerce이 필요하고 클라우드 또는 온프레미스 인프라에 대한 제어를 유지하려면 Adobe Commerce on Cloud 또는 온프레미스를 평가합니다.
1. **장바구니, 체크아웃, 주문 및 기타 트랜잭션을 처리하려면 Adobe Commerce이 필요합니까?**
   - 예: Adobe Commerce on Cloud, 온프레미스 또는 Adobe Commerce as a Cloud Service을 평가합니다. 이러한 옵션은 Commerce Foundation을 트랜잭션 백엔드로 사용합니다.
   - 아니요: 기존 또는 타사 트랜잭션 백엔드를 유지합니다. Adobe 검색 및 머천다이징 기능도 필요한 경우 독립형 Adobe Commerce Optimizer을 평가하십시오.
1. **기존 타사 상거래 백엔드에서 Adobe Commerce Optimizer을 사용하여 제품 검색 및 머천다이징을 개선하시겠습니까?**
   - 예: 트랜잭션을 위해 타사 백엔드를 유지하면서 독립형 Adobe Commerce Optimizer을 평가합니다.
1. **클라우드나 온프레미스에서 Adobe Commerce을 이미 운영하고 있으며 더 강력한 검색과 머천다이징을 원하십니까?**
   - 예: Adobe Commerce에서 트랜잭션을 계속 처리하는 동안 Adobe Commerce Optimizer 커넥터를 평가하여 카탈로그 및 가격책정 데이터를 동기화합니다.

아래 비교 표를 사용하여 시작점에 대한 답변을 일치시키십시오. 자세한 시스템 다이어그램은 [아키텍처 옵션](../architecture-options/overview.md)을 참조하십시오.

## Commerce 비교 옵션

| 요구 사항 | 권장 시작 지점 | 거래를 소유하는 시스템 | 머천다이징 및 검색 |
| --- | --- | --- | --- |
| Adobe은 Commerce 플랫폼을 SaaS로 관리합니다. | [Adobe Commerce as a Cloud Service](/help/cloud-service/overview.md) | Adobe Commerce as a Cloud Service 기반 | Adobe Commerce as a Cloud Service에 대해 프로비저닝된 Commerce 서비스를 사용합니다. Adobe Commerce Optimizer 통합 가용성은 이 표 아래의 참고 사항을 참조하십시오. |
| Adobe Commerce이 필요하며 클라우드 또는 온프레미스 인프라에 대한 제어를 유지하고자 합니다. | [클라우드 또는 온프레미스의 Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-admin/start/guide-overview) | Adobe Commerce 재단 | 필요에 따라 지원되는 Commerce 서비스를 사용하십시오. |
| Adobe Commerce 온 클라우드 또는 온프레미스에서 검색 및 머천다이징을 위해 Adobe Commerce Optimizer을 채택하려고 합니다. | [Adobe Commerce Optimizer 커넥터](/help/aco-connector/overview.md)가 있는 Adobe Commerce | Adobe Commerce은 거래에 대한 기록 시스템으로 남아 있습니다. | 커넥터는 검색 및 머천다이징 경험을 제공하는 Adobe Commerce Optimizer에 카탈로그 및 가격 데이터를 동기화합니다. |
| 서드파티 상거래 백엔드가 있으며 해당 백엔드를 교체하지 않고 Adobe Commerce Optimizer 검색 및 머천다이징을 원합니다. | 독립 실행형 [Adobe Commerce Optimizer](/help/optimizer/overview.md) | 타사 상거래 백엔드 | 카탈로그 및 가격 데이터를 Adobe Commerce Optimizer으로 보냅니다. API Mesh, App Builder 또는 직접 통합을 통해 장바구니, 체크아웃 및 기타 트랜잭션 작업을 백엔드와 통합합니다. |

>[!NOTE]
>
>Adobe Commerce as a Cloud Service과 Adobe Commerce Optimizer 간의 통합이 Commerce 로드맵에 있습니다. 두 플랫폼 모두 필요한 경우 지금은 별도의 아키텍처 옵션으로 사용할 계획입니다. 통합에 대한 타임라인에 대한 자세한 내용은 Adobe 계정 관리자에게 문의하십시오.

## 관련 지침

- [플랫폼 및 서비스](platform-and-services.md)
- [아키텍처 옵션](../architecture-options/overview.md)
- [시작하기](../get-started/get-started-by-role.md)
