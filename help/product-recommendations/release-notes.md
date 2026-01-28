---
title: '[!DNL Product Recommendations] 릴리스 정보'
description: Adobe Commerce의  [!DNL Product Recommendations] 에 대한 최신 릴리스 정보입니다.
feature: Services, Recommendations, Release Notes
exl-id: 37404605-5b62-4c71-90d1-4f09e6105c4b
source-git-commit: 09a0d46688da848881fe70c2b1292b9831411136
workflow-type: tm+mt
source-wordcount: '1935'
ht-degree: 0%

---

# [!DNL Product Recommendations] 릴리스 정보

릴리스 노트에는 다음 [!DNL Product Recommendations] 모듈에 대한 업데이트가 포함되어 있습니다.

* [!DNL Product Recommendations] 메타패키지: `magento/product-recommendations`
* [!DNL Product Recommendations]&#x200B;(선택 사항) 모듈의 페이지 빌더 지원: `magento/module-page-builder-product-recommendations`
* [!DNL Product Recommendations]&#x200B;(선택 사항) 모듈에 대한 시각적 유사성 권장 사항 유형 지원: `magento/module-visual-product-recommendations`

최신 릴리스 버전에 대한 지원이 제공됩니다. 이전 버전에 대한 릴리스 노트는 참조를 위해 제공됩니다.
릴리스 노트는 다음과 같습니다.

새 기능 ![개](../assets/new.svg)개
![수정](../assets/fix.svg) 수정 사항 및 개선 사항
![버그](../assets/bug.svg) 알려진 문제

개발자 설명서를 참조하여 [제품 지원에 대해 알아보세요](https://experienceleague.adobe.com/en/docs/commerce-operations/release/product-availability).

## 호스팅된 서비스 업데이트

이 참고 사항에서는 버전이 지정된 릴리스 또는 호스팅된 서비스에 대한 개선 사항 외부에서 게시되거나 발견된 업데이트 또는 알려진 문제에 대해 설명합니다.

_2025년 11월 19일_

![새로 만들기](../assets/new.svg) 이제 각 페이지 유형에 대해 최대 50개의 활성 권장 사항 단위를 만들 수 있습니다. 이전에는 5개로 제한되었습니다.

_2025년 10월 1일_

![새로 만들기](../assets/new.svg) 고객이 로그인한 데이터에 대해 이름이 `ds-logged-in`인 새 데이터 저장소 키를 추가했습니다.

_2025년 1월 31일_

![새로 만들기](../assets/new.svg) 테스트 환경에서 쿼리되지 않은 카탈로그 데이터에 대한 새 데이터 보존 정책이 있습니다. [자세히 알아보기](overview.md#catalog-data-retention-policy)

_2024년 6월 28일_

장바구니 페이지의 ![ 장치에서 장바구니에 추가한 ](../assets/bug.svg)버그[!DNL Product Recommendations] 제품은 장바구니 페이지가 다시 로드될 때 권장 제품 목록에서 제거되지 않습니다.
장바구니에서 제거된 ![버그](../assets/bug.svg) 제품은 장바구니 페이지가 다시 로드될 때까지 `cartSkus` 배열에서 계속 유지됩니다.

_2023년 7월 18일_

이제 ![새](../assets/new.svg) [!DNL Product Recommendations]에 GraphQL [`recommendations`](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/) 쿼리가 있습니다.

_2023년 4월 25일_

![신규](../assets/new.svg) [!DNL Product Recommendations] 고객은 이제 [SaaS 가격 인덱싱](../price-index/price-indexing.md)를 이용할 수 있습니다.

## 현재 메이저 버전

### 6.6.0 magento/product-recommendations

_2026년 1월 28일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새로 만들기](../assets/new.svg) 종속성이 [데이터 피드 동기화 상태 모니터링 대시보드](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status)에 추가되었습니다. 이 대시보드를 사용하면 제품 및 카테고리 데이터를 Commerce에서 제품 추천과 같은 외부 서비스로 전송하는 데이터 내보내기 피드의 상태와 성능에 대한 실시간 인사이트를 볼 수 있습니다.

### 이전 버전

### 6.5.0 magento/product-recommendations

_2025년 11월 3일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![수정](../assets/fix.svg) 제품 추천 단위가 다른 환경에서 상호 작용하는 방법을 개선했습니다.

### 6.4.0 magento/product-recommendations

_2025년 9월 17일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![수정](../assets/fix.svg) 로컬 저장소 데이터를 사용할 수 없을 때 JavaScript 오류로 인해 제품 추천 단위가 사라지는 간헐적인 문제를 해결했습니다. 이 수정 사항으로 로컬 저장소에 `ds-view-history-time-decay`이(가) 누락된 경우 PREX에서 더 이상 오류가 발생하지 않습니다.
![새로 만들기](../assets/new.svg)에서 `recommendations-sdk`에 대한 CDN URL을 `adobe.io` 도메인으로 업데이트했습니다.

### magento/product-recommendations 6.3.0

_2025년 9월 5일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새로 만들기](../assets/new.svg) [제품 권장 사항 작업 영역](page-builder.md)에서 기본이 아닌 저장소 보기에서 만든 [PageBuilder 권장 사항 단위](workspace.md)에 대한 지표를 표시할 수 있는 지원이 추가되었습니다.
![새](../assets/new.svg) 제품 권장 사항은 이제 제한을 사용하도록 설정할 때 쿠키/로컬 저장소에 데이터 수집 및 저장을 금지하여 [쿠키 제한 모드](setting-cookie.md)를 완전히 준수합니다.

### magento/제품 권장 사항 6.2.1

_2025년 7월 14일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![수정](../assets/fix.svg): [권장 사항 미리 보기](./create.md#preview-recommendations) 패널을 개선했습니다.

### magento/product-recommendations 6.2.0

_2025년 4월 4일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새로 만들기](../assets/new.svg) `recommendations-admin-ui`에 대한 CDN URL을 `adobe.io` 도메인에 업데이트했습니다.

### magento/product-recommendations 6.1.0

_2025년 3월 11일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새로 만들기](../assets/new.svg)에서 PHP 8.4 지원을 추가했습니다.

### magento/product-recommendations 6.0.3

_2024년 11월 6일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![수정](../assets/fix.svg) [범주 필터](filters.md#category)에 현재 저장소 보기에 속하지 않는 범주가 포함된 문제가 해결되었습니다.
![수정](../assets/fix.svg) `magento/product-recommendations` 메타패키지에서 종속성 문제를 해결했습니다.

### magento/product-recommendations 6.0.2

_2024년 5월 9일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![수정](../assets/fix.svg) 제품 추천 장치에서 간단한 제품의 **[!DNL Add to Cart]** 단추를 클릭하면 구매자가 현재 페이지에 머무르지 않고 홈 페이지로 리디렉션되는 문제가 해결되었습니다.
![버그](../assets/bug.svg) `referenceBlock` XML 파일의 `ProductRecommendations Layout` 요소로 인해 유효성 검사 오류가 발생했습니다.

### magento/제품 권장 사항 6.0.1

_2024년 3월 19일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새로 만들기](../assets/new.svg)에서 PHP 8.3 지원을 추가했습니다.

### magento/제품 권장 사항 6.0.0

_2024년 2월 22일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새로 만들기](../assets/new.svg) 이제 [!DNL Catalog Sync Dashboard]이(가) [[!DNL Data Management Dashboard]](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard)입니다. 이렇게 개조된 대시보드는 [!DNL Product Recommendations], [!DNL Live Search] 및 [!DNL Catalog Service]의 데이터 스트림에 대한 통찰력을 제공합니다.
![수정](../assets/fix.svg) [!DNL Product Recommendations]에 대해 체크아웃 오류가 발생하는 문제를 해결했습니다.

+++5.0.0 및 이전

### magento/product-recommendations 5.0.1

_2023년 9월 15일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새로 만들기](../assets/new.svg) [Saas 가격 인덱서](../price-index/price-indexing.md)를 지원하는 새 모듈을 추가했습니다.
![새로 만들기](../assets/new.svg) 번들 제품 및 기프트 카드를 포함하여 더 많은 제품 형식을 내보내는 것을 지원하기 위해 새로운 데이터 내보내기 모듈을 추가했습니다.
![수정](../assets/fix.svg) 제품 및 가격 피드의 테이블 크기가 크게 줄었습니다. 표 `catalog_data_exporter_products` 및 `catalog_data_exporter_product_prices`에 크기가 상당히 감소해야 합니다.

#### 알려진 제한 사항

* 밑줄(_)이 포함된 경우 `websiteCode` 값이 잘못 반환됩니다.

### magento/product-recommendations 5.0.0

_2023년 3월 20일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새로 만들기](../assets/new.svg) Adobe Commerce 2.4.6을 지원하도록 [!DNL Product Recommendations]을(를) 업데이트했습니다.
![새로 만들기](../assets/new.svg) 주요 버전 릴리스입니다. 프로젝트의 루트 [ 파일을 ](install-configure.md#update)편집`composer.json`합니다.
![새로 만들기](../assets/new.svg) [!DNL Product Recommendations]은(는) 이제 Commerce(이전에는 Multi-Source Inventory 또는 MSI로 알려짐)에서 전체 [Inventory management](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/introduction) 기능을 지원합니다. 전체 지원을 활성화하려면 종속성 모듈 [을(를) 버전 102.2.0+로 ](install-configure.md#update)업데이트`commerce-data-export`해야 합니다.

### magento/제품 권장 사항 4.0.1

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![수정](../assets/fix.svg) 이전에는 표시 통화가 기본값이 아닌 통화로 전환되면 [!DNL Product Recommendations]에 오류가 표시되었습니다. 이제 통화 전환이 제대로 작동합니다.

### magento/제품 권장 사항 4.0.0

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새로 만들기](../assets/new.svg) 각 권장 사항 유형의 교육 진행률을 시각화하는 데 도움이 되도록 [준비 지표](create.md)를 추가했습니다.
![새로 만들기](../assets/new.svg) 주요 버전 릴리스입니다. 프로젝트의 루트 [ 파일을 ](install-configure.md#update)편집`composer.json`합니다. 또한 이 릴리스에서는 [!DNL Product Recommendations]을(를) 설치 및 구성할 때 두 개의 API 키([프로덕션 키 및 샌드박스 키](../landing/saas.md))를 제공해야 합니다.

#### 알려진 제한 사항

* 밑줄(_)이 포함된 경우 `websiteCode` 값이 잘못 반환됩니다.

### magento/product-recommendations 3.3.7

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.x 이상

![새로 추가](../assets/new.svg) PHP 8.1 지원 추가됨
![새로 만들기](../assets/new.svg) 이미지 크기 조정이 참조 표시 템플릿에서 보다 일관되게 처리되도록 이미지 크기 조정이 개선되었습니다.

### magento/product-recommendations 3.3.6

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.x 이상

![새로 만들기](../assets/new.svg) 종속성을 명시적으로 나열하여 [!DNL Product Recommendations] 메타패키지를 최적화했습니다.

### magento/product-recommendations 3.3.5

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.x 이상

![새로 추가](../assets/new.svg) [에 ](onboarding.md#b2bsupport)B2B 지원[!DNL Product Recommendations]이 추가됨
Commerce ![새로 만들기](../assets/new.svg) 명령줄을 통해 [카탈로그 데이터 동기화](https://experienceleague.adobe.com/en/docs/commerce/user-guides/data-services/catalog-sync)에 새 피드를 추가했습니다.

### magento/product-recommendations 3.3.3

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.x 이상

![새로 만들기](../assets/new.svg) 새 [권장 사항 유형](type.md) 추가: 전환(장바구니로 보기), 전환(구매로 보기) 및 최근에 본 항목. 이러한 새로운 권장 사항 유형은 `magento/product-recommendations` 모듈 3.2.2 이상에서 사용할 수 있습니다.
![수정](../assets/fix.svg) Fastly의 웹 응용 프로그램 방화벽(WAF)에서 쿠키를 잘못 차단하는 문제를 해결했습니다
![수정](../assets/fix.svg) 특정 스토어 보기에 대한 권장 사항을 만들 때 기본값이 아닌 스토어 보기에 할당된 제품이 _권장 사항 제품 미리 보기_ 패널에 표시되지 않는 문제가 해결되었습니다
![수정](../assets/fix.svg) 페이지 빌더의 특정 권장 사항 단위 이름이 권장 사항 단위를 상점 앞에 표시하지 못하게 하는 문제가 해결되었습니다

### magento/product-recommendations 3.3.2

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.x 이상

![수정](../assets/fix.svg) B2B 지원에 대한 누락된 종속성을 해결했습니다.

### magento/product-recommendations 3.3.1

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.x 이상

![새로 만들기](../assets/new.svg) B2B 고객 그룹 가격에 대한 지원이 추가되었습니다. 추천 단위에서 [가격 필터](filters.md)를 설정하면 로그인한 B2B 고객은 표시된 제품에 대해 설정된 고객 그룹 가격을 볼 수 있습니다.

### magento/product-recommendations 3.3.0

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.x 이상

![새로 만들기](../assets/new.svg) Adobe 기능 및 서비스 전반에 걸쳐 동작 데이터 수집을 표준화하기 위해 Adobe Commerce 클라이언트 데이터 레이어에 대한 지원을 추가했습니다. 자세한 내용은 [readme](https://github.com/adobe/commerce-events/blob/main/packages/storefront-events-collector/README.md)을(를) 참조하십시오.

### magento/product-recommendations 3.2.6

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.x 이상

![수정](../assets/fix.svg) JavaScript 모달 오류를 수정했습니다.
![수정](../assets/fix.svg) Fastly의 웹 응용 프로그램 방화벽(WAF)에서 쿠키를 잘못 차단하는 문제를 해결했습니다

### magento/product-recommendations 3.2.5

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.x 이상

![새로 만들기](../assets/new.svg) Magento 서비스의 이름이 [Commerce 서비스](https://experienceleague.adobe.com/en/docs/commerce/user-guides/integration-services/saas)&#x200B;(으)로 변경되었으며 관리자의 사용성이 개선되었습니다.

### magento/product-recommendations 3.2.4

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.x 이상

![수정](../assets/fix.svg) 제품 특성을 색인화할 때 &quot;구성 가능한 제품 옵션 데이터를 검색할 수 없음&quot; 오류를 수정했습니다.

### magento/product-recommendations 3.2.3

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.x 이상

![수정](../assets/fix.svg) 카탈로그 동기화 중 &quot;구성 가능한 제품 옵션 데이터를 검색할 수 없음&quot; 오류를 수정했습니다.
![수정](../assets/fix.svg) &quot;URL에 저장소 코드 추가&quot; 구성을 사용하도록 설정할 때 저장소 코드가 올바르게 설정되지 않는 문제를 해결했습니다
![수정](../assets/fix.svg) 관리 패널 구성 변경 내용을 검색하여 이러한 변경 내용이 카탈로그 동기화 데이터에 반영되도록 합니다

### magento/product-recommendations 3.2.2

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.x 이상

![새로 만들기](../assets/new.svg)이(가) 만들 때 [추천 결과를 미리 보기](create.md)하는 기능을 추가했습니다. 이렇게 하려면 모듈을 최신 버전으로 업데이트해야 할 수 있습니다.
![새로 만들기](../assets/new.svg) 관리자가 카탈로그 동기화 프로세스를 [모니터링 및 관리](https://experienceleague.adobe.com/en/docs/commerce/user-guides/data-services/catalog-sync)하는 기능을 추가했습니다.
![새로 만들기](../assets/new.svg) 권장 사항에 표시되는 제품을 제어하기 위해 [필터](filters.md)을 추가했습니다.
![새로 만들기](../assets/new.svg)에서 [시각적 유사성](type.md#visualsim) 권장 사항 형식을 추가했습니다.

### 페이지 빌더를 위한 magento/module-page-builder-product-recommendations 1.2.1

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.x 이상

![새로 만들기](../assets/new.svg) `magento/product-recommendations` 모듈의 3.2.0 이상 버전에 대한 지원을 추가했습니다.

### magento/product-recommendations 3.1.0

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.x 이상

![새로 만들기](../assets/new.svg) 명령줄을 통해 카탈로그를 SaaS 서비스에 [다시 동기화](https://experienceleague.adobe.com/en/docs/commerce/user-guides/data-services/catalog-sync)하는 기능이 추가되었습니다.
![새로 만들기](../assets/new.svg) 데이터베이스 테이블 접두사에 대한 지원을 추가했습니다.
![수정](../assets/fix.svg) PHP 7.1 지원을 제거함

### magento/product-recommendations 3.0.8

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.x 이상

![수정](../assets/fix.svg) 모듈이 구성되기 전에 데이터 수집을 위해 이벤트가 전송되어 잘못된 트래픽이 발생하는 문제를 해결했습니다

### magento/product-recommendations 3.0.6

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.x 이상

![새로 만들기](../assets/new.svg) **(Beta)** 새 [시각적 유사성](type.md#visualsim) 권장 사항 유형에 대한 지원이 포함되어 있습니다.

### magento/module-visual-product-recommendations 1.0.0

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.x 이상

![새로 만들기](../assets/new.svg) **(Beta)** [시각적 유사성](type.md#visualsim). _시각적 유사성_ 권장 사항 유형을 사용하면 보고 있는 제품과 시각적으로 유사한 제품을 표시하는 제품 세부 사항 페이지에 권장 사항 단위를 배포할 수 있습니다.

### magento/product-recommendations 3.0.5

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.x 이상

![수정](../assets/fix.svg) 카탈로그 내보내기 중에 발생할 수 있는 &quot;제품 옵션 데이터를 검색할 수 없음&quot; 오류를 수정했습니다.
![수정](../assets/fix.svg) 이제 _대시보드의_&#x200B;수입&#x200B;_[!DNL Product Recommendations]_열에 있는 통화 기호가 구성된 기본 통화를 올바르게 반영합니다.

### magento/product-recommendations 3.0.4

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.x 이상

![수정](../assets/fix.svg) Adobe Commerce 2.4.0에 대한 지원을 추가했습니다.

### magento/product-recommendations 3.0.3

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.x 이상

![수정](../assets/fix.svg) storefront 템플릿의 기호 구현이 개선되었습니다

### 페이지 빌더를 위한 magento/module-page-builder-product-recommendations 1.0.4

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.x 이상

![새로 만들기](../assets/new.svg) 페이지 빌더 콘텐츠 형식을 편집할 때 제품 추천 이름을 추가했습니다.

### 3.0.2 magento/product-recommendations

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.x 이상

![새로 만들기](../assets/new.svg) 페이지 빌더에서 추천 단위를 선택할 때 그리드에 상태 열을 추가했습니다.
![수정](../assets/fix.svg) 제품 및 이미지 URL에서 잘못된 http/https 프로토콜 관련 문제를 해결했습니다

### magento/product-recommendations 3.0.1

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.x 이상

주요 버전 릴리스입니다. 프로젝트의 루트 작성기.json 파일을 [편집](install-configure.md#update)합니다.

![새로 만들기](../assets/new.svg) 대체 SaaS 데이터 공간에서 [!DNL Product Recommendations]을(를) 가져옵니다. 이를 통해 다른 비프로덕션 환경의 제품 환경에서 계산된 [!DNL Product Recommendations]을(를) 사용할 수 있습니다. [SaaS 데이터 공간 전환](settings.md)에서 이 기능에 대해 자세히 설명합니다.

![수정](../assets/fix.svg) uBlock 원본을 사용하여 구매자가 체크아웃할 수 없는 문제를 해결했습니다
![수정](../assets/fix.svg) 외부 장바구니 추가 이벤트를 전송하는 문제를 해결했습니다.

### 페이지 빌더를 위한 magento/module-page-builder-product-recommendations 1.0.3

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.x 이상

![새](../assets/new.svg) 페이지 빌더 지원. 페이지 빌더 통합을 사용하면 페이지 빌더가 작성한 콘텐츠의 임의 위치에 권장 사항 단위를 정확하고 세분화하여 배치할 수 있습니다. 머리글과 추천 단위 자체의 스타일을 지정할 수도 있습니다. 자세한 내용을 보려면 [페이지 빌더](https://experienceleague.adobe.com/en/docs/commerce-admin/page-builder/add-content/recommendations)&#x200B;(으)로 이동하십시오.

### magento/제품 권장 사항 2.0.0

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.x 이상

![새로운](../assets/new.svg) 일반 가용성 릴리스!

+++

## 설명서

[!DNL Product Recommendations] 및 [!DNL Product Recommendations] 개발에 대해 자세히 알아보려면:

* [사용 안내서](overview.md)
* [개발자 설명서](https://experienceleague.adobe.com/en/docs/commerce/product-recommendations/developer/development-overview)
