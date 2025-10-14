---
title: 동작 이벤트
description: 각 행동 이벤트가 캡처하는 데이터를 알아봅니다.
role: Admin, Developer
feature: Personalization, Integration, Eventing
exl-id: bcabccc9-8a2e-4045-9306-1d999bb75624
source-git-commit: 631dfacd26a333e70a70f354d191d256d90d946f
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---

# [!DNL Data Connection] 동작 이벤트

다음은 [!DNL Data Connection] 확장을 설치할 때 사용할 수 있는 Commerce 동작 이벤트 목록입니다. 이러한 이벤트가 수집하는 데이터는 Adobe Experience Platform으로 전송됩니다. 또한 [사용자 지정 이벤트](custom-events.md)를 만들어 기본 제공되지 않은 추가 데이터를 수집할 수 있습니다.

다음 이벤트에서 수집하는 데이터 외에 Adobe Experience Platform Web SDK에서 제공하는 [기타 데이터](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/automatic-information.html?lang=ko)도 가져옵니다.

행동 이벤트는 사이트를 탐색할 때 쇼핑객으로부터 익명으로 처리된 행동 데이터를 수집합니다. 이러한 이벤트가 수집하는 데이터를 사용하여 특정 쇼핑객 집합을 대상으로 하는 프로모션 및 캠페인을 만들 수 있습니다.

>[!NOTE]
>
>모든 동작 이벤트에는 사용 가능한 경우 구매자 전자 메일 주소 및 ECID가 포함된 [`identityMap`](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/identitymap.html?lang=ko) 필드가 포함됩니다.

## Storefront 이벤트

Storefront 이벤트는 사이트에서 구매자의 상호 작용에서 데이터를 캡처하고 `addToCart`, `pageView`, `createAccount`, `editAccount`, `startCheckout`, `completeCheckout`, `signIn`, `signOut` 등의 이벤트를 포함합니다. Storefront 이벤트는 간단하고 구성 가능한 제품에만 적용됩니다.

storefront 이벤트에 대한 자세한 내용은 [개발자 설명서](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#data-connection)를 참조하세요.

## 고객 프로필 이벤트

상점 첫 화면에서 캡처된 프로필 이벤트에는 `signIn`, `signOut`, `createAccount`, `editAccount` 등의 계정 정보가 포함됩니다. 이 데이터는 등록 할인 오퍼, 계정 변경 확인 전송 등과 같이, 세그먼트를 더 잘 정의하거나 마케팅 캠페인을 실행하는 데 필요한 주요 고객 세부 정보를 채우는 데 사용됩니다.

고객 프로필 이벤트에 대한 자세한 내용은 [개발자 설명서](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#data-connection)를 참조하세요.

## 이벤트 검색

검색 이벤트는 구매자의 의도와 관련된 데이터를 제공합니다. Insight을 쇼핑객의 의도로 만들면 쇼핑객이 품목을 검색하는 방법, 고객이 클릭하는 항목, 궁극적으로 구매 또는 포기를 수행하는 방법을 상인이 확인할 수 있습니다. 이 데이터를 사용하는 방법의 예로는 상위 제품을 검색하지만 제품을 구매하지 않는 기존 구매자를 타겟팅하려는 경우입니다. 이 이벤트에 액세스하려면 [[!DNL Live Search]](../live-search/install.md) 확장을 설치해야 합니다.

`searchRequest.id` 및 `searchResponse.id` 이벤트 모두에 있는 `searchRequestSent` 및 `searchResponseReceived` 필드를 사용하여 검색 요청을 해당 검색 응답과 상호 참조합니다.

검색 이벤트에 대한 자세한 내용은 [개발자 설명서](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#data-connection)를 참조하세요.

## B2B 이벤트

![Adobe Commerce용 B2B](../assets/b2b.svg) B2B 판매자의 경우 이러한 이벤트에 액세스하려면 [&#x200B; 확장을 &#x200B;](install.md#install-the-b2b-extension)설치`experience-platform-connector-b2b`해야 합니다.

B2B 이벤트에는 [구매요청 목록](https://experienceleague.adobe.com/docs/commerce-admin/b2b/requisition-lists/requisition-lists.html?lang=ko) 정보가 포함되어 있습니다(예: 구매요청 목록이 생성, 추가 또는 삭제된 경우). 구매요청 목록과 관련된 이벤트를 추적하여 고객이 자주 구매하는 제품을 확인하고 해당 데이터를 기반으로 캠페인을 생성할 수 있습니다.

B2B 이벤트에 대한 자세한 내용은 [개발자 설명서](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#data-connection)를 참조하세요.
