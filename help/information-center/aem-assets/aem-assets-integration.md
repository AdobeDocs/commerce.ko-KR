---
title: Commerce용 AEM Assets 통합
description: AEM Assets을 Adobe Commerce, Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer과 통합하여 제품 이미지 및 미디어를 중앙에서 관리하는 방법에 대해 알아봅니다.
role: Admin, Developer, Leader
feature: Storefront, Integration
recommendations: noCatalog
autotag-review: '2026-10-20T01:34:13.564Z'
TQID: 'https://experienceleague.adobe.com/v15DE37DoqpstrsWqnwd6DYpa5moT-BhQ80zDq2KP6I'
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
  - id: 00451af3-7b97-5414-9992-3a6c269e413f
    internal-label: Paas
  - id: 4067ab89-2e97-5de1-8d98-de8318461a8d
    internal-label: Products
  - id: 4ca54350-01cb-5b22-8966-5f2873dc6d90
    internal-label: Media
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
source-git-commit: ca6bb3543583c865c42b8f4d84f01e27a04f9223
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 4%
---

# Commerce용 AEM Assets 통합

AEM Assets 통합을 통해 Adobe Commerce의 제품 시각화 기능을 사용할 수 있으므로 AEM Assets의 중심에서 제품 이미지, 비디오 및 기타 미디어를 관리할 수 있습니다. 별도의 Commerce 플랫폼이 아닌 모든 Commerce 아키텍처 옵션과 함께 작동하는 선택적 추가 기능입니다.

## 아키텍처별 통합 경로

두 가지 통합 경로가 있습니다. 경로는 Commerce 아키텍처에 따라 다릅니다.

| Commerce 아키텍처 | AEM Assets 통합 경로 | 자세히 알아보기 |
| --- | --- | --- |
| 클라우드 또는 온프레미스의 [!DNL Adobe Commerce] | Commerce에 대한 [!DNL AEM Assets] 통합. Commerce 통합 패키지를 사용하여 [!DNL Adobe Commerce]과(와) [!DNL AEM Assets] 간에 제품 이미지, 비디오 및 기타 미디어를 동기화하고 관리합니다. | [Commerce용 AEM Assets 통합](/help/aem-assets-integration/overview.md) |
| [!DNL Adobe Commerce as a Cloud Service] | [!DNL AEM Assets]에서 제공하는 [!DNL Product Visuals] | [AEM Assets 통합 설정](/help/aem-assets-integration/overview.md#next-steps) |
| 독립 실행형 [!DNL Adobe Commerce Optimizer] | [!DNL AEM Assets]에서 제공하는 [!DNL Product Visuals]. 기본 카탈로그 및 가격 데이터가 [Optimizer 데이터 수집 API](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/)를 통해 도착합니다. | [AEM Assets을 사용한 제품 시각적 개체](/help/optimizer/setup/product-visuals.md) |
| [!DNL Adobe Commerce Optimizer Connector]이(가) 있는 [!DNL Adobe Commerce] | [!DNL AEM Assets]에서 제공하는 [!DNL Product Visuals]. 카탈로그 및 가격 데이터는 커넥터가 [!DNL Adobe Commerce]에서 동기화합니다. | [Commerce Optimizer 통합](/help/optimizer/integrations/integrations-overview.md) |

[!DNL Product Visuals]은(는) Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer의 통합 경로입니다. AEM에서 관리하는 제품 이미지를 Commerce 카탈로그 계층에 동기화하고 상점 API를 통해 상점 경험에 전달합니다.

## 선택하기 전에

- 설정 및 라이선스 요구 사항은 Commerce on cloud 또는 on-premise 경로와 Commerce as a Cloud Service 또는 Adobe Optimizer [!DNL Product Visuals] 경로 간에 다릅니다. 먼저 배포별 요구 사항을 검토하십시오.
- [!DNL AEM Assets]에서 디지털 자산을 관리합니다. Commerce 카탈로그, 가격 책정, 장바구니, 체크아웃 또는 주문 시스템을 대체하지 않습니다.
- 제품 에셋은 SKU 또는 기타 문서화된 일치 메타데이터를 사용하여 Commerce 제품과 일치합니다.
- 마케팅 및 머천다이징 팀에 중앙 집중식 제품 이미지 및 자산 워크플로우가 필요한 경우 Commerce 아키텍처와 일치하는 경로를 선택합니다.

## 관련 정보

- [Adobe Experience Manager Assets 설명서](https://experienceleague.adobe.com/ko/docs/experience-manager-cloud-service/content/assets/overview)
- [아키텍처 개요](../architecture-options/overview.md)
- [API](../apis/commerce-apis.md)
