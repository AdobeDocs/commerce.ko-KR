---
title: 상점 설정
description: ' [!DNL Adobe Commerce Optimizer] Storefront를 설정하는 방법에 대해 알아봅니다.'
role: Developer
badgeSaas: label="SaaS만" type="Positive" url="https://experienceleague.adobe.com/ko/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 [!DNL Adobe Commerce Optimizer] 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."
exl-id: 2b4c9e98-a30c-4a33-b356-556de5bd721a
source-git-commit: 0cd9749574460374a8fe875f1eff54f2a4a8d614
workflow-type: tm+mt
source-wordcount: '1397'
ht-degree: 0%

---

# 상점 설정

이 안내서에서는 Adobe Edge Delivery Services를 사용하여 [!DNL Adobe Commerce Optimizer] 인스턴스에 대한 상점 전면을 설정하는 과정을 안내합니다. 상점에는 상용 코드, 샘플 콘텐츠 및 제품 세부 사항 페이지와 제품 검색(검색 및 필터링)에 대한 지원이 포함되어 있습니다.

**완료 예상 시간:** 30~45분

## 사전 요구 사항

* 저장소를 만들 수 있고 로컬 개발용으로 구성된 **GitHub 계정**(github.com)
* 샘플 데이터와 구성된 카탈로그 보기 및 정책이 있는 **[!DNL Adobe Commerce Optimizer]인스턴스**
   * 설치 지침은 [샘플 데이터 추가](get-started.md#add-sample-data)를 참조하십시오.

### 필수 인스턴스 데이터

시작하기 전에 [!DNL Adobe Commerce Optimizer] 인스턴스에서 다음 정보를 수집합니다.

* **테넌트 ID**(인스턴스 ID라고도 함)
   * [인스턴스 세부 정보 페이지](get-started.md#manage-instances)에서 사용 가능
* 인스턴스의 **GraphQL 끝점**
   * [인스턴스 세부 정보 페이지](get-started.md#manage-instances)에서 사용 가능
* 글로벌 카탈로그 보기의 **카탈로그 보기 ID**
   * [카탈로그 세부 정보 페이지](./setup/catalog-view.md#manage-catalog-view)에서 사용 가능
* 카탈로그 보기용 **Source 로케일**
   * 샘플 데이터의 기본값은 `en-US`입니다.

>[!NOTE]
>
>체험판 액세스 고객은 인스턴스가 생성될 때 받은 시작 이메일에서 GraphQL 엔드포인트를 찾을 수 있습니다. 체험판 인스턴스는 샘플 데이터, 카탈로그 보기 및 정책으로 사전 구성됩니다.

## 단계 설정

1. **[Storefront 프로젝트 만들기](#create-your-storefront-project)** - [Site Creator 도구](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator)를 사용하여 표준 코드, 샘플 콘텐츠 및 구성 파일로 새 Storefront 프로젝트를 만듭니다.

1. **[Storefront 구성을 사용자 지정](#customize-the-storefront-configuration)**-저장소의 `config.json` 파일을 업데이트하여 [!DNL Adobe Commerce Optimizer] 인스턴스에 연결합니다.

1. **[설정 확인](#verify-your-setup)**(10분)
   * 상점가 사이트 미리 보기
   * 제품 세부 사항 페이지 및 검색 기능 테스트

## Storefront 프로젝트 만들기

사이트 작성자 도구는 다음 구성 요소로 전체 Storefront 프로젝트를 만듭니다.

* **사이트**: 표준 서식 컨텐츠가 포함된 Storefront 랜딩 페이지
* **코드**: 표준 서식 소스 파일이 있는 리포지토리
* **콘텐츠**: 사이트 콘텐츠 파일이 있는 문서 작성 환경
* **Commerce 구성**: 인스턴스별 구성에 대한 `config.json` 파일

### 1단계: 프로젝트 생성

1. [사이트 작성자 도구 열기](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator)

   ![[!DNL Site Creator tool]](./assets/storefront-setup-site-creator.png){width="700" zoomable="yes"}

1. **새 사이트 만들기(코드 및 콘텐츠)**&#x200B;를 선택합니다.

1. 사이트 구성을 완료합니다.

   * **GitHub 조직/사용자 이름**: GitHub 사용자 이름 또는 조직 이름을 입력하십시오.
   * **사이트 이름**: 상점 이름을 설명하는 이름을 선택하세요.
   * **Commerce GraphQL 끝점(선택 사항)**: [!DNL Adobe Commerce Optimizer] 인스턴스에 대한 GraphQL 끝점을 입력합니다.

1. **사이트 만들기**&#x200B;를 클릭하여 Storefront 상용구 코드를 사용하여 GitHub 리포지토리를 만듭니다.

   저장소가 생성되면 사이트 생성자가 업데이트하고 코드 동기화 앱을 설치하라는 메시지를 표시합니다.

### 2단계: 코드 동기화 앱 설치

1. 새 탭에서 코드 동기화 설치 관리자를 열려면 **[!UICONTROL Install AEM Code Sync App]**&#x200B;을(를) 클릭하십시오.

1. 코드 동기화 앱을 구성합니다.
   * GitHub 조직을 선택한 다음 **[!UICONTROL Configure]**&#x200B;을(를) 클릭합니다.
   * 코드 동기화 인터페이스에서 **[!UICONTROL Only select repositories]**&#x200B;을(를) 클릭합니다.
   * **[!UICONTROL Select repositories]** 메뉴를 클릭한 다음 만든 상점 코드 저장소를 선택합니다.
   * 저장소를 등록하려면 **[!UICONTROL Save]**&#x200B;을(를) 클릭하십시오.

1. 사이트 작성자가 열려 있는 브라우저 창으로 돌아가서 **사이트 만들기**&#x200B;를 클릭합니다.

   사이트 작성자는 Storefront Boilerplate 콘텐츠를 문서 작성 환경에 복사합니다. 이 프로세스는 1~2분 정도 소요됩니다.

### 3단계: 프로젝트 링크 저장

1. 사이트 세부 정보 섹션에서 상점 프로젝트 링크를 검토하십시오.

   ![[!DNL Storefront setup complete]](./assets/storefront-setup-complete.png){width="700" zoomable="yes"}

   이러한 링크를 사용하여 상점 코드, 콘텐츠 및 구성을 관리하십시오.

1. 나중에 참조할 수 있도록 다음 링크를 복사하고 저장하십시오. **[!UICONTROL Copy]을(를) 클릭하십시오.

## 상점 구성

[!DNL Adobe Commerce Optimizer] 인스턴스에 연결하려면 Storefront 구성을 업데이트하십시오.

1. 상용구 코드 저장소에서 `config.json` 파일을 엽니다.

   `https://github.com/<username or org>/<repo name>/config.json`

1. 구성에서 `cs`(카탈로그 서비스) 섹션을 찾습니다.

1. 자리 표시자 값을 인스턴스에 대한 값으로 바꿉니다. [필수 구성 요소](#prerequisites)를 참조하십시오.

   ```json
   "cs": {
      "AC-View-ID": "{catalogViewId}",
      "AC-Source-Locale": "en-US",
      "AC-Price-Book-ID": "{priceBookId}"
   }
   ```

   >[!NOTE]
   >
   >가격 장부 ID를 찾으려면 Adobe Commerce Optimizer에서 [카탈로그 보기 구성 세부 정보](./setup/catalog-view.md)를 확인하여 지정된 가격 장부를 확인하십시오. 가격 장부가 지정되지 않은 경우 구성 파일에서 이 헤더를 제거할 수 있습니다. 가격 장부가 카탈로그 보기에 할당되면 다시 추가합니다.

1. 구성 파일을 저장합니다.

   구성 변경 사항이 적용되는 데 몇 분 정도 걸릴 수 있습니다. 데이터가 즉시 표시되지 않으면 2~3분 정도 기다린 후 문제를 해결하십시오.

## 설정 확인

[!DNL Adobe Commerce Optimizer] 인스턴스에 제대로 연결되어 있는지 확인하려면 Storefront를 테스트하십시오.

### 1단계: 상점 홈페이지 보기

1. 라이브 미리보기 URL로 이동합니다.

   `https://main--{SITE}--{ORG}.aem.live`

   `{ORG}` 및 `{SITE}`을(를) GitHub 조직 및 사이트 이름으로 바꾸십시오.

1. **성공 기준**: 표준 컨텐츠가 포함된 상점 홈 페이지가 표시됩니다.

   ![[!DNL ACO storefront site with boilerplate]](./assets/aco-storefront-site-boilerplate.png){width="700" zoomable="yes"}

### 2단계: 제품 세부 사항 페이지 테스트

기본 제품 세부 사항 페이지를 보고 제품 데이터가 올바르게 로드되는지 확인하십시오.

1. 샘플 제품 페이지로 이동합니다.
   `https://main--{SITE}--{ORG}.aem.live/products/placeholder/{sku}`

   샘플 데이터의 SKU를 사용합니다. 예:
   `https://main--{SITE}--{ORG}.aem.live/products/placeholder/aur-flu-tir-std-2017`

   기본 상점의 경우 경로에서 `placeholder` 값을 사용하여 제품을 볼 수 있습니다. Storefront 맞춤화를 시작하면 Storefront 코드를 맞춤화하여 카탈로그에 정의된 제품 경로를 기반으로 제품 세부 사항 페이지에 대한 경로를 설정할 수 있습니다.

   >[!TIP]
   >
   >[&#x200B; 인스턴스의 &#x200B;](./setup/data-sync.md)데이터 동기화[!DNL Adobe Commerce Optimizer] 페이지에서 사용 가능한 SKU를 봅니다.

1. **성공 기준**: 페이지가 표시되어야 합니다.
   * 제품 이름, 설명 및 가격
   * 제품 이미지
   * 장바구니에 추가 기능
   * [!DNL Adobe Commerce Optimizer] 인스턴스에서 검색된 데이터

   ![[!DNL Default product detail page showing a product from the sample data]](./assets/storefront-boilerplate-product-page.png){width="700" zoomable="yes"}

### 3단계: 기본 검색 기능 테스트

검색 및 필터링을 포함한 기본 제품 기능을 테스트합니다.

1. 상점 첫 페이지의 머리글에서 돋보기 아이콘을 클릭합니다.

1. 검색 문자열 `tires`을(를) 입력하고 **Enter**&#x200B;를 누릅니다.

1. **성공 기준**: 다음이 표시됩니다.
   * 타이어 제품이 포함된 검색 결과 페이지
   * 사이드바의 필터링 옵션
   * 이미지 및 가격 정보가 포함된 제품 목록

   ![[!DNL View search results page]](./assets/storefront-with-aco-search-results-page.png){width="675" zoomable="yes"}

1. 타이어 제품을 클릭하면 상세 페이지가 표시됩니다.

   ![[!DNL View product details page]](./assets/storefront-with-aco-pdp-page.png){width="675" zoomable="yes"}

## 문제 해결

설치하는 동안 문제가 발생하면 웹 페이지 관리자 콘솔을 사용하여 오류를 확인합니다. 또한 브라우저 캐시를 지우거나 다른 브라우저를 사용해 보십시오.

다음 지침을 사용하여 일반적인 문제를 확인하십시오.

### 일반적인 문제

| 문제 | 증상 | 솔루션 |
|-------|----------|----------|
| **코드 동기화 설치 실패** | 코드 동기화 설정을 완료할 수 없음 | <ul><li>GitHub 조직에 대한 관리자 액세스 권한이 있는지 확인하십시오.</li><li>조직 대신 개인 저장소를 사용해 보십시오.</li><li>GitHub 권한을 확인하고 다시 시도하십시오.</li></ul> |
| **사이트가 로드되지 않음** | 404 또는 연결 오류 | <ul><li>사이트 URL 형식 확인: `https://main--{SITE}--{ORG}.aem.live`</li><li>코드 동기화 앱이 제대로 설치되었는지 확인합니다.</li><li>저장소가 공용인지 또는 올바르게 구성되었는지 확인합니다.</li></ul> |
| **제품 데이터가 표시되지 않음** | 제품 페이지에 자리 표시자 또는 오류가 표시됨 | <ul><li>`config.json`에서 구성 값 확인</li><li>[!DNL Adobe Commerce Optimizer] 인스턴스에서 [데이터 동기화] 페이지에서 샘플 제품이 로드되었는지 확인합니다. 사용할 수 있는 제품이 없는 경우 샘플 데이터를 다시 로드하거나 [데이터 수집 API](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/using-the-api/#make-your-first-request)를 사용하여 제품을 추가하십시오. 구성 변경 사항이 반영될 때까지 몇 분 정도 기다립니다.</li><li>[&#x200B; 파일에 구성된 것과 동일한 헤더를 사용하여 머천다이징 서비스 &#x200B;](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/use-cases/#return-product-details)products 쿼리`config.json`를 사용하여 제품 세부 정보를 검색해 보십시오. 데이터를 검색할 수 있는 경우 카탈로그 보기 구성 또는 색인 오류의 문제일 수 있습니다.</li></ul> |
| **검색 결과 없음** | 빈 검색 결과 페이지 | <ul><li>[&#x200B; 파일에 구성된 것과 동일한 헤더를 사용하여 머천다이징 서비스 &#x200B;](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/use-cases/#product-search)productSearch 쿼리`config.json`를 사용하여 제품 검색 결과를 검색할 수 있는지 확인하십시오. 데이터를 검색할 수 있는 경우 카탈로그 보기 구성 또는 색인 오류의 문제일 수 있습니다.</li><li>`config.json` 파일의 카탈로그 보기 ID가 [!DNL Adobe Commerce Optimizer]의 카탈로그 보기 ID와 일치하는지 확인하십시오.</li><li>Adobe Commerce Optimizer에서 storefront 헤더 구성에서 사용한 정책, 로케일 및 가격 장부의 구성을 확인합니다.</li><li>[특성 메타데이터 설정](https://developer.adobe.com/commerce/services/reference/rest/#operation/createProductMetadata)이 검색에 대해 올바르게 설정되어 있는지 확인하십시오.</li></ul> |

### 유효성 검사 목록

다음 단계를 진행하기 전에 다음을 확인하여 상점이 올바르게 작동하는지 확인하십시오.

![검사 목록](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg) 구성 값이 인스턴스 설정과 일치함<br>
![검사 목록](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg) Storefront 홈 페이지가 오류 없이 로드됨<br>
![검사 목록](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg) 하나 이상의 제품 세부 정보 페이지에 전체 정보가 표시됨<br>
![검사 목록](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg) 검색 기능이 관련 결과를 반환함<br>
![검사 목록](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg) 제품 이미지가 올바르게 로드됨<br>
![검사 목록](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg) 구성 값이 인스턴스 설정과 일치함<br>

### 도움말 보기

문제가 지속되는 경우:

* [Adobe Commerce Storefront 설명서](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=ko) 검토
* [Adobe Commerce Optimizer 개발자 안내서](https://developer.adobe.com/commerce/services/optimizer/)를 확인하세요.
* [Adobe Commerce 지원 리소스](https://experienceleague.adobe.com/ko/docs/commerce-knowledge-base/kb/overview) 방문

## 다음 단계

상점을 설정하고 확인한 후 다음을 수행할 수 있습니다.

1. 웹 사이트에서 직접 콘텐츠를 편집하고 미리 보고 게시할 수 있도록 **[Sidekick 설치](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/?lang=ko#install-and-configure-sidekick)**-Browser 확장.

2. **[로컬 개발 환경 설정](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/?lang=ko#set-up-local-environment)**—로컬 환경을 만들어 상점 코드 및 콘텐츠를 사용자 지정합니다.

### 학습 및 탐색

* **[엔드 투 엔드 사용 사례 완료](./use-case/admin-use-case.md)** - [!DNL Adobe Commerce Optimizer]을(를) 사용한 상점 설정 및 카탈로그 관리에 대해 자세히 알아봅니다.

* **[Storefront 사용자 지정 살펴보기](https://experienceleague.adobe.com/developer/commerce/storefront/setup/?lang=ko)**—고급 설정 및 구성 옵션에 대해 알아봅니다.

* **[Commerce 드롭인을 사용하여 Storefront 경험을 사용자 지정](https://experienceleague.adobe.com/developer/commerce/storefront/dropins/all/introduction/?lang=ko)** 미리 빌드된 구성 요소를 추가하여 Storefront 경험을 개선합니다.

* **Storefront 구성 서비스로 마이그레이션**—초기 Storefront를 만든 후 구성을 마이그레이션하여 Repoless 구성 및 오버레이와 같은 고급 사용 사례를 지원하는 구성 서비스를 사용할 수 있습니다. 자세한 내용은 Adobe Experience Manager의 [구성 서비스](https://www.aem.live/docs/config-service-setup) 설명서를 참조하십시오.

>[!MORELIKETHIS]
>
> 사이트 콘텐츠를 업데이트하고 Adobe Commerce 프론트엔드 구성 요소 및 백엔드 데이터와 통합하는 방법에 대한 자세한 내용은 [Commerce Storefront 설명서](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=ko)를 참조하십시오.
