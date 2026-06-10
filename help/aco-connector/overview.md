---
title: '[!DNL Adobe Commerce Optimizer Connector]'
description: 카탈로그 동기화, 검색 및 상점 게재를 위한  [!DNL Adobe Commerce] 과(와) [!DNL Adobe Commerce Optimizer]  간의  [!DNL Adobe Commerce Optimizer Connector] 통합에 대해 알아봅니다.
feature: Integration, Storefront, Configuration
badgePaas: label="PaaS만" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce 온 클라우드 프로젝트(Adobe 관리 PaaS 인프라) 및 온프레미스 프로젝트에만 적용됩니다."
autotag-review: '2026-06-09T19:00:00.000Z'
TQID: 'https://experienceleague.adobe.com/-C-XP5YYxwyGrkvVR6CDd-FpDybqnlaKMmFPKOKUbFA'
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75id: c32adafa-ed01-4b31-997e-2413013911b0id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
subfeature_v2: id: ae62cf09-5996-4921-bda8-fbe67b62e470id: f8ddfd3b-6194-46e8-a176-0e918039be56id: dad884f1-e840-49a1-970e-2f965bdbc410
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: eddd9b14-83bd-4ff4-9072-54a4a484abb7id: e0eb8757-182f-49f3-94a4-1587d16f5094id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: 6d4493db5e0714577a8800007cc6d2c552578fa4
workflow-type: tm+mt
source-wordcount: 1037
ht-degree: 0%

---

# Adobe Commerce Optimizer 커넥터

[!DNL Adobe Commerce Optimizer Connector]은(는) [!DNL Adobe Commerce]&#x200B;(클라우드 또는 온-프레미스)와 [!DNL Adobe Commerce Optimizer] 간의 기본 자사 통합입니다. [!DNL Adobe Commerce] 저장소의 카탈로그 및 가격 책정 데이터를 [!DNL Adobe Commerce Optimizer]&#x200B;(으)로 동기화하여 다음과 같은 작업을 수행할 수 있습니다.

- **AI 기반 제품 검색 및 권장 사항 강화**
- **고성능 헤드리스 상점** 실행([!DNL Edge Delivery Services]에서 제공하는 Commerce 상점 포함)
- 한 곳에서 **이전 및 이후**&#x200B;개의 KPI와 데이터 동기화 상태 분석

[!DNL Adobe Commerce]은(는) 제품, 가격 및 카탈로그 구조에 대한 기록 시스템으로 남아 있습니다. [!DNL Adobe Commerce Optimizer]은(는) 귀하의 경험 및 머천다이징 계층이 되어 연결된 모든 상점 또는 채널에 신속하고 적절한 결과를 제공합니다.

## 주요 이점 {#key-benefits}

| 이익 | 어떤 의미입니까? |
| --- | --- |
| **빌드할 사용자 지정 커넥터가 없습니다** | 맞춤형 피드 및 스크립트를 작성 및 유지 관리하는 대신 지원되는 자사 통합을 사용하십시오. |
| [!DNL Adobe Commerce Optimizer]**을(를) 사용하여 값을 계산하는 데 걸리는 시간** | 기존 [!DNL Adobe Commerce] 배포 위에 AI 검색, 권장 사항 및 Headless 상점 전면을 켭니다. |
| **Commerce 범위와 일치함** | 웹 사이트, 스토어 보기 및 고객 그룹을 [!DNL Adobe Commerce Optimizer]개의 카탈로그 구문(카탈로그 원본 및 가격 책)에 자동으로 매핑합니다. |
| **작동 가시성** | 전용 [!UICONTROL Data Feed Sync Status] 보기에서 피드 상태, 마지막 동기화 시간 및 SKU당 상태를 모니터링합니다. |
| **SaaS를 위한 향후 준비 경로** | PaaS에서 [!DNL Adobe Commerce as a Cloud Service] + [!DNL Adobe Commerce Optimizer]&#x200B;(으)로 리플랫폼 없이 위험이 낮은 현대화 경로를 제공합니다. |

## 커넥터 아키텍처 {#connector-architecture}

다음 다이어그램은 [!DNL Adobe Commerce]부터 [!DNL Adobe Commerce Optimizer]까지 그리고 상점 및 체크아웃 시스템까지 커넥터에 대한 엔드 투 엔드 아키텍처를 보여 줍니다.

![Adobe Commerce Optimizer 커넥터 전체 아키텍처 다이어그램](./assets/aco-connector-end2end-architecture.png){width="700" zoomable="yes"}

이 아키텍처에서는

- [!DNL Adobe Commerce]&#x200B;(클라우드 또는 온프레미스)은 레코드 및 피드 제작자 시스템입니다.
- 커넥터가 카탈로그, 가격 및 범주 피드를 내보냅니다.
- [!DNL Adobe Commerce Optimizer]에서 피드 데이터를 수집하여 카탈로그 원본, 가격 장부 및 카탈로그 보기로 정규화합니다.
- 상점([!DNL Edge Delivery Services]의 Commerce 상점 또는 사용자 지정 Headless 빌드)에서 검색 및 권장 사항을 위해 [!DNL Commerce Optimizer] GraphQL API를 호출하고 장바구니 및 체크아웃 작업을 위해 [!DNL Adobe Commerce] 또는 연결된 다른 타사 플랫폼을 호출합니다.

## 커넥터가 [!DNL Adobe Commerce]에서 작동하는 방식

[!DNL Adobe Commerce Optimizer Connector]은(는) 기존 Commerce 범위(웹 사이트 및 스토어 보기) 및 고객 세분화를 사용하여 [!DNL Adobe Commerce Optimizer] 카탈로그 모델을 채우는 방식으로 작동합니다.

![Adobe Commerce Optimizer에 Commerce 데이터 매핑](./assets/storeview-to-catalogview-mapping.png){width="750" zoomable="yes"}

- **카탈로그 원본→ 저장소 보기** — 각 저장소 보기는 [!DNL Adobe Commerce Optimizer]에서 별도의 카탈로그 Source이 됩니다. 해당 소스에는 현지화된 제품 속성 및 스토어-뷰별 데이터가 포함됩니다
- **웹 사이트→ 요금제 정보** — 각 [!DNL Adobe Commerce] 웹 사이트가 [!DNL Commerce Optimizer]에 있는 하나 이상의 요금제에 매핑됩니다. 가격 장부 및 가격 입력사항으로 웹 사이트 가격 책정 및 고객 그룹 가격 책정 내보내기
- **고객 그룹 → 가격 변동** — [!DNL Adobe Commerce] 고객 그룹 가격이 관련 가격 장부에 추가 항목으로 나타납니다.

[!DNL Commerce Optimizer]에서 데이터를 수집한 후 다음을 구성할 수 있습니다.

- [!DNL Adobe Commerce Optimizer] Studio의 **카탈로그 보기 및 정책**(지역별, 브랜드 또는 고객별 하위 집합 작성)
- **제품 검색**(검색, 패싯, 머천다이징 규칙)
- **[!DNL Product Recommendations]**

커넥터를 사용하면 [!DNL Adobe Commerce] 인스턴스는 카탈로그 및 가격 데이터의 기록 시스템으로 유지됩니다. [!DNL Adobe Commerce]에서 데이터를 업데이트하면 커넥터가 해당 업데이트를 [!DNL Adobe Commerce Optimizer] 인스턴스와 동기화합니다.

>[!NOTE]
>
>[!DNL Adobe Commerce Optimizer] 구성에 대한 자세한 내용은 [[!DNL Adobe Commerce Optimizer] 머천다이징 도구](../optimizer/overview.md#quick-tour)를 참조하십시오.

## 일반 워크플로우 {#typical-workflows}

이 워크플로에서는 팀이 [!DNL Adobe Commerce Optimizer Connector]을(를) 설정하고 사용하는 방법을 설명합니다. 통합을 설정하고 이러한 워크플로를 활성화하는 방법에 대한 자세한 내용은 [시작하기](get-started.md)를 참조하십시오.

### 초기 설정 및 구성 {#initial-setup}

_시작_ 안내서에서 [구성 단계](./get-started.md#configuration-steps)를 참조하십시오.

### 지속적인 데이터 동기화 {#ongoing-sync}

초기 구성 후 커넥터는 다음을 지원합니다.

- 초기 마이그레이션 또는 대규모 구조적 변경에 대한 **전체 카탈로그 동기화**
- 제품 또는 가격이 변경될 때 지속적인 업데이트에 대한 **델타 동기화**
- 타깃팅된 피드에 대해 **명령 재동기화**

[!DNL Adobe Commerce Optimizer Connector]에 다음 피드를 사용할 수 있습니다.

- `products` - 제품 데이터
- `productAttributes` - 제품 특성에 대한 메타데이터
- `priceBooks` - 가격 장부
- `prices` - 제품 가격
- `categories` - 범주 데이터

자세한 내용은 다음 주제를 참조하십시오.

- [!DNL Adobe Commerce] CLI 재동기화 작업의 경우 [CLI 재동기화 명령](../data-export/data-export-cli-commands.md#sync-using-cli-commands){target="_blank"}을 참조하십시오.
- [[!DNL Commerce Optimizer Connector]개의 모듈 및 피드 끝점](reference/connector-reference.md)
- [커넥터 피드에 대한 필드 매핑](reference/field-mapping.md)

### 머천다이징 및 상점 전선 구성 {#merchandising-storefronts}

[!DNL Adobe Commerce Optimizer]에서 [!DNL Adobe Commerce]개의 데이터를 사용할 수 있게 되면 [[!DNL Commerce Optimizer] Studio](https://experienceleague.adobe.com/en/docs/commerce/optimizer/overview#quick-tour)을(를) 사용하여 머천다이징 및 상점 경험을 동기화된 카탈로그에 연결합니다.

**[!DNL Commerce Optimizer] Studio에서 머천다이징 및 상점 전면을 구성하려면:**

1. [!UICONTROL Store setup] 메뉴에서 **카탈로그 보기 및 정책 만들기**.

   - 브랜드, 지역, 고객 세그먼트 또는 채널별로 카탈로그 필터링
   - 상점 또는 파트너별로 데이터 액세스 규칙 적용

1. [!UICONTROL Merchandising] 메뉴에서 **제품 검색 및 권장 사항을 구성**&#x200B;합니다.

   - 머천다이징 규칙, 패싯, 동의어 및 추천 단위 만들기
   - 커넥터가 모든 검색 및 권장 사항 구성을 [!DNL Commerce Optimizer]에 오프로드합니다(Commerce 관리자의 [!DNL Live Search] 규칙 및 [!DNL Product Recommendations]은(는) 이러한 흐름에 더 이상 적용되지 않음).

1. [!DNL Commerce Optimizer]에 **상점 연결**:

   - [!DNL Edge Delivery Services]에서 제공하는 Commerce Storefront의 경우, 올바른 Optimizer 테넌트 및 카탈로그 보기를 사용하고 머천다이징 API를 통해 검색 및 추천 끝점을 호출하도록 Storefront를 구성하십시오
   - 서드파티 스토어프론트에서는 검색 및 추천 호출에 Optimizer 공개 API 또는 SDK를 사용하십시오

   >[!NOTE]
   >
   >타사 통합의 예를 보려면 [Salesforce Commerce Connector for [!DNL Adobe Commerce Optimizer]](../optimizer/developer/salesforce-connector.md)를 참조하십시오.

1. 기존 플랫폼에서 **체크 아웃 유지**:

   - 장바구니, 체크아웃, 주문 관리 및 고객 계정을 [!DNL Adobe Commerce] 또는 타사 플랫폼에 보관
   - 외부 체크아웃 시스템과 통합할 때 장바구니 핸드오프에 [!DNL App Builder] 및 [!DNL API Mesh] 사용

## 지원되는 시나리오 {#supported-scenarios}

이 커넥터는 [!DNL Adobe Commerce]이(가) 클라우드 및 온-프레미스 배포에 있고 백엔드를 다시 빌드하지 않고 [!DNL Adobe Commerce Optimizer]을(를) 채택하려는 B2C 가맹점을 위해 설계되었습니다.

**일반적인 사용 사례:**

- **Storefront만 현대화**
기존 [!DNL Adobe Commerce] 백엔드를 유지하고 PLP/Search/PDP를 [!DNL Adobe Commerce Optimizer]에서 제공하는 [!DNL Edge Delivery Services] 상점으로 이동합니다.

- **카탈로그 및 검색 성능 크기 조정**
[!DNL Adobe Commerce]에서 제품 및 가격 소유권을 유지하면서 대량 카탈로그 색인 지정 및 검색을 [!DNL Adobe Commerce Optimizer]의 SaaS 서비스로 오프로드합니다.

- **증분 SaaS 채택**
호환 가능한 [!DNL Adobe Commerce] 카탈로그와 함께 커넥터를 [!DNL Adobe Commerce as a Cloud Service] + [!DNL Adobe Commerce Optimizer]을(를) 위한 디딤돌로 사용하십시오.

## 책임 및 구현 사전 요구 사항 {#responsibilities-prerequisites}

[!DNL Adobe Commerce]은(는) 제품, 가격 및 고객 그룹에 대한 신뢰할 수 있는 소스입니다. [!DNL Adobe Commerce]에서 변경합니다. 커넥터가 [!DNL Adobe Commerce Optimizer]에 동기화합니다.

**[!DNL Adobe Commerce Optimizer]은(는)**&#x200B;에 대한 책임이 있습니다.

- 카탈로그 모델링(카탈로그 소스, 가격 장부, 카탈로그 뷰, 정책)
- 제품 검색 및 권장 사항
- Storefront 지표, 데이터 동기화 대시보드 및 성공 지표 보고서

**커넥터가 없습니다.**

- [!DNL Adobe Commerce] 장바구니, 체크아웃 또는 주문 흐름 수정
- Storefront 프로젝트 자동 프로비저닝(Commerce Storefront / [!DNL Edge Delivery Services]개 도구 핸들)

**시작하기 전:**

- [!DNL Adobe Commerce]이(가) 최소 버전 및 [!DNL Commerce Optimizer Connector] 요구 사항을 충족하는지 확인하십시오. 자세한 내용은 [시작하기](get-started.md#requirements-to-use-the-integration)를 참조하십시오.
- IMS 조직 액세스 권한, [!DNL Adobe Commerce Optimizer] 인스턴스, 필요한 자격 증명과 지역 세부 정보가 있는지 확인하십시오.

## 관련 설명서 {#related-documentation}

- 통합을 설정하고 주요 워크플로를 사용하도록 설정합니다. [시작하기 [!DNL Commerce Optimizer Connector]](get-started.md)
- [!DNL Adobe Commerce Optimizer] 개념 및 아키텍처에 대해 알아봅니다. [정의 [!DNL Adobe Commerce Optimizer]?](../optimizer/overview.md)
- 동기화 메커니즘, 초기화 및 오류 처리를 이해합니다. [커넥터 동기화 파이프라인](connector-sync-pipeline.md)
- 모든 피드에 대한 필드 수준 데이터 매핑: [커넥터 피드에 대한 필드 매핑](reference/field-mapping.md)
- GraphQL 및 번들 인코딩을 사용하여 헤드리스 상점 통합: [헤드리스 상점 통합](headless-storefront.md)
- 동기화 및 구성 문제 진단: [문제 해결](troubleshooting.md)
