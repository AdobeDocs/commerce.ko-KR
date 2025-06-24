---
title: 권장 사항 필터
description: 필터를 사용하여  [!DNL Adobe Commerce Optimizer] 권장 사항에 표시할 제품을 제어하는 방법에 대해 알아봅니다.
badgeSaas: label="SaaS만" type="Positive" url="https://experienceleague.adobe.com/ko/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."
source-git-commit: 746c016f149fb49b9c483968a8a5f40196b163ed
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%

---

# 제품 필터링

[!DNL Adobe Commerce Optimizer]은(는) 구성 불가능한 기본 필터를 권장 사항 단위에 자동으로 적용합니다. 페이지에 여러 개의 추천 단위가 배포되어 있는 경우 [!DNL Adobe Commerce Optimizer]은(는) 해당 단위로 반복되는 모든 제품을 필터링합니다. 다른 제품을 추천할 수 있는 공간을 만들기 위해 반복 제품에 대한 첫 번째 참조만 사용됩니다. [!DNL Adobe Commerce Optimizer]은(는) 이전에 구매한 제품과 장바구니에 있는 제품도 필터링합니다.

권장 사항 단위를 [만들기](create.md)할 때 권장 사항에 표시할 수 있는 제품을 제어하는 필터를 정의할 수 있습니다. 이러한 필터는 사용자가 정의하는 포함 또는 제외 조건 집합을 기반으로 합니다. 모든 포함 조건과 일치하는 제품만 권장 사항에 표시됩니다. 제외 조건과 일치하는 제품은 권장하지 않습니다.

각 필터 페이지에서 토글을 선택하여 여러 필터를 구성하고 원하는 필터만 활성화할 수 있습니다. 나중에 사용할 수 있도록 필터의 초안을 만들 수 있습니다. 각 탭에 활성화된 필터의 수가 표시됩니다.

## 조건

조건은 정적이거나 동적일 수 있습니다.

- 정적 조건은 기존 제품 속성을 사용하여 단위에 나타날 수 있는 제품을 결정합니다. 예를 들어 가격이 $25보다 큰 재고 제품만 단위에 나타나도록 지정할 수 있습니다.

- 동적 조건은 현재 표시된 카테고리 또는 제품과 같은 구매자의 현재 컨텍스트를 기반으로 합니다. 예를 들어 제품 세부 사항 페이지에 배포할 제품 권장 사항을 생성할 때 현재 표시된 제품의 상대 가격 범위 내에 있는 제품만 추천하는 조건을 생성할 수 있습니다.

### 논리 연산자

논리 연산자 `AND` 및 `OR`을(를) 사용하여 여러 조건을 연결합니다. 포함 필터와 제외 필터를 모두 사용하는 경우, 먼저 포함을 평가하여 추천할 수 있는 모든 가능한 제품을 결정한 다음 제외 필터와 일치하는 제품은 목록에서 제거됩니다.

- `AND` - 두 개의 포함 필터링 조건 조인
- `OR` - 두 개의 제외 필터링 조건에 조인

## 필터 유형

![필터](../../assets/rec-conditions.png)

### 제품

제품 필터는 권장 사항에 표시할 적격 또는 부적격 제품을 지정합니다. 비활성화되거나 개별적으로 표시되지 않는 제품은 권장 사항에 표시되지 않으므로 선택할 수 없습니다.

>[!NOTE]
>
>구성 가능한 제품의 하위 제품은 _개별적으로 표시되지 않음_&#x200B;의 가시성을 가지므로 추천 단위에 표시되지 않습니다.

### 가격

제품 가격을 기반으로 하는 필터는 최종 가격을 사용하여 비교를 수행합니다. 최종 가격에는 익명의 구매자가 이용할 수 있는 할인 또는 특별 가격이 포함됩니다.

<!--### Attribute

You can filter products based on attribute criteria, including attribute values. Selected values use OR logic to either include or exclude products when any of the specified values are found.-->
