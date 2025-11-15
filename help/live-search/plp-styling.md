---
title: 제품 목록 페이지 위젯
description: ' [!DNL Live Search Product Listing Page Widget] 사용 및 스타일링'
exl-id: 50ba8046-869a-4071-b3a3-a6392544c07b
source-git-commit: 7684d5cded63f2b0805ee307dff77932607c47eb
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 0%

---

# 제품 목록 페이지 위젯

[!DNL Live Search Product Listing Page Widget]&#x200B;(PLP)은 Commerce 서비스 플랫폼을 사용하여 성능 좋고, 검색 가능하며, 패싯 가능한 제품 목록 페이지를 제공합니다. 이 항목에서는 PLP 위젯을 활성화하고 스타일링하는 방법을 설명합니다.

## PLP 위젯 활성화

[!DNL Live Search] 서비스가 설치되면 기본 검색 기능이 자동으로 [!DNL Live Search]&#x200B;(으)로 변환됩니다.

새 설치에 대해 [!DNL Live Search] PLP 위젯이 기본적으로 활성화됩니다.

[!DNL Live Search]을(를) 업그레이드하고 있으며 PLP 위젯이 이미 꺼져 있는 경우 그대로 유지됩니다. 켜려면:
1. → Adobe Commerce 관리자에서 저장소 설정 → 구성으로 이동합니다.
1. 왼쪽 탐색에서 **[!UICONTROL Live Search]** > **[!UICONTROL Storefront Features]**&#x200B;을(를) 클릭합니다.
1. [!UICONTROL Storefront Features] 섹션을 클릭합니다.
1. [!UICONTROL Enable Product Listing Widget] = 예 설정
1. 구성 저장
1. 메시지가 표시되면 캐시를 플러시합니다( 시스템 > 도구 > 캐시 관리 > [!UICONTROL Flush Magento Cache]&#x200B;(으)로 이동).

>[!IMPORTANT]
>
>[!DNL Live Search Product Listing Page Widget]이(가) 활성화되면 제품 목록 페이지의 정렬 순서 방향을 변경할 수 없습니다.

## 위젯 기능

PLP 위젯은 다음과 같은 기본 기능을 제공합니다.

- 장바구니에 추가 버튼 - 간단한 제품에만 사용할 수 있습니다.
- 제품당 여러 이미지 - 구성 가능한 제품에 대해 다른 색상을 선택하면 이미지가 변경될 수 있습니다.
- 색상 견본 지원 - 코드의 유효성을 제대로 검사하려면 색상 특성의 맞춤법이 `color`이어야 합니다.

### 위젯 사용자 정의

PLP 위젯의 기본 기능 외에도 다음과 같은 기능을 포함하도록 위젯을 추가로 사용자 정의할 수 있습니다.

- 속성별 필터링
- 다중 언어 지원
- 가격 슬라이더

위의 기능을 처리하기 위해 PLP 위젯을 사용자 정의하는 방법에 대한 자세한 내용은 다음 `storefront-product-listing-page`repository[의 ](https://github.com/adobe/storefront-product-listing-page/) 추가 정보를 참조하십시오. 이 저장소의 추가 정보는 PLP 위젯을 사용자 정의하고 이러한 사용자 정의를 사이트에 배포하는 방법에 대한 예를 제공합니다.

>[!WARNING]
>
>리포지토리에서 사용할 수 있는 코드를 사용하여 PLP 위젯을 사용자 정의하는 경우 유지 관리와 필요한 모든 업데이트를 수행해야 합니다. Adobe이 릴리스하는 모든 새로운 PLP 위젯 기능은 사용자 지정된 구현과 호환되지 않을 수 있습니다.

## 스타일 예

[CSS](https://developer.adobe.com/commerce/frontend-core/guide/css/)를 사용하여 사이트에 맞게 PLP 위젯의 모양과 느낌을 사용자 지정할 수 있습니다.

>[!NOTE]
>
>Adobe Commerce 테마 내에 사용자 지정 클래스가 있는 요소는 상속되지 않습니다. 사용자 정의 클래스와 일치하도록 이러한 요소를 특정 클래스에서 타깃팅해야 합니다. 기본 작업 클래스는 위젯 단추에서 작동하지 않습니다. CSS 내의 제네릭 타깃팅된 요소는 상속됩니다. `button`은(는) 위젯 단추에 적용됩니다.

강조 표시된 div에 대상 클래스 `ds-sdk-product-item__product-name`이(가) 포함되어 있습니다.

![페이지 매김](assets/plp-css-example.png)

제품 이름을 대문자로 만드는 규칙을 추가하여 사용자 지정합니다.

```css
.ds-sdk-product-item__product-name {
 text-transform: uppercase;
}
```

![페이지 매김](assets/plp-css-example-after.png)

## CSS 클래스

### 제품 목록

- `.ds-sdk-product-list`: 외부 div
- `.ds-sdk-product-list__grid`: 내부 div

![페이지 매김](assets/plp-css-product-list.png)

#### 제품 목록 페이지 매김

- `.ds-plp-pagination`

![페이지 매김](assets/plp-css-pagination.png)

- `.ds-plp-pagination_item`

![페이지 매김 항목](assets/plp-css-pagination-item.png)

- `.ds-plp-pagination_item--current`

![현재 항목 페이지 매김](assets/plp-css-pagination-item-current.png)

### 위젯

- `.ds-widgets`: 외부 div
- `.ds-widgets__actions`: 왼쪽 내부 div
- `.ds-widgets__results`: 오른쪽 내부 div

![위젯 결과](assets/plp-css-widgets.png)

### 정렬 드롭다운

- `.ds-sdk-sort-dropdown`

![드롭다운 정렬](assets/plp-css-dropdown.png)

- `.ds-sdk-sort-dropdown__button`

![드롭다운 단추](assets/plp-css-dropdown-button.png)

- `.ds-sdk-sort-dropdown__items`

![드롭다운 항목](assets/plp-css-dropdown-items.png)

- `.ds-sdk-sort-dropdown__items--item`

![드롭다운 항목](assets/plp-css-dropdown-item.png)

- `.ds-sdk-sort-dropdown__items--item-selected`

![선택한 항목 드롭다운](assets/plp-css-dropdown-selected.png)

- `.ds-sdk-sort-dropdown__items--item-active`

![드롭다운 활성 선택](assets/plp-css-dropdown-active.png)

### 패싯

- `.ds-plp-facets`
- `.ds-plp-facets__header`
- `.ds-plp-facets__header_title`
- `.ds-plp-facets__header__clear-all`

![패싯 헤더 제목](assets/plp-css-facets-title-clear.png){width="350"}

- `.ds-plp-facets__pills`
- `.ds-sdk-pill`

![패싯 알약](assets/plp-css-facets-pill.png){width="350"}

- `.ds-sdk-pill__label`
- `.ds-sdk-pill__cta`

![패싯 레이블](assets/plp-css-pill-label-cta.png){width="350"}

- `.ds-plp-facets__list`

![패싯 목록](assets/plp-css-facets-list.png){width="350"}

- `.ds-sdk-input`
- `.ds-sdk-input__label`
- `.ds-sdk-product-item__product-swatch-group`
- `ds-sdk-product-item__product-swatch-item`
- `.ds-sdk-input_fieldset_show-more`

![입력](assets/plp-css-sdk-input.png)

- `.ds-sdk-labelled-input`

![레이블이 지정된 입력](assets/plp-css-labelled-input.png)

- `.ds-sdk-labelled-input__input`
- `.ds-sdk-labelled-input__label`

![입력 레이블](assets/plp-css-labelled-input-label.png)

### 제품 항목

- `.ds-sdk-product-item`
- `.ds-sdk-product-item__image`
- `.ds-sdk-product-item__product-name`
- `.ds-sdk-product-item__product-options`
- `.ds-sdk-product-price`
   - `.ds-sdk-product-price--no-discount`
   - `.ds-sdk-product-price--grouped`
   - `.ds-sdk-product-price--bundle`
   - `.ds-sdk-product-price--discount`

![제품](assets/plp-css-product.png)

### 로드 중

- `.ds-sdk-loading`
- `.ds-sdk-loading__spinner`
- `.ds-sdk-loading__spinner-label`

![표시기 로드](assets/plp-css-loading.png)

## PLP 위젯 비활성화

PLP 위젯을 비활성화하려면 다음과 같이 하십시오.

1. **스토어** > 설정 > **구성** > **[!DNL Live Search]** > **상점 기능**(으)로 이동하여 **제품 목록 위젯 사용**&#x200B;을(를) &quot;아니요&quot;로 설정합니다.
1. 설정을 저장하려면 **구성 저장**&#x200B;을 선택하십시오.
