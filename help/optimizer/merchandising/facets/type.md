---
title: Facet 유형
description: ' [!DNL Adobe Commerce Optimizer]의 다양한 패싯에 대해 알아봅니다.'
badgeSaas: label="SaaS만" type="Positive" url="https://experienceleague.adobe.com/ko/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."
exl-id: f4ab1f27-b393-45e0-94bf-c77d46e3f994
source-git-commit: 458f34c45406db871ec61ff408aa624f163b6ee0
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# 패싯 유형

[!DNL Adobe Commerce Optimizer]은(는) 다양한 패싯 유형을 사용하며 관련성이 있을 때만 *필터* 목록에 표시됩니다. 사용 가능한 패싯 목록은 반환된 제품에 따라 변경됩니다. 다음은 프레젠테이션과 동작에 영향을 주는 특성입니다.

- 고정 패싯 - 가장 일반적으로 사용되는 패싯을 목록의 맨 위에 고정할 수 있습니다. 나머지 패싯은 고정된 패싯 다음에 *정렬 형식* 순서로 나열됩니다.
- 동적 패싯 - [Adobe AI](https://business.adobe.com/kr/ai.html)가 제품 집합 및 쿼리와 가장 관련이 있는 제품 특성입니다. 이 계산은 전체 카탈로그의 속성 메타데이터를 고려하고 쿼리 시간에 쿼리에 가장 적합한 패싯을 결정합니다.
- 가격 패싯 - 가격 범위별로 제품을 반환합니다. [*설정*](../../settings.md) 작업 영역에서 선택 항목 수와 가격 범위 간격을 지정할 수 있습니다.

## Facet 레이블

[Faceting 작업 영역](workspace.md)에서 Facet 레이블을 편집할 수 있습니다.

## 정렬 유형

상점 앞에 대해 렌더링된 모든 패싯은 알파벳순 또는 개수별로 정렬됩니다.

| 정렬 유형 | 설명 |
|--- |--- |
| 알파벳 | 상점 *필터* 목록에서 패싯은 알파벳순으로 정렬됩니다. |
| 계수 | 패싯은 현재 반환된 제품 세트에서 패싯당 찾은 값의 수로 정렬할 수도 있습니다. |
