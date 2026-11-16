---
source-git-commit: bc3ebc0514874b9678e8b632cc2c48102959d439
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%
---
# 동의어 모범 사례

다음은 동의어를 생성할 때 모범 사례 목록을 제공합니다.

- 시스템은 기본적으로 철자 오류를 관리합니다. 쇼핑객이 사용할 수 있는 단어를 포함하려면 동의어를 설정하십시오. 이 단어는 카탈로그에 지정된 단어와 다릅니다. 제품이 &quot;소파&quot;로 나열되는 동안 다른 사람이 &quot;소파&quot;를 찾고 있으므로 판매에서 지고 싶지 않습니다. 고객이 제품을 찾을 때 사용할 수 있는 모든 단어를 입력하여 광범위한 검색어를 캡처합니다. 결과를 향상시키려면 [동의어를 단방향 또는 양방향](https://experienceleague.adobe.com/ko/docs/commerce/optimizer/merchandising/synonyms/add#step-2-define-the-synonym-by-type)으로 설정하십시오.

- 브랜드 이름과 약어를 전체 이름에 매핑 (예: &quot;HP&quot;에서 &quot;Hewlett-Packard&quot;로, 일반적인 제품 별명 (예: &quot;iPhone&quot;에서 &quot;Apple iPhone&quot;로).

- &quot;운동화&quot;와 &quot;운동화&quot;와 같이 쇼핑객들이 상호 교환하여 사용할 수 있는 산업별 전문 용어와 용어를 포함하십시오.

- 새 검색 트렌드, 제품 추가 및 구매자 행동을 기반으로 동의어 목록을 정기적으로 업데이트합니다.

- 검색 결과 및 구매자 피드백을 분석하여 동의어 매핑의 효과를 테스트합니다. 정확성과 관련성을 향상시키려면 매핑을 구체화합니다.

- 정지어는 동의어를 더 의미 있게 만들지 않고, 오히려 처리해야 하는 데이터의 양을 늘려주는 것이므로 사용하지 마십시오. 일반적인 영어 &quot;정지어&quot;는 다음과 같이 동의어에서 필터링됩니다.

  a, an, and, are, as, at, be, but, by, for, if, in, into, is, it, no, not, of, on, or, such, that, the, their, then, there, these, they, this, to, was, will, with

- 단어의 단수 형태와 복수 형태를 모두 동의어로 정의할 필요는 없다. 카탈로그에 단수 용어와 복수 용어가 혼합되어 있는 경우 검색 결과 올바른 제품 세트를 찾습니다. 예를 들어 &quot;pant&quot;를 사용하고 쇼핑객이 &quot;pants&quot;를 검색하면 Search는 올바른 제품을 반환합니다. 단수형인 &quot;바지&quot;는 패션 산업에서 종종 사용되며 때로는 소매업에서 사용되기도 하지만, 복수형인 &quot;바지&quot;가 일부 영역에서 더 일반적으로 사용됩니다. (바지)라는 단어는 기술적으로 옷의 한쪽 다리를 덮는 부분을 말합니다. 양쪽 다리를 덮으려면 &quot;바지 한 벌&quot;이 필요합니다.)

- 카탈로그에서 용어가 사용되는 방식을 일관하십시오. 지역별 사용 차이가 있으며 경우에 따라 업계 차이도 있다는 점을 기억하십시오.
