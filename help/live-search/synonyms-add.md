---
title: 동의어 추가
description: 검색 요청에 대한 응답을 향상시키려면  [!DNL Live Search] 동의어를 추가하십시오.
exl-id: 2dc535ea-35a3-45a8-8171-901005223cc9
source-git-commit: 6dcfd0a54e6a6814b7f5708e0c221452b8af4537
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---

# 동의어 추가

[!DNL Live Search] 동의어의 선별된 목록을 추가하여 고객 참여를 늘리십시오. [!DNL Live Search]은(는) 스토어 보기당 최대 200개의 동의어를 관리할 수 있습니다.

![[!DNL Live Search] 동의어](assets/synonym-workspace.png)

## 1단계: 동의어 추가

1. 관리자의 **마케팅** > SEO 및 검색 > **[!DNL Live Search]**(으)로 이동합니다.
1. 여러 스토어의 경우 동의어 설정이 적용되는 [스토어 보기](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html?lang=ko#scope-settings)&#x200B;(으)로 **범위**&#x200B;를 설정합니다.
1. **동의어** 탭을 클릭합니다.
1. **동의어 추가** 단추를 클릭합니다.

## 2단계: 유형별 동의어 정의

만들려는 [동의어 유형](synonyms-type.md)의 지침을 따르십시오.

### 양방향 동의어

1. 기본 **양방향** 옵션을 사용합니다.

   ![양방향 동의어 추가](assets/synonym-add-two-way.png)

1. 일치시킬 **키워드** 용어 또는 구를 입력하십시오.
1. 키워드에 동의어로 추가할 **Expansion** 용어를 입력하십시오. 쉼표로 여러 용어를 구분하십시오.
이 예에서 일치시킬 키워드는 &quot;pants&quot;이고 확장 용어 세트는 &quot;bars, slacks&quot;입니다.

   ![양방향 동의어 예제](assets/synonym-add-two-way-example.png)

1. 완료되면 **저장**&#x200B;을 클릭하세요.
동의어 집합은 각 용어 사이에 양방향 화살표가 있는 목록에 나타나며, 이 화살표는 각 용어가 상호 교환 가능하다는 것을 의미합니다.

   ![양방향 동의어](assets/synonym-two-way.png)

### 단방향 동의어

1. **단방향** 동의어 유형을 클릭합니다.

   ![단방향 동의어 추가](assets/synonym-add-one-way.png)

1. **키워드** 및 **확장** 용어를 입력하십시오. 쉼표로 여러 용어를 구분하십시오.

   ![단방향 동의어 예제](assets/synonym-add-one-way-example.png)

   이 예에서 키워드는 &quot;pants&quot;이고 단방향 확장 용어 &quot;capris, peddle-pushers&quot;는 각각 &quot;pants&quot;의 하위 집합이지만 특정 의미가 있습니다.

1. 완료되면 **저장**&#x200B;을 클릭하세요.
동의어 집합은 확장 용어에서 키워드로 가리키는 단방향 화살표와 함께 목록에 표시되어 용어가 키워드의 하위 집합임을 나타냅니다. 더하기 기호는 각 확장 항을 구분합니다.

   ![단방향 동의어](assets/synonym-one-way.png)

## 3단계: 변경 사항 게시

1. 동의어가 완료되면 **변경 내용 게시**&#x200B;를 클릭합니다.
1. 스토어에서 업데이트를 사용할 수 있을 때까지 최대 2시간을 기다립니다.

## 필드 설명

| 필드 | 설명 |
|--- |--- |
| [유형](synonyms.md) | 동의어가 키워드와 동일한 의미를 갖는지 또는 키워드의 하위 집합인지 여부를 결정합니다. 옵션:<br />양방향(기본값) - 키워드와 의미가 같고 동일한 검색 결과를 반환하는 용어<br />단방향 - 키워드의 하위 집합인 용어. 단방향 동의어는 특정 제품의 더 좁은 목록을 반환합니다. |
| 키워드 | 카탈로그의 제품 선택과 일반적으로 관련된 단어입니다. |
| 확장 | 키워드와 동일하거나 유사한 의미를 갖는 추가 용어입니다. |
