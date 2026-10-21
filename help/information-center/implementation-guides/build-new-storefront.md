---
title: 새 상점 만들기
description: Edge Delivery Services, Commerce 드롭인 구성 요소, 콘텐츠 블록 및 템플릿을 사용하여 새 Adobe Commerce 스토어를 계획하고 구축하는 방법에 대해 알아봅니다.
role: Developer, Leader
feature: Storefront
recommendations: noCatalog
autotag-review: '2026-10-20T10:58:53.700Z'
TQID: 'https://experienceleague.adobe.com/z-PCoaJzaOyd7SlxjyWs-0tEVo3hpdHucdgq4cZSeQw'
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
  - id: bcd8874c-7b93-5596-bdaa-22660e84df14
    internal-label: Deploy
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: ca6bb3543583c865c42b8f4d84f01e27a04f9223
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%
---

# 새 상점 만들기

Adobe Commerce 고객 중 다음과 같은 배포 유형을 사용하는 고객은 Edge Delivery Services, Commerce 드롭인 구성 요소 및 콘텐츠 블록을 사용하여 새 스토어를 구축할 수 있습니다.

- Adobe Commerce as a Cloud Service
- Adobe Commerce Optimizer
- Adobe Commerce on cloud 또는 Adobe Commerce Optimizer 없이 Storefront 서비스를 사용하는 온프레미스
- Adobe Commerce on cloud 또는 Adobe Commerce Optimizer Connector를 사용한 온프레미스

Adobe Commerce 보일러판을 사용하면 Adobe Commerce 또는 [!DNL Adobe Commerce Optimizer] 인스턴스를 사용자 지정하고 연결할 수 있는 작업 저장소를 제공합니다.

>[!NOTE]
>
>Adobe Commerce 온 클라우드 인프라 또는 온프레미스의 경우 커넥터를 통해 Adobe Commerce Optimizer을 채택하는 것은 요구 사항이 아닌 하나의 상점 현대화 옵션입니다. 이 경로를 선택하는 경우 [Luma Bridge](https://experienceleague.adobe.com/en/tools/commerce-storefront/setup/discovery/luma-bridge/)을(를) 사용하여 Luma 스토어프런트 및 Edge Delivery Services 스토어를 연결합니다.

## 시작

1. 아키텍처 및 사용 가능한 드롭인 구성 요소를 이해하려면 [Adobe Commerce Storefront 개요](https://experienceleague.adobe.com/en/tools/commerce-storefront/merchants/quick-start/create-content/) 및 [Storefront 아키텍처](https://experienceleague.adobe.com/en/tools/commerce-storefront/get-started/architecture/) 설명서를 검토하십시오.

1. Storefront를 설정하려면 다음 Storefront 설명서를 따르십시오.

   - [상점 만들기](https://experienceleague.adobe.com/en/tools/commerce-storefront/get-started/create-storefront/)
   - 프로젝트를 범위 지정, 설정 및 시작하려면 [Storefront 개발자 안내서](https://experienceleague.adobe.com/en/tools/commerce-storefront/get-started/).

1. Commerce 백엔드에 스토어프론트를 연결합니다.

   배포 모델을 기반으로 지침을 따릅니다. 자세한 내용은 _Storefront 개발자 안내서_&#x200B;의 [백엔드 옵션](https://experienceleague.adobe.com/en/tools/commerce-storefront/get-started/backends/){target="_blank"}을 참조하십시오.

## 관련 지침

- [Adobe Commerce Storefront 개요](https://experienceleague.adobe.com/en/tools/commerce-storefront/merchants/quick-start/create-content/)
- [Adobe Commerce Optimizer 활성화](enable-aco.md)
- [Adobe Commerce Optimizer 커넥터](../../aco-connector/overview.md)
- [AEM Assets 연결](connect-aem-assets.md)
- [Storefront 백엔드 옵션](https://experienceleague.adobe.com/en/tools/commerce-storefront/get-started/backends/){target="_blank"}
