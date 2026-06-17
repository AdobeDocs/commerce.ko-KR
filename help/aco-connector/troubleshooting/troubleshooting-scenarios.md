---
title: ' [!DNL Adobe Commerce Optimizer Connector]에 대한 시나리오 문제 해결'
description: 동기화 결과를 잘못 구성하거나 잘못 해석하여  [!DNL Adobe Commerce Optimizer Connector] 의 예기치 않은 동작을 진단하고 해결합니다.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="PaaS만" type="Informative" url="https://experienceleague.adobe.com/ko/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce 온 클라우드 프로젝트(Adobe 관리 PaaS 인프라) 및 온프레미스 프로젝트에만 적용됩니다."
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
subfeature_v2:
  - id: a40ebd6b-b542-4432-a730-1803ef74518d
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 516
ht-degree: 0%

---


# [!DNL Adobe Commerce Optimizer Connector]에 대한 시나리오 문제 해결

이 페이지에서는 [!DNL Adobe Commerce Optimizer Connector] 작업을 수행할 때 일반적으로 잘못된 구성 또는 동기화 결과 해석으로 인해 발생할 수 있는 동작을 설명합니다. 아래 설명을 사용하여 근본 원인을 식별하고 적절한 해결 방법을 적용하십시오.

## 피드 상태에 &quot;성공&quot;이 표시되지만 데이터가 [!DNL Adobe Commerce Optimizer]에 표시되지 않습니다.

**문제:** **[!UICONTROL Data Feed Sync Status]** 페이지에서 동기화가 성공했다고 보고했지만 제품, 가격 등이 [!DNL Adobe Commerce Optimizer]에 예상대로 표시되지 않습니다.

**원인:** 피드 상태가 성공하면 수집 끝점에서 데이터를 수락한 것이며 [!DNL Adobe Commerce Optimizer]을(를) 통해 전파가 완료된 것이 아닙니다. 전파 시간은 수집 후 몇 분 정도 소요될 수 있습니다.

**솔루션:**

- 잠시 기다린 후 [!DNL Adobe Commerce Optimizer] 보기를 새로 고치십시오.
- [!DNL Adobe Commerce]에 구성된 테넌트 ID가 확인 중인 [!DNL Commerce Optimizer] 환경과 일치하는지 확인하십시오.
- [!DNL Commerce Optimizer]에서 올바른 [카탈로그 원본](../../optimizer/setup/catalog-sources.md)(스토어 보기 코드) 또는 가격 책자가 선택되어 있는지 확인하십시오.

## 내보낸 카탈로그에 제품이 없습니다.

**문제:** 전체 카탈로그 동기화 후 일부 제품이 [!DNL Adobe Commerce Optimizer]에 표시되지 않습니다.

**원인:** 내보내는 동안 제품의 유효성 검사가 실패하면 동기화에서 생략됩니다. 비활성화되거나 카탈로그에 표시되지 않는 제품은 제품 API에서 반환되지 않습니다.

**솔루션:**

- 영향을 받는 제품이 웹 사이트 및 카탈로그 소스로 사용되는 스토어 보기에 할당되었는지 확인합니다.
- 제품이 활성화되어 있고 카탈로그 목록이 포함된 가시성으로 설정되어 있는지 확인하십시오.
- **[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Feed Sync Status]**&#x200B;에서 카탈로그 피드에 대한 항목별 오류 세부 정보를 검토하십시오.

## [!DNL Adobe Commerce Optimizer]에서 가격이 잘못되었거나 누락되었습니다.

**문제:** 제품이 [!DNL Adobe Commerce Optimizer]에 표시되지만 [제품 GraphQL 쿼리](https://developer.adobe.com/commerce/services/reference/graphql/#products){target="_blank"}와(과) 함께 반환된 가격이 표시되지 않거나 [!DNL Adobe Commerce]에 구성된 가격과 일치하지 않습니다.

**원인:** 가격 정보 피드에서는 특정 웹 사이트 및 고객 그룹에 매핑되는 범위를 사용합니다. [카탈로그 보기](../../optimizer/setup/catalog-view.md) 구성이 잘못되면 가격이 누락되거나 잘못 책정될 수 있습니다.

**솔루션:**

- 웹 사이트가 커넥터의 내보내기 구성에서 동기화되도록 구성되어 있는지 확인합니다. [데이터 내보내기 구성 사용자 지정](../get-started.md#customize-the-commerce-scopes-export-configuration)을 참조하십시오.
- [!DNL Commerce Optimizer]에서 사용된 가격 장부 ID가 제품 쿼리를 수행하는 데 사용되는 [카탈로그 보기](../../optimizer/setup/catalog-view.md){target="_blank"} 구성에 있는지 확인하십시오.

## 동기화 후 [!DNL Adobe Commerce Optimizer]의 데이터를 덮어쓰거나 예기치 않게 수정했습니다.

**문제:** 외부 시스템(예: PIM 또는 ERP)에 의해 [!DNL Adobe Commerce Optimizer]에 직접 적용된 데이터 변경 내용은 커넥터가 동기화를 실행한 후 손실되거나 되돌려집니다.

**원인:** [!DNL Adobe Commerce] 이외의 시스템이 [!DNL Adobe Commerce Optimizer]에 직접 쓰는 경우(예: PIM 또는 다른 외부 시스템) 데이터 충돌이 발생할 수 있습니다. 커넥터는 [!DNL Adobe Commerce]에서 [!DNL Adobe Commerce Optimizer]&#x200B;(으)로 데이터 *단방향*&#x200B;을 동기화하며 변경 내용을 다시 [!DNL Adobe Commerce]&#x200B;(으)로 동기화하지 않습니다. 따라서 [!DNL Adobe Commerce Optimizer]에 직접 기록된 데이터는 [!DNL Adobe Commerce]에 반영되지 않으며 나중에 동기화하는 동안 덮어쓸 수 있습니다.


**솔루션:**

카탈로그 수정 사항을 [!DNL Adobe Commerce Optimizer]에 직접 쓰지 않고 [카탈로그 레이어](../../optimizer/setup/catalog-layer.md){target="_blank"}를 사용하여 [!DNL Adobe Commerce] 외부에서 변경 사항을 적용합니다. 카탈로그 계층을 사용하면 외부 시스템이 커넥터 동기화와 충돌하지 않고 [!DNL Adobe Commerce Optimizer] 내에서 카탈로그 데이터를 보강하거나 재정의할 수 있습니다.

## 일반적인 [!DNL SaaS Data Export] 문제에 대한 시나리오 문제 해결

커넥터에 영향을 줄 수 있는 기본 [!DNL SaaS Data Export]과(와) 관련된 문제에 대해서는 [시나리오 문제 해결 [!DNL SaaS Data Export]](../../data-export/troubleshooting/troubleshooting-scenarios.md)을 참조하십시오.
