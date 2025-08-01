---
title: 시작하기
description: ' [!DNL Adobe Commerce Optimizer]을(를) 시작하는 방법에 대해 알아봅니다.'
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="SaaS만" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."
exl-id: de57d93d-e156-45c1-86aa-de29a8c34bd2
source-git-commit: f920cfe7cd433e85f343fefe1062a1972e5e5e5f
workflow-type: tm+mt
source-wordcount: '852'
ht-degree: 0%

---

# 시작

이 안내서에서는 처음부터 끝까지 [!DNL Adobe Commerce Optimizer]을(를) 설정하는 과정을 안내합니다. 이 안내서에서는 모든 역할을 다루지만, 자세한 개발자 관련 내용은 [개발자 설명서](https://developer.adobe.com/commerce/services/optimizer/)를 참조하십시오.

## 사전 요구 사항

시작하기 전에 다음을 확인하십시오.

- **개의 권한을 가진** Adobe Experience Cloud 계정[!DNL Adobe Commerce Optimizer]
- 인스턴스를 만들고 사용자를 관리하기 위한 **조직 관리자 액세스**
- **GitHub 계정**(샘플 데이터 및 상점 개발용)
- 전자 상거래 개념의 **기본 이해**

## 빠른 시작 안내서

[!DNL Adobe Commerce Optimizer] 환경을 실행하려면 다음 필수 단계를 따르십시오.

### 1단계. 인스턴스 만들기

1. [Adobe Experience Cloud](https://experience.adobe.com/)에 로그인합니다.
1. **Commerce** > **Commerce Cloud 관리자**(으)로 이동합니다.
1. **인스턴스 추가** > **Commerce Optimizer**&#x200B;을 클릭합니다.

   ![인스턴스 만들기](./assets/create-aco-instance.png){width="60%" zoomable="yes"}

1. 인스턴스 설정 구성:
   - **이름**: 설명하는 이름(예: &quot;내 회사 샌드박스&quot;)
   - **설명**: 목적에 대한 간략한 설명
   - **지역**: 선호하는 지역을 선택하세요.
   - **환경 유형**: 테스트를 위해 **샌드박스** 환경으로 시작

1. **인스턴스 추가**&#x200B;를 클릭합니다.

   Cloud Manager이 업데이트되어 새 인스턴스가 포함됩니다. 액세스 및 관리에 대한 자세한 내용은 [인스턴스 관리](#manage-an-instance)를 참조하십시오.

>[!NOTE]
>
>샌드박스 인스턴스는 북미 지역으로 제한됩니다. 생성 후에는 영역을 변경할 수 없습니다.

### 2단계. 환경 설정

인스턴스를 만든 후:

1. Commerce Cloud 관리자에서 [인스턴스 관리](#manage-an-instance).
1. [사용자 관리 가이드](./user-management.md)를 사용하여 사용자 액세스를 구성하십시오.

### 3단계. 샘플 데이터 추가(선택 사항)

테스트 및 학습을 위해 [샘플 데이터 로드](#add-sample-data) 지침을 따르십시오.

## 역할 기반 워크플로

[!DNL Adobe Commerce Optimizer] 설정 및 관리는 세 가지 주요 역할에 의존합니다. 각 역할에는 다음과 같은 특정 작업과 책임이 있습니다.

![높은 수준의 워크플로](./assets/high-level-workflow.png){zoomable="yes"}

### 관리자 작업

관리자는 인스턴스, 사용자 및 조직 설정을 관리합니다.

| 작업 | 설명 | 링크 |
|---|---|---|
| **사용자 관리** | 사용자, 개발자 및 관리자 추가 | [사용자 관리](./user-management.md) |
| **인스턴스 만들기** | 샌드박스 및 프로덕션 환경 설정 | [인스턴스 만들기](#create-an-instance) |
| **액세스 구성** | 카탈로그 보기 및 정책 설정 | [카탈로그 보기](./setup/catalog-view.md) |

### 개발자 작업

개발자는 플랫폼 아키텍처 작업을 포함하여 기술 구현 및 데이터 통합을 처리합니다.

| 작업 | 설명 | 링크 |
|---|---|---|
| **Developer Console 액세스** | 프로젝트 만들기 및 자격 증명 생성 | [Developer Console](https://developer.adobe.com/developer-console/docs/guides/getting-started) |
| **카탈로그 데이터 수집** | 기존 시스템에서 제품 데이터 가져오기 | [데이터 수집 API](https://developer-stage.adobe.com/commerce/services/composable-catalog/data-ingestion/using-the-api/) |
| **Storefront 설정** | Edge Delivery Services 상점 구성 | [Storefront 설치](./storefront.md) |

### 머천다이저 작업

머천다이저는 제품 검색 및 추천을 통해 쇼핑 경험을 최적화하고 개인화합니다. 또한 쇼핑객 데이터와 분석을 사용하여 상점 내 제품 배치, 가격 책정 및 프로모션에 대한 전략적 결정을 내립니다.

| 작업 | 설명 | 링크 |
|---|---|---|
| **제품 검색** | 검색 및 필터링 구성 | [머천다이징 개요](./merchandising/overview.md) |
| **권장 사항** | AI 기반 제품 추천 설정 | [제품 추천](./merchandising/recommendations/overview.md) |
| **성능 추적** | 성공 지표 모니터링 | [성공 지표](./manage-results/success-metrics.md) |

## 인스턴스 관리

1. [Adobe Experience Cloud](https://experience.adobe.com/)에 로그인합니다.

1. Commerce Cloud Manager 열기:
   - **빠른 액세스**&#x200B;에서 **Commerce**&#x200B;을(를) 클릭합니다.
   - 사용 가능한 인스턴스를 봅니다.

1. 인스턴스에 액세스:

   인스턴스 이름을 클릭하여 [!DNL Adobe Commerce Optimizer] 응용 프로그램을 엽니다. 응용 프로그램 내에서 페이지 상단의 드롭다운을 사용하여 다른 [!DNL Adobe Commerce Optimizer] 인스턴스 간에 전환할 수 있습니다.

   ![인스턴스 전환기](./assets/context-switcher.png){zoomable="yes"}

   표시된 모든 인스턴스가 동일한 조직에 속합니다. 인스턴스 간에 전환하여 각 인스턴스에 대한 데이터 및 설정(예: 샌드박스와 프로덕션 환경 간)을 볼 수 있습니다.

1. 인스턴스 세부 사항 가져오기:
   - 인스턴스 이름 옆에 있는 정보 아이콘을 클릭합니다.
   - GraphQL 끝점, 데이터 수집을 위한 Catalog Service 끝점 및 인스턴스 ID(`tenant ID`)를 참고하십시오.

   ![인스턴스 세부 정보](./assets/aco-instance-details.png){width="60%" zoomable="yes"}

   프론트엔드 애플리케이션 및 백엔드 시스템과 통합하려면 엔드포인트 및 인스턴스 ID(테넌트 ID) 세부 정보가 필요합니다. [!DNL Adobe Commerce Optimizer] 응용 프로그램에 액세스하기 위한 URL도 여기에 제공됩니다.

   모든 Adobe Commerce Optimizer 사용자가 Cloud Manager 및 인스턴스 세부 사항에 액세스할 수 있는 것은 아닙니다. 액세스는 사용자 계정에 할당된 역할 및 권한에 따라 다릅니다. 액세스 권한이 없는 경우 조직 관리자에게 문의하여 인스턴스 세부 정보를 얻으십시오.

1. 인스턴스 이름 및 설명 편집:
   - 인스턴스 이름 옆에 있는 **편집** 아이콘을 클릭합니다.
   - 필요에 따라 이름과 설명을 업데이트합니다.
   - **저장**&#x200B;을 클릭합니다.

   검색 및 필터 옵션을 사용하여 특정 인스턴스를 빠르게 찾을 수도 있습니다.

## 샘플 데이터 추가

Adobe은 [!DNL Adobe Commerce Optimizer] 기능을 학습하고 테스트하는 데 도움이 되는 샘플 데이터 및 도구를 갖춘 GitHub 리포지토리를 제공합니다.
샘플 데이터는 [Carvelo 비즈니스 시나리오](./use-case/admin-use-case.md)를 기반으로 하며 다음을 포함합니다.

- 자동차 부품을 포함한 제품 카탈로그
- 복수 가격 장부 및 가격 시나리오
- 다양한 딜러를 위한 카탈로그 보기 및 정책
- 전체 워크플로 예

**샘플 데이터 로드:**

1. GitHub 저장소에 액세스:
   - [샘플 카탈로그 데이터 수집 리포지토리](https://github.com/adobe-commerce/aco-sample-catalog-data-ingestion)를 방문하십시오.

1. 저장소의 README 파일에 있는 설치 지침을 따릅니다.

   - 데이터 수집 구성 및 실행
   - 샘플 데이터를 사용하여 카탈로그 정책 및 보기 구성
   - 샘플 데이터 정리(선택 사항)

## 다음 단계

설치를 완료한 후:

1. 상점을 설정합니다.
   - [Edge Delivery Services 상점](./storefront.md) 구성
   - 카탈로그 데이터에 연결

1. Carvelo 사용 사례 살펴보기:
   - [전체 워크플로](./use-case/admin-use-case.md) 팔로우
   - 실제 시나리오를 사용한 연습

1. 머천다이징 구성:
   - [제품 검색](./merchandising/overview.md) 설정
   - [권장 사항](./merchandising/recommendations/overview.md) 만들기

1. 성능 모니터링:
   - [성공 지표](./manage-results/success-metrics.md) 추적
   - [검색 성능 분석](./manage-results/search-performance.md)

## 문제 해결

### 일반적인 문제

| 문제 | 솔루션 |
|---|---|
| **인스턴스를 만들 수 없음** | [!DNL Adobe Commerce Optimizer]개의 권한 및 관리자 권한이 있는지 확인하십시오. |
| **인스턴스가 표시되지 않음** | Adobe IMS 조직을 확인하고 페이지를 새로 고칩니다. |
| **인스턴스에 액세스할 수 없음** | Admin Console에서 사용자로 추가되었는지 확인합니다. |
| **샘플 데이터가 로드되지 않음** | 인스턴스 자격 증명 및 API 끝점을 확인합니다. |

### 도움말 보기

- **개발자 리소스**: [개발자 설명서](https://developer-stage.adobe.com/commerce/services/composable-catalog/)
- **Storefront 리소스**: [Commerce Storefront 설명서](https://experienceleague.adobe.com/developer/commerce/storefront/)
- **지원**: [Adobe Commerce 지원 리소스](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/overview)
