---
title: '[!DNL Live Search] 릴리스 정보'
description: Adobe Commerce의  [!DNL Live Search] 에 대한 최신 릴리스 정보입니다.
feature: Services, Search, Release Notes
exl-id: 099cf79c-968c-4381-b66d-7f6141ad2db3
source-git-commit: a7fecafe005c68c58a3491a2aad206d16d6d621b
workflow-type: tm+mt
source-wordcount: '2577'
ht-degree: 0%

---

# [!DNL Live Search] 릴리스 정보

이 릴리스 노트는 [!DNL Live Search]의 최신 버전에 대해 설명합니다.
현재 주요 릴리스 버전에 대한 지원이 제공됩니다. 이전 버전에 대한 릴리스 노트는 참조를 위해 제공됩니다.
업데이트에는 다음이 포함됩니다.

새 기능 ![개](../assets/new.svg)개
![수정](../assets/fix.svg) 수정 사항 및 개선 사항
![버그](../assets/bug.svg) 알려진 문제

## 호스팅된 서비스 업데이트

이 참고 사항에서는 버전 관리된 릴리스 외부에 게시된 업데이트 또는 호스팅된 서비스에 대한 개선 사항에 대해 설명합니다.

_2025년 4월 29일_

![수정](../assets/fix.svg) **성능** 탭의 [**CSV로 내보내기**](./performance.md) 보고서에 날짜 범위에 지정된 모든 데이터가 포함되지 않는 문제를 해결했습니다.
![수정](../assets/fix.svg) 검색 쿼리 필터를 사용한 경우 [머천다이징 규칙](./rules.md)을 저장할 수 없는 문제를 해결했습니다.
![수정](../assets/fix.svg) [고정된 제품](./facets-manage.md#pinunpin-facet)이 결과 페이지의 맨 위에 나열되지 않는 문제를 해결했습니다.

_2025년 4월 21일_

![수정](../assets/fix.svg) 상위 범위와 동일한 제품이 결과에 포함되지 않도록 가격에 대한 범위 필터의 문제를 해결했습니다. 이 변경 사항은 패싯에 대해 가격 범위를 정의하는 방식에 맞춰 조정됩니다.

_2025년 4월 3일_

![수정](../assets/fix.svg) B2B 판매자에 대해 &quot;제품이 루트 범주에 할당되어야 합니다&quot; [제한](boundaries-limits.md#b2b-and-category-permissions)을(를) 제거하기 위해 SaaS 데이터 내보내기 확장 프로그램을 업데이트했습니다. SaaS 데이터 내보내기 확장을 버전 103.4.0+로 업데이트하는 방법은 [데이터 내보내기 확장 관리](../data-export/manage-extension.md)를 참조하십시오.

_2025년 2월 20일_

![새로 만들기](../assets/new.svg) Commerce에서 여러 단어 동의어를 지원합니다. [자세히 알아보기](synonyms-type.md#multi-word-synonym-behavior). 다중 단어 동의어에 대한 지원은 2월 20일 릴리스일 이후에만 가능합니다. 기존의 여러 단어 동의어가 작동하려면 전체 색인 재지정이 필요합니다. [지원 티켓을 만드는 중](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide)에 요청할 수 있습니다.

_2025년 1월 31일_

![새로 만들기](../assets/new.svg) 테스트 환경에서 쿼리되지 않은 카탈로그 데이터에 대한 새 데이터 보존 정책이 있습니다. [자세히 알아보기](overview.md#catalog-data-retention-policy)

_2024년 9월 19일_

![새로 만들기](../assets/new.svg) 계층화, 다음으로 시작, 포함 등 세 가지 새로운 검색 기능을 지원하는 베타 버전을 릴리스했습니다. [자세히 알아보기](install.md#install-the-live-search-beta)

_2024년 9월 4일_

![수정](../assets/fix.svg) 패싯 내에서 [반환할 수 있는 최대 버킷 수를 늘렸습니다](boundaries-limits.md#facets).

_2024년 8월 7일_

![수정](../assets/fix.svg) [가격 팩팅](settings.md#price-faceting)의 최대 간격 값 또는 가격 범위를 10,000에서 40,000,000으로 늘렸습니다.

_2024년 2월 13일_

![새로 만들기](../assets/new.svg) [!DNL Live Search]은(는) 이제 [머천다이징 검색](rules.md)에 대한 기본 규칙 설정을 지원합니다.

_2023년 10월 12일_

![새](../assets/new.svg) Commerce 관리자는 이제 [!DNL Live Search]에 대한 인덱스의 언어를 지정할 수 있습니다. [설정](settings.md)을 참조하세요.
![수정](../assets/fix.svg) &quot;검색 규칙&quot; 탭의 이름이 &quot;머천다이징 검색&quot;으로 변경되었습니다.

_2023년 6월 13일_

![수정](../assets/fix.svg) 따옴표나 아포스트로피와 같은 일부 문자로 인해 순위 문제가 발생하는 문제를 해결했습니다. 리인덱싱하면 이러한 문제가 해결됩니다.

_2023년 4월 25일_

![신규](../assets/new.svg) [!DNL Live Search] 고객이 이제 새로운 [SaaS 가격 인덱서](../price-index/price-indexing.md)를 이용할 수 있습니다.

### PLP 위젯

_2025년 5월 22일_

![수정](../assets/fix.svg) 로케일이 프랑스어, 독일어, 이탈리아어 또는 스페인어로 변경되었을 때 장바구니에 추가 단추가 영어로 유지되던 문제를 해결했습니다.
![수정](../assets/fix.svg) 품절 제품에 대해 장바구니에 추가 단추가 표시되는 문제를 해결했습니다.

_2024년 5월 31일_

다음 기능에 대한 지원을 추가하는 PLP 위젯의 ![새로운](../assets/new.svg) 버전 2.0.0이 릴리스되었습니다.

- 장바구니에 추가 버튼 - 간단한 제품에만 사용할 수 있습니다.
- 제품당 여러 이미지 - 구성 가능한 제품에 대해 다른 색상을 선택하면 이미지가 변경될 수 있습니다.

_2023년 10월 27일_

![새로 만들기](../assets/new.svg) 이제 [!DNL Live Search] PLP 위젯에서 색상 견본을 지원합니다.

## [!DNL Live Search] 4.5.0

_2025년 9월 5일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새](../assets/new.svg) Live Search는 이제 제한을 사용하도록 설정할 때 쿠키/로컬 저장소에 데이터 수집 및 저장을 금지하여 [쿠키 제한 모드](install.md#cookies)를 완전히 준수합니다.

## [!DNL Live Search] 4.4.1

_2025년 8월 11일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

샌드박스 환경에 대한 ![수정](../assets/fix.svg) 카탈로그 서비스 끝점을 수정했습니다.

## [!DNL Live Search] 4.4.0

_2025년 7월 14일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새로 만들기](../assets/new.svg) [가격 그룹화](./settings.md#price-faceting) 제한을 50개에서 100개로 늘렸습니다.

## [!DNL Live Search] 4.3.0

_2025년 3월 11일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![수정](../assets/fix.svg) [!DNL Live Search]은(는) 이제 Adobe Commerce 2.4.8-beta2를 실행하는 설치에서 PHP 8.4를 지원합니다.
![수정](../assets/fix.svg) 검색 어댑터가 `psr/http-message:2.0`과(와) 호환되지 않는 문제를 해결했습니다.

## [!DNL Live Search] 4.2.3

_2025년 2월 13일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![수정](../assets/fix.svg) 주문 세부 사항 페이지에 주문 번호, 날짜 및 **[!UICONTROL Reorder]** 단추가 없는 문제를 해결했습니다.

## [!DNL Live Search] 4.2.2

_2025년 1월 6일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![수정](../assets/fix.svg) Adobe Commerce 버전 2.4.5 및 이전 버전에서 `categoryList` GraphqL 쿼리에 오류가 발생하는 문제를 해결했습니다.

## [!DNL Live Search] 4.2.1

_2024년 7월 31일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![수정](../assets/fix.svg) 특정 스크립트가 체크아웃 페이지에서 로드되지 않는 문제를 해결했습니다.
![수정](../assets/fix.svg) `composer.json` 파일에서 종속성 버전을 수정했습니다.

## [!DNL Live Search] 4.2.0

_2024년 5월 31일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새로 만들기](../assets/new.svg) PLP 위젯 버전 2.0.0을 사용하도록 라이브 검색 확장 기능이 업데이트되었습니다.

## [!DNL Live Search] 4.1.2

_2024년 5월 16일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

### 업데이트

![수정](../assets/fix.svg) 범주의 [`productSearch` 및 ](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#filtering-by-categories)을(를) 기반으로 올바르게 필터링하도록 `categoryPath``categoryList` GraphQL 쿼리를 수정했습니다.

## [!DNL Live Search] 4.1.1

_2024년 3월 19일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

### 새로운 기능

![새로 만들기](../assets/new.svg) 폴란드에 대한 언어 지원을 추가했습니다.
![새로 만들기](../assets/new.svg) [!DNL Live Search]은(는) 이제 Adobe Commerce 2.4.4를 실행하는 설치에서 PHP 8.3을 지원합니다.

## [!DNL Live Search] 4.1.0

_2024년 2월 22일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

### 새로운 기능

![새로 만들기](../assets/new.svg) 이제 [[!DNL Data Management Dashboard]](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard)을(를) 사용할 수 있습니다. 이렇게 개조된 대시보드는 [!DNL Product Recommendations], [!DNL Live Search] 및 [!DNL Catalog Service]의 데이터 스트림에 대한 통찰력을 제공합니다.

### 업데이트

![수정](../assets/fix.svg) 게스트 사용자가 기본이 아닌 스토어 보기에서 장바구니에 제품을 추가할 때 오류가 발생하는 문제를 해결했습니다.
![수정](../assets/fix.svg) 로케일 설정에 관계없이 검색 팝오버에 항상 가격 값 앞에 통화 기호가 표시되는 문제를 해결했습니다.
![수정](../assets/fix.svg) 설치 시 호환성 문제를 해결하기 위해 비활성화된 핵심 플러그인에 대한 불필요한 형식 정의를 제거했습니다.

## [!DNL Live Search] 4.0.0

_2023년 11월 13일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

### 새로운 기능

![새로 만들기](../assets/new.svg) [!DNL Live Search]은(는) 이제 PLP 위젯에서 색상 견본을 지원합니다.
이제 ![새로 만들기](../assets/new.svg) [!DNL Live Search]에 범주 ID가 아닌 범주 이름이 표시됩니다.
![신규](../assets/new.svg) [!DNL Live Search]은(는) 이제 PLP 위젯에서 취소선 가격을 지원합니다.
![새로 만들기](../assets/new.svg) 필터 패널을 숨기기 위해 &quot;필터 숨기기&quot; 단추를 도입했습니다.


### 업데이트

![수정](../assets/fix.svg) 이제 새 설치에 대해 [!DNL Live Search] PLP 위젯이 기본적으로 활성화됩니다.
![수정](../assets/fix.svg) 검색 어댑터가 더 이상 사용되지 않습니다. 앞으로는 보안 문제를 해결하기 위해 검색 어댑터만 업데이트됩니다.
![수정](../assets/fix.svg) 위젯 클래스를 더 잘 격리하도록 CSS 스타일을 다시 구성했습니다.
![수정](../assets/fix.svg) 사소한 버그 수정

버전 3.1.1 이상을 설치한 후 새 인덱서를 활성화합니다.

- 제품 가격 피드
- 범위 웹 사이트 데이터 피드
- 고객 그룹 데이터 피드 범위 지정

업그레이드 후 변경 사항을 프로덕션에 푸시하기 전에 QA 또는 스테이징에서 업데이트된 구성을 테스트하십시오.

+++3.1.1 및 이전

### [!DNL Live Search] 3.1.1

_2023년 9월 15일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새로 만들기](../assets/new.svg) 새 범주 머천다이징 탭이 추가되었습니다. 이제 카테고리당 지능형 순위 및 수동 순위(고정, 증폭, 파기, 숨기기)를 추가할 수 있습니다.
![신규](../assets/new.svg) 사용자는 지능적 또는 수동 등급으로 하나의 범주 규칙을 추가할 수 있습니다.
![신규](../assets/new.svg) 사용자는 이제 지능형 등급 규칙을 하위 범주에 추가할 수 있습니다.
![새로 만들기](../assets/new.svg) 지능형 순위가 있는 하위 범주를 삭제할 때 자세한 정보가 제공됩니다
![새로 만들기](../assets/new.svg) 상속된 순위 전략에 대한 규칙을 삭제하는 기능을 추가했습니다.
![새로 만들기](../assets/new.svg) 단일 범주에 대한 규칙을 삭제하는 기능을 추가했습니다.
![새](../assets/new.svg) 사용자는 이제 규칙을 추가할 때 범주 이름으로 검색할 수 있습니다.
![새로 만들기](../assets/new.svg) 이제 범주 트리 보기를 사용하여 규칙이 적용된 범주를 볼 수 있습니다.
![새로 만들기](../assets/new.svg) 범주 미리 보기에는 선택한 범주만 표시됩니다.
![새로 만들기](../assets/new.svg) AEM CIF [팝오버 위젯](https://github.com/adobe/aem-cif-guides-venia/pull/319) 및 [PLP 위젯](https://github.com/adobe/aem-cif-guides-venia/pull/320) 구성 요소를 통해 AEM 사이트에서 [!DNL Live Search]을(를) 활용할 수 있습니다.

#### 업데이트

![수정](../assets/fix.svg) 제품 및 가격 피드의 테이블 크기가 크게 줄었습니다. 표 `catalog_data_exporter_products` 및 `catalog_data_exporter_product_prices`에 크기가 상당히 감소해야 합니다.
![수정](../assets/fix.svg) &#39;규칙&#39; 탭의 이름이 &#39;검색 규칙&#39;으로 바뀝니다.
![수정](../assets/fix.svg) &#39;트렌드&#39;로 순위를 매길 때 이제 다음 중 하나를 선택할 수 있습니다.
- 3일(기본값)
- 14일
- 30일
![수정](../assets/fix.svg) &#39;이벤트&#39;(증폭/고정/저장/숨기기)의 이름이 &#39;수동 순위&#39;로 변경되었습니다.
![수정](../assets/fix.svg) &#39;순위 유형&#39;의 이름이 &#39;지능형 순위&#39;로 변경되었습니다.
![수정](../assets/fix.svg)작은 버그 수정

### [!DNL Live Search] 3.1.0

_2023년 9월 1일_

[!BADGE 지원됨]{type="Informative" tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

#### 업데이트

![수정](../assets/fix.svg) 제품 목록 위젯이 [카탈로그 서비스 API](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/)를 사용하도록 업데이트되었습니다.

### [!DNL Live Search] 3.0.2

_2023년 8월 7일_

[!BADGE 지원됨]{type="Informative" tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

#### 새로운 기능

![새로 만들기](../assets/new.svg) 다음 값이 `storeDetails` 개체에 추가되었습니다.

- &quot;페이지당 모든 제품 허용&quot;
- 통화 비율
- &quot;그리드 허용 값의 페이지당 제품&quot;
- &quot;그리드 기본값의 페이지당 제품&quot;
- 언어 저장

#### 업데이트

고급 데이터 검색을 지원하기 위해 ![수정](../assets/fix.svg) 카탈로그 서비스 모듈이 메타패키지에 추가되었습니다.
![수정](../assets/fix.svg) 제품 목록 페이지 위젯을 사용할 때 **내 계정** 페이지 탐색이 더 이상 사라지지 않습니다.

이러한 기능에 액세스하려면 판매자가 [!DNL Live Search] 확장 버전 >= 3.0.2를 업그레이드해야 합니다.

프로덕션으로 푸시하기 전에 업그레이드 및 테스트하는 것이 좋습니다. 테스트 환경 결과를 확인한 후 사용량이 적은 시간 동안 프로덕션 환경을 업그레이드하는 것이 좋습니다.

#### 제한 사항

라이브 검색 제품 목록 페이지 위젯을 사용하면 Google Tag Manager가 실패합니다. Google 태그 관리자가 필요한 경우 기본 검색 어댑터를 사용합니다.

### [!DNL Live Search] 3.0.1

_2023년 3월 14일_

[!BADGE 지원됨]{type="Informative" tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

#### 새로운 기능

규칙 미리 보기의 ![새](../assets/new.svg) 제품 항목 카드
![새로 만들기](../assets/new.svg) [제품 목록 페이지 위젯](https://experienceleague.adobe.com/en/docs/commerce/live-search/live-search-storefront/plp-styling)
![새로 만들기](../assets/new.svg) [범주 필터링 옵션](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#facets)
![새로 만들기](../assets/new.svg) 고정 이벤트를 만들기 위해 끌어서 놓는 기능을 추가했습니다
새 Pin 동작 ![새로 만들기](../assets/new.svg):
- 고정점 - 고정 단추를 클릭하여 고정 이벤트를 만듭니다.
- 상단에 고정 - 제품을 첫 번째 위치에 배치합니다.
- 맨 아래에 고정 - 제품을 결과의 맨 아래에 배치합니다.
- 한 번의 클릭으로 이벤트 고정 해제
![새로 만들기](../assets/new.svg) [규칙에 대한 지능형 순위](https://experienceleague.adobe.com/en/docs/commerce/live-search/live-search-admin/rules/rules-add)
![신규](../assets/new.svg) [!DNL Live Search]은(는) 이제 Commerce(이전에는 Multi-Source Inventory 또는 MSI로 알려짐)에서 전체 [Inventory management](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/introduction) 기능을 지원합니다. 전체 지원을 활성화하려면 종속성 모듈 [을(를) 버전 102.2.0+로 ](install.md#update)업데이트`commerce-data-export`해야 합니다.

#### 업데이트

![수정](../assets/fix.svg) 이제 규칙을 구성하면 위치가 고유하게 자동으로 정렬됩니다.
![수정](../assets/fix.svg) 기존 이벤트를 삭제하면 미리 보기가 업데이트됩니다.
이벤트가 없는 ![규칙 수정](../assets/fix.svg)을(를) 저장할 수 없습니다
![수정](../assets/fix.svg) &quot;Select Type&quot; 선택기를 제거합니다.
![수정](../assets/fix.svg) 저장하지 않은 규칙에 대해 새 &quot;편집 중&quot; 상태를 추가했습니다.

#### 수정 사항

저장하는 동안 완료되지 않은 이벤트가 있는 경우 ![수정](../assets/fix.svg) 서버 오류를 해결했습니다.
![수정](../assets/fix.svg) 여러 이벤트가 있는 경우 특정 이벤트를 올바르게 삭제하는 문제를 해결했습니다
![수정](../assets/fix.svg) 새 이벤트가 추가되었을 때 기존 규칙 이벤트가 업데이트되지 않는 문제를 해결했습니다
![수정](../assets/fix.svg) 세부 정보에서 두 번째 &quot;편집&quot; 클릭을 수정했습니다. [!DNL Live Search] 페이지를 다시 로드해야 합니다.
![수정](../assets/fix.svg) 동의어: 사용자가 입력을 클릭했을 때 필드에 포커스를 반환할 수 없는 문제가 해결되었습니다.
![수정](../assets/fix.svg) 기타 사소한 버그 수정 및 성능 업데이트
![버그](../assets/bug.svg) - &quot;추천&quot;의 순위는 라이브 검색 위젯 내에서만 지원됩니다. 기본 Luma 및 PWA 검색 기능에서는 지원되지 않습니다.
![버그](../assets/bug.svg) - 사용자 지정 가격 특성 패싯이 Luma에서 올바르게 렌더링되지 않지만 API가 해당 패싯을 제대로 필터링합니다.

이러한 기능에 액세스하려면 판매자가 [!DNL Live Search] 확장 버전 >= 3.0.1을 업그레이드해야 합니다.

프로덕션으로 푸시하기 전에 업그레이드 및 테스트하는 것이 좋습니다. 테스트 환경 결과를 확인한 후 사용량이 적은 시간 동안 프로덕션 환경을 업그레이드하는 것이 좋습니다.

### [!DNL Live Search] 2.0.5

[!BADGE 지원됨]{type="Informative" tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![수정](../assets/fix.svg) - 네트워크 문제로 인해 SDK 리소스를 사용할 수 없으면 실시간 검색에서 오류가 발생합니다. 이 버그는 수정되었습니다.

이러한 기능에 액세스하려면 Live Search 확장 버전 >= 2.0.5를 업그레이드해야 합니다.

프로덕션으로 푸시하기 전에 업그레이드 및 테스트하는 것이 좋습니다. 테스트 환경 결과를 확인한 후 사용량이 적은 시간 동안 프로덕션 환경을 업그레이드하는 것이 좋습니다.

### [!DNL Live Search] 2.0.4

[!BADGE 지원됨]{type="Informative" tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새로 만들기](../assets/new.svg) 실시간 검색은 이제 관리자의 &#39;재고 부족 제품 표시&#39; 설정에 의한 필터링을 지원합니다. &#39;재고 부족 제품 표시&#39;를 false로 설정하면 `inStock = true`이(가) 필터에 추가됩니다.
![수정](../assets/fix.svg) 성능을 개선하기 위해 &#39;제안&#39; 블록이 라이브 검색 팝업에서 제거되었습니다. 기능을 교체하려는 경우 데이터는 여전히 GraphQL을 통해 전달됩니다.
![수정](../assets/fix.svg) `categories` 및 `categoryPath`이(가) 범주 필터링에 대해 `categoryIds`을(를) 대체했습니다. [productSearch](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/) 항목에서 자세히 알아보십시오.
![수정](../assets/fix.svg) 이전에는 B2B 회사에 연결된 사용자가 검색을 수행할 때 잘못된 고객 그룹 코드를 받았습니다. 이제 Live Search에서 올바른 값을 반환합니다.
![수정](../assets/fix.svg) 이전에는 존재하지 않는 용어를 검색할 때 Live Search에서 오류를 반환합니다. 해당 버그는 이제 수정되었습니다.

이러한 기능에 액세스하려면 판매자가 [!DNL Live Search] 확장 버전 >= 2.0.4를 업그레이드해야 합니다.

사용자는 프로덕션으로 푸시하기 전에 업그레이드 및 테스트하는 것이 좋습니다. 테스트 환경 결과를 확인한 후 사용량이 적은 시간 동안 프로덕션 환경을 업그레이드하는 것이 좋습니다.

### [!DNL Live Search] 2.0.3

[!BADGE 지원됨]{type="Informative" tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새로운 ](../assets/new.svg) 라이브 검색은 이제 범주 권한, 공유 카탈로그 및 고객 그룹별 가격을 준수하여 B2B 기능을 지원합니다.

이러한 기능에 액세스하려면 판매자가 [!DNL Live Search] 확장 버전 >= 2.0.3을 업그레이드해야 합니다.

사용자는 프로덕션으로 푸시하기 전에 업그레이드 및 테스트하는 것이 좋습니다. 테스트 환경 결과를 확인한 후 사용량이 적은 시간 동안 프로덕션 환경을 업그레이드하는 것이 좋습니다.

### [!DNL Live Search] 2.0

[!BADGE 지원됨]{type="Informative" tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

다음과 같은 새로운 기능, 수정 사항 및 향상된 기능을 활용하려면 기존 [!DNL Live Search] 설치를 [!DNL Live Search] 2.0.0으로 업그레이드해야 합니다.

![새로 만들기](../assets/new.svg) [!DNL Live Search]은(는) 이제 Adobe Commerce 2.4.4를 실행하는 설치에서 PHP 8.1을 지원합니다.
![새로 만들기](../assets/new.svg) 설치하는 동안 사용하지 않도록 설정된 모듈 목록에 `Magento_ElasticsearchCatalogPermissionsGraphQl` 모듈이 추가됩니다.
![새로 만들기](../assets/new.svg) [[!DNL storefront popover]](overview.md)관리자&#x200B;*에서*의 사용 가능한 줄 수를 구성할 수 있습니다.
![에 대해 ](../assets/new.svg)새[ Beta ](https://developer.adobe.com/commerce/pwa-studio/)PWA[!DNL Live Search]이(가) 지원됩니다.
![새로 만들기](../assets/new.svg) [!DNL Live Search] 설치 프로세스가 고급 프로세스 변경 내용으로 업데이트됩니다.
![수정](../assets/fix.svg) [고급 검색](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search) 링크가 상점 바닥글에서 제거되었습니다.
![버그](../assets/bug.svg) 다음 제품 특성은 PWA의 베타 릴리스와 관련하여 사용할 때 [Commerce GraphQL API](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/)에서 지원되지 않습니다. `description`, `name`, `short_description`
![버그](../assets/bug.svg) [!DNL Live Search]용 PWA 베타 릴리스는 [이벤트 처리](https://developer.adobe.com/commerce/services/shared-services/storefront-events/sdk/)를 지원하지 않습니다.

### [!DNL Live Search] 1.3.1

[!BADGE 지원됨]{type="Informative" tooltip="지원됨"} Adobe Commerce 버전 2.4.x 이상

![수정](../assets/fix.svg) [사용자 지정 가격 특성](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/attributes-input-types)이(가) [facet](facets-add.md)(으)로 구성된 경우 더 이상 오류를 반환하지 않습니다.
![수정](../assets/fix.svg) 사용 가능한 [통화 기호](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/currency/currency-configuration#step-5-customize-currency-symbols-optional)&#x200B;(`data-currency-symbol`)가 없을 때 오류가 발생하는 문제를 해결했습니다.
사용 가능한 경우 ![수정](../assets/fix.svg) [[!DNL Storefront popover]](storefront-popover.md)에 [특별 가격](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/pricing/product-price-special)&#x200B;(최소 최종 가격)이 표시됩니다.

### [!DNL Live Search] 1.3.0

[!BADGE 지원됨]{type="Informative" tooltip="지원됨"} Adobe Commerce 버전 2.4.x 이상

![새로 만들기](../assets/new.svg) [성능](performance.md) 보고 대시보드는 쇼핑객이 사용하는 검색어에 insight을 제공합니다.
![새로 만들기](../assets/new.svg) [!DNL Live Search] [Storefront Events SDK](https://developer.adobe.com/commerce/services/shared-services/storefront-events/sdk/)에서는 이벤트 게시 및 구독 서비스와 지표가 있는 공통 데이터 레이어에 액세스할 수 있습니다.
![수정](../assets/fix.svg) [[!DNL Storefront popover]](storefront-popover.md)에 가시성을 제어하는 `active` 컨테이너에 대한 새 `.search-autocomplete` 클래스가 있습니다.
![수정](../assets/fix.svg) 상점 첫 화면에서 [검색어](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search-terms) 바닥글 링크가 제거되고 해당 캐시가 [!DNL Live Search] 설치에 사용할 수 없습니다.
검색 어댑터용 ![버그](../assets/bug.svg) 패치가 중복 제품을 처리합니다.
![버그](../assets/bug.svg) [!DNL Live Search]은(는) 다중(가상) [재고](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/sources/sources-manage)가 있는 [단일 소스](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/stocks/stocks-manage)&#x200B;(실제) 인벤토리 위치를 지원합니다. 지금은 여러 인벤토리 소스가 지원되지 않습니다.

### [!DNL Live Search] 1.2.0

[!BADGE 지원됨]{type="Informative" tooltip="지원됨"} Adobe Commerce 버전 2.4.x 이상

![새로 만들기](../assets/new.svg) [[!DNL Storefront popover]](storefront-popover.md) 쇼핑객이 검색 상자에 쿼리를 입력할 때 추천 제품 및 상위 검색 결과의 썸네일 이미지를 표시합니다.
![새](../assets/new.svg) Commerce *관리자* 세션이 오랫동안 키보드를 사용하지 않는 동안에는 열려 있습니다.
온보딩 후 ![새로 만들기](../assets/new.svg) [!DNL Live Search]이(가) 자동으로 활성화됨
![수정](../assets/fix.svg) 초기 인덱싱 시간은 1시간 미만입니다.
![수정](../assets/fix.svg) 실시간(설치 및 설치 후) 증분 제품 업데이트
동의어 편집기의 정렬 가능한 열 ![수정](../assets/fix.svg)
![수정](../assets/fix.svg) [!DNL Live Search] 검색 조건에 빈 정렬 순서 값이 포함된 경우 더 이상 오류가 발생하지 않습니다
![수정](../assets/fix.svg) 특성 코드에 문자열 &quot;to&quot; 또는 &quot;from&quot;이 포함된 경우 범위 필터링이 더 이상 중단되지 않습니다.

### [!DNL Live Search] 1.1.0

[!BADGE 지원됨]{type="Informative" tooltip="지원됨"} Adobe Commerce 버전 2.4.x 이상

![버그](../assets/bug.svg) [!DNL Live Search] 서비스는 Adobe Commerce 설치의 [기본 통화](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/currency/currency-configuration)만 지원합니다.
![버그](../assets/bug.svg) 패싯을 추가할 때 `Update on Save`(으)로 설정하면 제품 특성 피드가 올바르게 업데이트되지 않습니다. 이 문제를 방지하려면 [인덱스 관리](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management)&#x200B;(으)로 이동하여 제품 특성 피드를 `Update by Schedule`(으)로 설정하십시오.
![버그](../assets/bug.svg) [!DNL Live Search] 동의어는 저장소 보기별로 정의되지만, 현재 웹 사이트별로 저장되고 `environmentId`과(와) `storeViewCode`의 조합으로 식별됩니다. 따라서 Adobe Commerce 설치 내의 모든 웹 사이트 및 스토어 보기는 동의어를 공유합니다. 저장소 보기에 대해 가장 최근에 생성된 동의어 집합이 우선합니다.
![버그](../assets/bug.svg) 동의어 용어에 여러 단어가 포함된 경우 각 단어는 별도의 동의어로 처리됩니다. 예를 들어 &quot;time piece&quot;를 &quot;watch&quot;의 동의어로 정의하면 &quot;time&quot;과 &quot;piece&quot;는 모두 watch의 동의어로 처리됩니다.

+++

## 설명서

자세한 내용은 다음을 참조하십시오.

- [Adobe Commerce 개발자 설명서](https://developer.adobe.com/commerce/docs)
- [Adobe Commerce 사용 안내서](https://experienceleague.adobe.com/en/docs/commerce)
- [[!DNL Live Search] 마켓플레이스](https://commercemarketplace.adobe.com/magento-live-search.html)
