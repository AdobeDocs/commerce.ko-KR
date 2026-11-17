---
source-git-commit: 4032a0871d0a9b129ad870c93f62a2a7596ea8b7
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 0%
---
<!--
SOURCE OF TRUTH: Edit this file in the commerce.en repo:
https://github.com/Adobe-Enterprise-Docs/commerce.ko-KR/blob/main/help/_includes/ccdm-shared/setup/catalog-view.md

This content is shared by the Adobe Commerce Optimizer Guide (commerce.en) and the
Merchandising Services with CCDM Guide (commerce-admin.en). Changes made in commerce.en
are synced automatically to commerce-admin.en, so do not edit the copy in that repo.
This includes related images in help/assets/ccdm-shared/.
-->

# Adobe Merchandising 서비스에 대한 카탈로그 보기 개요

<!--This shared include file contains the conceptual and architecture overview of catalog views for Adobe Merchandising Services-->

카탈로그 보기는 클라이언트가 검색할 수 있는 제품 및 가격을 정의합니다. 카탈로그 소스, 카탈로그 계층, 정책 및 가격 장부를 결합하여 다양한 브랜드, 지역, 비즈니스 단위 또는 채널을 지원합니다.

## 카탈로그 보기란 무엇입니까?

카탈로그 보기는 제품 카탈로그를 구성하고 표시하는 방법을 정의합니다. 이는 다음을 결정하는 필터 역할을 합니다.

- **표시되는 제품** 비즈니스 구조(브랜드, 지역, 대리점)에 따라
- **연결된 가격 장부를 통해 표시되는 가격**
- 정책(브랜드, 모델, 범주 등의 특성)을 사용하여 **제품을 필터링하는 방법**
- **로케일과 같은 특성을 기반으로 [카탈로그 원본](/help/optimizer/setup/catalog-sources.md)을(를) 사용하는 항목**
- **보기의 데이터에 액세스할 수 있는 사용자**&#x200B;[카탈로그 보호](private-catalog-view.md) 및 [제한된 액세스 키](restricted-access-keys.md)

예를 들어 다음에 대해 별도의 카탈로그 보기를 만들 수 있습니다.

- 브랜드 또는 비즈니스 단위
- 지리적 지역
- 딜러 또는 파트너 채널
- 특정 가격을 제공하는 고객 세그먼트

## 아키텍처 개요

카탈로그 보기는 Adobe Merchandising 기본 설정에서 사용되는 웹 사이트, 스토어, 스토어뷰 프레임워크를 보다 유연한 모델로 대체하는 Adobe Commerce 서비스 프레임워크의 일부입니다.

![[!DNL Merchandising Services] 아키텍처](/help/assets/ccdm-shared/setup/merchandising-svcs-architecture.png)

### 작동 방식

**1. 데이터 수집**
Adobe Commerce 백엔드 또는 다른 타사 백엔드(예: PIM 또는 ERP) 및 기타 시스템의 카탈로그 데이터는 Adobe Merchandising 서비스 데이터 레이어에 수집됩니다. 각 SKU에는 카탈로그 보기, 정책 및 로케일에 매핑되는 로케일 정보와 제품 특성이 포함되어 있습니다. 데이터 수집 프로세스는 소스 시스템 및 통합 방법에 따라 다릅니다.

- **Adobe Commerce 백엔드** - 시스템이 Commerce 카탈로그 피드를 내보내고 데이터 수집 REST API에 필요한 형식으로 매핑하며 피드 데이터를 Adobe Merchandising 서비스 데이터 레이어에 동기화합니다. 이 모델에서 Adobe Commerce은 초기 동기화 및 후속 업데이트를 관리합니다. 피드에는 제품, 카테고리, 제품 속성, 가격 및 가격 장부가 포함됩니다.

- **타사 백엔드 또는 소스 시스템**—커넥터 또는 통합 서비스는 API, 이벤트 또는 내보내기 피드를 통해 소스에서 카탈로그 데이터를 검색한 다음 구성 가능한 카탈로그 데이터 모델(CCDM) 스키마에 대해 매핑하고 유효성을 검사한 다음 데이터 수집 REST API를 사용하여 Adobe Merchandising 서비스 레이어에 데이터를 동기화합니다. 통합은 초기 로드 및 이후 변경 사항 전송을 담당합니다. Adobe의 [Salesforce Commerce 커넥터](https://experienceleague.adobe.com/ko/docs/commerce/optimizer/developer/salesforce-connector)와 같은 플랫폼별 커넥터가 시작점을 제공할 수 있습니다.

**2. 통합 기본 카탈로그**
수집된 데이터는 카탈로그 서비스 데이터 파이프라인에 통합 기본 카탈로그를 만듭니다. 이 단일 소스는 여러 사업부에서 데이터 중복을 제거합니다.

**3. 카탈로그 보기**
여러 카탈로그 보기는 서로 다른 비즈니스 단위를 나타냅니다(예: &quot;Texas Retail&quot;, &quot;Texas Retail Seasonal&quot;). 카탈로그 보기에서 로케일, 정책 및 가격 책자를 공유하여 유연성을 높일 수 있습니다.

**4. 다중 채널 게재**
필터링된 카탈로그 데이터는 Edge Delivery Services, 마켓플레이스, 광고 플랫폼 및 사용자 지정 마이크로 스토어와 같은 대상에 제공됩니다. 카탈로그 데이터 배달에 대한 자세한 내용은 [개발자 설명서](https://developer.adobe.com/commerce/services/optimizer/)를 참조하세요.

카탈로그 보기에서 **[!UICONTROL Catalog Protection]**&#x200B;을(를) 사용하도록 설정한 경우 해당 대상으로 배달하려면 할당된 [제한된 액세스 키](restricted-access-keys.md)에서 서명된 올바른 토큰이 필요합니다. 카탈로그 데이터를 받는 대신 승인되지 않은 요청이 거부됩니다.

### 주요 구성 요소

| 구성 요소 | 목적 | 예 |
|---|---|---|
| **카탈로그 보기** | 사업부 또는 배포 채널 | 딜러 네트워크, 지역 스토어 |
| **정책** | 속성을 기반으로 한 제품 필터 | 브랜드, 모델, 카테고리 |
| **로케일** | 언어/지역 설정 | en-US, fr-CA, es-MX |
| **가격표** | 가격 구조 | 소매, 도매, 직원 |
| **제한된 액세스 키** | 보호된 카탈로그 보기에 대한 액세스를 여는 서명된 토큰 자격 증명 | 파트너 포털 키, B2B 가격 키 |

### 데이터 흐름

1. **수집** - Adobe Commerce 백엔드의 카탈로그 데이터
2. **프로세스** - 카탈로그 보기, 정책 및 가격 적용
3. **배달** - 필터링된 카탈로그를 상점, 마켓플레이스 등에 제공합니다.

## 주요 기능

| 기능 | 이익 |
|---|---|
| **단일 기본 카탈로그** | 여러 사업부에서 데이터 중복 제거 |
| **유연한 가격** | 다양한 고객 세그먼트에 대한 SKU당 여러 가격 장부 |
| **확장 가능** | 2억 개 이상의 SKU를 효율적으로 관리 |
| **다중 채널** | 상점, 시장 및 광고 플랫폼에 카탈로그 제공 |
| **실시간 업데이트** | 프로모션 및 캠페인에 대한 카탈로그 데이터를 빠르게 업데이트 |
| **비공개 카탈로그 보기** | 서명된 토큰 유효성 검사를 사용하여 승인된 클라이언트로 카탈로그 보기 제한 |

## 사용 사례

### 멀티브랜드 복합 기업

**과제**: 여러 브랜드, 국가 및 언어 관리<br>
**솔루션**: 각 브랜드/지역 조합에 대한 카탈로그 보기가 있는 단일 카탈로그

### 자동차 부품 딜러

**과제**: 같은 제품이지만 가격이 다른 3,000개의 딜러<br>
**솔루션**: 판매자별 카탈로그 보기 및 가격 책자가 있는 카탈로그 1개

### 다중 위치 retailer

**과제**: 위치별로 다른 가격 및 인벤토리<br>
**솔루션**: 지역별 정책이 있는 위치 기반 카탈로그 보기

>[!NOTE]
>
>카탈로그 데이터 수집 및 배달에 대한 자세한 내용은 [개발자 설명서](https://developer.adobe.com/commerce/services/optimizer/)를 참조하세요.
