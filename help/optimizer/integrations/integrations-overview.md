---
title: Commerce Optimizer 통합
description: 카탈로그 동기화, 에셋 관리, 상점 최적화 및 Salesforce Commerce Cloud 연결을 위한 Adobe Commerce Optimizer 통합에 대해 알아봅니다.
solution: Commerce
feature: Integration, Catalog Management
role: Developer, Admin
level: Beginner
badgeSaas: label="SaaS만" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip=" [!DNL Adobe Commerce Optimizer] 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."
exl-id: 8f3a2c1b-9d4e-5f6a-bc7d-1e2f3a4b5c6d
source-git-commit: d8cd6f543353e1b11f3aa14b3b97b02155d23809
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---


# [!DNL Adobe Commerce Optimizer] 통합

[!DNL Adobe Commerce Optimizer]에는 Adobe Commerce on cloud 또는 온-프레미스에서 데이터를 동기화하고, 자산을 관리하고, 상점 경험을 개선하고, 외부 시스템을 연결할 수 있는 통합이 포함되어 있습니다. 아래 섹션에서는 각 통합이 [!DNL Adobe Commerce Optimizer]에서 작동하는 방식을 설명합니다. 설정, 구성 및 일상적인 사용을 위해 링크를 따르십시오.

## Adobe Commerce Optimizer 커넥터 {#aco-connector}

Adobe Commerce Optimizer 커넥터는 Adobe Commerce(클라우드 또는 온-프레미스)와 [!DNL Adobe Commerce Optimizer] 간의 카탈로그 및 가격 데이터를 동기화하는 브리지입니다. 커넥터를 사용하도록 설정하면 Commerce은 제품 데이터 기록 시스템으로 남고, [!DNL Adobe Commerce Optimizer]은(는) 제품 검색, 권장 사항, 머천다이징 규칙, 분석 및 Headless Storefront 경험을 강화합니다.

- [Adobe Commerce Optimizer 커넥터 개요](../../aco-connector/overview.md){target="_blank"}
- [커넥터 시작](../../aco-connector/get-started.md){target="_blank"}

## AEM Assets을 사용한 제품 시각화 {#product-visuals}

제품 비주얼을 사용하면 Adobe Experience Manager(AEM) Assets을 통해 제품 이미지를 관리할 수 있습니다. Commerce Optimizer용 AEM Assets을 구성하여 제품 비주얼을 활성화합니다. 구성을 마친 후에는 AEM Assets 카탈로그와 이미지를 계속 동기화할 수 있는 자동화된 자산 검토 및 관리 워크플로우를 통해 Commerce Optimizer을 제품 이미지에 대한 중앙 집중식 디지털 자산 관리 솔루션으로 사용합니다. 이 통합은 자산을 SKU별 제품에 일치시킵니다. 업데이트는 Adobe의 통합 서비스를 통해 진행되므로 상점이 수동으로 다시 업로드하지 않고도 최신 미디어를 반영합니다.

- [AEM Assets을 사용한 제품 시각화](../setup/product-visuals.md)
- [Commerce Optimizer용 AEM Assets 구성](../../aem-assets-integration/get-started/configure-aco.md){target="_blank"}

## Adobe Experience Manager Sites Optimizer {#aem-sites-optimizer}

Adobe Experience Manager Sites Optimizer은 Commerce 웹 사이트를 분석하고 검색, 참여 및 전환을 개선하는 데 도움이 되는 권장 사항인 AI 기반 **[!UICONTROL Opportunities]**&#x200B;을(를) 표시하여 성능을 향상시킵니다.

>[!AVAILABILITY]
>
>이 기능을 사용하려면 **Ultima** Adobe Sites Optimizer 라이선스가 필요합니다. Adobe Customer Technical Advisor를 통해 라이선스를 요청할 수 있습니다. 계정이 프로비저닝되면 [!DNL Adobe Commerce Optimizer] 인터페이스에서 영업 기회 기능을 사용할 수 있으며, AI 기반 인사이트를 사용하여 상점 및 머천다이징 전략을 최적화할 수 있습니다.

- [영업 기회](../manage-results/opportunities.md)

## Commerce Salesforce 커넥터 {#commerce-salesforce-connector}

Commerce Salesforce 커넥터(Adobe App Builder에 구축됨)는 카탈로그와 Salesforce Commerce Cloud B2C의 가격 데이터를 [!DNL Adobe Commerce Optimizer]&#x200B;(으)로 동기화하므로 Salesforce 상거래 백엔드를 교체하지 않고도 Adobe 상점 및 머천다이징 기능을 사용할 수 있습니다. Salesforce Commerce API를 사용하여 동기화를 예약하고, 온디맨드 업데이트를 실행하고, 통합을 확장할 수 있습니다.

- [Salesforce Commerce 커넥터](../developer/salesforce-connector.md)

>[!MORELIKETHIS]
>
>- [Adobe Commerce Optimizer 기술 설명서](https://developer.adobe.com/commerce/services/optimizer/){target="_blank"}
>- [Adobe Commerce Optimizer 시작](../get-started.md)
