---
title: Adobe Commerce Optimizer 커넥터
description: Commerce 클라우드 또는 온프레미스 프로젝트에서 Adobe Commerce Optimizer으로 데이터를 연결하는 방법에 대해 알아봅니다
feature: Personalization, Integration, Configuration
badgePaas: label="PaaS만" type="Informative" url="https://experienceleague.adobe.com/ko/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce 온 클라우드 프로젝트(Adobe 관리 PaaS 인프라) 및 온프레미스 프로젝트에만 적용됩니다."
source-git-commit: 380d2c91a17a3e6b84d435774de1b05ada7d3a52
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 0%

---


# Adobe Commerce Optimizer 커넥터

Adobe Commerce Optimizer 커넥터는 Adobe Commerce 온 클라우드 인프라 또는 온-프레미스 배포와 [!DNL Adobe Commerce Optimizer] 간에 카탈로그 및 가격 책정 데이터를 동기화하는 통합 브리지입니다. 데이터를 Adobe Commerce Optimizer으로 동기화하면 동적 AI 검색, 권장 사항, Edge Delivery Services의 Adobe Commerce 스토프런트를 비롯한 빠른 로드 Headless 스토어프론트 및 실시간 성능 분석과 같은 기능이 활성화됩니다.

## 아키텍처 및 경험

Adobe Commerce Optimizer 커넥터는 다음 그림과 같이 Commerce 웹 사이트 및 스토어 보기를 Commerce Optimizer 프로젝트에 매핑하여 작동합니다.

![Adobe Commerce Optimizer에 Commerce 데이터 매핑](./assets/storeview-to-catalogview-mapping.svg){width="600" zoomable="yes"}

Commerce에서 Commerce Optimizer으로 데이터를 내보낼 때:

* Commerce 스토어 보기는 카탈로그 소스에 매핑됩니다
* 웹 사이트는 가격 장부에 매핑됩니다.

연관된 카탈로그 및 가격 데이터를 내보내고 나중에 사용하여 카탈로그 보기를 만들고 선택적으로 특정 비즈니스 사용 사례에 대한 카탈로그 및 가격 데이터를 필터링하는 정책을 정의합니다.

Commerce 관리자로부터 Commerce 서비스(라이브 검색 및 제품 권장 사항)를 구성하고 관리하는 대신 [[!DNL Adobe Commerce Optimizer] 머천다이징 도구](../optimizer/merchandising/overview.md)를 사용하여 제품 검색(라이브 검색) 및 권장 사항(제품 권장 사항) 규칙 구성을 관리합니다. Adobe Commerce 인스턴스는 카탈로그 및 가격 데이터의 데이터 소스가 됩니다. Commerce에서 데이터가 업데이트되면 업데이트가 [!DNL Adobe Commerce Optimizer] 인스턴스에 동기화됩니다.

## 워크플로

커넥터를 사용하면 다음과 같은 몇 가지 주요 워크플로를 사용할 수 있습니다.

* **Commerce 카탈로그 데이터를[!DNL Adobe Commerce Optimizer]**(으)로 내보내기 - 가격 및 가격 장부 데이터를 웹 사이트 및 고객 그룹 수준에서 내보냅니다. 제품 및 제품 특성 데이터를 `store view` 수준에서 내보냅니다. 기본적으로 모든 Commerce 범위(웹 사이트 및 스토어 보기)에 대해 카탈로그 데이터 동기화가 활성화됩니다.

  이 워크플로를 사용하려면 `adobe-commerce/commerce-data-export-aco-adapter` PHP 확장을 설치하고 내보내기 구성을 검토한 다음 Commerce 관리자의 Commerce과 Commerce Optimizer 간 통합을 사용하도록 설정하십시오. 자세한 지침은 [시작하기](#get-started)를 참조하세요.

* **Commerce 웹 사이트를 매핑하고 보기 데이터를 저장하여[!DNL Adobe Commerce Optimizer]**(으)로 내보내기

  선택적으로 특정 웹 사이트 또는 스토어 보기에 대해서만 데이터를 동기화하도록 내보내기 설정을 사용자 지정합니다. 예를 들어 특정 시장 또는 지역에 대한 검색 및 검색 경험을 최적화하는 등 특정 사용 사례에 사용할 하나의 스토어 보기에 대한 카탈로그 데이터만 내보내도록 선택할 수 있습니다.

* **머천다이징 규칙 구성 및 관리**

  커넥터를 사용하면 Commerce 관리자의 [!DNL Adobe Commerce Optimizer] 및 [!UICONTROL Live Search] 페이지가 아닌 [!UICONTROL Product Recommendations] UI에서 제품 검색 및 권장 사항에 대한 머천다이징 규칙을 정의하고 관리할 수 있습니다.

* **Edge Delivery Services에서 Commerce 상점 배포**

  [!DNL Adobe Commerce Optimizer]과의 통합을 설정한 후 Edge Delivery Services에 Commerce Storefront를 설치 및 배포하여 [!DNL Adobe Commerce Optimizer]에서 사용할 수 있는 구성 가능한 API 기반 아키텍처 및 모듈식 구성 요소를 사용하여 초고속 성능, 확장성, 원활한 콘텐츠 작성, 통합 개인화 및 운영 비용 절감을 제공할 수 있습니다.

통합을 설정하고 이러한 워크플로를 활성화하는 방법에 대한 자세한 내용은 [시작하기](get-started.md)를 참조하십시오.
