---
title: Salesforce Commerce 커넥터
description: 카탈로그 데이터를 동기화하고 비즈니스 작업을 지원하기 위해 커넥터를 구현하고 사용자 지정하기 위해 Salesforce Commerce B2C를  [!DNL Commerce Optimizer SFCC Connector] 과(와) 통합하는 시작점을 제공하는  [!DNL Adobe Commerce Optimizer] 에 대해 알아봅니다.
role: Admin, Developer
source-git-commit: c6725fc524e9d239ccc0f16701e92ad5d2fc7729
workflow-type: tm+mt
source-wordcount: '1115'
ht-degree: 0%

---

# Adobe Commerce Optimizer용 Salesforce Commerce 커넥터

Adobe App Builder 기술을 기반으로 구축된 [!DNL Commerce Optimizer Salesforce Commerce Connector]을(를) 통해 Salesforce Commerce Cloud B2C에서 [!DNL Adobe Commerce Optimizer]&#x200B;(으)로 카탈로그 데이터를 원활하게 전송하고 관리할 수 있습니다. 두 플랫폼 간에 브리지를 제공하여 제품 정보, 가격 및 업데이트를 재구성하지 않고 동기화 상태로 유지합니다.

즉시 사용 가능한 이 커넥터는 안정적인 데이터 동기화 기능과 비즈니스 요구 사항에 맞게 워크플로우를 사용자 지정할 수 있는 유연성을 제공합니다.

전체 비디오 튜토리얼 시리즈를 보려면 [Salesforce Commerce 클라우드 시작 키트에 대해 알아보기](https://experienceleague.adobe.com/ko/docs/commerce-learn/tutorials/adobe-commerce-optimizer/sfcc-starter-kit/overview)를 참조하십시오.

## 주요 기능

* **카탈로그 데이터 동기화:** 상점 및 경험 기반 응용 프로그램을 최신 상태로 유지하기 위해 Salesforce Commerce B2C에서 Adobe Commerce Optimizer으로 제품 데이터(변형, 가격 장부 및 구조 포함)를 푸시합니다.
* **가격 동기화:** Salesforce Commerce B2C에서 직접 가격 데이터를 가져오고 관리합니다.
* **여러 데이터 형식을 지원합니다.** 제품, 가격 및 카탈로그 구조를 동기화하여 복잡한 머천다이징 구성을 반영합니다.

* **유연한 동기화 워크플로**
   * **예약된 동기화:** cron 작업 일정을 사용하여 업데이트를 자동화합니다. 수작업이 필요하지 않습니다.
   * **주문형 업데이트:** 긴급 변경, 수정 또는 제품 출시에 대한 SKU 수준 업데이트를 즉시 트리거합니다.

* **확장성을 위해 빌드됨**
   * 호환성을 위해 사용자 지정 [Salesforce Commerce B2C API](https://developer.salesforce.com/docs/commerce/commerce-api/guide/get-started.html)&#x200B;(SCAPI) 끝점을 사용하고 고유 사용 사례 또는 고급 사용 사례에 쉽게 적응합니다.
   * 카탈로그 및 가격 동기화를 통해 비즈니스 시작으로 확장한 다음 추가 통합 또는 비즈니스 논리를 지원하도록 워크플로우를 확장합니다.
   * 핵심 통합을 재구축하지 않고도 워크플로우를 구성하고 발전시킬 수 있습니다.

>[!NOTE]
>
>커넥터는 Salesforce Commerce Cloud B2C용으로 특별히 설계되었습니다. 다른 기술 스택에 구축된 Salesforce B2B 또는 D2C 제품을 지원하지 않습니다.

## Salesforce 커넥터의 장점은 무엇입니까?

[!DNL Salesforce Commerce Connector]은(는) 다음에 이상적입니다.

* **기존 Salesforce Commerce Cloud B2C 고객** 상점 개선 기능
* **여러 상점에서 고급 머천다이징 및 개인화 기능이 필요한 다중 브랜드 조직**
* 더 빠른 상점 경험을 위해 Adobe의 Edge Delivery Services을 통해 **성능을 개선하려는 기업**
* **복잡한 가격 구조를 가진 회사** 정교한 가격 책자와 로케일별 가격 책정 동기화
* **AEM 고객** Edge Delivery Services과 함께 Adobe Commerce 스토어프론트 를 사용하는 동안 Salesforce Commerce B2C에서 제품 카탈로그를 관리합니다.
* **다중 로케일 요구 사항이 있는 소매점** 시장 및 언어 간에 지역화된 제품 정보 동기화

## 사용 사례

커넥터는 다음과 같은 몇 가지 주요 사용 사례를 지원합니다.

### 카탈로그 데이터 수집 및 상점 첫 화면 표시

이 주요 사용 사례는 Salesforce Commerce B2C에서 Adobe Commerce 스토프론트로의 전체 데이터 흐름을 보여 줍니다.

1. **초기 카탈로그 수집:** 변형이 있는 간단한 제품, 가격 장부 및 가격 정보를 포함하여 전체 Salesforce 상거래 카탈로그를 대량으로 로드합니다.
1. **자동화된 델타 업데이트:** Salesforce Commerce 카탈로그 관리 UI에서 [!DNL Commerce Optimizer]&#x200B;(으)로 제품 업데이트를 자동으로 동기화합니다.
1. **Storefront 통합:** [!DNL Commerce Optimizer]개의 storefront API를 사용하여 Adobe Commerce Edge Delivery 서비스 스토어프론트에서 동기화된 카탈로그 데이터를 표시합니다.
1. **실시간 업데이트:** Salesforce에서 변경 작업을 수행한 후 업데이트된 제품 정보(이름, 가격, 설명)를 바로 매장에 표시합니다.

### 다중 로케일 제품 관리

Salesforce Commerce B2C 현지화 기능 활용:

* 다양한 로케일에 대해 Salesforce Commerce B2C의 현지화된 제품 텍스트 필드 버전(이름, 설명)을 동기화합니다.
* Salesforce 로케일 개념 1:1을(를) [!DNL Commerce Optimizer] 로케일로 매핑합니다.
* 다양한 현지화에 대해 여러 제품 수집 주기를 지원합니다.
* 글로벌 제품 카탈로그 간 일관성 유지

## 아키텍처 및 구성 요소

[!DNL SFCC Connector]은(는) Salesforce Commerce B2C 인스턴스와 [!DNL Commerce Optimizer] 간에 강력한 통합 계층을 제공합니다. 커넥터는 카탈로그 데이터, 가격 장부 및 제품 정보를 전송하는 일련의 동기화 작업을 통해 작동합니다.

1. **데이터 추출** - Salesforce Commerce B2C 인스턴스로 인증하고 사용자 지정 SCAPI API를 사용하여 카탈로그 데이터를 추출합니다.
1. **데이터 변환** - [!DNL Commerce Optimizer] 데이터 모델 및 스키마 요구 사항과 일치하도록 제품 데이터를 변환합니다.
1. **데이터 수집**—ACO TypeScript SDK을 사용하여 변환된 데이터를 [!DNL Commerce Optimizer]에 안전하게 전송합니다.
1. **Storefront 통합** - Storefront 경험에 대해 [!DNL Commerce Optimizer] API를 통해 동기화된 데이터를 사용할 수 있습니다.

다음 다이어그램은 통합에 대한 높은 수준의 데이터 흐름을 보여 줍니다.

![Salesforce Commerce 커넥터 아키텍처](../assets/sfcc_starter_kit.png){zoomable="yes"}

### 주요 구성 요소

[!DNL Commerce Optimizer SFCC Connector]은(는) 다음과 같은 몇 가지 주요 구성 요소로 구성됩니다.

* **ACO SFCC 스타터 키트 App Builder 응용 프로그램** - SFCC와 Adobe Commerce Optimizer 간의 데이터 동기화를 처리하는 서버리스 기능을 제공합니다.
* **사용자 지정 SFCC 카트리지** - 데이터 추출에 필요한 API로 Salesforce Commerce Cloud 인스턴스를 확장하는 필수 카트리지.
* **관리 UI** - 동기화 상태를 모니터링하고 커넥터 작업을 관리하기 위한 웹 인터페이스입니다.

### 동기화 프로세스

커넥터가 여러 동기화 모드를 지원합니다.

| 동기화 모드 | 설명 |
|-----------|-------------|
| **전체 사이트 동기화** | 구성된 Salesforce Commerce Cloud 사이트 및 로케일에 대해 모든 제품, 가격 장부 및 가격을 종합적으로 동기화합니다. 여기에는 다음이 포함됩니다 <ul><li>제품 메타데이터 및 속성</li><li>카탈로그 구조 및 범주</li><li>가격 장부</li><li>가격 정보</li><li>다중 로케일 제품 데이터</li></ul> |
| **델타 동기화** | 마지막 동기화 이후 Salesforce 제품 및 가격 데이터에서 변경된 사항만 검색하고 동기화하여 효율적이고 시기 적절한 업데이트를 보장합니다.<br>데이터 새로 고침을 유지하기 위해 델타 동기화가 일정에 따라 자동으로 실행됩니다(기본값: 시간별). |
| **대상 동기화 옵션** | 세분화된 동기화 기능 제공: <ul><li>**가격 장부 동기화** 가격 장부 정보만 동기화</li><li>**메타데이터 동기화**&#x200B;는 제품 메타데이터 및 특성 정의를 업데이트합니다.</li><li>**특정 제품 동기화** SKU별로 개별 제품 동기화</li></ul> |

## 중요한 고려 사항

구현을 계획할 때 다음 주요 요소를 고려하십시오.

### 데이터 매핑 및 속성

* **검색 가능한 특성:** Salesforce Commerce B2C는 UI를 통해 API에 표시되지 않는 검색 가능한 특성을 설정합니다. [[!DNL Catalog Data Ingestion metadata APIs]](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/#metadata)을(를) 사용하여 Adobe Commerce Optimizer에서 이러한 검색 가능한 특성을 수동으로 구성하십시오.
* **특성 매핑:** 비즈니스 요구 사항에 따라 [!DNL Commerce Optimizer] 메타데이터에 대한 Salesforce Commerce B2C 제품 특성 매핑을 계획합니다.
* **기본 검색 가능한 필드:** 커넥터는 기본적으로 코어 특성(`name`, `description`, `ID`)을 자동으로 검색합니다.

### 동기화 범위

* **사이트 선택:** Salesforce Commerce B2C에는 카탈로그가 연결되는 사이트 개념이 있습니다. 전체 동기화 중에 동기화할 Salesforce 사이트를 선택합니다.
* **로케일 관리:** 각 Salesforce Commerce 로케일은 [!DNL Commerce Optimizer]에서 별도의 제품 수집 주기를 만듭니다.
* **데이터 볼륨:** 구현을 계획할 때 카탈로그 크기 및 동기화 빈도를 고려하십시오.

## 모니터링 및 관리

설치 및 구성이 완료되면 [!DNL Commerce Optimizer SFCC Connector]은(는) [!DNL SFCC to ACO Sync Panel]에서 포괄적인 모니터링 및 관리 기능을 제공합니다.

![Salesforce Commerce 커넥터 관리 UI](../assets/sfcc_management_ui.png){width="700" zoomable="yes"}

이 인터페이스의 URL은 [!DNL Commerce Optimizer SFCC Connector Starter Kit]을(를) App Builder 프로젝트에 배포한 후에 제공됩니다.

주요 기능은 다음과 같습니다.

* **동기화 상태 추적:** 모든 동기화 작업의 상태 및 타임스탬프를 모니터링합니다.
* **연결 유효성 검사:** Salesforce Commerce Cloud과 Adobe Commerce Optimizer 모두에 대한 연결을 테스트합니다.
* **제품 데이터 유효성 검사:** 동기화된 제품 데이터가 상점 앞에 올바르게 표시되는지 확인하십시오.
* **오류 로깅 및 문제 해결:** 문제 해결을 위한 오류 로그는 App Builder CLI를 통해 액세스할 수 있습니다.
* **상태 관리:** 동기화 진행 상황을 추적하고 기본 제공 상태 관리와의 충돌을 방지합니다.

## Source 코드 및 개발 리소스

[!DNL Commerce Optimizer SFCC Connector]은(는) 오픈 소스이며 사용자 지정할 수 있습니다. 주요 저장소는 다음과 같습니다.

* **[ACO SFCC 시작 키트](https://github.com/adobe-commerce/aco-sfcc-starter-kit)** - 기본 커넥터 응용 프로그램 및 설명서.
* **[ACO SFCC 카트리지](https://github.com/adobe-commerce/aco-sfcc-cartridges)** - API 통합에 필요한 SFCC 카트리지.
* **[ACO TypeScript SDK](https://github.com/adobe-commerce/aco-ts-sdk)** - Adobe Commerce Optimizer 통합용 SDK.

이러한 저장소는 커넥터를 구현하고 사용자 정의하기 위한 전체 소스 코드, 자세한 설명서 및 예를 제공합니다.

## 다음 단계

Salesforce Commerce Cloud 데이터를 Adobe Commerce Optimizer과 통합할 준비가 되셨습니까? 먼저 [ACO SFCC 시작 키트 저장소](https://github.com/adobe-commerce/aco-sfcc-starter-kit)에서 자세한 구현 안내서를 검토하고 필요한 필수 구성 요소가 있는지 확인하십시오.
