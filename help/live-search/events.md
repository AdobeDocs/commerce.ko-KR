---
title: '[!DNL Live Search]개 이벤트'
description: 이벤트가  [!DNL Live Search]에 대한 데이터를 수집하는 방법을 알아봅니다.
feature: Services, Eventing
exl-id: a9f4f254-d8ff-46f1-8deb-a75b90d70d52
source-git-commit: 94d2a9911ab10d164d75779d1f310e5bdf2aea74
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---

# [!DNL Live Search]개 이벤트

[!DNL Live Search]은(는) 이벤트를 사용하여 &quot;가장 많이 본 항목&quot; 및 &quot;이 항목을 보고 다른 항목을 본 항목&quot;과 같은 검색 알고리즘을 실행합니다. [Commerce 샘플 Luma 테마](https://experienceleague.adobe.com/ko/docs/commerce-admin/content-design/design/themes/themes#the-default-theme)는 즉시 사용할 수 있는 이벤트이지만 Headless 및 기타 사용자 지정 구현은 자체 요구 사항에 맞게 이벤트를 구현해야 합니다.

이 표에서는 [!DNL Live Search] [순위 전략](rules-add.md#intelligent-ranking)에서 사용하는 이벤트에 대해 설명합니다.

| 순위 전략 | 이벤트 | 페이지 |
| --- | --- | --- |
| 가장 많이 본 항목 | `page-view`<br>`product-view` | 제품 세부 사항 페이지 |
| 최다 구매 | `page-view`<br>`place-order` | 장바구니/체크아웃 |
| 장바구니에 가장 많이 추가됨 | `page-view`<br>`add-to-cart` | 제품 세부 사항 페이지<br>제품 목록 페이지<br>장바구니<br>위시리스트 |
| 이 항목을 보고 다른 항목도 보았습니다. | `page-view`<br>`product-view` | 제품 세부 사항 페이지 |

>[!NOTE]
>
>[!DNL Live Search]을(를) 위한 데이터 수집에는 PII(개인 식별 정보)가 포함되지 않습니다. 쿠키 ID 및 IP 주소와 같은 모든 사용자 식별자는 엄격히 익명으로 처리됩니다. [자세히 알아보기](https://www.adobe.com/privacy/experience-cloud.html).

## 필수 대시보드 이벤트

[실시간 검색 대시보드](performance.md)를 채우는 데 일부 이벤트가 필요합니다.

| 대시보드 영역 | 이벤트 | 조인 필드 |
| ------------------- | ------------- | ---------- |
| 고유 검색 | `page-view`, `search-request-sent`, `search-response-received` | `searchRequestId` |
| 결과 없음 검색 | `page-view`, `search-request-sent`, `search-response-received` | `searchRequestId` |
| 결과 없음 비율 | `page-view`, `search-request-sent`, `search-response-received` | `searchRequestId` |
| 자주 찾는 검색 | `page-view`, `search-request-sent`, `search-response-received` | `searchRequestId` |
| 평균 클릭 위치 | `page-view`, `search-request-sent`, `search-response-received`, `search-results-view`, `search-product-click` | `searchRequestId` |
| 클릭스루 비율 | `page-view`, `search-request-sent`, `search-response-received`, `search-results-view`, `search-product-click` | `searchRequestId`, `sku`, `parentSku` |
| 전환율 | `page-view`, `search-request-sent`, `search-response-received`, `search-results-view`, `search-product-click`, `product-view`, `add-to-cart`, `place-order` | `searchRequestId`, `sku`, `parentSku` |

### 필수 컨텍스트

모든 이벤트에는 `Page` 및 `Storefront` 컨텍스트가 필요합니다. 이는 개별 이벤트를 생성할 때가 아니라 페이지 수준/상점 응용 프로그램 계층에서 발생해야 합니다(예를 들어, PHP 상점 앞에서는 PHP 응용 프로그램 컨테이너가 런타임 시 설정을 담당합니다).

## 사용

다음은 `search-request-sent` 이벤트의 샘플 구현입니다.

```javascript
const mse = window.magentoStorefrontEvents;

/* set in application container */
// mse.context.page(pageCtx);
// mse.context.setStorefrontInstance(storefrontCtx);

/* set before firing event */
mse.context.setSearchInput(searchInputCtx);
mse.publish.searchRequestSent("search-bar");
```

## 주의 사항

- 광고 차단기 및 개인 정보 설정을 사용하면 이벤트가 캡처되지 않을 수 있으며, 이로 인해 참여 및 매출 [지표](performance.md)이(가) 제대로 보고되지 않을 수 있습니다. 또한 페이지 또는 네트워크 문제로 인해 일부 이벤트가 전송되지 않을 수 있습니다.
- Headless 구현은 지능형 머천다이징을 향상시키기 위해 이벤트를 구현해야 합니다.

>[!NOTE]
>
>[쿠키 제한 모드](https://experienceleague.adobe.com/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law.html?lang=ko)가 활성화된 경우, Adobe Commerce은 구매자가 쿠키 사용에 동의할 때까지 행동 데이터를 수집하지 않습니다. 쿠키 제한 모드 가 비활성화되면 Adobe Commerce은 기본적으로 동작 데이터를 수집합니다.
