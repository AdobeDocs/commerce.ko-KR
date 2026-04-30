---
title: Adobe Commerce Optimizer 커넥터
description: Commerce 클라우드 또는 온프레미스 프로젝트에서 Adobe Commerce Optimizer으로 데이터를 연결하는 방법에 대해 알아봅니다
feature: Personalization, Integration, Configuration
badgePaas: label="PaaS만" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce 온 클라우드 프로젝트(Adobe 관리 PaaS 인프라) 및 온프레미스 프로젝트에만 적용됩니다."
source-git-commit: c9cce4766ef3f30390d50f53237328be1cfeefdf
workflow-type: tm+mt
source-wordcount: '1233'
ht-degree: 0%

---


# Adobe Commerce Optimizer 커넥터

Adobe Commerce Optimizer 커넥터는 Adobe Commerce(클라우드 또는 온프레미스)와 Adobe Commerce Optimizer 간의 기본 자사 통합입니다. Adobe Commerce 저장소의 카탈로그 및 가격 데이터를 Commerce Optimizer에 동기화하여 다음과 같은 작업을 수행할 수 있습니다.

- **AI 기반 제품 검색 및 권장 사항 강화**
- **고성능 헤드리스 상점** 실행(Edge Delivery에서 제공하는 Commerce 상점 포함)
- 한 곳에서 **이전 및 이후**&#x200B;개의 KPI와 데이터 동기화 상태 분석

Commerce은 제품, 가격 및 카탈로그 구조에 대한 기록 시스템으로 유지됩니다. Commerce Optimizer은 고객 경험 및 머천다이징 계층이 되어 연결된 모든 상점 또는 채널에 신속하고 적절한 결과를 제공합니다.

## 주요 이점 {#key-benefits}

| 이익 | 어떤 의미입니까? |
| --- | --- |
| **빌드할 사용자 지정 커넥터가 없습니다** | 맞춤형 피드 및 스크립트를 작성 및 유지 관리하는 대신 지원되는 자사 통합을 사용하십시오. |
| **Commerce Optimizer을 사용하여 더 빠른 가치 창출** | 기존 Adobe Commerce 배포 위에 AI 검색, 권장 사항 및 헤드리스 상점 전면을 켭니다. |
| **Commerce 범위와 일치함** | 웹 사이트, 스토어 보기 및 고객 그룹을 Commerce Optimizer 카탈로그 구문(카탈로그 소스 및 가격 장부)에 자동으로 매핑합니다. |
| **작동 가시성** | 전용 데이터 피드 동기화 상태 보기에서 피드 상태, 마지막 동기화 시간 및 SKU당 상태를 모니터링합니다. |
| **SaaS를 위한 향후 준비 경로** | PaaS에서 Adobe Commerce as a Cloud Service + Optimizer로 리플랫폼 없이 위험이 적은 현대화 경로를 제공합니다. |

## 커넥터 아키텍처 {#connector-architecture}

다음 다이어그램은 Adobe Commerce에서 Commerce Optimizer을 거쳐 상점 및 체크아웃 시스템에 이르기까지 커넥터에 대한 엔드 투 엔드 아키텍처를 보여 줍니다.

![Commerce Optimizer 커넥터 전체 아키텍처 다이어그램 Commerce](./assets/aco-connector-end2end-architecture.png){width="700" zoomable="yes"}

이 아키텍처에서는

- Adobe Commerce(온 클라우드 또는 온프레미스)는 기록 및 피드 제작자 시스템입니다
- 커넥터가 카탈로그, 가격 및 범주 피드를 내보냅니다.
- Commerce Optimizer은 피드 데이터를 카탈로그 소스, 가격 장부 및 카탈로그 보기로 수집하고 표준화합니다
- 상점(Edge Delivery 또는 사용자 정의 Headless 빌드의 Commerce 상점)은 검색 및 추천을 위해 Commerce Optimizer GraphQL API를 호출하고 장바구니 및 체크아웃 작업을 위해 Commerce 또는 다른 연결된 타사 플랫폼을 호출합니다

## Adobe Commerce에서 커넥터 작동 방식 {#how-it-works}

- Commerce Optimizer은 피드 데이터를 카탈로그 소스, 가격 장부 및 카탈로그 보기로 수집하고 표준화합니다.

- 상점(Edge Delivery 또는 사용자 정의 Headless 빌드의 Commerce 상점)은 검색 및 추천을 위해 Commerce Optimizer GraphQL API를 호출하고 장바구니 및 체크아웃 작업을 위해 Commerce 또는 다른 연결된 타사 플랫폼을 호출합니다.

## Adobe Commerce에서 커넥터 작동 방식

Adobe Commerce Optimizer 커넥터는 기존 Commerce 범위(웹 사이트 및 스토어 보기) 및 고객 세분화를 사용하여 Commerce Optimizer 카탈로그 모델을 채워서 작동합니다.

![Adobe Commerce Optimizer에 Commerce 데이터 매핑](/help/aco-connector/assets/storeview-to-catalogview-mapping.png){width="750" zoomable="yes"}

- **카탈로그 소스→ 저장소 보기** - 각 저장소 보기는 Commerce Optimizer에서 별도의 카탈로그 Source이 됩니다. 해당 소스에는 현지화된 제품 속성 및 스토어-뷰별 데이터가 포함됩니다
- **웹 사이트 → 가격 장부** — 각 Commerce 웹 사이트는 Commerce Optimizer에 있는 하나 이상의 가격 장부에 매핑됩니다. 가격 장부 및 가격 입력사항으로 웹 사이트 가격 책정 및 고객 그룹 가격 책정 내보내기
- **고객 그룹 → 가격 변동** - Commerce 고객 그룹 가격이 관련 가격 장부의 추가 항목으로 표시됩니다.

Commerce Optimizer이 데이터를 수집한 후 다음을 구성할 수 있습니다.

- Commerce Optimizer의 **카탈로그 보기 및 정책**(빌드 지역, 브랜드 또는 고객별 하위 집합용)
- **제품 검색**(검색, 패싯, 머천다이징 규칙)
- **제품 추천**

커넥터를 활성화하면 Adobe Commerce 인스턴스가 카탈로그 및 가격 데이터의 기록 시스템으로 유지됩니다. Commerce에서 데이터를 업데이트하면 커넥터가 해당 업데이트를 [!DNL Adobe Commerce Optimizer] 인스턴스와 동기화합니다.

>[!NOTE]
>
>Commerce Optimizer 구성에 대한 자세한 내용은 [[!DNL Adobe Commerce Optimizer] 머천다이징 도구](../optimizer/overview.md#quick-tour)를 참조하십시오.

## 일반 워크플로우 {#typical-workflows}

이러한 워크플로우는 팀이 Adobe Commerce Optimizer 커넥터를 설정하고 사용하는 방법을 설명합니다. 통합을 설정하고 이러한 워크플로를 활성화하는 방법에 대한 자세한 내용은 [시작하기](get-started.md)를 참조하십시오.

### 초기 설정 및 구성 {#initial-setup}

1. 작성기를 사용하여 **Adobe Commerce에 커넥터 패키지를 설치**:

   `composer require adobe-commerce/commerce-data-export-aco-adapter`

1. Commerce 관리자 또는 CLI를 통해 **인증 및 환경 세부 정보 구성**:

   ```terminal
   bin/magento aco:config:init \
     --org_id=<your-org> \
     --tenant_id=<your-tenant> \
     --client_id=<your-client-id> \
     --client_secret=<your-secret> \
     --region=na1 \
     --type=production
   ```

1. **Commerce 범위를 Commerce Optimizer에 매핑:**

   - 범위 내에 있어야 하는 웹 사이트 및 스토어 조회수 확인
   - 고객 그룹 및 가격 규칙이 예상대로 모델링되는지 확인합니다.

1. **연결 확인:**

   - 테스트 동기화를 실행하고 카탈로그 소스, 가격 장부 및 초기 제품이 Commerce Optimizer에 표시되는지 확인합니다.
   - 유효성 검사를 위해 Commerce의 데이터 피드 동기화 상태 페이지 및 Commerce Optimizer의 데이터 동기화 대시보드를 사용합니다

### 지속적인 데이터 동기화 {#ongoing-sync}

초기 구성 후 커넥터는 다음을 지원합니다.

- 초기 마이그레이션 또는 대규모 구조적 변경에 대한 **전체 카탈로그 동기화**
- 제품 또는 가격이 변경될 때 지속적인 업데이트에 대한 **델타 동기화**
- 타깃팅된 피드에 대한 **명령 재동기화**(v1.0.12 기준 범주 포함):

   - `bin/magento saas:resync --feed=products`
   - `bin/magento saas:resync --feed=prices`
   - `bin/magento saas:resync --feed=categories`

### 머천다이징 및 상점 전선 구성 {#merchandising-storefronts}

Commerce Optimizer에서 Commerce 데이터를 사용할 수 있게 되면 Commerce Optimizer Studio를 사용하여 머천다이징 및 상점 경험을 동기화된 카탈로그에 연결합니다.

**머천다이징 및 상점 전면을 구성하려면:**

1. Commerce Optimizer Studio에서 **카탈로그 보기 및 정책 만들기**:

   - 브랜드, 지역, 고객 세그먼트 또는 채널별로 카탈로그 필터링
   - 상점 또는 파트너별로 데이터 액세스 규칙 적용

1. Optimizer UI에서 **제품 검색 및 권장 사항 구성**:

   - 머천다이징 규칙, 패싯, 동의어 및 추천 단위 만들기
   - 커넥터는 모든 검색 및 권장 사항 구성을 Commerce Optimizer으로 오프로드합니다(Commerce 관리자의 라이브 검색 규칙 및 제품 권장 사항은 더 이상 이러한 흐름에 적용되지 않음)

1. Commerce Optimizer에 **상점 연결**:

   - Edge Delivery Services에서 제공하는 Commerce Storefront의 경우, 올바른 Optimizer 테넌트 및 카탈로그 보기를 사용하고 머천다이징 API를 통해 검색 및 추천 엔드포인트를 호출하도록 스토어를 구성하십시오
   - 서드파티 스토어프론트에서는 검색 및 추천 호출에 Optimizer 공개 API 또는 SDK를 사용하십시오

   >[!NOTE]
   >
   >타사 통합의 예를 보려면 [Commerce Optimizer용 Salesforce Commerce 커넥터](../optimizer/developer/salesforce-connector.md)를 참조하십시오.

1. 기존 플랫폼에서 **체크 아웃 유지**:

   - Adobe Commerce 또는 서드파티 플랫폼에서 장바구니, 체크아웃, 주문 관리 및 고객 계정을 유지합니다.
   - 외부 체크아웃 시스템과 통합할 때 App Builder 및 API Mesh를 사용하여 장바구니 전달

## 지원되는 시나리오 {#supported-scenarios}

이 커넥터는 Adobe Commerce on cloud 및 온프레미스 배포를 사용하는 B2C 판매자가 백엔드를 다시 빌드하지 않고 Commerce Optimizer을 채택하도록 설계되었습니다.

**일반적인 사용 사례:**

- **Storefront만 현대화**
기존 Commerce 백엔드를 유지하고 PLP/Search/PDP를 Commerce Optimizer에서 제공하는 Edge Delivery 상점 앞으로 이동합니다.

- **카탈로그 및 검색 성능 크기 조정**
Commerce에서 제품 및 가격 소유권을 유지하면서 Commerce Optimizer의 SaaS 서비스로 대량의 카탈로그 색인 지정 및 검색 작업 부담 감소

- **증분 SaaS 채택**
호환되는 Commerce 카탈로그와 함께 이 커넥터를 Adobe Commerce as a Cloud Service + Optimizer의 디딤돌로 사용하십시오

## 책임 및 구현 사전 요구 사항 {#responsibilities-prerequisites}

Commerce은 제품, 가격 및 고객 그룹에 대한 신뢰할 수 있는 소스입니다. Commerce에서 변경합니다. 커넥터가 이를 Commerce Optimizer에 동기화합니다.

**Commerce Optimizer은**&#x200B;의 담당자입니다.

- 카탈로그 모델링(카탈로그 소스, 가격 장부, 카탈로그 뷰, 정책)
- 제품 검색 및 권장 사항
- Storefront 지표, 데이터 동기화 대시보드 및 성공 지표 보고서

**커넥터가 없습니다.**

- Commerce 장바구니, 체크아웃 또는 주문 흐름 수정
- Storefront 프로젝트 자동 프로비저닝(Commerce Storefront/Edge Delivery 도구 핸들)

**시작하기 전:**

- Commerce이 최소 버전 및 서비스 커넥터 요구 사항을 충족하는지 확인합니다. 자세한 내용은 [시작하기](get-started.md#prerequisites)를 참조하십시오.
- IMS 조직 액세스 권한, [!DNL Adobe Commerce Optimizer] 인스턴스, 필요한 자격 증명과 지역 세부 정보가 있는지 확인하십시오.

## 관련 설명서 {#related-documentation}

- 통합을 설정하고 주요 워크플로를 사용하도록 설정합니다. [Adobe Commerce Optimizer 커넥터 시작](get-started.md)
- Commerce Optimizer 개념 및 아키텍처에 대해 알아봅니다. [Adobe Commerce Optimizer이란?](../optimizer/overview.md)
