---
title: ' [!DNL Adobe LLM Optimizer] 함께 사용 [!DNL Adobe Commerce]'
description: LLM Optimizer에서 Commerce 기회를 탐색하고, PDP 및 카탈로그 데이터 보강 작업을 검토하고,  [!DNL Adobe Commerce]에 업데이트를 배포하고, 관리 및 상점 첫 화면에서 확인하고, 재정의 및 수집이 기회를 부실 상태로 표시하는 방법에 대해 알아봅니다.
role: Admin, User
recommendations: noCatalog
badgePaas: label="PaaS만" type="Informative" url="https://experienceleague.adobe.com/ko/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce 온 클라우드 프로젝트(Adobe 관리 PaaS 인프라) 및 온프레미스 프로젝트에만 적용됩니다."
source-git-commit: 47348a44ff7c5f890c10594f44cae6e771be046f
workflow-type: tm+mt
source-wordcount: '1175'
ht-degree: 0%

---

# [!DNL Adobe Commerce]과(와) 함께 [!DNL Adobe LLM Optimizer] 사용

>[!IMPORTANT]
>
>이 통합에 대한 액세스가 제한됩니다. 자세한 내용은 기술 계정 관리자에게 문의하십시오.

[Commerce을 LLM Optimizer에 연결](connect-to-llmo.md)한 후에는 주로 **[!DNL Adobe LLM Optimizer]** UI에서 작업을 수행하여 기회를 검토하고 준비가 되면 승인된 변경 내용을 카탈로그에 푸시합니다. 이 문서에서는 두 가지 Commerce 중심 최적화 유형, **[!UICONTROL Opportunities]** 사용 방법, 배포 작업이 [!DNL Adobe Commerce]에서 작동하는 방법 및 외부 업데이트가 LLM Optimizer 제안과 상호 작용하는 방법에 대해 설명합니다. 통합에 대한 자세한 내용은 [통합 개요](../overview.md)를 참조하십시오.

## LLM Optimizer의 Commerce 최적화 이해 {#understand-optimizations}

Commerce 지원 카탈로그의 경우 LLM Optimizer은 **[!UICONTROL Product Detail Page Enrichment]** 및 **[!UICONTROL Product Catalog Enrichment]**&#x200B;을(를) 제공합니다.

| 포커스 | 용도는 무엇입니까 |
| --- | --- |
| **[!UICONTROL Product Detail Page Enrichment]**(PDP 보강) | 상점 레이아웃을 대체하지 않고 AI 기반 검색을 위한 제품 페이지 읽기 방식을 개선하는 제안입니다. |
| **[!UICONTROL Product Catalog Enrichment]** | 검토, 필요한 경우 편집 및 Commerce 카탈로그에 적용할 수 있는 특정 제품에 대해 **제품 이름** 및 **제품 설명** 업데이트를 제안했습니다. |

**[!UICONTROL Opportunities]**&#x200B;을(를) 사용하여 제품 또는 URL 목록을 열고 선택한 유형에 대한 제안을 통해 작업합니다.

## Commerce 기회 탐색 {#navigate-commerce-opportunities}

**Commerce 관련 기회를 열려면 다음을 수행하십시오.**

1. 왼쪽 레일에서 **[!UICONTROL Opportunities]**&#x200B;을(를) 클릭합니다.
1. [!DNL Adobe Commerce] 카탈로그를 대상으로 하는 최적화 유형을 표시하려면 **[!UICONTROL Commerce Opportunity]**&#x200B;을(를) 클릭하십시오.
1. 작업할 내용에 따라 **[!UICONTROL Product Catalog Enrichment]** 또는 **[!UICONTROL Product Detail Page Enrichment]**&#x200B;을(를) 선택하십시오.

![Commerce 기회 필터 및 최적화 유형](../assets/llmo-opportunities.png)

### 영업 기회 지표 이해 {#opportunity-metrics}

각 영업 기회 보기에는 영향을 요약하므로 작업의 우선 순위를 지정할 수 있습니다.

- **제품 페이지** 또는 **URL**: 해당 최적화 유형에 대해 평가된 페이지 또는 제품입니다.
- **에이전트 트래픽**: 영향력이 큰 기회의 우선 순위를 지정하는 데 도움이 되는 AI 에이전트가 시작한 방문 및 상호 작용

### 제안 상태 이해 {#suggestion-states}

두 데이터 보강 유형 모두 동일한 워크플로우 보기를 사용합니다.

- **[!UICONTROL Current Suggestions]**: 검토할 새 항목 또는 활성 항목입니다.
- **[!UICONTROL Fixed Suggestions]**: 이미 배포했거나 해결한 항목입니다.
- **[!UICONTROL Ignored Suggestions]**: 작업에서 의도적으로 제외한 항목입니다.

### PDP 보강 검토 및 배포 {#review-deploy-pdp}

PDP 보강은 AI 기반 검색에서 보다 명확한 제품 페이지 메시징을 원하는 팀을 위한 것이며 머천다이저가 설계된 상점 경험을 유지합니다.

**PDP 데이터 보강 검토 및 배포하려면:**

1. **[!UICONTROL Opportunities]**&#x200B;에서 **[!UICONTROL Product Detail Page Enrichment]** 열기
1. **[!UICONTROL URLs with Suggestions]** 테이블에서 **[!UICONTROL Current Suggestions]**&#x200B;을(를) 선택합니다.
1. URL 또는 SKU의 경우 **[!UICONTROL Preview]**&#x200B;을(를) 클릭하여 AI 분석 및 제안된 데이터 보강 기능을 검토합니다.
1. 선택 사항: 콘텐츠를 외부 편집기에 붙여넣으려면 **[!UICONTROL Copy]**&#x200B;을(를) 클릭하고, 바로 편집하려면 **[!UICONTROL Edit suggestion]**&#x200B;을(를) 클릭하십시오.
1. 선택 사항: 제안 사항이 전략과 일치하지 않으면 **[!UICONTROL Ignored Suggestions]**(으)로 이동하십시오.
1. 검토 및 승인되면 업데이트할 URL 또는 SKU의 행을 선택한 다음 **[!UICONTROL Deploy optimizations]**&#x200B;을(를) 클릭하고 확인합니다.

배포 후 제안이 LLM Optimizer에서 최적화 상태로 **[!UICONTROL Fixed Suggestions]**(으)로 이동합니다.

>[!NOTE]
>
>PDP 보강 배포에는 LLM Optimizer에서 완료된 **Edge에서 최적화** 온보딩이 필요합니다. 온보딩이 완료되지 않은 경우 UI에서 배포 전에 설정을 완료하라는 메시지를 표시합니다.

### 제품 카탈로그 보강 검토 및 배포 {#review-deploy-catalog}

카탈로그 보강은 Commerce에서 직접 제품 이름과 긴 설명을 조이려는 팀을 위한 것이며, 어떤 것도 저장하기 전에 검토할 수 있는 제안입니다.

**제품 카탈로그 데이터 보강 검토 및 배포하려면:**

1. **[!UICONTROL Opportunities]**&#x200B;에서 **[!UICONTROL Product Catalog Enrichment]** 열기
1. **[!UICONTROL URLs with Suggestions]** 테이블에서 **[!UICONTROL Current Suggestions]**&#x200B;을(를) 선택합니다.
1. 제안된 **제품 이름** 및 **제품 설명** 업데이트를 표시하려면 URL 또는 SKU 행의 확장 컨트롤을 클릭합니다.
1. 선택 사항: 배포하기 전에 제안된 이름 또는 설명을 조정하려면 편집 아이콘을 클릭합니다.
1. 선택 사항: 제안 사항이 전략과 일치하지 않으면 **[!UICONTROL Ignored Suggestions]**(으)로 이동하십시오.
1. 검토 및 승인되면 업데이트할 URL 또는 SKU의 행을 선택한 다음 **[!UICONTROL Deploy optimizations]**&#x200B;을(를) 클릭하고 확인합니다.

승인된 이름 및 설명 변경 내용은 다른 제품 업데이트처럼 [!DNL Adobe Commerce] 카탈로그에 저장됩니다.

>[!IMPORTANT]
>
>배포를 프로덕션 카탈로그 변경으로 처리합니다. 일반적인 변경 제어, 스테이징 및 QA 사례를 사용합니다. 머천다이징 및 SEO 이해 당사자가 최종 사본에 동의한 후에만 배포합니다.

배포 후 제안이 **적용됨** 상태로 **[!UICONTROL Fixed Suggestions]**(으)로 이동합니다.

## Commerce 관리에서 업데이트 확인 {#verify-in-admin}

**배포된 카탈로그 데이터 보강 확인:**

1. [!DNL Adobe Commerce] **관리자**&#x200B;에 로그인합니다.
1. **[!UICONTROL Catalog]** > **[!UICONTROL Products]**(으)로 이동합니다.
1. 필요에 따라 필터 및 **스토어 보기** 선택기를 사용한 다음(예: **[!UICONTROL Default Store View]**) **SKU**&#x200B;를 검색합니다.
1. 제품을 편집 모드로 엽니다.

   제품 양식에 보강된 **제품 이름**&#x200B;이 표시됩니다.

   ![LLM Optimizer 데이터 보강 후 제품 이름 필드](../assets/llmo-admin-name.png)

1. 선택 사항: 대신 수동으로 입력한 이름을 유지하려면 **[!UICONTROL Override LLM Optimizer provided Product Name]**&#x200B;을(를) 선택하십시오.

수동 재정의는 기회가 카탈로그와 계속 동기화되는 방식에 영향을 줍니다. [관리자의 수동 재정의](#manual-override-in-the-admin)를 참조하십시오.

1. **[!UICONTROL Content]** 섹션을 확장하고 **설명** 필드를 찾습니다.

   설명 변경을 배포하면 보강된 설명이 나타납니다.

   ![LLM Optimizer 데이터 보강 후 설명 필드](../assets/llmo-admin-description.png)

1. 선택 사항: 수동으로 입력한 설명을 대신 유지하려면 **[!UICONTROL Override LLM Optimizer provided Description]**&#x200B;을(를) 선택합니다.

## 상점 첫 화면에서 업데이트 확인 {#verify-storefront}

상점에서 SKU를 검색하고 PDP를 엽니다. **name**&#x200B;과(와) 긴 **description**&#x200B;을(를) 나타내는 모든 지역이 귀하가 승인한 내용을 반영하는지 확인하십시오. 또한 롤아웃과 관련이 있는 경우 동일한 카탈로그 속성을 사용하는 다운스트림 채널을 확인합니다.

<!--
## PDP enrichment rollback {#pdp-rollback}

If your project includes PDP enrichment opportunities, **rollback** behavior may support **bulk** or **per-URL** actions, depending on your LLM Optimizer release. Follow the in-product options for rollback. For **[!UICONTROL Product Catalog Enrichment]**, undoing a name or description in Commerce is effectively a new catalog edit or a follow-up opportunity, not a separate undo control in the Admin unless your team implements one.
-->

## 재정의, 수집 및 부실 기회 {#overrides-ingestion}

LLM Optimizer이 제품의 이름이나 설명을 업데이트하면 REST API 호출, CSV 가져오기, PIM 피드 또는 유사한 프로세스와 같은 다른 수집 시스템이 동일한 필드를 변경할 수 있습니다. 다음 섹션에서는 이 경우 발생하는 상황에 대해 설명합니다.

### 수집이 원래 카탈로그 값을 다시 보냅니다.

외부 프로세스가 원래 이름이나 설명(LLM Optimizer의 배포 전에 존재했던 값)을 작성하는 경우 Commerce은 통합 규칙에 따라 해당 필드에 LLM Optimizer이 배포한 값을 계속 적용합니다. 해당 수집만으로는 영업 기회가 자동으로 되돌릴 수 없습니다.

### 수집이 새 값을 전송합니다.

외부 프로세스에서 단순히 LLM Optimizer 이전 텍스트 반복이 아닌 새 값을 보내는 경우(예: &quot;Red Shoes&quot;를 &quot;Iconic Red Shoes&quot;로 이름 변경), 해당 새 카탈로그 값이 적용되며, 라이브 카탈로그가 더 이상 제안 컨텍스트와 일치하지 않으므로 관련된 LLM Optimizer 영업 기회는 일반적으로 LLM Optimizer에서 *Stale*&#x200B;으로 표시됩니다.

### 관리자의 수동 재정의 {#manual-override-in-the-admin}

[!DNL Adobe Commerce] *관리자*&#x200B;에서 제품 이름 또는 설명을 수동으로 편집하는 경우:

- *Admin* 값이 해당 수동 변경에 대한 레코드 시스템으로 사용됩니다.
- LLM Optimizer 영업 기회가 *부실*(으)로 표시되었습니다.
- LLM Optimizer에서 UI는 해당 영업 기회의 원래 상태로 돌아가므로 분석을 다시 실행할 경우 기준을 다시 지정하거나 새 제안을 수락할 수 있습니다.

이러한 규칙을 사용하면 여러 채널이 동일한 SKU를 터치할 때 LLM Optimizer, 수집 피드 또는 *관리자* 편집 권한이 있는지 여부를 알 수 있습니다.

## 우수 사례

- PIM 또는 피드 작업이 실수로 LLM Optimizer의 예상과 충돌하지 않도록 **제품 이름 및 설명에 대한 문서 시스템 소유권**.
- 제목 또는 설명을 일괄 배포하기 전에 **SEO 및 브랜드 팀과 조정**.
- 주요 카탈로그 가져오기 후 **다시 동기화** 또는 **다시 분석**&#x200B;하여 기회에 현재 카탈로그 상태가 반영되도록 합니다.

## 데모에서 사용해 보기

Frescopa 데모 환경을 사용하여 두 Commerce 영업 기회 유형이 작동 중인지 확인하십시오.

- [제품 카탈로그 강화 데모 보기](https://play.llmo.now/org/demo-org/opportunities/commerce-product-catalog-enrichment/e5f2a854-7477-421c-820f-74d5dd595647?siteId=9ae8877a-bbf3-407d-9adb-d6a72ce3c5e3)
- [제품 세부 사항 페이지 강화 데모 보기](https://play.llmo.now/org/demo-org/opportunities/commerce-product-page-enrichment/4e8b0428-0893-4864-a00e-fc1d77fb3372?siteId=9ae8877a-bbf3-407d-9adb-d6a72ce3c5e3)

## 관련 항목

- [Adobe Commerce을 LLM Optimizer에 연결](connect-to-llmo.md)
- [통합 개요](../overview.md)
- [통합 제한 및 경계](../boundaries-limits.md)
