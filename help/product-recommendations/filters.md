---
title: 제품 필터링
description: 권장 사항으로 사용되는 제품을 포함하거나 제외하는 조건을 정의합니다.
exl-id: 140bf047-4f6a-48da-b536-d96e78ae3d17
source-git-commit: 59aa4ae67a1a8a853b72d78cd65a6cc44a6bc662
workflow-type: tm+mt
source-wordcount: '800'
ht-degree: 0%

---

# 제품 필터링

Adobe Commerce은 구성 불가능한 기본 필터를 권장 사항 단위에 자동으로 적용합니다. 페이지에 여러 개의 권장 사항 단위가 배포되어 있는 경우, Adobe Commerce은 해당 단위로 반복되는 모든 제품을 필터링합니다. 다른 제품을 추천할 수 있는 공간을 만들기 위해 반복 제품에 대한 첫 번째 참조만 사용됩니다. Adobe Commerce은 이전에 구매한 제품과 장바구니에 있는 제품도 필터링합니다.

권장 사항 단위를 [만들기](create.md)할 때 권장 사항에 표시할 수 있는 제품을 제어하는 필터를 정의할 수 있습니다. 이러한 필터는 사용자가 정의하는 포함 또는 제외 조건 집합을 기반으로 합니다. 모든 포함 조건과 일치하는 제품만 권장 사항에 표시됩니다. 제외 조건과 일치하는 제품은 권장하지 않습니다.

각 필터 페이지에서 토글을 선택하여 여러 필터를 구성하고 원하는 필터만 활성화할 수 있습니다. 나중에 사용할 수 있도록 필터의 초안을 만들 수 있습니다. 각 탭에 활성화된 필터의 수가 표시됩니다.

## 조건

조건은 정적이거나 동적일 수 있습니다.

- 정적 조건은 기존 제품 속성을 사용하여 단위에 나타날 수 있는 제품을 결정합니다. 예를 들어 가격이 $25보다 큰 재고 제품만 단위에 나타나도록 지정할 수 있습니다. 정적 조건은 모든 페이지 유형에서 사용할 수 있습니다.

- 동적 조건은 현재 표시된 카테고리 또는 제품과 같은 구매자의 현재 컨텍스트를 기반으로 합니다. 예를 들어 제품 세부 사항 페이지에 배포할 제품 권장 사항을 생성할 때 현재 표시된 제품의 상대 가격 범위 내에 있는 제품만 추천하는 조건을 생성할 수 있습니다. 동적 조건은 홈 페이지를 제외한 모든 페이지 유형과 페이지 빌더와 함께 배치된 권장 사항이 있는 페이지에서 사용할 수 있습니다.

### 논리 연산자

논리 연산자 `AND` 및 `OR`을(를) 사용하여 여러 조건을 연결합니다. 포함 필터와 제외 필터를 모두 사용하는 경우, 먼저 포함을 평가하여 추천할 수 있는 모든 가능한 제품을 결정한 다음 제외 필터와 일치하는 제품은 목록에서 제거됩니다.

- `AND` - 두 개의 포함 필터링 조건 조인
- `OR` - 두 개의 제외 필터링 조건에 조인

>[!NOTE]
>
> 포함 및 제외 필터는 `magento/product-recommendations` 모듈의 버전 3.2.2 이상에서 기존 범주 제외를 대체합니다. Adobe Commerce 릴리스에 대한 자세한 내용은 [릴리스 정보](release-notes.md)를 참조하세요.

## 필터 유형 {#filtertypes}

![필터](assets/rec-conditions.png)

### 범주

[!BADGE PaaS만]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce 온 클라우드 프로젝트(Adobe 관리 PaaS 인프라) 및 온프레미스 프로젝트에만 적용됩니다."}

카테고리를 기반으로 제품을 필터링합니다. 범주 필터는 직접 범주 할당 및 해당 하위 범주를 사용합니다. 예를 들어 `Gear` 범주에 대한 제외 조건을 활성화하면 `Gear`에 할당된 제품과 `Gear/Bags` 또는 `Gear/Fitness Equipment`과(와) 같은 모든 하위 범주가 제외됩니다. 범주의 포함 필터에 대해서도 마찬가지입니다. 예를 들어 범주 `Gear`에 대한 포함 조건을 활성화하면 `Gear`에 할당된 제품과 `Gear/Bags` 또는 `Gear/Fitness Equipment`과(와) 같은 모든 하위 범주가 포함됩니다.

카테고리 필드에는 현재 스토어에 속한 카테고리가 표시됩니다.

>[!NOTE]
>
>B2B 판매자의 경우 범주 필터는 사용자가 구성한 [고객별 제품 범주](https://experienceleague.adobe.com/docs/commerce-admin/catalog/categories/category-permissions.html)를 준수합니다.

Adobe Commerce에서는 페이지 유형에 권장 사항을 배포할 때 다음 카테고리 필터 구성을 사용하는 것을 권장합니다.

| 페이지 | 필터링 기준 |
|---|---|
| 홈 | 제품을 필터링하지 마십시오. |
| 범주 | 특정 범주의 제품을 필터링합니다. |
| 제품 세부 사항 | 동일한 범주의 제품을 필터링합니다. |
| 장바구니 | 장바구니에 있는 제품 범주를 필터링합니다. |
| 주문 확인 | 구매한 제품의 범주를 필터링합니다. |

### 제품

제품 필터는 권장 사항에 표시할 적격 또는 부적격 제품을 지정합니다. 비활성화되거나 개별적으로 표시되지 않는 제품은 권장 사항에 표시되지 않으므로 선택할 수 없습니다.

>[!NOTE]
>
>구성 가능한 제품의 하위 제품은 _개별적으로 표시되지 않음_&#x200B;의 가시성을 가지므로 추천 단위에 표시되지 않습니다.

### 유형

[!BADGE PaaS만]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce 온 클라우드 프로젝트(Adobe 관리 PaaS 인프라) 및 온프레미스 프로젝트에만 적용됩니다."}

제품 유형에 따른 필터는 특정 유형의 모든 제품을 포함하거나 제외합니다. 지원되는 형식에는 _simple_, _configurable_, _virtual_, _downloadable_ 또는 _기프트 카드_&#x200B;가 있습니다. _번들_, _그룹화됨_ 및 사용자 지정 제품 유형은 지원되지 않습니다.

### 가시성

[!BADGE PaaS만]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce 온 클라우드 프로젝트(Adobe 관리 PaaS 인프라) 및 온프레미스 프로젝트에만 적용됩니다."}

가시성을 기준으로 제품을 필터링합니다(예: _카탈로그_, _검색_ 또는 둘 다).

### 가격

제품 가격을 기반으로 하는 필터는 최종 가격을 사용하여 비교를 수행합니다. 최종 가격에는 익명의 구매자가 이용할 수 있는 할인 또는 특별 가격이 포함됩니다. B2B 판매자의 경우 표시된 가격은 사용자가 구성한 [고객별 그룹 가격](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html)을 반영합니다.

### 재고 상태

다음 제외 필터를 사용하여 재고 상태에 따라 제품을 필터링할 수 있습니다.

- 품절 - (제외만 해당) 품절된 제품을 제외합니다.
- 재고 부족 - (제외만 해당) 재고 부족 제품은 제외합니다. 재고 부족 상태는 [재고 구성](https://experienceleague.adobe.com/docs/commerce-admin/config/catalog/inventory.html)의 _X만 남은 임계값_ 값을 기반으로 합니다.
