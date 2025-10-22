---
title: 릴리스 정보
description: Adobe Commerce의  [!DNL Data Connection] 확장에 대한 최신 릴리스 정보입니다.
feature: Personalization, Integration, Release Notes
exl-id: f3b92632-947d-40cd-89b7-24ed0680be51
source-git-commit: 5dd290a4e10bdbd1f6c96b67ab6c9ba1598705dc
workflow-type: tm+mt
source-wordcount: '1290'
ht-degree: 1%

---

# 릴리스 정보

>[!IMPORTANT]
>
>Experience Platform 커넥터의 이름이 [!DNL Data Connection]&#x200B;(으)로 변경되었습니다.

이 릴리스 노트에는 [!DNL Data Connection] 확장에 대한 업데이트가 포함되어 있으며 다음이 포함됩니다.

![새로운 기능](../assets/new.svg) - 새로운 기능
![수정](../assets/fix.svg) - 수정 사항 및 개선 사항
![버그](../assets/bug.svg) - 알려진 문제

[!DNL Data Connection] 확장에서 사용하는 확장과 관련된 기능 변경 및 수정 사항에 대해서는 **지원되는 서비스 업데이트**&#x200B;를 참조하십시오.

릴리스 일정 및 지원에 대한 자세한 내용은 [예정된 릴리스](https://experienceleague.adobe.com/en/docs/commerce-operations/release/planning/schedule)를 참조하세요.

개발자 설명서를 참조하여 [이 모듈을 지원하는 Commerce 버전을 알아보세요](https://experienceleague.adobe.com/en/docs/commerce-operations/release/product-availability).

## 지원되는 서비스 업데이트

이 릴리스 노트는 [!DNL Data Connection] 확장에서 사용하는 확장과 관련된 기능 변경 및 수정 사항에 대해 설명합니다.

+++지원되는 서비스 업데이트

_2025년 8월 7일_

![새로 만들기](../assets/new.svg) - 3.3.0 릴리스를 통해 이제 [사용자 지정 특성을 프로필에 추가](custom-identities.md)할 수 있습니다.

_2024년 8월 2일_

![수정](../assets/fix.svg) - 주문 합계가 세금을 포함하도록 구성된 경우 결제 총액을 수정했습니다.
![새로 만들기](../assets/new.svg) - 구매 이벤트를 주문하기 위해 `taxAmount` 필드를 추가했습니다.
![새로 만들기](../assets/new.svg) - 사용자 지정 데이터를 이벤트에 추가하는 기능을 추가했습니다. [예](https://github.com/adobe/commerce-events/blob/main/examples/events/custom-event-override.md)에 대해서는 다음을 참조하세요.

_2024년 1월 24일_

![새로 만들기](../assets/new.svg) - B2B 판매자에 대해 `data-services-b2b`(이)라는 새 요청 이벤트를 포함하도록 `deleteRequisitionList` 확장을 업데이트했습니다.

_2023년 11월 16일_

![수정](../assets/fix.svg) - 배송 주소가 여러 개인 주문을 했을 때 오류 메시지가 잘못 표시되는 문제를 해결했습니다.
![수정](../assets/fix.svg) - 스토어 보기에서 통화를 전환한 후 `productPageView` 이벤트 필드가 가격을 전환하지 않는 `productListItems.priceTotal` 이벤트 문제를 해결했습니다.
![수정](../assets/fix.svg) - 가맹점이 스토어 보기를 전환할 때 통화 코드가 업데이트되지 않는 `productListItems` 이벤트 필드의 문제를 해결했습니다.

_2023년 10월 10일_

![새로 만들기](../assets/new.svg) - 새 주문 상태 이벤트 추가: [인보이스 발행 주문](events-backoffice.md#orderinvoiced), [주문 항목 반환이 시작됨](events-backoffice.md#orderitemsreturninitiated), [주문 항목 반환이 완료됨](events-backoffice.md#orderitemreturncompleted).
![수정](../assets/fix.svg) - 캐시를 새로 고친 후 통화 구성 변경 내용이 이벤트에 반영되지 않는 문제를 해결했습니다.
![수정](../assets/fix.svg) - 비동기 주문 배치가 활성화된 경우 주문 확인 메시지가 표시되지 않는 경우 오류가 수정되었습니다.
![새로 만들기](../assets/new.svg) - 범주 보기 페이지에서 간단한 제품에 대한 데이터를 `addToRequisitionList` 이벤트에 추가했습니다.
![수정](../assets/fix.svg) - 주문 확인 페이지에서 제품을 추가할 때 `selectedOptions` 이벤트의 `addToRequisitionList` 데이터 문제를 해결했습니다.
![새로 만들기](../assets/new.svg) - 범주 보기 페이지의 구매요청 목록에 제품이 추가되면 `addToRequisitionList` 이벤트에 제품 데이터가 추가되었습니다.
![새로 만들기](../assets/new.svg) - 구성 가능한 제품이 제품 보기 페이지의 구매요청 목록에 추가되면 `addToRequisitionList` 이벤트가 추가되었습니다.
![새로 만들기](../assets/new.svg) - 구매요청 목록에서 제품 수량이 증가 및/또는 감소할 때 `addToRequisitionList` 및 `removeFromRequisitionList` 이벤트가 추가되었습니다.

_2023년 6월 10일_

![수정](../assets/fix.svg) - Commerce 주문 식별자의 접두사로 인해 `orderId`이(가) 컨텍스트에서 전달되지 않는 문제를 해결했습니다.
![수정](../assets/fix.svg) - 콘텐츠 보안 정책 구성을 업데이트했습니다.

_2023년 3월 30일_

![새로 만들기](../assets/new.svg) - B2B 판매자에 대한 `data-services-b2b`구매요청 목록 이벤트[를 포함하는 ](events.md#b2b-events)(이)라는 확장이 추가되었습니다.
![새로 만들기](../assets/new.svg) - `uniqueIdentifier`검색[ 이벤트에 ](events.md#search-events) 필드를 추가했습니다. 이 새 필드를 사용하면 판매자가 검색 요청과 검색 응답을 상호 참조할 수 있습니다.

_2022년 10월 12일_

![새로 만들기](../assets/new.svg) - 두 개의 [Storefront 이벤트](events.md), `openCart` 및 `removeFromCart`을(를) Adobe Commerce Storefront 이벤트 SDK 및 Collector에 추가했습니다.
![새로 만들기](../assets/new.svg) - [AEM 상점](overview.md#aem-support)에 대한 지원이 추가되었습니다.

+++

## 3.4.0

_2025년 9월 16일_

[!BADGE 호환성]{type=Informative tooltip="호환성"} Adobe Commerce 버전 2.4.4 이상

![새로 만들기](../assets/new.svg) [!DNL Data Connection]은(는) 이제 제한을 사용하도록 설정할 때 쿠키/로컬 저장소에 데이터 수집 및 저장을 금지하여 쿠키 제한 모드를 완전히 준수합니다.

## 3.3.0

_2025년 3월 21일_

[!BADGE 호환성]{type=Informative tooltip="호환성"} Adobe Commerce 버전 2.4.4 이상

![새로 만들기](../assets/new.svg)에서 PHP 8.4 지원을 추가했습니다.

## 3.2.1

_2025년 1월 17일_

[!BADGE 호환성]{type=Informative tooltip="호환성"} Adobe Commerce 버전 2.4.4 이상

![새로 만들기](../assets/new.svg) - 상인이 [ 백 오피스 이벤트 데이터를 Experience Platform과 공유하고 HIPAA 준수를 유지할 수 있도록 ](hipaa-readiness.md)HIPAA 지원 확장[!DNL Data Connection]을 [!DNL Commerce]에 추가했습니다.
![수정](../assets/fix.svg) - [!DNL Data Connection] 확장에서 `eventForwarding` 데이터를 덮어쓰고 모든 고객에 대해 `HIPAA` 플래그를 설정하는 문제가 해결되었습니다. 이제 확장은 HIPAA 고객에 대한 플래그만 설정합니다.

## 3.2.0

_2024년 10월 7일_

[!BADGE 호환성]{type=Informative tooltip="호환성"} Adobe Commerce 버전 2.4.4 이상

![새로 만들기](../assets/new.svg) - 백 오피스 데이터에 대한 [사용자 지정 순서 특성](custom-attributes.md)을(를) 만드는 기능이 추가되었습니다.
![새로 만들기](../assets/new.svg) - [에 구성되어 Experience Platform으로 전송된 사용자 지정 특성을 보는 데 도움이 되는 새 ](connect-data.md#data-customization)사용자 지정 순서 특성[!DNL Commerce] 테이블을 추가했습니다.
![새로 만들기](../assets/new.svg) - [프로필 레코드 수집 및 보내기](connect-data.md#send-customer-profile-data) 및 데이터를 Experience Platform에 보내는 기능이 추가되었습니다.

## 3.2.0-베타3

_2024년 8월 27일_

[!BADGE 호환성]{type=Informative tooltip="호환성"} Adobe Commerce 버전 2.4.4 이상

![새로 만들기](../assets/new.svg) - Beta에 참여하는 경우 `composer.json` 파일의 루트 수준이 `"minimum-stability": "beta"`인지 확인하세요. 또한 `composer require "magento/customers-connector: ^1.2.0"`을(를) 추가하여 Commerce 인스턴스에서 SaaS로 고객 프로필을 보냅니다.
![새로 만들기](../assets/new.svg) - 이 릴리스에는 3.1.1, 3.1.2, 3.1.3 및 3.1.4에 릴리스된 패치가 포함되어 있습니다.

## 3.1.4

_2024년 8월 9일_

[!BADGE 호환성]{type=Informative tooltip="호환성"} Adobe Commerce 버전 2.4.4 이상

![수정](../assets/fix.svg) - 사용하지 않는 데이터 내보내기 및 인덱서를 추가로 제거하도록 `experience-platform-connector` 메타패키지를 업데이트했습니다.

## 3.1.3

_2024년 7월 22일_

[!BADGE 호환성]{type=Informative tooltip="호환성"} Adobe Commerce 버전 2.4.4 이상

![수정](../assets/fix.svg) - 사용하지 않는 데이터 내보내기 및 인덱서를 제거하도록 `experience-platform-connector` 메타패키지를 업데이트했습니다.

## 3.1.2

_2024년 6월 5일_

[!BADGE 호환성]{type=Informative tooltip="호환성"} Adobe Commerce 버전 2.4.4 이상

![수정](../assets/fix.svg) - [내역 동기화](connect-data.md#specify-order-history-date-range)를 시작할 때 잘못된 날짜 형식이 사용되는 문제가 해결되었습니다.
![수정](../assets/fix.svg) - Adobe Commerce 2.4.7에서 `startCheckout` 이벤트가 전송되지 않는 문제가 해결되었습니다.

## 3.1.1

_2024년 4월 4일_

[!BADGE 호환성]{type=Informative tooltip="호환성"} Adobe Commerce 버전 2.4.4 이상

![새로 만들기](../assets/new.svg) - 모든 [!DNL Data Connection] 확장에 대해 PHP 8.3에 대한 지원을 추가했습니다.
![새로 만들기](../assets/new.svg) - Adobe Experience Platform Mobile SDK과 Commerce을 [통합](mobile-sdk-epc.md)하는 방법에 대한 문서가 추가되었습니다.

## 3.2.0-베타2

_2024년 3월 4일_

[!BADGE 호환성]{type=Informative tooltip="호환성"} Adobe Commerce 버전 2.4.4 이상

![새로 만들기](../assets/new.svg) - Beta에 참여하는 경우 `composer.json` 파일의 루트 수준이 `"minimum-stability": "beta"`인지 확인하세요. 또한 `composer require "magento/customers-connector: ^1.2.0"`을(를) 추가하여 Commerce 인스턴스에서 SaaS로 고객 프로필을 보냅니다.
![새로 만들기](../assets/new.svg) - [사용자 지정 특성을 추가](custom-attributes.md)하는 기능이 추가되었습니다.
![새로 만들기](../assets/new.svg) - [프로필 레코드 수집 및 보내기](connect-data.md#send-customer-profile-data) 및 데이터를 Experience Platform에 보내는 기능이 추가되었습니다.

## 3.1.0

_2023년 11월 16일_

[!BADGE 호환성]{type=Informative tooltip="호환성"} Adobe Commerce 버전 2.4.4 이상

![새로 만들기](../assets/new.svg) - Experience Platform 커넥터의 이름이 [!DNL Data Connection]&#x200B;(으)로 변경되었습니다.
![수정](../assets/fix.svg) - Adobe IMS에서 액세스 토큰을 생성할 수 없는 경우 오류 응답을 기록하는 기능이 추가되었습니다.
![수정](../assets/fix.svg) - 이전 주문을 동기화하려고 시도했지만 계정 자격 증명을 지정하지 않은 경우 알림 메시지를 추가했습니다.

## 3.0.0

_2023년 10월 10일_

[!BADGE 호환성]{type=Informative tooltip="호환성"} Adobe Commerce 버전 2.4.4 이상

주요 버전 릴리스입니다. 프로젝트의 루트 작성기.json 파일을 [편집](install.md#update-the-data-connection)합니다.

![새로 만들기](../assets/new.svg) - [내역 주문 보내기](connect-data.md#send-historical-order-data) 데이터 및 상태를 Experience Platform에 대한 일반 가용성.
![새로 만들기](../assets/new.svg) - [ 확장을 ](connect-data.md#connect-commerce-data-to-adobe-experience-platform)구성[!DNL Data Connection]할 때 OAuth 2.0에 대한 지원이 추가되었습니다.
![새로 만들기](../assets/new.svg) - Adobe Commerce 2.4.3에 대한 지원이 종료되었습니다.

## 2.3.0

_2023년 6월 27일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.3 이상

![새로 만들기](../assets/new.svg) - Experience Platform에 대한 [상점 이벤트 전송을 해제](connect-data.md#data-collection)하는 기능이 추가되었습니다.
![수정](../assets/fix.svg) - 콘텐츠 보안 정책 구성을 업데이트했습니다.
![수정](../assets/fix.svg) - Commerce 2.4.7 버전에서 백 오피스 이벤트에 대한 지원이 수정되었습니다.
![새로 만들기](../assets/new.svg) - [!DNL Data Connection] 확장 양식의 변경 사항을 저장할 때 캐시 무효화에 대한 알림 메시지를 추가했습니다.

## 3.0.0-beta1(내부용)

_2023년 6월 13일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.3 이상

![새로 만들기](../assets/new.svg) - (Beta) Experience Platform에 [이전 순서 보내기](connect-data.md#beta-send-historical-order-data) 데이터 및 상태를 보내는 기능이 추가되었습니다.

## 2.2.0

_2023년 3월 30일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.3 이상

![새로 만들기](../assets/new.svg) - `commerce-data-export` 및 `saas-export` 종속성을 `experience-platform-connector` 확장과 함께 번들로 제공했습니다. 이전에는 이러한 종속성을 별도로 설치해야 했습니다. 이러한 종속성은 판매자 구성과 함께 [백 오피스 이벤트](events-backoffice.md)의 서버측 처리를 가능하게 합니다.
![새로 만들기](../assets/new.svg) - [`orderShipmentCompleted`](events-backoffice.md#ordershipmentcompleted)(이)라는 새 백 오피스 이벤트를 추가했습니다.

## 2.1.1

_2023년 2월 28일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.3 이상

![새로 만들기](../assets/new.svg) - 모든 [!DNL Data Connection] 확장에 대해 PHP 8.2에 대한 지원을 추가했습니다.

## 2.1.0

_2023년 1월 17일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.3 이상

![새로 만들기](../assets/new.svg) - 고유한 AEP Web SDK(alloy)를 지정할 수 있도록 [[!DNL Data Connection] 확장 관리자](connect-data.md)를 업데이트했습니다.
![수정](../assets/fix.svg)이(가) 에지에 푸시된 데이터에 대한 기본 ID를 설정할 때 `identityMap` 대신 `personID`을(를) 사용하도록 변경되었습니다.

## 2.0.1

_2022년 11월 10일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.3 이상

![수정](../assets/fix.svg) - 이제 Adobe Experience Platform 컨텍스트는 Storefront 이벤트 수집기 및 Storefront 이벤트 SDK이 성공적으로 로드된 후에만 설정됩니다.

## 2.0.0

_2022년 10월 12일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.3 이상

![새로 만들기](../assets/new.svg) - Adobe Commerce 인스턴스를 Experience Platform에 [연결](connect-data.md)할 때 고유한 AEP Web SDK을 지정하는 기능이 추가되었습니다.
![수정](../assets/fix.svg) - 데이터 스트림 ID의 범위가 저장소 뷰가 아닌 웹 사이트로 지정되도록 데이터 스트림 범위 요구 사항이 업데이트되었습니다.

## 1.0.0

_2022년 8월 9일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.3 이상

![새로 만들기](../assets/new.svg) - 일반 가용성 릴리스.
