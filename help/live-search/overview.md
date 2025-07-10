---
title: ' [!DNL Live Search]이란?'
description: Adobe Commerce의 [!DNL Live Search]는 빠르고, 관련성이 높고, 직관적인 검색 경험을 제공합니다.
recommendations: noCatalog
exl-id: 15399216-6a96-4d0b-bbc1-293190cb9e14
source-git-commit: d07f36a71247a96bc2dd950867c2862205238d88
workflow-type: tm+mt
source-wordcount: '954'
ht-degree: 1%

---

# [!DNL Live Search]이란?

[!DNL Live Search]은(는) Adobe Commerce의 표준 검색 기능을 대체하는 기능입니다. [!DNL Live Search] 기능을 활성화하고 구성하면 기본 검색 텍스트 필드가 [!DNL Live Search] 텍스트 필드로 바뀝니다. [!DNL Live Search]에는 검색 결과를 검색할 때 강력한 필터링 기능을 제공하는 PLP(제품 목록 페이지) 위젯도 포함되어 있습니다.

[!DNL Live Search]을(를) 사용하여 다음을 수행할 수 있습니다.

- 의미 있는 검색 경험을 만들어 쇼핑객과 구매자가 가능한 한 적은 노력으로 원하는 것을 찾을 수 있도록 지원합니다.
- 세션 내 구매자 행동에 대응하여 검색 결과를 AI에서 제공하는 동적 팩팅 및 재순위를 활용하십시오.
- 간단한 업데이트를 제공하고 라이선스에 포함되어 TCO를 절감하는 간단한 SaaS 기반 서비스를 사용합니다.
- GraphQL API, Headless 유연성, API 샌드박스 환경 및 초고속 SaaS를 활성화하여 기술을 얻으십시오.

>[!IMPORTANT]
>
>사이트 검색과 관련하여 Adobe Commerce은 옵션을 제공합니다. 구현하기 전에 [경계 및 제한](boundaries-limits.md) 정보를 검토하여 [!DNL Live Search]이(가) 비즈니스 요구 사항에 맞는지 확인하십시오.

## 아키텍처

아키텍처의 Adobe Commerce 측에는 검색 *관리자*&#x200B;를 호스팅하고, 카탈로그 데이터를 동기화하고, 쿼리 서비스를 실행하는 작업이 포함됩니다. [!DNL Live Search]을(를) 설치하고 구성한 후 Adobe Commerce에서 검색 및 카탈로그 데이터를 SaaS 서비스와 공유하기 시작합니다. 이제 관리자는 검색 [패싯](facets.md), [동의어](synonyms.md) 및 [머천다이징 규칙](category-merch.md)을 설정하고, 사용자 지정하고, 관리할 수 있습니다.

![실시간 검색 데이터 흐름](assets/ls-cs-data-flow.png)

## 빠른 둘러보기

속도, 관련성 및 사용 편의성에 중점을 둔 [!DNL Live Search]은(는) 쇼핑객과 판매자 모두에게 게임 체인저입니다. 다음 비디오를 시청한 다음 상점 앞에서 [!DNL Live Search]을(를) 간단히 둘러보십시오.

>[!VIDEO](https://video.tv.adobe.com/v/3418797?learn=on)

Live Search 사용 및 구성에 대한 자세한 비디오는 [전체 데모 위치 [!DNL Live Search]](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/getting-started/capabilities/live-search-full-demonstration) 항목을 참조하십시오.

### 입력할 때 검색

[!DNL Live Search]이(가) 쇼핑객이 [검색](storefront-popover.md) 상자에 쿼리를 입력할 때 [팝오버](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search)에 있는 상위 검색 결과의 추천 제품 및 썸네일 이미지로 응답합니다. 쇼핑객이 추천 또는 추천 제품을 클릭하면 [제품 세부 정보](https://experienceleague.adobe.com/en/docs/commerce-admin/start/storefront/storefront) 페이지가 표시됩니다. 팝오버의 바닥글에 있는 _모두 보기_ 링크에 검색 결과 페이지가 표시됩니다.

[!DNL Live Search]이(가) 둘 이상의 문자에 대한 &quot;입력한 대로 검색&quot; 결과를 반환합니다. 부분 일치의 경우 단어 당 최대 문자 수는 20자입니다. 쿼리의 문자 수를 구성할 수 없습니다. 팝오버에는 `name`, `sku` 및 `category_ids` 필드가 포함됩니다.

![Example storefront - 입력한 대로 검색](assets/storefront-search-as-you-type.png)

### 모든 검색 결과 보기

&quot;입력할 때 검색&quot; 쿼리에서 반환된 모든 제품을 나열하려면 팝오버의 바닥글에서 _모두 보기_&#x200B;를 클릭합니다.

![Example storefront - 가격 패싯](assets/storefront-view-all-search-results.png)

### [!DNL Live Search]에서 오타를 처리하는 방법

검색을 수행하면 [!DNL Live Search]에서 오타가 없는 비유사 검색을 실행합니다. 결과가 없으면 [!DNL Live Search]에서 사소한 오타를 고려하여 두 번째 유사 항목 검색을 수행합니다. 퍼지 검색은 최대 편집 거리가 1인 상태에서 실행됩니다. 이 편집 거리는 [Levenshtein distance](https://en.wikipedia.org/wiki/Levenshtein_distance) 개념을 사용하며 세 가지 유형의 작업을 허용합니다.

| 작업 | 설명 | 예 |
|---|---|---|
| 삽입 | 문자 추가. | &quot;cat&quot; -> &quot;cart&quot; |
| 삭제 | 문자 제거 | &quot;cart&quot; -> &quot;cat&quot; |
| 대체 | 한 문자를 다른 문자로 바꾸기. | &quot;cart&quot; -> &quot;cast&quot; |

유사 항목 검색 논리 외에도 전치도 고려됩니다. 즉, 단어에서 인접한 두 문자가 교체됩니다(예: &quot;the&quot; 대신 &quot;the&quot;). 이러한 편집 제한은 단어 단위이며 전체 구문이 아닙니다.

### 패싯으로 필터링된 검색

필터링된 검색에서는 특성 값의 여러 차원 또는 [패싯](facets.md)을 검색 기준으로 사용합니다. 필터 선택은 판매자에 의해 정의되며 반환되는 제품에 따라 변경되며, 가장 일반적으로 사용되는 패싯은 목록의 맨 위에 고정됩니다.

패싯을 URL 매개 변수 `http://yourwebsite.com?color=red`(으)로 사용하고 이러한 특성 값을 기반으로 하는 실시간 검색 필터 결과를 사용합니다.

### 동의어

[동의어](synonyms.md) 범위를 확장하고 쇼핑객이 카탈로그에 있는 것과 다른 단어를 사용하여 쿼리의 초점을 선명하게 합니다. 동의어 사전을 미세 조정하여 쇼핑객이 구매 경로에 계속 참여하도록 할 수 있습니다.

### 머천다이징 규칙

머천다이징 [규칙](rules.md)은(는) 검색할 논리 및 이벤트를 추가하는 if-then 문을 사용하여 쇼핑 경험을 형성합니다. 프로모션, 계절 또는 기타 기간 동안 제품을 쉽게 부스트하거나 묻을 수 있습니다.

### 검색어 지원

[!DNL Live Search]이(가) Commerce [검색어 리디렉션](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search-terms)을 지원합니다. 예를 들어 &quot;배송비&quot;와 같은 용어를 검색하여 배송비 페이지로 바로 이동할 수 있습니다.

## 라이브 검색 구성 요소

- [!DNL Live Search] [팝오버 위젯](storefront-popover.md)은(는) 검색 결과가 포함된 검색 필드 아래에서 열리는 상자입니다.
- [제품 목록 페이지 위젯](plp-styling.md)(PLP)은 패싯 및 동의어 지원과 함께 검색 가능한 제품 목록 페이지를 제공합니다. 위젯은 라이브 검색 4.0.0+에 설치되고 활성화되며 검색 어댑터를 대체합니다.
- (**사용하지 않음**) 검색 어댑터는 PLP 위젯의 전조이며 라이브 검색 &lt; 4.0.0과 함께 설치되었습니다. 4.0.0 이전 버전의 라이브 검색 을 사용하는 경우 Commerce에서 업그레이드하여 PLP 위젯 기능과 향후 개선 사항의 이점을 얻을 수 있습니다. 앞으로는 보안 문제를 해결하기 위해 검색 어댑터만 업데이트됩니다.

## [!DNL Live Search] 작업 영역

[!DNL Live Search] [작업 영역](workspace.md)은(는) 관리자가 동의어, 패싯 및 카테고리 머천다이징과 같은 [!DNL Live Search] 기능을 구성하는 영역입니다.

## 이벤트

[!DNL Live Search]은(는) [이벤트](events.md)를 사용하여 [지능형 머천다이징](category-merch.md) 및 [성능](performance.md) 대시보드를 계산합니다. 이벤트에는 기본 구현이 제공됩니다. 헤드리스 상점 첫 화면의 이벤트는 수동으로 활성화해야 합니다.

## 카탈로그 데이터 보존 정책

테스트 환경에서 카탈로그 데이터에 대한 검색 쿼리를 90일 연속 제출하지 않으면 카탈로그 데이터가 최대 절전 모드로 설정되고 검색 쿼리에 대해 데이터가 반환되지 않습니다. 프로덕션 환경의 카탈로그 데이터는 이 정책의 영향을 받지 않습니다.

테스트 환경에서 카탈로그 데이터를 다시 활성화하려면 [지원 요청을 제출](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#experience-league-start-page)하고 제목은 &quot;[!DNL Live Search] 다시 활성화&quot;로 지정하고 환경 ID를 포함하십시오. 테스트 환경의 카탈로그 데이터는 2시간 이내에 복원되어야 합니다.
