---
title: '[!DNL Catalog Service] 릴리스 정보'
description: Adobe Commerce의  [!DNL Catalog Service] 에 대한 최신 릴리스 정보입니다.
feature: Services, Catalog Service, Release Notes
exl-id: 74f2e46a-5592-4857-a6d7-b95b85d8b4cc
source-git-commit: 5dd290a4e10bdbd1f6c96b67ab6c9ba1598705dc
workflow-type: tm+mt
source-wordcount: '1020'
ht-degree: 0%

---

# [!DNL Catalog Service] 릴리스 정보

이 릴리스 노트는 [!DNL Catalog Service]의 최신 버전에 대해 설명합니다.
현재 주요 릴리스 버전에 대한 지원이 제공됩니다. 이전 버전에 대한 릴리스 노트는 참조를 위해 제공됩니다.
업데이트에는 다음이 포함됩니다.

새 기능 ![개](../assets/new.svg)개
![수정](../assets/fix.svg) 수정 사항 및 개선 사항
![버그](../assets/bug.svg) 알려진 문제

## 현재 메이저 버전

### V1.26 릴리스

_2024년 10월 22일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새로 만들기](../assets/new.svg) 이제 GraphQL 스키마에 제품 정보에 `lastModifiedAt` 특성이 포함됩니다. 이 정확한 타임스탬프는 사이트 맵이 제품의 최신 업데이트를 정확하게 반영하도록 하는 데 도움이 됩니다. 또한 Google과 같은 검색 엔진이 색인 재지정이 필요한 시기를 판별하는 데 도움을 주어 크롤링 프로세스를 최적화하고 정확한 정보를 사용할 수 없을 때 사용되는 공격적인 마지막 수정 날짜와 관련된 문제를 방지합니다. <!--DATA-6209-->

## 이전 버전

+++ 이전 버전

### V1.23 릴리스

_2024년 8월 22일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![수정](../assets/fix.svg) 이제 제품 재정의(가격) 데이터 없이 제품 정보를 검색할 수 있습니다. 이전 릴리스에서 이러한 쿼리가 다음 오류를 반환했습니다.
`The following sku does not have product override data in the DB: <SKU value>. Make sure data is synced.` <!--DATA-6121-->

### V1.22 릴리스

_2024년 8월 13일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새로 만들기](../assets/new.svg) 제품 SKU별로 모든 변형을 검색할 수 있는 지원이 추가되었습니다. [카탈로그 서비스 API 참조](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/)를 참조하세요. <!--DATA-6067-->

### V1.22 릴리스

_2024년 8월 13일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새로 만들기](../assets/new.svg) 제품 SKU별로 모든 변형을 검색할 수 있는 지원이 추가되었습니다. [카탈로그 서비스 API 참조](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/)를 참조하세요. <!--DATA-6067-->

### V1.19 릴리스

_2024년 5월 23일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상


![수정](../assets/fix.svg) <!--DATA-5033-->옵션 값에 대한 `InStock` 플래그는 이제 제품 변형의 범위 `enabled` 상태를 고려합니다.

![수정](../assets/fix.svg) <!--DATA-5888-->큰 숫자(최대 16자리)와 더 큰 소수점 이하 자릿수(최대 4자리)가 필요한 제품 가격에 대한 지원을 추가하십시오. 기존 카탈로그에 가격 구성 업데이트를 적용하려면 [데이터 관리 대시보드](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard)에서 또는 [Adobe Commerce 명령줄 인터페이스](../landing/catalog-sync.md#command-line-interface)를 사용하여 카탈로그 데이터를 다시 동기화하십시오.

#### 알려진 제한 사항

다음 기능은 아직 지원되지 않습니다.

* 동적 특성 페이로드의 최대 크기는 9MB입니다.
* 그룹 제품 가격은 간단한 제품 가격으로 계산할 수 있습니다.
* 이미지 배열에서는 첫 번째 이미지만 역할을 포함합니다.

API Mesh 및 Core GraphQL API를 사용하여 다음 제한 사항을 해결합니다.

* 최소 광고 가격
* 계층 가격
* 고정 가격으로 묶음 제품

자세한 내용과 예제는 [카탈로그 서비스 및 API Mesh](mesh.md)를 참조하세요.

### V1.18 릴리스

_2024년 4월 11일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새로 만들기](../assets/new.svg)에서 PHP 8.3에 대한 지원을 추가했습니다.

![새로 만들기](../assets/new.svg) [`products`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/) 및 [`refineProduct`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/refine-product/) 쿼리가 이제 단순 제품과 복합 제품 모두에 대해 사용자 지정 가능한 옵션 데이터를 반환합니다.<!--DATA-5538-->

### V1.17 릴리스

_2024년 2월 22일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새로 만들기](../assets/new.svg) 이제 [[!DNL Data Management Dashboard]](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-dashboard.html)을(를) 사용할 수 있습니다. 이렇게 개조된 대시보드는 [!DNL Product Recommendations], [!DNL Live Search] 및 [!DNL Catalog Service]의 데이터 스트림에 대한 통찰력을 제공합니다. 이 기능에 대한 지원은 `catalog-service` 메타패키지의 v3.1.0에 도입되었습니다.

### V1.16 릴리스

_2024년 2월 13일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새](../assets/new.svg) 제품 비디오는 이제 카탈로그 서비스 API에서 지원됩니다.
![수정](../assets/fix.svg) 재고 부족 옵션이 이제 PDP 위젯에 표시됩니다.

#### 알려진 제한 사항

다음 기능은 아직 지원되지 않습니다.

* 동적 특성 페이로드의 최대 크기는 9MB입니다.
* 그룹 제품 가격. 이 값은 간단한 제품 가격으로 계산할 수 있다.
* 이미지 배열에서는 첫 번째 이미지만 역할을 포함합니다.

API Mesh 및 Core GraphQL API를 사용하면 다음 제한 사항을 해결할 수 있습니다.

* 최소 광고 가격
* [계층 가격](mesh.md)

### V1.13 릴리스

_2023년 10월 12일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새](../assets/new.svg) 카탈로그 서비스는 제품 변형에 대해 `inStock` 플래그를 지원합니다.
![새로 만들기](../assets/new.svg) `urlKey` 및 `externalId` 필드가 GraphQL 스키마에 추가되었습니다.
![새로운](../assets/new.svg) 다운로드 가능한 제품 및 기프트 카드가 지원됩니다.

### V1.12 릴리스

_2023년 9월 19일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새](../assets/new.svg) 카탈로그 서비스가 이제 [SaaS 가격 인덱싱](../price-index/price-indexing.md)를 사용합니다.
![수정](../assets/fix.svg) 이 릴리스에는 서비스 측의 버그 수정 및 개선 사항이 포함되어 있습니다.

### V1.11 릴리스

_2023년 7월 18일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새](../assets/new.svg) 카탈로그 서비스가 이제 제품 권장 사항에 대한 [`recommendations`](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/recommendations/) GraphQL 쿼리를 지원합니다.

### V1.10 릴리스

_2023년 6월 27일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새로 만들기](../assets/new.svg) 이제 카탈로그 서비스 API가 `related products`을(를) 지원합니다.

### V1.7 릴리스

_2023년 4월 12일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새](../assets/new.svg) 카탈로그 서비스가 삭제된 제품 변형을 정리합니다.
![인프라 확장성 및 성능 개선 사항을 수정](../assets/fix.svg)합니다.

### V1.6 릴리스

_2023년 3월 28일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새로 만들기](../assets/new.svg) [`products`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/) 쿼리에 견본을 추가했습니다.
![새로 만들기](../assets/new.svg)에서 `entityId`API Mesh[를 사용하여 &#x200B;](mesh.md)을(를) 가져오는 기능을 추가했습니다.

### V1.5 릴리스

_2023년 3월 6일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새로 만들기](../assets/new.svg)에 [`categories`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/) GraphQL 기능이 추가되었습니다.
![수정](../assets/fix.svg) 향상된 성능 및 API 확장성.

### V1.4 릴리스

_2023년 2월 7일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.x 이상

![새로 만들기](../assets/new.svg) 카탈로그 서비스 메타패키지를 게시하여 설치 단계를 간소화했습니다.
![API 확장성 및 성능 개선 사항을 수정](../assets/fix.svg)합니다.

### V1.3 릴리스

_2023년 1월 17일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.x 이상

![새로 만들기](../assets/new.svg) 온보딩 환경을 간소화하고 개선했습니다.
![새](../assets/new.svg) 새 고객 샌드박스 끝점을 프로덕션 전 테스트에 사용할 수 있습니다.
가상 제품에 대한 ![새](../assets/new.svg) 지원이 추가되었습니다.
![API 확장성 및 성능 개선 사항을 수정](../assets/fix.svg)합니다.

### V1.1 릴리스

_2022년 11월 18일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.x 이상

![새](../assets/new.svg) 카탈로그 서비스가 이제 Adobe의 [API Mesh](https://developer.adobe.com/graphql-mesh-gateway/)를 지원합니다.
![수정](../assets/fix.svg) 향상된 API 확장성 및 전체 성능.

### V1.0 릴리스

_2022년 10월 4일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.x 이상

![새로 만들기](../assets/new.svg) 이제 번들 및 그룹화된 제품을 지원합니다.
![새로 만들기](../assets/new.svg)에서 B2B 가시성 재정의를 추가했습니다. 이제 제품을 검색할 수 있으며 특정 고객 그룹을 위해 장바구니에 추가할 수 있습니다.
![수정](../assets/fix.svg) 서비스가 이제 안정적이며 성능이 향상되었습니다.

### 0.3 릴리스 - Beta+

_2022년 9월 12일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.x 이상

![New](../assets/new.svg) Images for variants 지원: 제품 이미지는 선택한 옵션에 따라 반환됩니다
가격 지원을 위한 ![새로운](../assets/new.svg) 역할: 특정 고객 그룹의 구성원만 제품 가격을 볼 수 있도록 허용
![수정](../assets/fix.svg) 서비스의 안정성 및 성능 향상
카탈로그에서 제품이 삭제되면 ![새](../assets/new.svg) 업데이트가 수신됨

### Beta 릴리스

_2022년 8월 9일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.x 이상

![새로 만들기](../assets/new.svg) `products` 및 `refineProduct` 쿼리가 다음 데이터를 반환합니다.

* 사전 정의된(시스템) 제품 속성.
* 동적 제품 속성을 확인하고 역할별로 필터링합니다(제품 표시 페이지/제품 목록 페이지).
* 제품 옵션.
* 제품 이미지를 만들고 역할(PDP/PLP)별로 필터링합니다.
* 간단한 제품에 대한 특정 가격 및 구성 가능한 제품에 대한 가격 범위입니다.
* 고객 그룹 가격 및 가격 범위. 고객 그룹이 없는 쇼핑객에 대해 대체 기본 가격을 반환합니다.
* B2B 고객별 가격을 사용하는 제품 유형입니다.
