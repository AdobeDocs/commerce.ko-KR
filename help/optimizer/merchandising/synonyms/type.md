---
title: 동의어 유형
description: ' [!DNL Adobe Commerce Optimizer]의 여러 가지 동의어 유형에 대해 알아봅니다.'
badgeSaas: label="SaaS만" type="Positive" url="https://experienceleague.adobe.com/ko/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."
source-git-commit: 3131cc27a25d1bf958071b973f1d4bf1a68be152
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---

# 동의어 유형

단방향 및 양방향 동의어는 키워드의 정의를 확장합니다. 일부는 키워드와 교환되는 반면, 일부는 키워드의 하위 집합을 나타냅니다.

## 양방향

양방향 동의어는 의미가 같고 동일한 검색 결과를 반환합니다. 다음 예제에서는 굵게 표시된 첫 번째 단어가 카탈로그에 사용된 키워드이고 그 뒤에 원래 키워드와 동일한 의미를 갖는 단어가 옵니다. 동일한 키워드에 대해 간단한 양방향 동의어 쌍이나 여러 양방향 동의어 체인을 만들 수 있습니다.

**재킷** ![양방향 선택기](../../assets/btn-two-way.png) 코트
**바지** ![양방향 선택기](../../assets/btn-two-way.png) 슬랙스 ![양방향 선택기](../../assets/btn-two-way.png) 바지

## 단방향

단방향 동의어는 키워드의 하위 집합이지만 보다 구체적인 의미가 있습니다. 예를 들어, 캐프리와 반바지는 바지이지만 모든 바지가 캐프리나 반바지는 아닙니다. 바지 검색에 카프리와 반바지가 포함됩니다. 그러나 반바지를 검색하면 캐퍼리가 반환되지 않습니다.

**스웨트 셔츠** ![단방향 선택기](../../assets/btn-one-way.png) 후드
**바지** ![단방향 선택기](../../assets/btn-one-way.png) capris ![여러 단방향 선택기](../../assets/btn-multiple-one-way.png) 종아리 길이 바지 ![여러 단방향 선택기](../../assets/btn-multiple-one-way.png) 페들 푸셔

## 다중 단어 동의어 동작

여러 단어 동의어의 경우 [!DNL Adobe Commerce Optimizer]은(는) 동의어를 구문으로 간주합니다. 예를 들어 양방향 동의어 **식사 테이블** ![양방향 선택기](../../assets/btn-two-way.png) **주방 테이블** ![양방향 선택기](../../assets/btn-two-way.png) **식사 테이블**&#x200B;을 만드는 경우 [!DNL Adobe Commerce Optimizer]은(는) **식사 테이블** 또는 **주방 테이블** 또는 **식사 테이블**&#x200B;의 발생 여부를 검색할 수 있도록 설정된 모든 필드를 검색합니다.

동의어가 만들어지지 않고 쇼핑객이 **주방 테이블**&#x200B;을(를) 검색하는 경우 [!DNL Adobe Commerce Optimizer]은(는) 검색 가능한 필드의 어디에서나 다른 필드(예: 이름 필드의 **테이블**, 메타 키워드의 **주방**)에서 용어를 찾습니다.

동의어를 만든 후 검색 동작이 정확히 일치하는 구 **kitchen table**&#x200B;을(를) 찾도록 변경됩니다. 이렇게 하면 구문이 정확한 제품만 표시되므로 결과 수가 줄어들 수 있습니다.

이전과 같이 용어를 개별적으로 검색하려는 경우 [지원 티켓을 만들 수 있습니다](https://experienceleague.adobe.com/ko/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide). 수요가 충분하면 [!DNL Adobe Commerce Optimizer]은(는) 향후 릴리스에서 이 기능을 제품에 추가하는 것을 고려합니다.
