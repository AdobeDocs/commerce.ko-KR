---
title: 경계 및 제한
description: 비즈니스 요구 사항을 충족하도록  [!DNL Product Recommendations] 의 경계 및 제한에 대해 알아봅니다.
role: Admin, Developer
source-git-commit: 66830c9d950a27269aca1bda0dcc7d0d86f05647
workflow-type: tm+mt
source-wordcount: '848'
ht-degree: 0%

---

# 경계 및 제한

[!DNL Product Recommendations]이(가) 비즈니스의 요구 사항을 충족하는지 확인하려면 다음 경계 및 제한을 검토하십시오. 이러한 제약 조건을 이해하면 구현을 계획하고, 필터를 구성하고, 일반적인 문제를 방지하는 데 도움이 됩니다.

## 일반

- **제품 유형** - 지원되는 제품 유형은 _단순_, _구성_, _가상_, _다운로드 가능_ 및 _기프트 카드_&#x200B;입니다. _번들_, _그룹화됨_ 및 사용자 지정 제품 유형은 지원되지 않습니다. 카탈로그에 지원되지 않는 제품 유형이 많이 포함된 경우 낮은 [준비 점수](create.md#readiness-indicators)를 기대할 수 있습니다. [제품 유형별 필터링](filters.md#type)을 참조하세요.
- 공백이 있는 **SKU** - 공백이 포함된 SKU는 권장 사항 관련성을 줄일 수 있으므로 가능한 한 피해야 합니다.
- **장바구니 페이지** - 장바구니에 제품을 추가한 후 바로 장바구니 페이지를 표시하도록 스토어가 [구성되어 있으면 장바구니 페이지에서 제품 권장 사항이 지원되지 않습니다](https://experienceleague.adobe.com/ko/docs/commerce-admin/stores-sales/point-of-purchase/cart/cart-configuration). [권장 사항 만들기](create.md)를 참조하세요.
- **하위 제품** - 구성 가능한 제품의 하위 제품(가시성 _개별적으로 표시되지 않음_)이 권장 단위에 표시되지 않습니다. 구성 가능한 (상위) 제품만 나타날 수 있습니다. [제품 필터링](filters.md#product)을 참조하세요.
- **비활성화되거나 개별적으로 표시되지 않는 제품** - 비활성화되거나 개별적으로 표시되지 않는 제품은 권장 사항에 표시할 수 없으며 제품 필터에서 선택할 수 없습니다.
- 시작 날짜와 종료 날짜가 포함된 **특별 가격** - [특별 가격](https://experienceleague.adobe.com/ko/docs/commerce-admin/catalog/products/pricing/product-price-special)은(는) 추천 단위에서 지원되지 않습니다. 특별 가격이 있는 제품은 권장 사항에 표시될 수 있지만 단위에 특별 가격, 시작 날짜 또는 종료 날짜가 표시되지 않습니다. 구매자는 제품 페이지를 열 때까지 일반 가격(또는 카탈로그/가격 피드에서 제공한 기타 가격 데이터)을 확인합니다.

## 추천 단위

- **페이지 유형당 활성 단위** - 각 페이지 유형(홈, 범주, 제품 세부 사항, 장바구니, 확인)에 대해 최대 50개의 활성 권장 사항 단위를 만들 수 있습니다. 제한에 도달하면 만들기 플로우에서 페이지 유형이 회색으로 표시됩니다.
- **단위당 제품** - 추천 단위에 표시되는 제품 수는 5(기본값)에서 최대 20개로 설정할 수 있습니다.
- **초안 상태** - 권장 사항을 초안으로 저장한 후에는 해당 단위에 대한 페이지 유형이나 권장 사항 유형을 수정할 수 없습니다. 활성화하기 전에 다른 설정을 편집할 수 있습니다.

## 필터 및 조건

- **동적 조건** - 홈 페이지를 제외한 모든 페이지 유형에서 동적 조건(예: &quot;현재 제품과 동일한 범주의 제품&quot; 또는 &quot;상대적 가격 범위&quot;)을 사용할 수 있습니다. 권장 사항이 Page Builder와 함께 배치된 페이지에서도 사용할 수 없습니다. [조건](filters.md#conditions)을 참조하세요.

## 미리보기 및 비프로덕션 환경

- **최근에 본 항목 미리 보기** - _최근에 본 항목_ 권장 사항 유형은 데이터가 브라우저 기록을 기반으로 하며 관리자 컨텍스트에서 사용할 수 없으므로 관리자에서 미리 볼 수 없습니다. [권장 사항 미리 보기](create.md#preview)를 참조하세요.
- **다른 데이터 공간의 권장 사항** - [다른 SaaS 데이터 공간에서 권장 사항을 가져올 때](settings.md)(예: 프로덕션)비프로덕션 상점 앞에서는 권장 사항을 볼 수 있지만 제품 페이지를 클릭스루할 수는 없습니다. 이는 미리 보기 및 테스트를 위한 디자인입니다.
- **GraphQL 및 대체 데이터 공간** - [GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/)을(를) 통해 제품 권장 사항을 사용할 때 `alternateEnvironmentId` 매개 변수(다른 데이터 공간에서 권장 사항을 가져오는 데 사용됨)를 사용할 수 없습니다. REST API 또는 관리 설정 을 사용하여 비프로덕션에서 권장 사항 소스를 전환합니다.

## API 및 구성

- **API 키(4.x 이상)** - 샌드박스와 프로덕션 환경 모두에 공개 및 비공개 API 키를 제공해야 합니다. 두 쌍의 API 키를 모두 제공하지 않으면 관리자에서 제품 권장 사항 기능에 액세스할 수 없습니다. 상점 및 기존 권장 사항에 대한 데이터 수집은 계속 작동합니다. [설치 및 구성](install-configure.md)을 참조하세요.

## 쿠키 제한

- [쿠키 제한 모드](setting-cookie.md)가 활성화되어 있고 쇼핑객이 쿠키를 수락하지 않은 경우 행동 데이터를 사용하는 특정 권장 사항 유형이 표시되지 않거나 제한된 결과를 표시할 수 있습니다.
- 동작 데이터에 의존하지 않는 권장 사항 유형(예: _가장 많이 본 항목_, _시각적 유사성_)은 쿠키 제한이 활성화된 경우에도 계속 작동합니다.
- 쿠키 제한이 활성화되면, 제품 권장 사항은 구매자의 동의가 있을 때까지 쿠키 또는 로컬 저장소에 행동 데이터를 수집하거나 저장하지 않습니다.

## 페이지 빌더

- **지표 및 스토어 보기** - Page Builder 권장 사항 단위에 대한 지표는 제품 권장 사항 작업 영역의 기본 스토어 보기에만 표시됩니다. 기본이 아닌 저장소 보기에서 Page Builder 권장 사항 지표를 보려면 해당 저장소 보기에서 Page Builder 권장 사항 단위를 열고 [편집](edit.md)한 후 저장해야 합니다. 그런 다음 해당 저장소 보기에 대한 지표가 나타납니다. [페이지 빌더 통합](page-builder.md)을 참조하세요.

## B2B

- 제품 권장 사항에는 [범주 권한](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/categories/category-permissions.html), [공유 카탈로그](https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/shared-catalogs/catalog-shared.html) 및 고객 그룹별 가격이 적용됩니다. 구매자는 세그먼트 및 카탈로그 할당에 따라 액세스할 수 있는 제품에 대한 권장 사항만 봅니다. [온보딩](onboarding.md)을 참조하세요.

## 데이터 및 준비

- **동작 데이터** - 많은 추천 형식에는 충분한 상점 동작 데이터(보기, 장바구니에 추가, 구매)가 필요합니다. 새로운 저장소 또는 트래픽이 적은 저장소는 적절한 데이터가 수집될 때까지 해당 유형에 대한 결과가 제한되거나 없을 수 있습니다. 관리자의 [준비 표시기](create.md#readiness-indicators)를 모니터링합니다.
- **프로덕션 데이터가 없는 스테이징** - 동작 데이터가 없는 비프로덕션 환경에서 프로덕션에서 가져오지 않고 테스트할 수 있는 유일한 권장 사항 형식은 _이와 같음_&#x200B;이며, 카탈로그 기반 유사성만 사용합니다. [스테이징 환경](staging-environment.md)을 참조하세요.

## 문제 해결

카탈로그 동기화에 대한 도움말, 표시되지 않는 권장 사항 또는 기타 일반적인 문제를 보려면 [Commerce 기술 자료](https://experienceleague.adobe.com/ko/docs/commerce-knowledge-base/kb/overview)를 검색하거나 [지원](https://experienceleague.adobe.com/ko/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide)에 문의하세요.
