---
title: 참조 아키텍처
description: 상점, 서비스 및 카탈로그 동기화 파이프라인과 같은 일반적인 Adobe Commerce 구현을 위한 참조 아키텍처 패턴에 대해 알아봅니다.
role: Developer, Leader
feature: Storefront, Integration
recommendations: noCatalog
autotag-review: '2026-10-20T11:42:09.021Z'
TQID: 'https://experienceleague.adobe.com/GVbGyRZz8llMWcUykcXXZwWnTaAomHVCTcV3ft49IEc'
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
  - id: 8dc0e58b-adf0-51bb-8db5-bb36e3e656fb
    internal-label: Inventory
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
  - id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
    internal-label: Commerce ecosystem
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
source-git-commit: ca6bb3543583c865c42b8f4d84f01e27a04f9223
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%
---

# 참조 아키텍처

다음 설명서는 다양한 배포 모델 및 사용 사례에서 Adobe Commerce 플랫폼 및 서비스에 대한 참조 아키텍처 패턴을 제공합니다.

- [Adobe Commerce as a Cloud Service 아키텍처](/help/cloud-service/overview.md#architecture)
- [Adobe Commerce 엔터프라이즈 참조 아키텍처](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/architecture/enterprise-blueprint){target="_blank"}
- [Adobe Commerce storefront 아키텍처](https://experienceleague.adobe.com/en/tools/commerce-storefront/get-started/architecture/){target="_blank"}
- [클라우드 인프라 아키텍처의 Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/architecture/cloud-architecture){target="_blank"}

## Edge Delivery Services 기반 Storefront

Adobe Commerce 또는 [!DNL Adobe Commerce Optimizer]에 백엔드로 연결된 드롭인 구성 요소 및 콘텐츠 블록을 사용하여 Adobe Commerce 보일러플레이트에 빌드된 상점. [Adobe Commerce 상점 개요](https://experienceleague.adobe.com/en/tools/commerce-storefront/)를 참조하세요.

- [Adobe Commerce storefront 아키텍처](https://experienceleague.adobe.com/en/tools/commerce-storefront/get-started/architecture/)

## 카탈로그 동기화 파이프라인

Adobe Commerce 및 Adobe Commerce 서비스(Commerce Optimizer, Live Search, Catalog Service, 제품 추천 및 기타 연결된 [Commerce 서비스](../../landing/home.md)) 간에 카탈로그, 가격 및 인벤토리 데이터를 동기화하기 위한 데이터 흐름입니다.

- Adobe Commerce as a Cloud Service, 클라우드 인프라 또는 온-프레미스 배포의 경우 [SaaS 데이터 내보내기와 데이터 동기화](/help/data-export/sync-overview.md)를 참조하십시오.

- Adobe Commerce on cloud infrastructure 또는 Adobe Commerce Optimizer Connector로 구성된 온프레미스의 경우 [커넥터 동기화 파이프라인](/help/aco-connector/connector-sync-pipeline.md)을(를) 참조하십시오.


## 관련 지침

- [구현 아키텍처](implementation-architectures.md)
