---
title: 경계 및 제한
description: 비즈니스 요구 사항을 충족하도록  [!DNL Live Search] 의 경계 및 제한에 대해 알아봅니다.
role: Admin, Developer
exl-id: 28b8d98f-0784-4c4d-b382-81c01838e0de
source-git-commit: bcddbb71b3c34701c7fb47a4ccc738b1f036c070
workflow-type: tm+mt
source-wordcount: '1104'
ht-degree: 0%

---

# 경계 및 제한

사이트 검색과 관련하여 Adobe Commerce은 옵션을 제공합니다. [!DNL Live Search]과(와) [!DNL Catalog Service]이(가) 귀하의 비즈니스 요구 사항을 충족하는지 확인하려면 다음 경계 및 제한을 검토하십시오. 콘텐츠 검색, BYOA(bring-your-own-algorithm) 또는 속성 기반 머천다이징과 같은 고급 검색 기능이 필요한 경우 서드파티 검색 솔루션을 고려하십시오.

## 일반

- [이(가) 설치되어 있고 상점 바닥글의 고급 검색 링크가 제거되면 &#x200B;](https://experienceleague.adobe.com/ko/docs/commerce-admin/catalog/catalog/search/search)고급 검색[!DNL Live Search] 모듈이 비활성화됩니다.
- [&#x200B; 필드 및 제품 목록 페이지 위젯에서는 &#x200B;](https://experienceleague.adobe.com/ko/docs/commerce-admin/catalog/products/pricing/product-price-tier)계층 가격 책정[!DNL Live Search]이 지원되지 않습니다.
- 제품 가격에는 부가가치세(VAT)가 포함되어 있지만 [!DNL Live Search]에서는 VAT를 별도의 값으로 표시할 수 없습니다.
- 컨텐츠 검색(CMS 페이지 및 블록)은 지원되지 않습니다.
- 페이지 번호를 지정할 수 있는 최대 결과 수는 10,000개입니다. 카테고리 또는 검색 결과에 많은 수의 제품이 포함되어 있는 경우 쇼핑객이 페이지 매김을 사용할 필요가 없도록 하려면 제품을 필터링할 수 있는 의미 있는 방법을 제공하십시오.
- 설명 및 사용자 지정 속성을 포함하여 속성당 1MB의 하드 제한이 있습니다.
- 검색 어댑터는 사용자 지정 소스 모델로 만들어져 패싯으로 사용되는 제품 속성을 지원하지 않습니다. 이 기능을 지원하려면 [제품 목록 페이지 위젯](plp-styling.md)을 사용해야 합니다.
- 검색 어댑터는 라이브 검색 4.0.0부터 더 이상 사용되지 않습니다.
- 사용자 지정 제품 유형은 지원되지 않습니다.
- `"is_user_defined": false`을(를) 사용하여 프로그래밍 방식으로 만든 사용자 지정 특성은 지원되지 않습니다.
- [개발자 설명서](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#limitations)에 설명된 대로 일부 제한 사항이 있는 &quot;다음으로 시작&quot; 또는 &quot;포함&quot; 조건을 사용하여 결과를 필터링할 수 있습니다.
- 지난 해 내에서만 성과 지표를 추적할 수 있습니다.
- 검색 쿼리에 여러 단어가 포함되어 있는 경우 단어 사이에 공백이 있으면 해당 단어가 별도의 검색어로 처리됩니다. 여러 단어 검색 쿼리를 처리하려면 [동의어](./synonyms.md)를 사용하십시오.
- [!DNL Live Search]은(는) 기본적으로 [검색어 리디렉션](https://experienceleague.adobe.com/ko/docs/commerce-admin/catalog/catalog/search/search-terms)을 지원하지 않습니다. Fastly 또는 다른 사용자 지정 구성을 사용하여 리디렉션을 구현합니다.

## 색인화

- 스토어 보기당 최대 총 450개의 제품 특성을 [!DNL Live Search] [인덱스](indexing.md). 이는 다음과 같이 배포됩니다.
   - 정렬 가능한 속성 50개
   - 필터링 가능한 특성 200개
   - 검색 가능한 속성 200개
- [!DNL Live Search]은(는) Adobe Commerce 데이터베이스의 제품만 인덱싱합니다.
- CMS 페이지는 색인화되지 않습니다.
- SKU, 이름 및 카테고리 속성은 기본적으로 검색할 수 있으며 검색에서 제외할 수 없습니다. 해당 범주에 포함시키려는 제품이 아닌 경우 해당 범주에서 제품 할당을 취소해야 합니다.

## 패싯

- 정의된 필터링 가능한 속성 집합에서 최대 100개의 속성을 패싯으로 구성할 수 있습니다.
- Facet 내에서 최대 100개의 버킷이 반환될 수 있습니다. 100개가 넘는 버킷을 반환해야 하는 경우 [지원 티켓을 만드십시오](https://experienceleague.adobe.com/ko/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide). 그러면 Adobe에서 성능에 대한 영향을 분석하고 환경에 대한 이 제한을 늘릴 수 있는지 확인할 수 있습니다.
- 동적 패싯은 큰 인덱스와 순서가 높은 인덱스에서 성능 문제를 일으킬 수 있습니다. 동적 패싯을 만들어 성능 저하 또는 페이지가 시간 초과 오류와 함께 로드되지 않은 것을 발견한 경우 패싯을 고정으로 변경하여 성능 문제가 해결되는지 확인하십시오.
- 재고 상태(`quantity_and_stock_status`)는 패싯으로 지원되지 않습니다. `inStock: 'true'`을(를) 사용하여 재고 제품을 필터링할 수 있습니다. 이는 `LiveSearchAdapter` 관리자의 &quot;재고 부족 제품 표시&quot;가 &quot;True&quot;로 설정된 경우 [!DNL Commerce] 모듈에서 즉시 지원됩니다.
- 날짜 유형 속성은 패싯으로 지원되지 않습니다.
- 해당 속성이 Facet으로 추가된 후 속성 메타데이터에 수행된 모든 변경 사항은 Facet에 반영되지 않습니다.
- 최대 50개의 정렬 가능한 속성과 200개의 검색 가능한 속성을 가질 수 있습니다.

## 쿼리

- [!DNL Live Search]은(는) 쿼리에 대해 고유한 [GraphQL 끝점](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/)을 사용하여 동적 팩팅 및 귀하가 입력한 대로 검색과 같은 기능을 지원합니다. [GraphQL API](https://developer.adobe.com/commerce/webapi/graphql/)와 비슷하지만 몇 가지 차이점이 있으며 일부 필드가 완전히 호환되지 않을 수 있습니다.
- 검색 쿼리에서 반환할 수 있는 최대 결과 수는 10,000개입니다.
- 페이지당 최대 결과 수는 500개입니다.
- 날짜 유형 특성을 사용하여 결과를 필터링할 수 없습니다.

## 머천다이징 검색

- 스토어 보기당 최대 검색 머천다이징 [규칙](rules.md) 수는 50개입니다.
- 규칙당 최대 조건 수는 10개입니다.
- 규칙당 최대 이벤트 수는 25개입니다.
- 기본 정렬 순서 &quot;정렬 기준: 가장 관련성&quot;을 선택하면 규칙 및 수동 등급 제품이 검색 결과에 적용됩니다. 쇼핑객이 정렬 순서를 이름별 또는 가격별 정렬과 같이 변경하는 경우, 규칙 및 수동 순위는 더 이상 적용되지 않습니다.
- 페이지가 매겨진 응답에서 예측할 수 없는 결과를 방지하려면 고정된 제품의 수가 요청된 페이지 크기를 초과하지 않아야 합니다.

## 동의어

- [!DNL Live Search]은(는) 스토어 보기당 최대 200개의 [동의어](synonyms.md)를 관리할 수 있습니다.

## 카테고리 머천다이징

- 각 스토어 보기에 대해 카테고리당 하나의 규칙을 만들 수 있습니다.
- 규칙당 최대 조건 수는 10개입니다.
- 규칙당 최대 이벤트 수는 25개입니다.
- 특정 카테고리가 상점 첫 화면에서 열리고 해당 카테고리에 대한 규칙이 있는 경우 규칙이 적용됩니다. 카테고리 머천다이징 규칙의 경우 기본 정렬 순서는 &quot;정렬 기준: 위치&quot;입니다. 쇼핑객이 정렬 순서를 변경하면 모든 숨겨진 제품, 고정된 제품 및 숨겨진 제품이 더 이상 정렬되지 않습니다.

## B2B 및 범주 권한

- 기본 공유 카탈로그에 추가되지 않은 제품은 표시되지 않습니다.
- [범주 권한](https://experienceleague.adobe.com/ko/docs/commerce-admin/catalog/categories/category-permissions)을 사용하여 고객 그룹을 제한하려면 다음을 수행하십시오.
   - 제품을 루트 범주에 할당해야 합니다. (**참고:** SaaS 데이터 내보내기 확장을 버전 103.4.0+로 업데이트하여 이 제한을 제거할 수 있습니다. [데이터 내보내기 확장 관리](../data-export/manage-extension.md)를 참조하십시오.
   - &quot;로그인되지 않은&quot; 고객 그룹에는 &quot;허용&quot; 검색 권한이 부여되어야 합니다.
   - 제품을 &quot;로그인되지 않음&quot; 고객 그룹으로 제한하려면 각 범주로 이동하여 각 [고객 그룹](https://experienceleague.adobe.com/ko/docs/commerce-admin/b2b/shared-catalogs/catalog-shared-manage)에 대한 권한을 설정합니다.
- PWA Studio에서 PLP 위젯을 사용하는 B2B에 대한 기본 지원은 현재 지원되지 않습니다. 그러나 [API를 사용](install.md#pwa-support)하여 이 기능을 구현할 수 있습니다.
- [!DNL Live Search]의 범주 패싯에 특정 [고객 그룹](https://experienceleague.adobe.com/ko/docs/commerce-admin/b2b/shared-catalogs/catalog-shared-manage)에 표시할 수 없는 범주가 표시될 수 있습니다.
- [!DNL Live Search]에서는 최대 1,000개의 고객 그룹을 지원할 수 있습니다.

## [!DNL Storefront popover]

- [[!DNL popover]](storefront-popover.md)은(는) *Luma* 테마 또는 *Luma*&#x200B;을(를) 기반으로 하는 사용자 지정된 테마를 사용하는 스토어에만 사용할 수 있습니다. 검색 결과 페이지의 탐색 표시에는 *Luma* 스타일이 없습니다.
- [!DNL popover]은(는) *Blank* 테마를 지원하지 않습니다.
- [!DNL popover]은(는) 빠른 주문 양식에서 지원되지 않습니다.
- 위시리스트 및 제품 비교는 지원되지 않습니다.
- 페루 솔(PEN)의 통화 기호는 지원되지 않습니다.

## 문제 해결

[!DNL Live Search]의 몇 가지 일반적인 문제를 해결하는 데 대한 도움말을 보려면 다음 기술 자료를 참조하십시오.

- [[!DNL Live Search] 카탈로그가 동기화되지 않음](https://experienceleague.adobe.com/ko/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/live-search-catalog-data-sync)
- [[!DNL Live Search] 대시보드 및 검색 결과 순위가 잘못됨](https://experienceleague.adobe.com/ko/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/live-search-dashboard-ranking-incorrect)
- [[!DNL Live Search] 관리자의 재고 상태 설정에 관계없이 품절 제품을 표시합니다](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/live-search-displays-out-of-stock-products)
- [[!DNL Live Search] 패싯이 알파벳순으로 정렬되지 않음](https://experienceleague.adobe.com/ko/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/live-search-facets-not-sorted)

추가 지원이 필요한 경우 [지원](https://experienceleague.adobe.com/ko/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide)에 문의하십시오.
