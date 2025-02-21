---
title: Workspace 환경 설정
description: ' [!DNL Live Search] 페이스팅 작업 영역에 대한 자세한 내용을 살펴보십시오.'
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# Workspace 환경 설정

*페이스팅* 작업 영역은 현재 사용 가능한 모든 패싯을 나열하며 패싯을 설정하고 관리하는 데 필요한 도구에 대한 액세스를 제공합니다. 고정된 패싯이 기존 패싯 목록에 먼저 나타나고 그 뒤에 동적 패싯이 나타납니다. 목록을 필터링하여 모든 패싯을 표시하거나 고정되거나 동적인 패싯만 표시할 수 있습니다.

![작업 공간 구성](assets/faceting-workspace.png)

## 범위 설정

Adobe Commerce 설치에 여러 스토어 보기가 포함된 경우 Facet 설정이 적용되는 [스토어 보기](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html#scope-settings)&#x200B;(으)로 **범위**&#x200B;를 설정합니다.

## 목록 필터링

1. **필터링 기준** 컨트롤을 클릭합니다.
1. 다음 옵션 중 하나를 선택합니다.

   * 모든 필터
   * 고정됨
   * 동적

## Facet 추가

1. **패싯 추가**&#x200B;를 클릭합니다.
1. 자세한 지침은 [패싯 추가](facets-add.md)를 참조하세요.

## 열 설명

| 열 | 설명 |
|--- |--- |
| (첫 열) | 구매자가 볼 수 있는 [레이블](facets-type.md)에 의해 고정된 동적 패싯과 동적 패싯을 나열합니다. |
| 정렬 유형 | Facet 값의 [정렬 순서](facets-type.md)입니다. 패싯은 모든 [!DNL Commerce] 상점 앞면에 대해 알파벳순으로 정렬됩니다. [headless] 구현의 경우 패싯을 알파벳순 또는 개수별로 정렬할 수 있습니다. 옵션: 알파벳, 개수(Headless만 해당) |
| 최대 값 | 상점에서 필터로 사용할 수 있는 최대 10개의 Facet 값 수입니다. |

## 컨트롤

| 제어 | 설명 |
|--- |--- |
| 패싯 추가 | [패싯 편집기](facets-add.md)를 엽니다. |
| 필터링 기준 | 목록에 나타나는 [패싯의 유형](facets-type.md)을(를) 결정합니다. 옵션: 모두, 고정됨, 동적 |
