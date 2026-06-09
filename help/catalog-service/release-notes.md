---
title: '[!DNL Commerce Storefront Catalog Service Release Notes]'
description: Adobe Commerce의  [!DNL Catalog Service] 에 대한 최신 릴리스 정보입니다.
feature: Services, Catalog Service, Release Notes
exl-id: 74f2e46a-5592-4857-a6d7-b95b85d8b4cc
TQID: https://experienceleague.adobe.com/-yxW4sTuk7LPjGy5YsQ65phtkBLiByg8SmBaQPHMevM
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: acc520f67bdd1bdafd34b356b59bb32145192497
workflow-type: tm+mt
source-wordcount: 2682
ht-degree: 0%

---

# [!DNL Commerce Storefront Catalog Service] 릴리스 정보

이러한 릴리스 노트는 다음을 포함한 최신 Commerce 카탈로그 서비스 업데이트를 다룹니다.

- **[Storefront 카탈로그 서비스 릴리스](#storefront-catalog-service)**

   - 개선된 데이터 검색을 위한 카탈로그 서비스 API 스키마 개선 사항
   - 카탈로그 서비스 API 및 기본 인프라의 보안, 성능 및 안정성 개선.

  이러한 API에 대한 자세한 내용은 Commerce 개발자 설명서에서 [Storefront Services 스키마](https://developer.adobe.com/commerce/webapi/graphql/schema/storefront-services/)를 참조하십시오.

- **[카탈로그 서비스 메타패키지 릴리스](#catalog-service-metapackage)**

   - 종속성을 업데이트하여 성능, 안정성 및 다른 Adobe Commerce 구성 요소와의 호환성을 개선했습니다.

- **[카탈로그 서비스 설치 관리자 릴리스](#catalog-service-installer)**

   - 카탈로그 서비스와 Commerce 스택 간의 호환성을 유지하기 위해 종속성이 업데이트되었습니다.

>[!NOTE]
>
>Commerce 프로젝트에서 Adobe Commerce Optimizer을 사용하여 카탈로그 데이터를 Commerce Edge Delivery Service 또는 Headless Storefront로 전달하는 경우 [Adobe Commerce Optimizer 릴리스 노트](../optimizer/release-notes.md)에서 최신 API 업데이트를 확인하십시오.

업데이트는 유형별로 분류됩니다.

새 기능 ![개](../assets/new.svg)개
![수정](../assets/fix.svg) 수정 사항 및 개선 사항
![버그](../assets/bug.svg) 알려진 문제

최신 버전에 대한 지원이 제공됩니다. 이전 버전에 대한 릴리스 노트는 참조를 위해 포함됩니다.

## Storefront 카탈로그 서비스

### 2026년 5월

**릴리스 날짜**: 2026년 5월 20일
<!-- v1.55 -->

![새로 만들기](../assets/new.svg) [문서화된 제한 및 경계](https://experienceleague.adobe.com/ko/docs/commerce/optimizer/boundaries-limits)에 따라 Adobe Commerce 및 Adobe Commerce as a Cloud Service 클라이언트 모두에 대해 요청당 최대 100개의 SKU를 강제 제한했습니다.
<!--DATA-7163-->

**릴리스 날짜**: 2026년 5월 13일
<!--v1.54-->

![새로 만들기](../assets/new.svg) **GraphQL의 범주 정렬 순서**—이제 `CategoryView` GraphQL 유형에 위치 필드가 포함되므로 상점 앞에는 카탈로그 계층 구조에서 판매자가 구성하는 순서로 범주를 표시할 수 있습니다.
<!--DATA-7166-->

**릴리스 날짜**: 2026년 5월 4일
<!-- v1.53 -->

![수정](../assets/fix.svg) 이제 상점 제품 가격에 모든 제품 유형에 대한 올바른 통화 코드(예: USD)가 표시됩니다. 이전에는 일부 제품에 예상 통화가 아닌 `NONE`이(가) 표시되어 가격이 누락되었습니다. 이 업데이트는 상점 전반에서 일관되고 정확한 가격 렌더링을 보장합니다.<!--DATA-7115-->

### 2026년 4월

**릴리스 날짜**: 2026년 4월 29일
<!--v1.52-->

Adobe Commerce Optimizer 및 Adobe Commerce as a Cloud Service에 대해 요청당 최대 100개의 SKU에 대한 ![새로운](../assets/new.svg) 강제 제한
[문서화된 제한 및 경계](https://experienceleague.adobe.com/ko/docs/commerce/optimizer/boundaries-limits)에 따른 클라이언트. <!--DATA-7156-->

**릴리스 날짜**: 2026년 4월 17일
<!--v1.51-->

![새로 만들기](../assets/new.svg) 클라이언트가 페이지 번호를 매긴 결과를 사용하여 이름별로 범주를 검색할 수 있는 새 `searchCategory` GraphQL 쿼리를 추가했습니다. 쿼리는 필수 `searchTerm`(최소 3자)과 선택적 `family`, `pageSize` 및 `currentPage` 매개 변수를 허용합니다. 결과에 전체 범주 메타데이터와 일치하는 `CategoryTreeView` 개체, 페이지 매김을 위한 `totalCount` 및 `pageInfo`이(가) 포함됩니다. <!--COMOPT-1819-->

이 쿼리는 Adobe Commerce Optimizer 머천다이징 서비스를 사용하는 고객에게만 제공됩니다. [searchCategory](https://developer.adobe.com/commerce/services/reference/graphql/)를 참조하십시오.

### 2026년 3월

**릴리스 날짜**: 2026년 3월 24일
<!--v1.49-->

![새로 만들기](../assets/new.svg) 동적 번들의 가격 범위를 계산하고 반환하는 지원이 추가되었습니다.
<!--DATA-7115-->

### 2025년 12월

**릴리스 날짜**: 2025년 12월 11일
<!-- v1.46 -->

![시스템 수준 및 인프라 개선을 수정하여 성능과 안정성을 개선합니다](../assets/fix.svg).
<!--DATA-6852, DATA-6864-->

### 2025년 11월

**릴리스 날짜**: 2025년 11월 17일
<!-- v1.45 -->

![새로 만들기](../assets/new.svg) **이름별 특성 필터링**-이제 `productSearch` GraphQL 쿼리에서 `names` 필드를 사용하여 제품 특성을 필터링할 수 있습니다. <!--DATA-6831--> 이 필터를 사용하여 다음과 같은 작업을 수행할 수 있습니다.

- 특정 속성만 요청하여 응답 페이로드 크기 줄이기
- 기존 `roles` 필터와 결합하여 가시성 역할 및 특성 이름으로 범위를 좁힙니다.
- 예:

  **특성 이름으로만 필터링**

  ```graphql
  query {
    products(skus: ["SKU-001"]) {
      attributes(names: ["color", "size", "material"]) {
        name
        label
        value
      }
    }
  }
  ```

  **역할과 이름을 기준으로 필터링:**

  ```graphql
  query {
    products(skus: ["SKU-001"]) {
      attributes(roles: ["visible in PDP"], names: ["eco_collection", "new"]) {
        name
        label
        value
        roles
      }
    }
  }
  ```

>[!NOTE]
>
>필터링하지 않고 모든 특성을 검색하려면 `names` 인수를 생략하거나 빈 배열을 제공하십시오.

**릴리스 날짜**: 2025년 11월 6일
<!-- v1.44 -->

![시스템 수준 및 인프라 개선을 수정하여 성능과 안정성을 개선합니다](../assets/fix.svg). <!--DATA-6852, DATA-6864-->

![수정](../assets/fix.svg) 이제 상위 제품에 가격표가 없을 때 그룹화된 제품에 대해 쿼리할 수 있습니다. 하위 제품은 고유한 표시 역할을 반환합니다.<!--DATA-6779-->

![시스템 수준 및 인프라 개선을 수정하여 성능과 안정성을 개선합니다](../assets/fix.svg). <!--DATA-6721, DATA-6864-->

### 2025년 9월

**릴리스 날짜**: 2025년 9월 8일
<!-- v1.42 -->

![새로 만들기](../assets/new.svg) **계층 가격 지원을 추가했습니다** 볼륨 가격을 쿼리하는 데 추가했습니다.<!--DATA-6643-->

계층 가격 검색 방법:

1. 원하는 SKU에 `products` 쿼리 사용
2. **SimpleProductView**&#x200B;의 경우 `price.tiers`에 액세스
3. **ComplexProductView**&#x200B;의 경우 `priceRange.minimum.tiers` 및 `priceRange.maximum.tiers`에 액세스
4. 각 계층에는 할인된 `tier` 가격 및 `quantity` 조건이 포함되어 있습니다.
5. `gte`(크거나 같음)과 `lt`(보다 작음)을 사용하여 수량 임계값을 정의합니다.

**예:**

```graphql
query {
  products(skus: ["SKU-001"]) {
    ... on SimpleProductView {
      price {
        regular { amount { value currency } }
        tiers {
          tier { amount { value currency } }
          quantity {
            ... on ProductViewTierRangeCondition { gte lt }
          }
        }
      }
    }
  }
}
```

![수정](../assets/fix.svg) **최소 최종 가격으로 필터링된 계층 가격** <!--DATA-6643-->

이제 API는 제품의 최소 최종 가격보다 할인된 가격이 **낮은 계층만 반환합니다.**&#x200B;대신 최소 최종 가격이 상점 앞에 적용되므로 더 높은 계층은 생략됩니다.

적용 대상:

- **단순 제품**: `price.tiers`에는 `tier.amount.value` &lt; `price.final.amount.value`(최소 최종)인 계층만 포함됩니다.
- **복잡한 제품**: `priceRange.minimum.tiers` 및 `priceRange.maximum.tiers`은(는) 가격 범위를 만들 때 동일한 규칙을 사용합니다.

**릴리스 날짜**: 2025년 9월 2일
<!-- v1.41 -->

![수정](../assets/fix.svg) **누락된 가격 정보에 대한 오류 처리 개선**—가격 데이터를 아직 받지 않은 경우 API에서 오류를 발생시키는 대신 가격 필드에 대해 `null`을(를) 반환하여 클라이언트가 누락된 데이터를 정상적으로 처리할 수 있습니다.<!--DATA-6612-->

!&lbrack;시스템 수준 및 인프라 개선을 수정하여 성능과 안정성을 개선합니다.<!--DATA-6671-->&rbrack;(../assets/fix.svg)

### 2025년 7월

**릴리스 날짜**: 2025년 7월 30일
<!-- v1.40 -->

보안, 성능 및 안정성을 개선하기 위해 시스템 수준 및 인프라를 ![수정](../assets/fix.svg)합니다.<!--DATA-6619-->

**릴리스 날짜**: 2025년 7월 24일
<!-- v1.39 -->

![새로 만들기](../assets/new.svg) **단위 ID별로 권장 사항 단위 검색**-새 GraphQL 끝점 `recommendationsByUnitIds`은(는) 보다 유연하고 타깃팅된 액세스를 위해 고유 ID별로 권장 사항 단위를 검색합니다.

- `unitIds`이(가) 필요합니다(가져올 recId 목록).
- 컨텍스트 매개 변수(`currentSku`, `cartSkus`, `userViewHistory`, `userPurchaseHistory`, `category`)는 기존 권장 사항 쿼리와 동일하게 동작합니다.

- **예**

  ```graphql
  query {
    recommendationsByUnitIds(
      unitIds: ["11ee89d1-bfae-4582-a921-2ced44ff6bf7"]
      currentSku: "24-MB01"
      cartSkus: ["24-MB01"]
    ) {
      totalResults
      results {
        unitId
        unitName
        totalProducts
        productsView {
          sku
        }
        pageType
        typeId
        storefrontLabel
        displayOrder
      }
    }
  }
  ```

보안, 성능 및 안정성을 개선하기 위해 시스템 수준 및 인프라를 ![수정](../assets/fix.svg)합니다.<!--DATA-6316-->

**릴리스 날짜**: 2025년 7월 15일
<!-- v1.38 -->

![새로운 기능](../assets/new.svg) **기프트 카드 제품 유형**-카탈로그 상점 서비스가 이제 제품 특성을 JSON 개체 또는 배열로 지원하므로 기프트 카드와 같은 복잡한 유형을 유연하게 관리할 수 있습니다.<!--DATA-6573-->

+++이전 버전

### 2025년 6월

**릴리스 날짜**: 2025년 6월 20일
<!-- v1.37 -->

![새로 만들기](../assets/new.svg) **계층 구조의 가격 장부 구성**—부모-자식 가격 장부의 정확한 가격 범위입니다. 계산은 계층 및 상속된 규칙을 준수하며, 여러 가격 장부가 연결될 때 가격책정 오류를 줄입니다. Adobe Commerce Optimizer만 해당. [가격 장부](https://experienceleague.adobe.com/ko/docs/commerce/optimizer/setup/pricebooks)를 참조하세요.

![새로 만들기](../assets/new.svg) **대/소문자를 구분하지 않는 키**—쿼리의 키 조회는 이제 대/소문자를 구분하지 않으므로 키 대/소문자에서 오류가 줄어듭니다. <!--DATA-6494, DCAT-2495-->

**릴리스 날짜**: 2025년 6월 20일
<!-- v1.36 -->

![새로 만들기](../assets/new.svg) **카탈로그 Storefront에 대한 공용 IO 이벤트**—실시간 통합 및 가시성(CSS 및 EDS)을 위한 공용 IO 이벤트가 추가되었습니다.<!--DATA-6329-->

![새로 만들기](../assets/new.svg) **SSR(서버측 렌더링)**—대규모 카탈로그에서 향상된 성능, SEO 및 UX를 위해 SSR을 지원하는 아키텍처 개선.<!--DATA-6278, DATA-6280-->

![새로 만들기](../assets/new.svg) **인프라 및 보안**—이벤트 서비스에 대한 새 AWS 역할, ServiceNow 통합 및 CI/CD 파이프라인.

![새로 만들기](../assets/new.svg) **이벤트 형식 및 관찰 가능성**—페이로드 간소화, 모니터링 개선, 변형 이벤트 데이터 개선<!--DATA-6332, DATA-6402, -->

보안, 성능 및 안정성을 개선하기 위해 시스템 수준 및 인프라를 ![수정](../assets/fix.svg)합니다.<!--DATA-6404, DATA-6410, -->

**릴리스 날짜**: 2025년 6월 13일
<!-- v1.35 -->

![새로 만들기](../assets/new.svg) **캐시되지 않은 데이터 검색**-카탈로그 끝점에서 캐시되지 않은 데이터를 Search Service에 전달하려면 `Magento-Is-Preview` 헤더를 사용하도록 설정합니다.<!--DATA-6345-->

![새로 만들기](../assets/new.svg) **다중 선택 제품 옵션**-GraphQL API는 이제 제품 옵션에서 다중 선택을 허용하는지 여부를 표시합니다(예: 번들 &quot;여러 항목 선택&quot;).<!--DATA-6487-->

![새로 만들기](../assets/new.svg) 데이터 수집에 대한 가격 유효성 검사를 업데이트하여 가격 없는 제품을 지원합니다.<!--DATA-6098-->

![수정](../assets/fix.svg) Adobe Commerce Optimizer의 단순 번들 가격에 대한 오류 처리가 개선되었습니다.<!--DATA-6541-->

보안, 성능 및 안정성을 개선하기 위해 시스템 수준 및 인프라를 ![수정](../assets/fix.svg)합니다.<!--DATA-6273, DATA-6485, -->

### 2025년 4월

**릴리스 날짜**: 2025년 4월 8일
<!-- v1.34 -->

보안, 성능 및 안정성을 개선하기 위해 시스템 수준 및 인프라를 ![수정](../assets/fix.svg)합니다.<!--DATA-5732-->

<!-- v1.33 -->
![수정](../assets/fix.svg) 인프라는 이제 기존 워크로드에 영향을 주지 않고 매우 큰 카탈로그(최대 4억4천만 SKU)를 지원합니다.

### 2025년 3월

**릴리스 날짜**: 2025년 3월 28일
<!-- v1.32 -->

역할이 없는 ![Fix](../assets/fix.svg) 특성은 구성 가능한 카탈로그에 대해 더 이상 기본적으로 인덱싱되지 않으므로 인덱싱 시간이 향상되고 저장소가 줄어듭니다. 기능 플래그를 통해 레거시 동작을 다시 활성화할 수 있습니다.

![시스템 수준 및 인프라 개선 사항을 수정하여 보안, 성능 및 안정성을 개선합니다.](../assets/fix.svg)
<!--DATA-6348, DATA-6440, DATA-6446, DATA-6641-->

### 2025년 2월

**릴리스 날짜**: 2025년 2월 18일
<!-- v1.31 -->

보안, 성능 및 안정성을 개선하기 위해 시스템 수준 및 인프라를 ![수정](../assets/fix.svg)합니다.<!--DATA-6389, DATA-6367, DATA-6373-->

### 2024년 12월

**릴리스 날짜**: 2024년 12월 9일
<!-- v1.30 -->

주요 릴리스: 헤드리스 상점, 헤더 관리 및 제품 데이터 처리를 위한 [구성 가능한 카탈로그 데이터 모델](https://developer.adobe.com/commerce/services/optimizer/).

![새로 만들기](../assets/new.svg) **CCDM(Composable Catalog Data Model)** - 헤드리스 상점 앞면에 대해 composable 카탈로그를 사용하는 고객을 지원합니다. 새 끝점은 카탈로그 보기 및 정책 ID(이전 버전과 호환)를 수락합니다. 기본 제공 페이지 매김으로 제품 세부 사항 및 가격을 구성할 수 있습니다.<!--DATA-6018, DATA-6288-->

구성 가능한 카탈로그 API 작업을 위해 ![새](../assets/new.svg) **헤더 관리**-`AC-Locale` 이름이 `AC-Scope-Locale`(으)로 바뀌었습니다. 헤더 매핑 및 기본값이 지정되었습니다.<!--DATA-6303, DATA-6078-->

![새로운 기능](../assets/new.svg) **제품 데이터 및 가격 책정** 구성 가능한 카탈로그 데이터 모델을 지원하고 구성 가능한 제품에 대한 가격 처리를 개선했습니다.<!--DATA-6279-->

`CurrencyEnum`이(가) 페더레이션 논리에 맞춰 제품 검색 쿼리에 대해 `NONE`을(를) 지원하도록 업데이트되었습니다.<!--DATA-6285-->

![수정](../assets/fix.svg) **인프라 및 업그레이드**—보안, 성능 및 안정성을 위한 시스템 수준의 개선 사항입니다.

![수정](../assets/fix.svg) 번들 제품 옵션이 이제 사용 가능한 제품만 표시됩니다.<!--DATA-6347-->

**릴리스 날짜**: 2024년 12월 9일
<!-- v1.29 -->

![새로 만들기](../assets/new.svg) **제품 쿼리의 이미지 순서 지정**—이제 일관된 상점 및 API 동작을 위해 GraphQL `images` 필드의 제품 이미지가 카탈로그 내보내기 `sortOrder`을(를) 따릅니다.<!--DATA-6258-->

보안, 성능 및 안정성을 개선하기 위해 시스템 수준 및 인프라를 ![수정](../assets/fix.svg)합니다.<!--DATA-6619-->

**릴리스 날짜**: 2024년 12월
<!-- v1.28 -->

![시스템 수준 및 인프라 개선 사항을 수정하여 보안, 성능 및 안정성을 개선합니다.](../assets/fix.svg)
<!--DATA-6180, DATA-6230, DATA-6254, DATA-6257-->

### 2024년 10월

**릴리스 날짜**: 2024년 10월 22일
<!-- v1.26 -->

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새](../assets/new.svg) GraphQL 스키마에는 정확한 사이트 맵 및 검색 엔진 리인덱싱을 위한 제품 정보에 `lastModifiedAt`이(가) 포함됩니다(예: Google).
<!--DATA-6209-->

### 2024년 9월

**릴리스 날짜**: 2024년 9월 26일
<!-- v1.27 -->

![시스템 수준 및 인프라 개선 사항을 수정하여 보안, 성능 및 안정성을 개선합니다.](../assets/fix.svg)
<!--DATA-6243-->

### 2024년 8월

**릴리스 날짜**: 2024년 8월 22일
<!-- v1.23 -->

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![수정](../assets/fix.svg) 이제 제품 재정의(가격) 데이터 없이 제품 정보를 검색할 수 있습니다. 이전에는 다음 쿼리가 반환되었습니다. `The following sku does not have product override data in the DB: <SKU value>. Make sure data is synced.`
<!--DATA-6121-->

**릴리스 날짜**: 2024년 8월 13일
<!-- v1.22 -->

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새로 만들기](../assets/new.svg) 제품 SKU별로 모든 변형을 검색할 수 있는 지원이 추가되었습니다. [카탈로그 서비스 API 참조](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/)를 참조하세요.
<!--DATA-6067-->

### 2024년 5월

**릴리스 날짜**: 2024년 5월 23일
<!-- v1.19 -->

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상


![수정](../assets/fix.svg) 옵션 값에 대한 `InStock` 플래그는 이제 제품 변형의 범위 `enabled` 상태를 따릅니다.

<!--DATA-5033-->

![수정](../assets/fix.svg) 최대 16자리 및 소수점 4자리까지 제품 가격에 대한 지원이 추가되었습니다. 업데이트를 적용하려면 [데이터 관리 대시보드](https://experienceleague.adobe.com/ko/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard) 또는 [CLI](../data-export/data-export-cli-commands.md)에서 다시 동기화하십시오.
<!--DATA-5033-->

#### 알려진 제한 사항

다음 기능은 아직 지원되지 않습니다.

- 동적 특성 페이로드의 최대 크기는 9MB입니다.
- 그룹 제품 가격은 간단한 제품 가격으로 계산할 수 있습니다.
- 이미지 배열에서는 첫 번째 이미지만 역할을 포함합니다.

API Mesh 및 핵심 GraphQL API를 사용하여 다음을 수행할 수 있습니다.

- 최소 광고 가격
- 계층 가격
- 고정 가격으로 묶음 제품

자세한 내용과 예제는 [카탈로그 서비스 및 API Mesh](mesh.md)를 참조하세요.

### 2024년 4월

**릴리스 날짜**: 2024년 4월 11일
<!-- v1.18 -->

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새로 만들기](../assets/new.svg)에서 PHP 8.3에 대한 지원을 추가했습니다.

![새로 만들기](../assets/new.svg) [`products`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/) 및 [`refineProduct`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/refine-product/) 쿼리가 이제 단순 제품과 복합 제품 모두에 대해 사용자 지정 가능한 옵션 데이터를 반환합니다.<!--DATA-5538-->

### 2024년 2월

**릴리스 날짜**: 2024년 2월 22일
<!-- v1.17 -->

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새로 만들기](../assets/new.svg) 이제 [[!DNL Data Management Dashboard]](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard.html?lang=ko)을(를) 데이터 스트림(제품 권장 사항, 실시간 검색, 카탈로그 서비스)에 사용할 수 있습니다. `catalog-service`개의 메타패키지 v3.1.0+가 필요합니다.

**릴리스 날짜**: 2024년 2월 13일
<!-- v1.16 -->

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새](../assets/new.svg) 제품 비디오는 이제 카탈로그 서비스 API에서 지원됩니다.
이제 PDP 위젯에 ![수정](../assets/fix.svg) 품절 옵션이 표시됩니다.

#### 알려진 제한 사항

다음 기능은 아직 지원되지 않습니다.

- 동적 특성 페이로드의 최대 크기는 9MB입니다.
- 그룹 제품 가격. 이 값은 간단한 제품 가격으로 계산할 수 있다.
- 이미지 배열에서는 첫 번째 이미지만 역할을 포함합니다.

API Mesh 및 핵심 GraphQL API를 사용하여 다음을 수행할 수 있습니다.

- 최소 광고 가격
- [계층 가격](mesh.md)

### 2023년 10월

**릴리스 날짜**: 2023년 10월 12일
<!-- v1.13 -->

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새](../assets/new.svg) 카탈로그 서비스는 제품 변형에 대해 `inStock` 플래그를 지원합니다.
![새로 만들기](../assets/new.svg) `urlKey` 및 `externalId` 필드가 GraphQL 스키마에 추가되었습니다.
이제 ![새로운](../assets/new.svg) 다운로드 가능한 제품 및 기프트 카드가 지원됩니다.

### 2023년 9월

**릴리스 날짜**: 2023년 9월 19일
<!-- v1.12 -->

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새](../assets/new.svg) 카탈로그 서비스가 이제 [SaaS 가격 인덱싱](../price-index/price-indexing.md)를 사용합니다.
![수정](../assets/fix.svg) 이 릴리스에는 서비스 측의 버그 수정 및 개선 사항이 포함되어 있습니다.

### 2023년 7월

**릴리스 날짜**: 2023년 7월 18일
<!-- v1.11 -->

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새](../assets/new.svg) 카탈로그 서비스가 이제 제품 권장 사항에 대한 [`recommendations`](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/) GraphQL 쿼리를 지원합니다.

### 2023년 6월

**릴리스 날짜**: 2023년 6월 27일
<!-- v1.10 -->

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새로 만들기](../assets/new.svg) 이제 카탈로그 서비스 API가 `related products`을(를) 지원합니다.

### 2023년 4월

**릴리스 날짜**: 2023년 4월 12일
<!-- v1.7 -->

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새](../assets/new.svg) 카탈로그 서비스가 삭제된 제품 변형을 정리합니다.
![인프라 확장성 및 성능 개선 사항](../assets/fix.svg).

### 2023년 3월

**릴리스 날짜**: 2023년 3월 28일
<!-- v1.6 -->

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새로 만들기](../assets/new.svg) [`products`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/) 쿼리에 견본을 추가했습니다.
![새로 만들기](../assets/new.svg)에서 [API Mesh](mesh.md)를 사용하여 `entityId`을(를) 가져오는 기능을 추가했습니다.

**릴리스 날짜**: 2023년 3월 6일
<!-- v1.5 -->

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새로 만들기](../assets/new.svg)에 [`categories`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/) GraphQL 기능이 추가되었습니다.
![수정](../assets/fix.svg) 향상된 성능과 API 확장성.

### 2023년 2월

**릴리스 날짜**: 2023년 2월 7일
<!-- v1.4 -->

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.x 이상

![새로 만들기](../assets/new.svg) 카탈로그 서비스 메타패키지를 게시하여 설치 단계를 간소화했습니다.
![수정](../assets/fix.svg) API 확장성 및 성능 개선 사항.

### 2023년 1월

**릴리스 날짜**: 2023년 1월 17일
<!-- v1.3 -->

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.x 이상

![새로 만들기](../assets/new.svg) 온보딩 환경을 간소화하고 개선했습니다.
![신규](../assets/new.svg) 새 고객 샌드박스 엔드포인트를 사전 프로덕션 테스트에 사용할 수 있습니다.
가상 제품에 대한 ![새로운](../assets/new.svg) 지원이 추가되었습니다.
![수정](../assets/fix.svg) API 확장성 및 성능 개선 사항.

### 2022년 11월

**릴리스 날짜**: 2022년 11월 18일
<!-- v1.1 -->

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.x 이상

![새](../assets/new.svg) 카탈로그 서비스가 이제 Adobe의 [API Mesh](https://developer.adobe.com/graphql-mesh-gateway/)를 지원합니다.
![수정](../assets/fix.svg) API 확장성과 전체 성능이 개선되었습니다.

### 2022년 10월

**릴리스 날짜**: 2022년 10월 4일
<!-- v1.0 -->

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.x 이상

번들 및 그룹화된 제품에 대한 ![새로운](../assets/new.svg) 지원
![새로 추가](../assets/new.svg) B2B 가시성 재정의를 추가했습니다. 이제 제품을 검색할 수 있으며 특정 고객 그룹을 위해 장바구니에 추가할 수 있습니다.
![수정](../assets/fix.svg) 서비스가 이제 안정적이며 성능이 향상되었습니다.

### 2022년 9월

**릴리스 날짜**: 2022년 9월 12일
<!-- v0.3 -->

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.x 이상

![새](../assets/new.svg) 변형 이미지: 선택한 옵션에 따라 제품 이미지가 반환되었습니다.
![신규](../assets/new.svg) 가격 역할: 특정 고객 그룹의 구성원만 제품 가격을 볼 수 있습니다.
![수정](../assets/fix.svg) 서비스의 안정성과 성능이 개선되었습니다.
카탈로그에서 제품이 삭제되면 ![새](../assets/new.svg) 업데이트가 수신됩니다.

### 2022년 8월

**릴리스 날짜**: 2022년 8월 9일
<!-- Beta -->

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.x 이상

![새로 만들기](../assets/new.svg) `products` 및 `refineProduct` 쿼리가 다음 데이터를 반환합니다.

- 사전 정의된(시스템) 제품 속성.
- 동적 제품 속성을 확인하고 역할별로 필터링합니다(제품 표시 페이지/제품 목록 페이지).
- 제품 옵션.
- 제품 이미지를 만들고 역할(PDP/PLP)별로 필터링합니다.
- 간단한 제품에 대한 특정 가격 및 구성 가능한 제품에 대한 가격 범위입니다.
- 고객 그룹 가격 및 가격 범위. 고객 그룹이 없는 쇼핑객에 대해 대체 기본 가격을 반환합니다.
- B2B 고객별 가격을 사용하는 제품 유형입니다.

+++

## 카탈로그 서비스 메타패키지

카탈로그 서비스 PHP 메타패키지(`magento/catalog-service`)를 업데이트합니다.

- Adobe Commerce as a Cloud Service 고객의 경우 최신 버전이 환경에 설치됩니다.

- 클라우드 또는 온프레미스의 Adobe Commerce에서는 Composer를 사용하여 클라우드 환경의 카탈로그 서비스 메타패키지를 최신 릴리스로 업그레이드하는 것이 좋습니다.

### v3.4.0 릴리스

**릴리스 날짜**: 2026년 6월 8일

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새로 만들기](../assets/new.svg) **데이터 피드 동기화 상태 모니터링 지원**—데이터 내보내기 상태 확장(`magento/module-data-exporter-status`)을 포함하도록 카탈로그 서비스 메타패키지 종속성을 업데이트했습니다. 이렇게 하면 추가 설치 또는 구성 단계를 수행하지 않고도 Commerce 관리자의 [데이터 피드 동기화 상태 모니터링](https://experienceleague.adobe.com/ko/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status)을 사용할 수 있습니다

![새로 만들기](../assets/new.svg) 카탈로그 서비스와 Commerce 스택 간의 호환성을 유지하기 위해 종속성이 업데이트되었습니다.

### v3.3.0 릴리스

**릴리스 날짜**: 2025년 10월 14일

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새로 만들기](../assets/new.svg) **데이터 서비스 업그레이드**—`magento/data-services` 종속성이 ^8.0.0으로 업데이트되었습니다. 업그레이드하기 전에 8.x 호환성에 대한 환경 및 사용자 지정 데이터 서비스 API 사용을 확인하십시오.

![새로 만들기](../assets/new.svg) 3.3.0 릴리스에 대한 버전 및 메타데이터를 업데이트했습니다.

### v3.2.0 릴리스

**릴리스 날짜**: 2024년 4월 12일

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새](../assets/new.svg) 버전 및 메타데이터가 3.2.0용으로 업데이트되었습니다. 다른 종속성 변경 사항은 없습니다.

### v3.1.0 릴리스

**릴리스 날짜**: 2024년 1월 26일

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새로 만들기](../assets/new.svg) 새 패키지 종속성 추가:

- 카탈로그 서비스에서 사용하는 범주 권한 데이터를 내보내기 위한 **범주 권한 데이터 내보내기**(`magento/module-category-permission-data-exporter`).
- 카탈로그 동기화와 관련된 관리 UI 및 구성에 대한 **카탈로그 동기화 관리자** `magento/module-catalog-sync-admin`.

![새로 만들기](../assets/new.svg) 버전 및 3.1.0 릴리스의 메타데이터를 업데이트했습니다.

## 카탈로그 서비스 설치 관리자

설치 관리자는 카탈로그 서비스 확장과 함께 제공되며 카탈로그 서비스가 Commerce 스택과 일치하도록 설치 및 환경 검사를 처리합니다.

- **Adobe Commerce as a Cloud Service** 고객의 경우 최신 설치 관리자 버전이 환경에 설치되어 있습니다.

- **클라우드 인프라의 Adobe Commerce** 또는 **온프레미스**&#x200B;의 경우 설치 관리자를 [카탈로그 서비스 메타패키지](#catalog-service-metapackage)와(과) 정렬하세요.

Composer를 사용하여 `magento/catalog-service`을(를) 업그레이드할 때마다 설치 관리자 패키지가 최신 버전으로 자동 업데이트됩니다. 이 릴리스 정보에서 필요한 변경 사항(예: 새 PHP 버전 지원)을 설명할 때 작성기를 사용하여 `magento/catalog-service-installer`을(를) 별도로 업그레이드할 수도 있습니다. 이렇게 하면 실행 중인 카탈로그 서비스 버전과 설치 도구가 호환됩니다.

### v1.0.6 릴리스

**릴리스 날짜**: 2026년 3월 25일

![새로 만들기](../assets/new.svg) **PHP 8.5**—카탈로그 서비스가 PHP 8.5에서 작동할 때 호환성을 보장합니다.

## 관련 설명서

- **Adobe Commerce on cloud, 온프레미스 또는 Adobe Commerce as a Cloud Service에 배포된 프로젝트의 경우 다음 설명서를 참조하십시오.

   - [카탈로그 서비스 안내서](overview.md)
   - [카탈로그 서비스 GraphQL API 참조](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/)
   - [Adobe Commerce 관리 안내서](https://experienceleague.adobe.com/en/docs/commerce-admin/)
   - [Adobe Commerce as a Cloud Service 안내서](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/)
   - [Adobe Commerce on Cloud 안내서](https://experienceleague.adobe.com/en/docs/commerce-cloud/)

- **Adobe Commerce Optimizer** 또는 **Adobe Commerce Optimizer 커넥터**&#x200B;를 사용하는 프로젝트의 경우 다음 설명서를 참조하십시오.

   - [머천다이징 서비스 개발자 안내서](https://developer.adobe.com/commerce/services/optimizer/)
   - [머천다이징 GraphQL API 참조](https://developer.adobe.com/commerce/services/reference/graphql/)
   - [Adobe Commerce Optimizer 안내서](../optimizer/overview.md)
