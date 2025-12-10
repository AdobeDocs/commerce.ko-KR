---
title: '[!DNL Storefront Popover]'
description: ' [!DNL Live Search storefront popover] 은(는) 추천 제품 및 썸네일을 동적으로 반환합니다.'
exl-id: 240a5333-15e9-4178-ba3c-ae6c62c2238c
source-git-commit: c6725fc524e9d239ccc0f16701e92ad5d2fc7729
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 0%

---

# [!DNL Storefront Popover]

[!DNL Live Search]이(가) [설치됨](install.md)인 경우 쇼핑객이 [!DNL popover]검색[&#x200B; 상자에 입력하면 상점 앞에 &#x200B;](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/search/search.html?lang=ko#quick-search)이(가) 표시됩니다. 각 문자를 입력하면 상위 검색 결과의 추천 제품 및 썸네일 이미지로 [!DNL popover]이(가) 업데이트됩니다.

[!DNL Live Search]이(가) 2자 이상의 쿼리에 대한 결과를 반환합니다. 부분 일치의 경우 단어 당 최대 문자 수는 20자입니다. &quot;입력할 때 검색&quot; 쿼리의 문자 수는 구성할 수 없습니다.

![[!DNL Live Search popover]](assets/storefront-search-as-you-type.png)

>[!TIP]
>
>[실시간 검색 설정](workspace.md) 문서에서 제품 특성을 검색 가능한 것으로 설정하는 방법을 알아봅니다.

## [!DNL Popover] 페이지 크기

[!DNL popover]의 페이지 크기는 자동 완성된 제품의 몇 줄을 반환할지 결정합니다. 실시간 검색을 설치하는 동안 `page_size` 값이 [카탈로그 검색](https://experienceleague.adobe.com/docs/commerce-admin/config/catalog/catalog.html?lang=ko) - `Autocomplete Limit` 설정의 현재 값으로 변경됩니다.

기본적으로 카탈로그 검색 - 자동 완성 제한 값은 8행(또는 행)으로 설정됩니다. [!DNL popover]의 페이지 크기를 변경하려면 다음을 수행하십시오.

1. *관리자* 사이드바에서 **스토어** > 설정 > **구성**(으)로 이동합니다.
1. 왼쪽 패널에서 **카탈로그**&#x200B;를 확장하고 설정 목록에서 **카탈로그**&#x200B;를 선택합니다.
1. *카탈로그 검색* 섹션을 확장합니다.
1. **자동 완성 제한**&#x200B;을(를) [!DNL popover]에서 허용할 줄 수로 설정하십시오.
1. 완료되면 **구성 저장**&#x200B;을 클릭하세요.

## [!DNL Popover] 예제 스타일링

회사의 스타일 및 브랜딩 지침에 맞게 [!DNL Popover] 위젯의 모양과 느낌을 사용자 지정할 수 있습니다.

[!DNL storefront popover]은(는) 항상 제품 `name` 및 `price`을(를) 표시하며 필드 선택을 구성할 수 없습니다. 그러나 [!DNL popover] 요소는 [CSS](https://developer.adobe.com/commerce/frontend-core/guide/css/) 클래스를 사용하여 스타일을 지정할 수 있습니다. 예를들어 다음 선언은 [!DNL popover] 컨테이너 및 바닥글의 배경색을 변경합니다.

```css
.livesearch.popover-container {
    background-color: lavender;
}

.livesearch.view-all-footer {
    background-color: magenta;
}
```

## 컨테이너 가시성

`.livesearch.popover-container`의 상위 구성 요소는 `.search-autocomplete`입니다.  `.active` 클래스는 컨테이너의 가시성을 나타냅니다. `.active`이(가) 열려 있으면 [!DNL popover] 클래스가 조건부로 추가됩니다.

```css
.search-autocomplete.active   /* visible */
.search-autocomplete          /* not visible */
```

Storefront 요소 스타일에 대한 자세한 내용은 [Frontend 개발자 안내서](https://developer.adobe.com/commerce/frontend-core/guide/css/)의 [CSS(Cascading Style Sheet)](https://developer.adobe.com/commerce/frontend-core/guide/)을 참조하세요.

## 클래스 선택기

다음 클래스 선택기를 사용하여 [!DNL popover]의 컨테이너 및 제품 요소의 스타일을 지정할 수 있습니다.

- `.livesearch.popover-container`
- `.livesearch.view-all-footer`
- `.livesearch.products-container`
- `.livesearch.product-result`
- `.livesearch.product-name`
- `.livesearch.product-price`

### 컨테이너 클래스 선택기

#### .livesearch.popover-container

![[!DNL Popover] 컨테이너](assets/livesearch-popover-container.png)

#### .livesearch.view-all-footer

![모든 바닥글 보기](assets/livesearch-view-all-footer.png)

### 제품 클래스 선택기

#### .livesearch.products-container

![제품 컨테이너](assets/livesearch-product-container.png)

#### .livesearch.product-result

![제품 결과](assets/livesearch-product-result.png)

#### .livesearch.product-name

![제품 이름](assets/livesearch-product-name.png)

#### .livesearch.product-price

![제품 가격](assets/livesearch-product-price.png)

#### .livesearch product-link

![제품 결과](assets/livesearch-product-link.png)

## 수정된 테마로 작업 {#working-with-modified-theme}

[!DNL storefront popover]Luma[에서 필요한 파일을 상속하는 사용자 지정된 &#x200B;](https://developer.adobe.com/commerce/frontend-core/guide/themes/)테마&#x200B;*와 함께*&#x200B;을(를) 사용할 수 있습니다. `top.search` 모듈의 `header-wrapper`에 있는 `Magento_Search` 블록은 수정하지 않아야 합니다.

```html
<referenceContainer name="header-wrapper">
   <block class="Magento\Framework\View\Element\Template" name="top.search" as="topSearch" template="Magento_Search::form.mini.phtml">
      <arguments>
         <argument name="configProvider" xsi:type="object">Magento\Search\ViewModel\ConfigProvider</argument>
      </arguments>
   </block>
</referenceContainer>
```

## [!DNL popover] 사용 안 함

[!DNL popover]을(를) 사용하지 않도록 설정하고 표준 [빠른 검색](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/search/search.html?lang=ko#quick-search) 기능을 복원하려면 다음 명령을 입력하십시오.

```bash
bin/magento module:disable Magento_LiveSearchStorefrontPopover
```

## Headless 구현

Headless 구현의 경우 [!DNL Live Search popover]npm 패키지[를 사용하여 &#x200B;](https://www.npmjs.com/package/@magento/ds-livesearch-storefront-utils)을(를) 설치할 수 있습니다.
