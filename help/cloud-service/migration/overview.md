---
title: ' [!DNL Adobe Commerce as a Cloud Service](으)로 마이그레이션'
description: ' [!DNL Adobe Commerce as a Cloud Service](으)로 마이그레이션하는 방법에 대해 알아봅니다.'
feature: Cloud
exl-id: 9065c92a-f6b2-4464-8ec0-5c549bf78104
badgeSaas: label="SaaS만" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."
role: Developer
level: Intermediate
autotag-review: '2026-06-18T16:12:28.840Z'
TQID: 'https://experienceleague.adobe.com/GmxaQdGKvAIDpZ2jvmlLFSYw0IFQysIMOT0lUnsJBsI'
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: ba9e5be9-7de1-4f71-a5d2-baead0e425eeid: bd989d82-1e15-4534-88db-f1f51dd77ffaid: c1256247-af4b-46d8-9dca-0c654ecfa157id: c18ed297-2187-4aec-affb-9d9654eca6fcid: c32adafa-ed01-4b31-997e-2413013911b0id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
subfeature_v2: id: e91a50b1-0b31-436e-9033-00e4776e94cbid: f56d26ed-050b-4fb7-b29b-8e6e994e80a2id: f8ddfd3b-6194-46e8-a176-0e918039be56
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2: id: addc3a3a-2b1c-4fdf-aea4-4b1eb2931ba6id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1id: d095671a-1355-40aa-8b5f-06c33c68080bid: eb30f47f-d87a-400f-8f78-63ce7979ff56id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: e03840ea9e0e43a005f385914e8599804383e79d
workflow-type: tm+mt
source-wordcount: 3305
ht-degree: 0%

---

# [!DNL Adobe Commerce as a Cloud Service]&#x200B;(으)로 마이그레이션

이 안내서는 개발자가 [!DNL Adobe Commerce on Cloud] 또는 온프레미스에서 [!DNL Adobe Commerce as a Cloud Service]&#x200B;(SaaS)로 전환하는 데 도움이 됩니다. 이 SaaS 모델은 향상된 성능, 확장성 및 [!DNL Adobe Experience Cloud]과의 통합을 제공합니다.

>[!NOTE]
>
>마이그레이션 도구에 대한 자세한 내용은 [대량 데이터 마이그레이션 도구](./bulk-data/migration-tool.md)를 참조하세요.

## 개요

설정된 [!DNL Adobe Commerce] 스토어를 [!DNL Adobe Commerce as a Cloud Service]&#x200B;(으)로 마이그레이션하는 것은 데이터를 이동하는 것 이상입니다. 실제 마이그레이션은 다음 영역에 적용됩니다.

- 응용 프로그램 - [!DNL Adobe Commerce on Cloud] 또는 온-프레미스 설치용 사용자 지정 및 확장
- 데이터 - 카탈로그, 주문, 고객 및 구성
- 상점 첫 화면
- 외부 시스템과 통합

[!DNL Adobe Commerce as a Cloud Service]은(는) 버전이 없는 SaaS 플랫폼입니다. 즉, 이러한 영역을 조정하지 않고 마이그레이션할 수 없습니다. 맞춤화는 [!DNL App Builder] 응용 프로그램으로 현대화되고, 저장소는 Edge Delivery Services(EDS)에 다시 빌드되고, 데이터는 새 [!DNL Adobe Commerce as a Cloud Service] 테넌트로 마이그레이션되고, 통합은 SaaS 패턴을 사용하여 다시 설정됩니다.

Adobe은 마이그레이션을 단일 모놀리식 프로젝트로 간주하는 대신 [3개의 마이그레이션 도구](#migration-tools-workflow)를 중심으로 빌드된 통합 마이그레이션 워크플로를 제공합니다.

이 공유 워크플로우는 검색을 통합하고 엔지니어링 및 제공 팀을 조정하고 일관된 마이그레이션 계획을 제공합니다.

![마이그레이션 흐름 다이어그램](../assets/migration-flow.png)

### PaaS 및 SaaS 비교

[!DNL Adobe Commerce on Cloud] 또는 PaaS(온-프레미스) 및 SaaS([!DNL Adobe Commerce as a Cloud Service])는 관리 방법과 판매자가 플랫폼과 상호 작용하는 방법이 다릅니다.

**주요 차이점**

- [!BADGE PaaS만]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce 온 클라우드 프로젝트(Adobe 관리 PaaS 인프라) 및 온프레미스 프로젝트에만 적용됩니다."}
- **[!DNL Adobe Commerce on Cloud Infrastructure]**: 판매자가 응용 프로그램 코드, 업그레이드, 패치 및 인프라 구성을 관리합니다.
- **[!DNL Adobe Commerce]온-프레미스**: 판매자가 Adobe의 호스팅 환경 내에서 응용 프로그램 코드, 업그레이드, 패치, 인프라 구성을 관리합니다.

  >[!NOTE]
  >
  >서비스(MySQL, Elasticsearch 등)에 대한 [공유 권한 모델](https://experienceleague.adobe.com/en/docs/commerce-operations/security-and-compliance/shared-responsibility).

- [!BADGE SaaS만 해당]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."} **SaaS(신규 - [!DNL Adobe Commerce as a Cloud Service])**: Adobe에서 핵심 응용 프로그램, 인프라 및 업데이트를 완전히 관리합니다. 판매자는 확장성 지점(API, App Builder, UI SDK)을 통한 사용자 지정에 중점을 둡니다. 핵심 응용 프로그램 코드가 잠겨 있습니다.

**아키텍처 의미**

- **버전이 없는 플랫폼**: 지속적인 업데이트로 인해 core에 대한 주요 버전이 더 이상 업그레이드되지 않습니다.
- **마이크로서비스 및 API 우선**: 확장성 및 통합을 위해 API에 더 많이 의존합니다.
- **기본적으로 헤드리스(선택 사항)**: 분리된 상점(예: Edge Delivery Services에서 제공하는 Commerce 상점)에 대한 강력한 지원
- **Edge Delivery Services**: 프론트엔드 성능 및 배포에 영향을 줍니다.

**새로운 도구 및 개념**

- [Adobe Developer App Builder](https://developer.adobe.com/app-builder/) 및 [Adobe Developer App Builder용 API Mesh](https://developer.adobe.com/graphql-mesh-gateway/)
- [Commerce Optimizer](../../optimizer/overview.md)
- [Edge Delivery Services](https://experienceleague.adobe.com/developer/commerce/storefront/)
- [Commerce Cloud 관리자](../getting-started.md#create-an-instance)를 사용한 셀프서비스 프로비저닝

### 마이그레이션 여정

마이그레이션은 다음 단계를 통해 이동합니다.

- **평가** - 기존 구현을 분석하고 재고 사용자 지정, 통합, 상점 특성 및 데이터 구조를 고려하십시오. 분석 후 마이그레이션 권장 사항, 복잡성 점수 및 노력 예측과 함께 로드맵을 만듭니다.
- **응용 프로그램 현대화 및 데이터 마이그레이션** - 비즈니스 데이터를 [!DNL Adobe Commerce as a Cloud Service]&#x200B;(으)로 마이그레이션하는 동안 사용자 지정을 [!DNL App Builder] 응용 프로그램으로 다시 빌드합니다.
- **Storefront 현대화** - Commerce용 Edge Delivery Services(EDS)에서 Storefront를 다시 빌드합니다.
- **전환 및 작동** - 트래픽을 [!DNL Adobe Commerce as a Cloud Service]&#x200B;(으)로 전환하고 레거시 시스템을 해제하며 진행 중인 작업으로 전환합니다.

마이그레이션은 일반적으로 선형적이지 않고 반복적입니다. 기업은 최종 생산 전환 전에 여러 환경을 평가하고, 권장 사항을 검증하고, 점진적으로 현대화하고, 구현 계획을 구체화할 수 있습니다.

### 마이그레이션 도구 워크플로

다음 워크플로에는 각각 고유한 도구가 있습니다. 마이그레이션 전체에 사용되는 일반적인 블루프린트 역할을 하는 마이그레이션 평가를 통해 이를 함께 사용하여 마이그레이션을 완료합니다.

| 워크플로 | 도구 | 설명 |
| --- | --- | --- |
| [평가](#migration-assessment-tool) | **마이그레이션 평가 도구** | 사용자 지정 모듈, 타사 확장, 통합, 상점 관측, 데이터베이스 스키마, 사용자 지정 테이블, 마이그레이션 권장 사항, 복잡성 점수 및 현대화 작업 예측 등의 인벤토리를 작성하는 기존 구현에 대한 AI 기반 평가입니다. |
| [응용 프로그램 및 상점 현대화](#code-and-storefront-migration-commerce-developer-mcp) | **Commerce 개발자 MCP** | AI 지원 Commerce 애플리케이션 현대화, 맞춤화 [!DNL App Builder]&#x200B;(으)로의 마이그레이션 가속화, Edge Delivery Services(EDS)로의 상점 변환 지원, 개발자에게 엔지니어링 팀에서 검토 및 확인한 구현과 함께 광범위한 애플리케이션 현대화 여정을 안내합니다. |
| [데이터 마이그레이션](#data-migration-commerce-data-migration-service) | **Commerce 데이터 마이그레이션 서비스** | 카탈로그, 고객 및 주문 데이터를 [!DNL Adobe Commerce as a Cloud Service]&#x200B;(으)로 추출, 로드 및 무결성 확인. |

이 트랙은 독립 실행형이 아닙니다. 올바른 순서로 함께 사용하면 재작업을 최소화할 수 있습니다.

- **먼저 평가 실행** - 먼저 평가를 실행하면 지원되지 않는 사용자 지정 항목을 식별하고 마이그레이션 노력을 예측하며 데이터 마이그레이션 고려 사항을 표시하고 구현이 시작되기 전에 통합 종속성을 강조 표시합니다. 평가는 애플리케이션 현대화와 데이터 마이그레이션 워크플로 모두에서 사용되는 마이그레이션 블루프린트가 됩니다.
- **응용 프로그램 현대화** - Commerce 개발자 MCP는 마이그레이션 평가를 사용하여 현대화할 사용자 지정과 방법을 결정합니다. 그런 다음 MCP는 해당 [!DNL App Builder]개의 응용 프로그램과 상점 첫 화면 구성 요소를 생성합니다.
- **데이터 마이그레이션** - 데이터 마이그레이션 범위 지정 설문지는 평가에서 표시된 범위, 볼륨 및 사용자 지정 테이블을 캡처합니다.
- **사용자 지정 및 타사 데이터** - 타사 확장에 의해 사용자 지정 테이블에 보관된 데이터는 평가 중에 식별되지만 표준 데이터 마이그레이션에 의해 처리되지 않으며 [!DNL App Builder] 사용자 지정이 필요합니다.

Storefront 현대화는 단순한 UI 마이그레이션이 아닙니다. 비즈니스 기능을 마이그레이션하는 것 외에도 경험 아키텍처, 재사용 가능한 구성 요소 현대화, 성능 최적화 및 Edge Delivery Services 패턴 채택을 고려해야 합니다.

통합은 마이그레이션 평가의 일부로 평가되지만 구현에 따라 다릅니다. 통합은 [!DNL App Builder], [!DNL API Mesh], Adobe I/O Events 및 [!DNL Adobe Commerce as a Cloud Service] API를 활용할 수 있습니다.

이러한 마이그레이션 도구는 마이그레이션 평가를 중심으로 통합 마이그레이션 워크플로를 계속 확장하고 유지 관리합니다.

### 다음 단계

마이그레이션할 준비가 되면 평가를 생성해 보십시오. 마이그레이션 평가는 다음과 같은 나머지 마이그레이션에 대한 계획을 수립합니다.

마이그레이션 평가 도구 및 Commerce 개발자 MCP는 AI를 사용하여 검색, 계획 및 구현을 지원합니다. 엔지니어링 워크플로와 마찬가지로 AI가 생성한 권장 사항 및 구현은 표준 아키텍처, 테스트 및 품질 보증 프로세스의 일부로 팀에서 신중하게 검토하고 확인해야 합니다.

## 마이그레이션 평가 도구

개발 또는 마이그레이션을 시작하기 전에 마이그레이션 크기를 고려하여 개발이 필요한 항목을 결정해야 합니다. [!DNL Adobe Commerce on Cloud] 또는 온-프레미스에 있는 [!DNL Adobe Commerce] 저장소에는 사용자 지정 모듈, 통합, 상점 사용자 지정 및 데이터 구조가 있을 수 있으며, 이는 누군가 구현을 분석하기 전에는 명확하지 않을 수 있습니다. 마이그레이션 평가 도구는 코드베이스를 자동으로 검색하여 이러한 항목을 개발용으로 식별합니다.

### 평가 개요

마이그레이션 평가 도구는 기존 구현에 대한 AI 평가를 수행하고 구조화된 현대화 평가 및 [!DNL Adobe Commerce as a Cloud Service] 마이그레이션 로드맵을 생성합니다. 또한 애플리케이션 사용자 지정, 통합, 데이터 구조, 상점 특성 및 현대화에 영향을 주는 기타 구현 세부 사항을 평가하여 마이그레이션에 대한 포괄적인 보기를 구축합니다. 검색을 빠르고 반복 가능한 프로세스로 전환하여 약속을 수행하기 전에 노력, 위험 및 순서를 평가할 수 있습니다.

마이그레이션 평가 툴이 제공하는 평가는 단순한 보고서가 아닙니다. 평가는 마이그레이션 수명주기 전반에 걸쳐 계획, 구현 및 검증을 알리는 공유 마이그레이션 아티팩트가 됩니다. 마이그레이션 여정의 첫 번째 단계로, 이 조사 결과는 이후 애플리케이션 현대화와 데이터 마이그레이션 작업의 범위를 넓힙니다.

마이그레이션 평가 보고서에 포함된 내용과 사용 방법에 대한 자세한 내용은 [마이그레이션 평가](./assessment.md)를 참조하십시오.

### 평가 단계

평가는 기존 구현에 대해 실행되며 일련의 자동화된 단계를 통해 진행됩니다.

- **인벤토리** — 구현을 카탈로그화합니다. 포함 사항: 사용자 지정 모듈, 작성기 종속성, 타사 확장, 구성, 상점 구성 요소(해당되는 경우), 파일, 확장성 지점, 이벤트, 플러그인, API, cron 작업, 큐, 데이터베이스 스키마 및 사용자 지정 데이터베이스 테이블.
- **분석** — 정적 분석을 수행하여 저장소 사용자 지정, 표준 [!DNL Adobe Commerce] 설치와의 차이 및 이러한 사용자 지정 내용이 응용 프로그램 전체에서 상호 작용하는 방식을 식별합니다.
- **분류** — AI를 사용하여 각 사용자 지정을 해석하고, 사용자 지정이 수행하는 작업을 요약하고, 관련 기능을 그룹화하고, 구현 패턴을 식별하며, 상황에 맞는 마이그레이션 권장 사항을 제공합니다.
- **매핑 및 권장** - 기본 기능, [!DNL App Builder] 응용 프로그램 또는 Adobe 서비스를 포함하여 각 기능을 해당 [!DNL Adobe Commerce as a Cloud Service]에 매핑합니다. 그런 다음 평가는 현대화 경로를 권장하고 복잡성, 종속성 및 구현 노력을 평가합니다.
- **보고서** — 관련자들에게 위험을 전달할 수 있도록 마이그레이션 실행을 계획하기 위한 내보내기 가능한 로드맵을 생성합니다. 또한 우선 순위, 종속성, 기술 부채 및 구현 위험을 식별합니다.

### 평가 가치

평가의 가치는 개발 세부 사항을 적용하기 전에 가질 수 있는 신뢰의 양입니다. 정기적인 범위 지정 방법을 사용하여 마이그레이션을 추정하는 대신, 평가를 통해 구현에 대한 증거 기반 이해를 제공합니다. 여기에는 어떤 사용자 지정이 마이그레이션하기 쉽고, 다시 설계해야 하며, 어떤 항목을 폐기할 수 있는지 포함됩니다. 평가 결과 일반적으로 더 이상 사용되지 않거나 사용되지 않는 기능이 표시되므로 기술적인 문제를 줄일 수 있습니다.

각 권장 사항에는 기본 구현에 대한 인용과 함께 지원 증거가 포함되어 있으므로 설계자 및 엔지니어가 계획 수립 중에 유효성을 검사할 수 있습니다. 모든 평가는 동일한 방법론을 따르므로 일관된 채점 및 계획 프레임워크를 사용하여 여러 개발 요구 사항을 비교할 수 있습니다.

평가가 출발점만 한 것은 아니다. 다운스트림 마이그레이션 툴은 평가 결과를 사용하여 구현을 가속화하고 승인된 마이그레이션 계획과의 일관성을 유지합니다. 사용자 지정 분석은 애플리케이션 현대화의 청사진이 되며, 데이터 평가는 데이터베이스 크기, 엔티티 인벤토리 및 사용자 지정 테이블을 분석하여 데이터 마이그레이션 작업의 범위를 지정합니다.

### 평가 범위

마이그레이션 평가 도구는 전체 마이그레이션 환경을 파악하는 데 중점을 둡니다. 사용자 정의 모듈, 플러그인, 이벤트, API, cron 작업, 큐, 외부 시스템과의 통합, storefront 특성 및 이러한 사용자 정의가 의존하는 데이터베이스 스키마를 분석합니다. 평가는 검색한 내용을 사용 가능한 [!DNL Adobe Commerce as a Cloud Service] 기능에 매핑하고 [!DNL App Builder]을(를) 사용하여 기능을 현대화하거나 SaaS 아키텍처에 맞게 다시 디자인해야 하는 위치를 식별합니다.

평가는 실행 도구라기보다는 계획 도구에 가깝다. 현대화해야 할 사항을 식별하고 구현 복잡성을 예측하며 권장 사항을 제공합니다. 구현 의사 결정 및 아키텍처 유효성 검사는 Adobe, 파트너 및 고객 엔지니어링 팀 간의 공동 작업 활동으로 유지됩니다.

서드파티 확장에 의해 사용자 지정 테이블에 저장된 데이터는 마이그레이션 고려 사항으로 표시됩니다. 표준 데이터 마이그레이션은 이 데이터를 자동으로 마이그레이션하지 않습니다. 이러한 시나리오를 지원하려면 사용자 지정 [!DNL App Builder] 응용 프로그램이 필요할 수 있습니다. 자세한 내용은 [데이터 마이그레이션 안내서](#data-migration-commerce-data-migration-service)를 참조하세요.

평가는 상점 사용자 정의 및 데이터 마이그레이션 워크플로우에 대한 분석을 제공합니다.

- 코드 및 상점 마이그레이션 - 평가의 애플리케이션 분석은 Commerce 개발자 MCP의 청사진이 됩니다.
- 데이터 마이그레이션 - 평가의 엔티티 인벤토리, 데이터베이스 특성 분석 및 사용자 지정 테이블 분석은 Commerce 데이터 마이그레이션 서비스의 범위를 설정합니다.

애플리케이션이 발전함에 따라 평가를 다시 실행할 수도 있습니다. 이를 통해 팀은 수정 작업의 유효성을 검사하고, 현대화 진행 상황을 측정하며, 서비스 전반에 걸쳐 마이그레이션 계획을 지속적으로 구체화할 수 있습니다.

### 다음 단계

모든 [!DNL Adobe Commerce as a Cloud Service] 마이그레이션은 평가로 시작해야 합니다. 구현을 시작하기 전에 범위를 설정하고, 불확실성을 줄이고, 공유 마이그레이션 블루프린트를 만드는 저렴한 방법입니다.

평가 도구 및 다운스트림 개발자 워크플로에 대한 자세한 내용은 [Adobe Commerce 개발자 MCP](https://developer.adobe.com/commerce/extensibility/developer-agent/)를 참조하십시오.

## 코드 및 상점 마이그레이션(Commerce 개발자 MCP)

[!DNL Adobe Commerce on Cloud] 또는 온-프레미스 사용자 지정에서는 응용 프로그램 내에서 실행되는 모듈, 플러그인 및 이벤트 관찰자 등 처리 중인 PHP를 사용할 수 있습니다. [!DNL Adobe Commerce as a Cloud Service]은(는) 버전이 없는 SaaS 플랫폼이며 해당 모델은 더 이상 적용되지 않습니다. 사용자 지정은 이벤트 및 API를 통해 Commerce과 통합되는 처리 중단된 [!DNL Adobe Developer App Builder] 응용 프로그램으로 실행됩니다. 이 아키텍처에 대한 스토어의 사용자 지정 현대화는 일반적으로 [!DNL Adobe Commerce as a Cloud Service] 마이그레이션에서 가장 중요한 엔지니어링 작업입니다.

### 코드 마이그레이션 개요

마이그레이션 평가부터 시작하여 Commerce 개발자 MCP는 기존 PHP 사용자 지정을 [!DNL App Builder] 응용 프로그램으로 현대화하기 위한 대화형 IDE 환경을 제공합니다. 또한 EDS(Edge Delivery Services)의 상점 재구축을 지원합니다. Commerce 개발자 MCP는 마이그레이션 평가 도구 결과를 직접 소비함으로써 수동 해석을 줄이고, 추적 가능성을 유지하며, 프로세스 전반에 걸쳐 일관성을 보장하여 승인된 마이그레이션 로드맵에 맞게 구현을 유지합니다.

마이그레이션이 주요 사용 사례이지만 Commerce 개발자 MCP는 [!DNL Adobe Commerce]을(를) 위한 포괄적인 AI 개발 에이전트로 설계되었습니다. MCP는 현대화, 새로운 개발, 운영 워크플로 및 [!DNL Adobe Commerce as a Cloud Service]에 대한 모든 업데이트를 지원합니다. 이러한 수준의 유연성을 통해 팀은 마이그레이션 후 한참 후에도 Commerce 애플리케이션을 계속 구축하고 확장할 수 있습니다.

### Commerce 개발자 MCP

Commerce 개발자 MCP는 [마이그레이션 평가](#migration-assessment-tool)의 결과를 사용하여, 확인된 사용자 지정 항목을 반복적인 개발 워크플로를 통해 [!DNL App Builder] 응용 프로그램으로 변환합니다. 이러한 도구를 사용하여 개발할 때는 다음 지침을 고려하십시오.

- **블루프린트로 시작** - Commerce 개발자 MCP는 식별된 사용자 지정, 권장 사항 및 마이그레이션 우선 순위를 구현 계획의 기반으로 사용하여 마이그레이션 평가를 사용합니다.

- **각 사용자 지정 계획** - 모든 사용자 지정에 대해 Commerce 개발자 MCP는 권장 [!DNL Adobe Commerce as a Cloud Service] 아키텍처, 필수 통합 패턴 및 프로세스 외부 응용 프로그램으로 전환하는 데 필요한 재설계를 설명하는 사양을 개발합니다.

- **공동 빌드** - 처음 코드를 생성하는 대신 Commerce 개발자 MCP는 구현을 계획하고, 아키텍처에 대해 논의하고, 코드를 생성 및 개선하고, 권장 패턴을 확인하고, 배포 지침을 제공하여 개발 수명 주기 전반에 걸쳐 사용자를 지원합니다. 개발자는 자연어를 통해 생성된 구현을 반복적으로 세분화하여 현대화 노력 전반에 걸쳐 프로젝트 세부 사항을 공동으로 발전시킬 수 있습니다.

  - 생성된 구현은 엔지니어링 팀에서 완전히 다시 보고, 테스트 및 확장 가능한 상태를 유지하면서 게재를 가속화하도록 설계되었습니다.

- **통합 및 배포** - Commerce 개발자 MCP는 적절한 통합 패턴을 통해 Commerce에 응용 프로그램을 연결하고, 배포 워크플로를 지원하고, 배포 전 권장 아키텍처 패턴에 대해 구현을 확인하여 일관성을 향상시키고 중복되는 노력을 줄입니다.

  - Commerce 개발자 MCP에는 개발 워크플로에서 직접 도메인 지식, 구현 패턴, 아키텍처 지침, 상황별 제품 전문 지식 및 검증된 코딩 사례를 제공하는 [!DNL Adobe Commerce App Builder] MCP가 포함되어 있습니다. 따라서 개발자가 Commerce 개발자 MCP를 직접 사용하거나 Claude, Cursor 또는 Copilot과 같은 다른 에이전트와 함께 작업하는 경우에도 MCP 권장 사항이 Adobe의 모범 사례와 일치하도록 합니다.

### Storefront 현대화

프론트엔드에서 Commerce 개발자 MCP는 Edge Delivery Services(EDS) 보일러플레이트, 드롭인 구성 요소 및 EDS 블록을 사용하여 Commerce용 EDS의 [storefrontns](https://experienceleague.adobe.com/developer/commerce/storefront/)을(를) 현대화합니다.

Commerce Developer MCP는 Commerce 보일러플레이트를 기반으로 기존 상점 프로젝트를 로드합니다. 다음과 같은 방법으로 상점을 현대화합니다.

- 응답형 EDS 블록 생성
- Commerce 인식 페이지 데이터(홈, PLP, PDP, 장바구니, 체크아웃, 계정) 생성
- 드롭인 구성 요소 작성 및 확장
- 디자인을 EDS 구현으로 번역
- 레거시 모놀리식 상점 전면을 컴포저블 EDS 블록 아키텍처로 변환

MCP는 또한 다음을 지원합니다.

- 구성 요소 현대화
- 재사용 가능한 블록 구성
- 경험 최적화
- 최신 Edge Delivery Services 모범 사례와 연계

### 개발자 MCP 값

처리 중인 PHP 사용자 지정에서 구성 가능한 [!DNL App Builder] 응용 프로그램으로 이동하면 중요한 아키텍처 전환이 나타납니다. Commerce 개발자 MCP는 [!DNL Adobe Commerce]개의 지식, [!DNL App Builder]개의 구현 패턴 및 제품 모범 사례를 개발 워크플로에 직접 포함시켜 해당 간격을 좁힙니다.

이 컨텍스트를 포함하면 게재 속도와 엔지니어링 품질 모두에서 일관성이 향상됩니다. 팀은 일관된 아키텍처 지침을 따르는 구현을 생성하면서 애플리케이션을 보다 빠르게 현대화할 수 있습니다.

Commerce 개발자 MCP는 권장 구현 패턴을 포함함으로써 개인의 전문성에 대한 의존도를 줄이고 조직이 프로젝트 전반에서 현대화 노력을 일관되게 확장할 수 있도록 지원합니다.

마이그레이션 프로세스는 기존 구현을 개선할 수 있는 기회이기도 합니다. Teams는 기존 맞춤화를 단순화하고, 오래된 기능을 폐기하고, SaaS 기능을 채택하고, 과거의 기술적 부담을 떠넘기는 대신 애플리케이션 아키텍처를 현대화할 수 있습니다.

Commerce 개발자 MCP는 마이그레이션 평가를 직접 소비하므로 모든 현대화 작업은 원래 평가로 추적성을 다시 유지하여 구현이 승인된 마이그레이션 로드맵과 일치하도록 합니다.

또한 Commerce 개발자 MCP는 비즈니스 요구 사항이 변경될 때 독립적으로 발전할 수 있는 모듈식 [!DNL App Builder] 응용 프로그램을 장려하여 구성 가능한 응용 프로그램 디자인을 촉진합니다.

### 개발자 MCP 범위

백엔드에서 Commerce 개발자 MCP는 PHP 모듈, 플러그인 및 이벤트 관찰자를 [!DNL App Builder] 응용 프로그램으로 변환하여 사용자 정의 및 통합 계층을 현대화하고 통합 패턴을 만들어 Adobe Commerce과 연결합니다. 또한 체크아웃, 결제 및 관리 UI에 대한 개발을 가속화합니다.

프론트엔드에서 Commerce 개발자 MCP [Edge Delivery Services의 Commerce 상점 ](#storefront-modernization)을(를) 현대화합니다.

MCP는 데이터 마이그레이션을 처리하지 않습니다. 비즈니스 데이터는 [Commerce 데이터 마이그레이션 서비스](#data-migration-commerce-data-migration-service)를 통해 마이그레이션됩니다. MCP는 비즈니스 논리 또는 사용자 지정 테이블에 응용 프로그램 현대화가 필요할 때 필요한 [!DNL App Builder] 응용 프로그램을 지원합니다.

### 다음 단계

마이그레이션 평가 도구 로드맵이 마이그레이션 범위 및 우선 순위를 정하면 코드 및 상점 현대화 작업이 시작됩니다.

MCP 설치 및 사용 방법에 대한 자세한 내용은 [Commerce 개발자 MCP](https://developer.adobe.com/commerce/extensibility/developer-agent/) 설명서를 참조하십시오.

## 데이터 마이그레이션(Commerce 데이터 마이그레이션 서비스)

[!DNL Adobe Commerce as a Cloud Service]&#x200B;(으)로 마이그레이션하려면 카탈로그, 주문, 고객 및 구성을 포함한 수년간의 데이터를 마이그레이션해야 할 수 있습니다.

Commerce 데이터 마이그레이션 서비스는 수동 마이그레이션을 반복 가능한 단일 자동화된 프로세스로 대체합니다. 복잡한 데이터베이스 마이그레이션을 보다 예측 가능하고 효율적으로 수행할 수 있습니다.

### Commerce 데이터 마이그레이션 서비스

마이그레이션은 Docker 명령줄 도구(`./bin/console migration`)를 통해 실행되는 안내식 워크플로우를 사용합니다. 시스템 통합자 또는 연산자는 소스 저장소에 대해 이 워크플로를 실행합니다.

핵심 데이터 마이그레이션은 자동화되지만 대부분의 마이그레이션은 비표준 스키마, 확장, Edge Case를 포함합니다. 따라서 모든 마이그레이션은 소스 스토어의 [평가](#migration-assessment-tool)에서 시작됩니다. 자격 증명 및 연결의 유효성을 검사하고, 마이그레이션을 등록하고, 확인 기준선을 설정한 후 데이터 마이그레이션을 진행할 수 있습니다.

마이그레이션 서비스 도구는 다음과 같은 데이터 관리 단계를 수행합니다.

1. **추출 및 변환** — 원본에서 모든 관련 데이터를 동시에 추출하고 [!DNL Adobe Commerce as a Cloud Service]에 대해 모양을 변경합니다. 호환되지 않는 데이터는 필터링되고 사용자 지정 특성 및 기타 구조가 다시 매핑됩니다.
1. **로드** — 추출한 데이터를 Commerce 데이터 마이그레이션 서비스로 전송합니다. 서비스가 데이터를 [!DNL Adobe Commerce as a Cloud Service]에 로드한 다음 색인을 다시 빌드하고 카탈로그를 수집합니다.
1. **확인** — 데이터베이스 수준에서 원본 데이터와 대상 데이터를 비교합니다. 그런 다음 서비스는 상점 GraphQL 및 관리자 REST API를 통해 라이브 레코드 샘플을 확인하여 데이터를 확인합니다.
1. **보고서** - 모든 단계의 결과를 최종 마이그레이션 보고서로 통합합니다.

이러한 데이터 이동 단계는 유지 관리 기간이 필요하지만 준비 단계 동안 스토어는 작동 상태를 유지하므로 가동 중지 시간을 최소화합니다.

### 마이그레이션 서비스 가치

Commerce 데이터 마이그레이션 서비스는 증거를 사용하여 데이터 무결성을 유지합니다. 모든 마이그레이션은 소스 데이터와 타겟 데이터를 비교하고 API를 통해 라이브 레코드 샘플을 확인하여 확인됩니다. 사용자 지정 특성과 같이 [!DNL Adobe Commerce as a Cloud Service]에 완전히 매핑되지 않은 데이터는 추출 중에 자동으로 필터링되고 다시 매핑됩니다.

마이그레이션 서비스는 엔터프라이즈 규모의 데이터베이스를 위해 설계되었습니다. 데이터 마이그레이션은 비동기적으로 분할되고 처리되므로 대규모 카탈로그와 광범위한 주문 내역을 안정적으로 마이그레이션할 수 있습니다. 파이프라인이 확장되면 여러 마이그레이션이 동시에 실행될 수 있습니다. 마이그레이션이 중단되면 마지막으로 완료된 단계에서 다시 시작되고 중단된 작업이 자동으로 검색되어 다시 시도됩니다.

다운타임은 다음과 같은 방식으로 최소화됩니다.

- 대부분의 작업은 매장이 살아있는 상태에서 이뤄지는데, 이는 최종 컷오버만 유지보수 기간이 필요하다는 의미다.
- 데이터 마이그레이션은 고효율의 직접 SQL 읽기 및 쓰기를 사용하며 마이그레이션할 필요가 없는 테이블 및 레코드를 건너뜁니다.

마이그레이션은 Adobe 인프라스트럭처를 통해 이동하는 운영 데이터를 포함하므로 전체 경로가 안전합니다.

- 대상에 도달하기 전에 맬웨어에 대한 모든 업로드가 검사됩니다.
- Intake 레이어는 파일 형식을 확인하고 안전하지 않은 데이터베이스 작업을 차단합니다
- 모든 요청은 Adobe IMS 및 게이트웨이 서명 확인을 사용하여 인증됩니다

Commerce Data Migration Service 는 전 세계 프로덕션에 있으며 이미 여러 엔터프라이즈 수준 마이그레이션을 제공하고 있습니다.

### 사용자 지정 및 타사 데이터

마이그레이션 서비스는 자사 핵심 상거래 데이터만 지원합니다. 마이그레이션 서비스는 사용자 지정 타사 엔티티를 처리하지 않습니다.

서드파티 데이터는 사례별로 마이그레이션할 수 있으므로 도커 추출 도구에 해당하는 맞춤화가 필요합니다. 사용자 지정 도구를 만든 후 소스에서 데이터를 추출하여 [!DNL App Builder] 또는 타사 데이터베이스에 쓸 수 있습니다.

각 확장에서는 데이터를 다르게 모델링하므로 소스 및 타겟 스토리지의 스키마와 위치를 결정한 후에만 타사 데이터에 대한 마이그레이션 경로를 디자인할 수 있습니다. 범위를 파악할 시간을 제공하기 위해 서드파티 데이터 마이그레이션을 조기에 식별해야 합니다.

### 다음 단계

마이그레이션할 준비가 되면 [데이터 마이그레이션 범위 설문 조사](../assets/data-migration-scoping-questionnaire.xlsx)를 완료하십시오. 원본 토폴로지, 엔터티 범위, 볼륨, 준수 제약 조건, 전환 역학 및 마이그레이션을 계획하는 데 필요한 [사용자 지정 테이블](#custom-and-third-party-data)이 필요합니다. 이 설문지를 작성하면 Adobe에서 환경을 평가하고 마이그레이션 기간을 계획할 수 있습니다.

워크플로우, 지원되는 데이터 및 확인에 대한 자세한 내용은 [대량 데이터 마이그레이션 도구 안내서](bulk-data/migration-tool.md) 설명서를 검토하십시오.

소스 환경을 준비하는 시스템 통합자는 표준 [Adobe Commerce Cloud CLI](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/dev-tools/cloud-cli/cloud-cli-overview) 및 IMS 자격 증명용 [Adobe Developer Console](https://developer.adobe.com)을 사용할 수도 있습니다.
