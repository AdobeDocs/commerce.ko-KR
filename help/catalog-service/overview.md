---
title: '[!DNL Catalog Service]'
description: Adobe Commerce용 [!DNL Catalog Service]은(는) 기본 Adobe Commerce GraphQL 쿼리보다 훨씬 빠르게 제품 표시 페이지 및 제품 목록 페이지의 콘텐츠를 검색할 수 있는 방법을 제공합니다.
role: Admin, Developer
recommendations: noCatalog
exl-id: 525e3ff0-efa6-48c7-9111-d0b00f42957a
source-git-commit: ff5c717dbdd638e114bccc3f6dec26f4be269194
workflow-type: tm+mt
source-wordcount: '1095'
ht-degree: 0%

---

# Adobe Commerce용 [!DNL Catalog Service]

Adobe Commerce 확장용 [!DNL Catalog Service]은(는) 다음을 포함하여 제품 관련 상점 경험을 빠르고 완벽하게 렌더링할 수 있도록 풍부한 보기 모델(읽기 전용) 카탈로그 데이터를 제공합니다.

* 제품 세부 사항 페이지
* 제품 목록 및 범주 페이지
* 검색 결과 페이지
* 제품 회전 메뉴
* 제품 비교 페이지
* 장바구니, 주문 및 위시리스트 페이지와 같이 제품 데이터를 렌더링하는 다른 모든 페이지

[!DNL Catalog Service]은(는) [GraphQL](https://graphql.org/)을(를) 사용하여 제품, 제품 특성, 재고 및 가격을 포함한 카탈로그 데이터를 요청하고 받습니다. GraphQL은 프론트엔드 클라이언트가 Adobe Commerce과 같은 백엔드에 정의된 API(애플리케이션 프로그래밍 인터페이스)와 통신하는 데 사용하는 쿼리 언어입니다. GraphQL은 가볍고 시스템 통합자가 각 응답의 내용과 순서를 지정할 수 있으므로 널리 사용되는 통신 방법입니다.

Adobe Commerce에는 두 개의 GraphQL 시스템이 있습니다. 핵심 GraphQL 시스템은 구매자가 제품, 고객 계정, 장바구니, 체크아웃 등을 포함한 다양한 유형의 페이지와 상호 작용할 수 있도록 광범위한 쿼리(읽기 작업)와 변형(쓰기 작업)을 제공합니다. 하지만 제품 정보를 반환하는 쿼리는 속도에 최적화되지 않습니다. 서비스 GraphQL 시스템은 제품 및 관련 정보에 대한 쿼리만 수행할 수 있습니다. 이러한 쿼리는 유사한 핵심 쿼리보다 성능이 뛰어납니다.

카탈로그 서비스에서 사용할 수 있는 데이터는 SaaS 데이터 내보내기 확장에 의해 전달됩니다. 이 확장은 Commerce 애플리케이션과 연결된 Commerce 서비스 간의 데이터를 동기화하여 서비스 GraphQL API 종단점에 대한 쿼리가 가장 최신 카탈로그 데이터를 반환하도록 합니다. SaaS 데이터 내보내기 작업 관리 및 문제 해결에 대한 자세한 내용은 [SaaS 데이터 내보내기 안내서](../data-export/overview.md)를 참조하십시오.

[!DNL Catalog Service] 고객은 더 빠른 가격 업데이트와 동기화 시간을 제공하는 [SaaS 가격 인덱서](../price-index/price-indexing.md)를 사용할 수 있습니다.

## 아키텍처

다음 다이어그램은 두 개의 GraphQL 시스템을 보여 줍니다.

![카탈로그 아키텍처 다이어그램](assets/catalog-service-architecture.png)

핵심 GraphQL 시스템에서 PWA은 Commerce 애플리케이션에 요청을 보내고, 이 애플리케이션은 각 요청을 수신하여 처리하고, 여러 하위 시스템을 통해 요청을 보낸 다음, 상점 앞에 응답을 반환합니다. 이 라운드트립은 페이지 로드 시간이 느려질 수 있으며, 이로 인해 전환율이 낮아질 수 있습니다.

[!DNL Catalog Service]은(는) Storefront Services 게이트웨이입니다. 이 서비스는 제품 세부 사항 및 관련 정보(예: 제품 속성, 변형, 가격 및 카테고리)가 포함된 별도의 데이터베이스에 액세스합니다. 이 서비스는 인덱싱을 통해 데이터베이스를 Adobe Commerce과 계속 동기화합니다.
이 서비스는 애플리케이션과의 직접 통신을 우회하기 때문에 요청 및 응답 주기의 지연을 줄일 수 있습니다.

핵심 및 서비스 GraphQL 시스템은 서로 직접 통신하지 않습니다. 다른 URL에서 각 시스템에 액세스하고 호출에는 다른 헤더 정보가 필요합니다. 두 GraphQL 시스템은 함께 사용하도록 설계되었습니다. [!DNL Catalog Service] GraphQL 시스템은 제품 상점 경험을 더 빠르게 만들기 위해 핵심 시스템을 늘립니다.

선택적으로 [Adobe Developer App Builder용 API Mesh](https://developer.adobe.com/graphql-mesh-gateway/)를 구현하여 두 Adobe Commerce GraphQL 시스템을 Adobe Developer을 사용하는 개인 및 서드파티 API 및 기타 소프트웨어 인터페이스와 통합할 수 있습니다. 각 끝점으로 라우팅되는 호출이 헤더에 올바른 인증 정보를 포함하도록 메쉬를 구성할 수 있습니다.

## 아키텍처 세부 정보

다음 섹션에서는 두 GraphQL 시스템 간의 몇 가지 차이점에 대해 설명합니다.

### 스키마 관리

Catalog Service는 서비스로 작동하므로 통합자는 Commerce의 기본 버전에 대해 신경쓰지 않아도 됩니다. 쿼리의 구문은 모든 버전에 대해 동일합니다. 또한 스키마는 모든 판매자에 대해 일관됩니다. 이러한 일관성을 통해 모범 사례를 보다 쉽게 설정하고 상점 위젯의 재사용을 크게 늘릴 수 있습니다.

### 제품 유형 단순화

스키마는 제품 유형의 다양성을 두 가지 사용 사례로 줄입니다.

* 단순 상품은 단일한 가격과 수량으로 정의되는 상품이다. Catalog Service는 단순, 가상, 다운로드 가능 및 기프트 카드 제품 유형을 `simpleProductViews`에 매핑합니다.

* 복잡한 제품은 여러 개의 간단한 제품으로 구성됩니다. 구성 요소 단순 제품은 가격이 다를 수 있습니다. 쇼퍼가 구성 요소 단순 제품의 수량을 지정할 수 있도록 복잡한 제품을 정의할 수도 있습니다. Catalog Service는 구성 가능한 제품, 번들 및 그룹화된 제품 형식을 `complexProductViews`에 매핑합니다.

복잡한 제품 옵션은 유형이 아닌 동작에 의해 통합되고 구별됩니다. 각 옵션 값은 간단한 제품을 나타냅니다. 이 옵션 값은 가격을 포함한 간단한 제품 속성에 액세스할 수 있습니다. 구매자가 복잡한 제품에 대한 모든 옵션을 선택하면 선택한 옵션의 조합이 특정 간단한 제품을 가리킵니다. 단순 제품은 구매자가 사용 가능한 모든 옵션에 대한 값을 선택할 때까지 모호한 상태로 유지됩니다.

#### 제품 보기 속성

단순 제품과 복합 제품 모두 상점에 표시할 수 있는 고객 정의 속성이 있습니다. 이러한 특성은 [ProductViewAttributes](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/#productviewattribute-type)&#x200B;(으)로 반환됩니다. Adobe Commerce에서 사용 가능한 속성은 제품을 만들 때 정의됩니다. Adobe Commerce 백엔드에서 또는 프로그래밍 방식으로 특성을 추가할 수 있습니다. [SaaS 데이터 내보내기 피드 데이터 확장 및 사용자 지정](../data-export/extensibility-and-customizations.md)을 참조하세요.

>[!TIP]
>
>Commerce 백엔드에 데이터 형식을 추가하는 대신 [카탈로그 서비스와 API Mesh](mesh.md)를 사용하여 카탈로그 서비스 GraphQL 스키마를 확장하여 데이터를 추가하거나 기존 카탈로그 데이터를 구성하여 새 기능을 사용하도록 할 수 있습니다.

### 가격

단순 제품은 가격이 있는 기본 판매 단위를 나타냅니다. [!DNL Catalog Service]은(는) 할인 전 정가와 할인 후 최종 가격을 계산합니다. 가격 계산에는 고정 제품 세금이 포함될 수 있습니다. 개인화된 프로모션은 제외됩니다.

복잡한 제품에는 정해진 가격이 없습니다. 대신 카탈로그 서비스는 연결된 단식의 가격을 반환합니다. 예를 들어 판매자는 구성 가능한 제품의 모든 변형에 초기에 동일한 가격을 할당할 수 있습니다. 특정 크기나 색상이 인기가 없으면 판매자는 해당 변형의 가격을 낮출 수 있습니다. 따라서 복합(구성 가능) 제품의 가격은 처음에는 표준 및 인기 없는 변형의 가격을 모두 반영하여 가격 범위를 보여 줍니다. 쇼핑객이 사용 가능한 모든 옵션에 대한 값을 선택하면 상점 전면에는 단일 가격이 표시됩니다.

카탈로그 서비스는 큰 값(최대 16자리)과 높은 소수점 이하 자리 수(최대 4자리)의 가격을 지원하여 정확한 가격 업데이트 및 계산을 보장합니다.

>[!NOTE]
>
> [!DNL Catalog Service]을(를) 보유한 Commerce 고객은 [SaaS 가격 인덱서](../price-index/price-indexing.md)를 통해 웹 사이트에서 더 빠른 가격 변경 업데이트 및 동기화 시간을 이용할 수 있습니다.

## 구현

[!BADGE PaaS만]{type=Informative url="https://experienceleague.adobe.com/ko/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce 온 클라우드 프로젝트(Adobe 관리 PaaS 인프라) 및 온프레미스 프로젝트에만 적용됩니다."}

설치 프로세스를 수행하려면 [Commerce 서비스 커넥터](../landing/saas.md)를 구성해야 합니다. 그런 다음 시스템 통합자는 [!DNL Catalog Service] 쿼리를 통합하기 위해 상점 코드를 업데이트합니다. 모든 [!DNL Catalog Service] 쿼리가 GraphQL 게이트웨이로 라우팅됩니다. 온보딩 프로세스 중에 URL이 제공됩니다.
