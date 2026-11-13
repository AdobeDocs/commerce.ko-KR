---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 0%
---
단방향 및 양방향 동의어는 키워드의 정의를 확장합니다. 일부는 키워드와 교환되는 반면, 일부는 키워드의 하위 집합을 나타냅니다.

## 양방향

양방향 동의어는 의미가 같고 동일한 검색 결과를 반환합니다. 다음 예제에서는 굵게 표시된 첫 번째 단어가 카탈로그에 사용된 키워드이고 그 뒤에 원래 키워드와 동일한 의미를 갖는 단어가 옵니다. 동일한 키워드에 대해 간단한 양방향 동의어 쌍이나 여러 양방향 동의어 체인을 만들 수 있습니다.

**재킷** ![양방향 선택기](/help/assets/ccdm-shared/synonyms/two-way.png) 코트
**바지** ![양방향 선택기](/help/assets/ccdm-shared/synonyms/two-way.png) 슬랙스 ![양방향 선택기](/help/assets/ccdm-shared/synonyms/two-way.png) 바지

## 단방향

단방향 동의어는 키워드의 하위 집합이지만 보다 구체적인 의미가 있습니다. 예를 들어, 캐프리와 반바지는 바지이지만 모든 바지가 캐프리나 반바지는 아닙니다. 바지 검색에 카프리와 반바지가 포함됩니다. 그러나 반바지를 검색하면 캐퍼리가 반환되지 않습니다.

**스웨트 셔츠** ![단방향 선택기](/help/assets/ccdm-shared/synonyms/one-way.png) 후드
**바지** ![단방향 선택기](/help/assets/ccdm-shared/synonyms/one-way.png) capris ![단방향 선택기](/help/assets/ccdm-shared/synonyms/one-way.png) 종아리 길이 바지 ![단방향 선택기](/help/assets/ccdm-shared/synonyms/one-way.png) 페들 푸셔

## 다중 단어 동의어 동작

여러 단어 동의어의 경우, 시스템은 동의어를 구문으로 간주한다. 예를 들어 양방향 동의어 **식사 테이블** ![양방향 선택기](/help/assets/ccdm-shared/synonyms/two-way.png) **주방 테이블** ![양방향 선택기](/help/assets/ccdm-shared/synonyms/two-way.png) **식사 테이블**&#x200B;을 만드는 경우, 시스템은 **식사 테이블** 또는 **주방 테이블** 또는 **식사 테이블**&#x200B;의 발생 여부를 검색할 수 있도록 설정된 모든 필드를 검색합니다.

동의어가 만들어지지 않고 쇼핑객이 **부엌 테이블**&#x200B;을 검색하는 경우, 시스템에서는 다른 필드에서도 검색 가능한 필드에서 용어를 찾습니다(예: 이름 필드에는 **테이블**, 메타 키워드에는 **부엌**).

동의어를 만든 후 검색 동작이 정확히 일치하는 구 **kitchen table**&#x200B;을(를) 찾도록 변경됩니다. 이렇게 하면 구문이 정확한 제품만 표시되므로 결과 수가 줄어들 수 있습니다.

이전과 같이 용어를 개별적으로 검색하려는 경우 [지원 티켓을 만들 수 있습니다](https://experienceleague.adobe.com/ko/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide).
