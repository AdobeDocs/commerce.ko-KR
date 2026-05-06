---
title: ' [!DNL Adobe LLM Optimizer]과(와)  [!DNL Adobe Commerce]  통합'
description: LLM의 카탈로그 신호를 모니터링하고 승인된 카탈로그 최적화를 배포하려면  [!DNL Adobe Commerce] to [!DNL Adobe LLM Optimizer] 을(를) 연결하세요.
role: Admin, User, Leader
recommendations: noCatalog
badgePaas: label="PaaS만" type="Informative" url="https://experienceleague.adobe.com/ko/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce 온 클라우드 프로젝트(Adobe 관리 PaaS 인프라) 및 온프레미스 프로젝트에만 적용됩니다."
source-git-commit: 47348a44ff7c5f890c10594f44cae6e771be046f
workflow-type: tm+mt
source-wordcount: '902'
ht-degree: 0%

---

# [!DNL Adobe Commerce]과(와) [!DNL Adobe LLM Optimizer] 통합

>[!IMPORTANT]
>
>이 통합에 대한 액세스가 제한됩니다. 자세한 내용은 기술 계정 관리자에게 문의하십시오.

[!DNL Adobe LLM Optimizer]은(는) 브랜드가 대형 언어 모델(LLM) 및 AI 어시스턴트의 응답에 콘텐츠가 표시되는 방식을 모니터링, 분석 및 최적화할 수 있도록 지원하는 엔터프라이즈 솔루션입니다. 쇼핑객들이 리서치 및 제품 검색에 AI 도구를 점점 더 많이 사용함에 따라 LLM Optimizer은 브랜드와 카탈로그가 컨텍스트에 맞게 정확하게 인용되고 표면화되도록 지원합니다.

이 안내서에서는 제품 카탈로그를 Commerce에 저장할 때 **[!DNL Adobe Commerce]**&#x200B;이(가) 해당 워크플로에 어떻게 적합한지 설명합니다. 사용 가능한 기능, 필요한 구성 및 배포된 최적화가 관리 및 수집 채널에서 어떻게 작동하는지 알아봅니다.

>[!NOTE]
>
>[!DNL Adobe LLM Optimizer]은(는) 독립 실행형 Adobe 솔루션입니다. 핵심 모니터링 및 영업 기회 워크플로에는 [!DNL Adobe Experience Manager]&#x200B;(AEM) 또는 기타 Adobe 애플리케이션이 필요하지 않습니다. Commerce 특정 배포 작업은 카탈로그가 LLM Optimizer에 연결되어 있고 승인된 변경 내용을 [!DNL Adobe Commerce]에 푸시하도록 선택하는 경우에만 적용됩니다.

## 통합으로 얻을 수 있는 이점 {#what-integration-enables}

LLM Optimizer을 [!DNL Adobe Commerce] 카탈로그에 연결하면 광범위한 콘텐츠 인사이트에서 **카탈로그 인식** 권장 사항으로 이동할 수 있습니다.

- LLM에서 제품을 해석하는 방식에 영향을 주는 제목, 설명, 구조화된 신호와 같은 카탈로그 데이터의 불일치와 **확인**&#x200B;합니다.
- **검토**&#x200B;에서는 유효성 검사 및 전후 비교를 포함하여 지원 컨텍스트와 관련된 개선 사항을 제안했습니다.
- **제품 이름 및 설명 업데이트와 같은 선택한 최적화 항목을 Commerce 카탈로그에 직접 배포하여 관리 워크플로, 그리드 및 상점 관련 데이터를 일관되게 유지합니다.**

카탈로그 원본이 [!DNL Adobe Commerce]인 경우 Adobe은 기회를 자동으로 식별하고, 변경 사항을 제안하고, 승인된 수정 사항을 적용하는 전체 통합 워크플로우를 지원할 수 있습니다. Commerce 외부에서 가져온 카탈로그의 경우 LLM Optimizer에서 여전히 분석하고 개선 사항을 제안할 수 있지만, 변경 사항을 적용하는 것은 통합 모델(예: 미러링된 카탈로그 또는 수동 업데이트)에 따라 다릅니다. [통합 제한 및 경계](boundaries-limits.md)를 참조하십시오.

## 이 대상이 누구입니까 {#who-this-is-for}

- LLM 기반 답변에서 제품 데이터가 정확하고 일관되기를 원하며 대규모로 카탈로그 복사본을 개선하기 위해 통제된 방법이 필요한 **디지털 마케터 및 머천다이저**.
- 제품 특성을 제공하는 카탈로그 무결성, 관리 프로세스 및 통합(API, CSV, PIM)을 소유한 **Commerce 관리자**.

## 사전 요구 사항 {#prerequisites}

Adobe LLM Optimizer과의 Adobe Commerce 통합에 대해 **액세스**&#x200B;를 받은 경우 다음 전제 조건이 적용됩니다. 자세한 내용은 기술 계정 관리자에게 문의하십시오.

- 이 LLM Optimizer 측정 및 크롤링 기능은 크롤링의 일반적인 카탈로그 인식 통찰력을 위한 전제 조건인 LLM 중심의 봇과 agen제틱 봇을 통해 스토어를 구성할 수 있습니다.
- Commerce 지원 배포 워크플로우의 경우 필요한 Commerce 서비스 및 카탈로그 연결이 활성화되며 정상입니다. 작업 수준 설정은 [Adobe Commerce과 LLM Optimizer 연결](get-started/connect-to-llmo.md)에 설명되어 있습니다.

또한 시스템 간에 데이터가 어떻게 이동하는지 이해해야 합니다.

### 높은 수준의 데이터 흐름 {#high-level-data-flow}

개념적으로 카탈로그 최적화는 다음 두 가지 패턴을 따릅니다(기능에 따라 프로젝트에서 하나 또는 둘 다를 사용할 수 있음).

| 방향 | 목적 |
| --- | --- |
| **Commerce 카탈로그 -> LLM Optimizer** | 카탈로그 및 URL은 LLM Optimizer UI에서 피드 기회와 제안을 신호로 보냅니다. |
| **LLM Optimizer -> Commerce** | 배포 작업을 승인하면 제품 이름 및 설명에 대한 업데이트가 기본 Commerce 카탈로그에 기록되므로 관리자와 상점 모두 최적화된 값을 반영합니다. |

### [!DNL Adobe Commerce]을(를) 타사 카탈로그와 비교 {#commerce-vs-third-party}

| 카탈로그 소스 | 일반적인 LLM Optimizer 범위 |
| --- | --- |
| **[!DNL Adobe Commerce]** | 식별 및 제안 사항에 대한 강력한 지원과 사용자가 구성하는 승인된 카탈로그 필드 업데이트 배포 |
| **타사 상거래** | 식별 및 제안 기능이 지원됩니다. 판매자 시스템으로의 자동 배포는 판매자의 소스 카탈로그에 대한 직접 쓰기가 아닌 내보내기, 미러링 또는 파트너 워크플로에 따라 달라집니다. |

## Catalog Agent, Storefront MCP 및 LLM Optimizer {#catalog-agent-and-mcp}

[!DNL Adobe Commerce] **제품 카탈로그**&#x200B;는 이름, 설명, 특성, 가격 및 인벤토리와 같은 제품 데이터의 기록 시스템입니다. AI 지원 검색 및 최적화를 지원하기 위해 **Adobe Commerce Storefront MCP**(Model Context Protocol)는 라이브 Commerce 카탈로그 데이터와 Adobe AI 경험 사이의 구조화된 인터페이스입니다.

**카탈로그 에이전트**&#x200B;이(가) Storefront MCP 위에 있습니다. 카탈로그 에이전트를 사용하면 [!DNL Adobe LLM Optimizer]에서 간격을 식별하고 개선 사항을 제안하고 승인할 때 변경 사항을 배포하여 카탈로그 및 PDP 컨텍스트를 쿼리하고 보강하고 사용할 수 있습니다. 이러한 기능은 [LLM Optimizer과 함께 LLM Optimizer 사용](get-started/use-llmo-with-commerce.md)에 설명된 Adobe Commerce 워크플로에 표시됩니다.

## 카탈로그 에이전트가 LLM용 Commerce을 개선하는 방법 {#catalog-agent-optimizations}

카탈로그 에이전트는 제품 세부 사항 페이지 보강과 제품 카탈로그 보강이라는 두 가지 상호 최적화 기능을 통해 검색 기능을 해결합니다.

### 제품 세부 사항 페이지 보강 {#pdp-enrichment-overview}

**PDP(Product Detail Page) 강화**&#x200B;는 제품 페이지 콘텐츠에 대한 세분화를 제안하므로 구매자가 AI 지원 및 유사한 도구를 통해 제품을 발견하는 경우 상품을 보다 명확하게 읽을 수 있습니다. 목표는 팀에서 이미 머천다이징한 상점 레이아웃을 변경하지 않고 명확성과 일관성을 향상시키는 것입니다. LLM Optimizer에서 제안을 검토하고 준비가 되면 배포합니다.

배포한 후 라이브 제품 페이지를 스팟 확인하여 쇼핑 경험이 예상대로 유지되는지 확인하십시오.

### 제품 카탈로그 강화 {#catalog-enrichment-overview}

**제품 카탈로그 보강**&#x200B;은(는) 사본이 얇거나 모호하거나 일관성이 없는 보다 명확한 **제품 이름** 및 **제품 설명**&#x200B;을 제안합니다. 각 제안에는 컨텍스트가 포함되어 있으므로 팀이 변경할 내용을 결정할 수 있습니다. 업데이트를 승인하면 해당 업데이트를 [!DNL Adobe Commerce] 카탈로그에 적용하여 관리자, 상점 및 해당 필드를 사용하는 다른 경험에서 동일한 단어를 반영하도록 할 수 있습니다.

이러한 필드는 Commerce에 있으므로 이름 또는 설명을 한 번 개선하면 해당 제품 데이터를 읽는 모든 채널에 도움이 될 수 있습니다(시스템을 새로 고치는 방법과 시기에 따라 다름).

## 관련 항목 {#related-topics}

- [Adobe Commerce을 LLM Optimizer에 연결](get-started/connect-to-llmo.md)
- [Adobe Commerce과 함께 LLM Optimizer 사용](get-started/use-llmo-with-commerce.md)
- [통합 제한 및 경계](boundaries-limits.md)
