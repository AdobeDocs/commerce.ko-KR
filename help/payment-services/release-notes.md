---
title: '[!DNL Payment Services] 릴리스 정보'
description: 모든 [!DNL Payment Services] 릴리스에 대한 정보는 릴리스 정보를 검토하십시오.
exl-id: 104aa2c7-7735-4ac2-8ed1-a03cd9911273
feature: Payments, Release Notes
source-git-commit: a1c02122cd58234268ba9f07aaba96f83f929720
workflow-type: tm+mt
source-wordcount: '4332'
ht-degree: 0%

---


# 릴리스 정보

이 릴리스 노트는 [!DNL Payment Services]의 초기 릴리스에 대해 설명하고 다음을 포함합니다.

새 기능 ![개](../assets/new.svg)개
![해결된 문제](../assets/fix.svg) 수정 사항 및 개선 사항
![알려진 문제](../assets/bug.svg)알려진 문제

일반 기능 릴리스 버전 외부에서 릴리스된 기능 변경 및 수정 사항에 대해서는 _호스팅된 서비스 업데이트_ 섹션을 검토하십시오.

예정된 릴리스, 제품 지원 및 [!DNL Payment Services] 확장을 지원하는 Adobe Commerce 버전에 대한 자세한 내용은 Adobe Commerce [릴리스 일정](https://experienceleague.adobe.com/en/docs/commerce-operations/release/planning/schedule) 및 [제품 가용성](https://experienceleague.adobe.com/en/docs/commerce-operations/release/product-availability) 항목을 참조하십시오.

## 호스팅된 서비스 업데이트

이러한 릴리스 노트는 호스팅 서비스에 대한 일반 기능 릴리스 외부에서 발생하거나 릴리스된 기능 변경 사항 및 수정 사항에 대해 설명합니다.

+++호스팅된 서비스 업데이트

_2025년 4월 25일_

![새 문제](../assets/new.svg)<!-- Issue PAY-6051 --> 이제 [!DNL Payment Services] 대시보드에 현재 확장 버전과 대시보드 버전이 모두 표시됩니다.

_2024년 8월 30일_

![새 문제](../assets/new.svg)<!-- Issue PAY-5658 --> 이제 가맹점은 보다 자세하고 정확한 결제 방법 데이터를 위해 [거래 보고서](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/transactions.html)의 결제 세부 정보별로 거래를 필터링할 수 있습니다.

_2024년 7월 15일_

![새 문제](../assets/new.svg)<!-- Issue PAY-5571 --> 이제 판매자는 [거래 보고서](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/transactions.html)에서 Commerce 고객 전자 메일로 거래를 필터링할 수 있습니다. 해당 특정 이메일에 대한 트랜잭션을 필터링할 고객 이메일을 입력합니다.

_2024년 7월 9일_

![새 문제](../assets/new.svg)<!-- Issue PAY-5488 --> 이제 판매자는 [거래 보고서](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/transactions.html)에서 Commerce 고객 ID를 열로 보고 특정 고객이 수행한 거래를 식별할 수 있습니다. 또한 가맹점은 연결된 주문에 대해 이 Commerce 고객 ID로 트랜잭션 보고서를 필터링할 수 있습니다.

_2024년 3월 5일_

![문제 해결](../assets/fix.svg)<!-- Issue PAY-5252 --> 이제 판매자는 단일 셀의 콘텐츠를 선택하여 대시보드 그리드에서 데이터를 복사할 수 있습니다.

_2023년 10월 10일_

![새 문제](../assets/fix.svg)<!-- Issue PAY-4888 --> 이제 가맹점은 [거래 보고서](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/transactions.html)에서 신용 카드 및 직불 카드 거래를 카드 번호의 마지막 4자리까지 필터링할 수 있습니다.

_2023년 7월 12일_

![해결된 문제](../assets/fix.svg)<!-- Issue PAY-4587 --> [!DNL Payment Services] 2.1.0 릴리스에 도입된 이전 확장 버전에서 지정한 권한 부여 공백이 방지되는 문제가 해결되었습니다. [!DNL Payment Services]의 모든 버전을 사용하는 가맹점은 권한을 무효화할 수 있습니다.

_2023년 6월 9일_

![새로 만들기](../assets/new.svg)<!-- Issue PAY-4288 --> 이제 판매자는 [PayPal 결제 단추를 _만_&#x200B;구성](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/payments-options.html#use-only-paypal-payment-buttons)할 수 있으며 _사용할 수 없음_&#x200B;은 PayPal 신용카드 결제 옵션을 사용합니다. 이를 통해 가맹점은 벤모와 페이팔 결제 버튼 등 다양한 결제 옵션을 제공하고, 페이팔 신용카드 결제 옵션 대신 기존 신용카드 제공업체를 이용할 수 있다.

![새로 만들기](../assets/new.svg)<!-- Issue PAY-4050 --> 주문 결제 상태 보고서에 대해 결제 서비스 홈에 표시되는 [데이터 시각화 보기](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/order-payment-status.html#order-payment-status-data-visualization-view)를 추가했습니다.

![해결된 문제](../assets/fix.svg)<!-- Issue PAY-4486--> 이전에는 PayPal PayLater 단추가 영국 판매자의 체크아웃에 표시되지 않았습니다. 해당 문제는 해결되었습니다.

![해결된 문제](../assets/fix.svg)<!-- Issue PAY-4485--> 보고서 데이터 시각화 보기가 [!DNL Payment Services]이(가) 비활성화되면 이제 [!DNL Payment Services] 홈에 표시됩니다.

_2023년 1월 25일_

![알려진 문제](../assets/bug.svg)<!-- Issue PAY-4102 --> [!DNL Payment Services]의 새 설치에서 Commerce 서비스를 구성할 수 없어 [!DNL Payment Services]을(를) 사용할 수 없습니다. 이 문제를 해결하려면 [!DNL Payment Services] 확장을 버전 1.5.3으로 업데이트하십시오.

_2022년 9월 12일_

![새로 만들기](../assets/new.svg)<!-- Issue PAY-3705 --> 이제 `increment_id`을(를) 외부 ERP 시스템에서 급여 조정 시 사용할 수 있습니다. [`custom_id` _및_ `invoice_id`](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/data.html#reconcile-with-erp-system)에 전파되었으며, PayPal 웹후크 및 결제 시 판매자 활동 세부 정보에 모두 표시됩니다.

_2022년 8월 31일_

![문제가 해결되었습니다](../assets/fix.svg)<!-- Issue PAY-3629 --> 새 판매자가 [!DNL Payment Services] 홈에 처음 액세스하면 페이지를 새로 고치지 않고 콘텐츠를 표시하기 위해 페이지가 즉시 로드됩니다.

_2021년 8월 9일_

![새로 만들기](../assets/new.svg)<!-- Issue PAY-3420 --> 이제 Apple Pay를 PayPal 스마트 단추로 사용할 수 있습니다. 이 [결제 옵션](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-options.html#apple-pay-button)을 통해 고객은 iOS 또는 macOS 장치에서 Touch ID 기능을 사용하여 Apple Pay를 선택할 수 있습니다. Apple Pay는 디바이스에 저장된 신용 및 직불 카드 결제 자격 증명을 사용하여 결제를 처리합니다.

_2021년 6월 28일_

![새로 만들기](../assets/new.svg)<!-- Issue PAY-1720 --> 스토어 주문에 대한 분쟁은 이제 [주문 결제 상태 보고서](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/order-payment-status.html#view-disputes)에서 사용할 수 있습니다. [!DNL Payment Services]에서 PayPal 해결 센터로 직접 이동하여 문제를 해결할 수 있습니다.

![ 홈의 ](../assets/new.svg)<!-- Issue PAY-2854 -->새로 만들기[!DNL Payment Services] 사용자 경험에는 현재 상속 수준에서 구성을 수정하는 기능과 헤더 및 탐색 표시에 대한 개선 사항이 포함되어 있습니다.

![새로 만들기](../assets/new.svg)<!-- Issue PAY-2854 --> 이제 샌드박스 모드에서 프로덕션 모드로 전환하거나 저장되지 않은 업데이트가 있는 보기에서 나가려고 하면 경고가 표시됩니다.

![새로 만들기](../assets/new.svg)<!-- Issue PAY-2761 --> 이제 열 설정 컨트롤을 사용하여 열을 표시하거나 숨김으로써 [주문 결제 상태 보고서](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/order-payment-status.html#show-and-hide-columns) 및 [결제 보고서](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/payouts.html#show-and-hide-columns)에 표시되는 데이터를 사용자 지정할 수 있습니다.

+++

>[!NOTE]
>
> 릴리스는 필요에 따라 새로운 기능 및 수정 사항을 제공하기 위해 자주 발생합니다. 릴리스 일정은 고정되어 있지 않습니다.

## v2.13.0

_2025년 11월 10일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새로 만들기](../assets/new.svg)<!-- PAY-xxxx --> 이제 [!DNL Payment Services]은(는) 기본 제공 연락처 및 게재 정보를 제공하는 PayPal의 **OTC(일회성 체크아웃)** 모달을 지원합니다.

![새로운 기능](../assets/new.svg)<!-- PAY-xxxx --> **PayPal 앱 스위치 인증**&#x200B;을 통해 모바일 환경을 개선하고 더 원활한 사용자 여정을 위한 API 통합을 개선했습니다. 이 기능은 미국 [!DNL Payment Services]의 고객에게만 제공됩니다.

![새로 추가](../assets/new.svg)<!-- PAY-xxxx --> **강력한 고객 인증(SCA)** 요구 사항을 충족하기 위해 Fastlane에 대한 **3D 보안(3DS) 인증** 지원을 추가했습니다. 이를 통해 영국 및 EU [!DNL Payment Services] 가맹점은 **3DS 인증**&#x200B;을 사용하여 거래를 처리할 수 있으므로 사기 방지 기능을 강화하고 지역 규정을 준수할 수 있습니다.

![새로 만들기](../assets/new.svg)<!-- PAY-xxxx --> 이제 [!DNL Payment Services] 판매자는 Fastlane 체크아웃 구성 요소에 대해 **밝은 테마와 어두운 테마** 중 하나를 선택할 수 있으므로 체크아웃 페이지가 사이트 디자인에 맞게 변경됩니다. 사용자 정의 스타일이 접근성 표준을 충족하지 않으면 시스템이 자동으로 기본 설정으로 되돌아갑니다.

![문제 해결](../assets/fix.svg)<!-- PAY-xxxx --> **3DS 챌린지가 있는 관리자 체크아웃** 중 로더 문제를 해결했습니다.

![해결된 문제](../assets/fix.svg)<!-- PAY-xxxx --> API를 통해 결제 구성을 저장할 때 **유효성 검사를 개선**&#x200B;했습니다.

## v2.12.2

_2025년 9월 23일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![해결된 문제](../assets/fix.svg)<!-- PAY-6275 --> 캡처 모드에서 거부된 [!DNL Fastlane] 트랜잭션은 더 이상 Commerce에서 주문을 만들지 않습니다.

## v2.12.1

_2025년 9월 18일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![문제 해결](../assets/fix.svg)<!-- PAY-6164 --> 이제 [!DNL Payment Services]은(는) **PayPal SSSC(서버측 배달 콜백)**&#x200B;에서 사용 가능한 배달 방법에 기본 통화를 사용합니다.

![문제 해결](../assets/fix.svg)<!-- PAY-6267 --> **ISPU(매장 내 픽업)**&#x200B;를 선택하면 체크아웃 페이지에서 **배송처** 블록이 숨겨집니다.

![해결된 문제](../assets/fix.svg)<!-- PAY-6271 --> 이제 [!DNL Payment Services]은(는) **고객 계정** > **저장된 결제 방법** 섹션에 PayPal PayFlow에서 저장된 신용 카드 세부 정보를 표시합니다.

## v2.12.0

_2025년 8월 20일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새로 만들기](../assets/new.svg)<!-- PAY-6022 --> [Fastlane](https://experienceleague.adobe.com/en/docs/commerce/payment-services/payments-checkout/payments-options)은(는) 게스트 체크아웃 중에 더 빠른 구매를 제공합니다.

![새로 만들기](../assets/new.svg)<!-- PAY-6168 -->에서 [`addProductsToNewCart`에 ](https://developer.adobe.com/commerce/webapi/graphql/payment-services-extension/mutations/)[!DNL Payment Services] 돌연변이를 추가하여 더 원활한 전환과 더 나은 장바구니 재사용을 가능하게 했습니다.

![새로 만들기](../assets/new.svg)<!-- PAY-6169 --> 견적 수명 주기 관리를 개선하기 위해 [`setCartAsInactive`에 ](https://developer.adobe.com/commerce/webapi/graphql/payment-services-extension/mutations/)[!DNL Payment Services] 돌연변이를 추가했습니다.

![새로 만들기](../assets/new.svg)<!-- PAY-6227 --> PayPal을 사용하여 체크아웃할 때 [!DNL Payment Services]에서 더 빠른 구매 프로세스를 위해 주문 확인 팝업을 건너뜁니다.

![새로 만들기](../assets/new.svg)<!-- PAY-6234 --> [나중에 지불](https://experienceleague.adobe.com/en/docs/commerce/payment-services/payments-checkout/payments-options) 결제 옵션에 대한 새 기능을 추가했습니다. 이제 BNPL 메시징 구성기를 통해 고객 체크아웃 페이지에 나중에 결제 BNPL 메시지를 보다 유연하게 표시할 수 있습니다.

![해결된 문제](../assets/fix.svg)<!-- PAY-5505 --> 이제 [!DNL Payment Services]은(는) 제품 페이지에서 Google Pay 또는 PayPal 팝업이 닫히면 견적을 비활성으로 설정합니다.

![해결된 문제](../assets/fix.svg)<!-- PAY-5754 --> [!DNL Payment Services]에서는 더 이상 빈 견적에서 주문을 만들 수 없습니다.

## v2.11.1

_2025년 3월 14일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![문제 해결](../assets/fix.svg)<!-- PAY-5849 --> 체크아웃 중에 [라인 항목](line-items.md)에 영향을 주는 문제를 해결했습니다. 이제 [!DNL Payment Services]이(가) **라인 항목**&#x200B;에 대한 체크아웃 프로세스 안정성을 개선했습니다. 유사한 문제가 발생하면 [!DNL Payment Services] 영업 담당자에게 지원을 요청하십시오.

## v2.11.0

_2025년 3월 13일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상


![새로 만들기](../assets/new.svg)<!-- PAY-5938 --> 이제 [!DNL Payment Services]을(를) 통해 가맹점은 결제 설정을 관리하여 비즈니스의 유연성을 극대화할 수 있습니다. 이 버전은 판매자가 지원하는 지역 및 브랜드에 대해 [여러 PayPal 계정](https://experienceleague.adobe.com/en/docs/commerce/payment-services/configure/settings#use-multiple-paypal-accounts)을 첨부하는 기능을 향상시킵니다. 우리 영업팀은 웹 사이트 및 스토어 보기 범위를 설정하기 위한 온보딩 링크를 제공할 수 있습니다.

![새로 만들기](../assets/new.svg)<!-- PAY-5968 --> 이제 [!DNL Payment Services]에서 **PayPal 판매자 ID** 및 **PayPal 판매자 상태** 값으로 관리자 구성을 업데이트합니다. 이러한 값을 통해 가맹점은 PayPal 계정 상태를 더 잘 파악할 수 있습니다.

![문제가 해결되었습니다](../assets/fix.svg)<!-- PAY-5816 --> 버전 v2.9.0의 모든 주문 배치에서 오류를 일으키는 문제를 해결하여 [!DNL Payment Services]의 정상적인 주문 기능을 복원했습니다.

![해결된 문제](../assets/fix.svg)<!-- PAY-5825 --> Apple Pay 미니 카트에서 로그인한 고객에 대해 잘못된 예상 합계 URL을 사용하던 문제를 해결했습니다. 이제 [!DNL Payment Services]이(가) 정확한 전체 계산을 보장합니다.

![문제 해결](../assets/fix.svg)<!-- PAY-5826 --> 견적 상태를 `inactive`(으)로 변경할 때 HTTP 500 오류가 발생하는 문제를 해결하여 주문 관리 안정성을 개선했습니다.

![해결된 문제](../assets/fix.svg)<!-- PAY-5849 --> `LineItemProvider`에서 소수 자릿수가 1보다 작은 경우 예외를 throw하는 문제가 해결되었습니다. 이제 [!DNL Payment Services]이(가) 분수 수량을 더 잘 지원합니다.

![해결된 문제](../assets/fix.svg)<!-- PAY-5868 --> 체크아웃 중 기프트 카드 금액 오류를 해결했습니다. 이제 [!DNL Payment Services]은(는) 체크아웃 프로세스 중에 정확한 값을 보장합니다.

![해결된 문제](../assets/fix.svg)<!-- PAY-5911 --> [!DNL Payment Services]이(가) 아닌 온라인 결제 방법을 사용하여 주문한 주문에 대한 배송 생성 중 오류가 해결되어 전반적인 안정성이 향상되었습니다.

![해결된 문제](../assets/fix.svg)<!-- PAY-5954 --> 이제 [!DNL Payment Services]에서 다른 신용 카드를 선택했을 때 Apple Pay에서 주문하지 못한 문제를 해결하여 더 원활한 체크아웃 환경을 제공합니다.

![해결된 문제](../assets/fix.svg)<!-- PAY-5971 --> [!DNL Payment Services]은(는) Apple Pay가 실패하면 더 이상 고객을 주문 검토 페이지로 리디렉션하지 않으므로 불필요한 체크아웃 중단을 방지합니다.

## v2.10.3

_2025년 2월 24일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![해결된 문제](../assets/fix.svg)<!-- PAY-xxxx --> 전반적인 안정성과 성능이 향상되었습니다.

![해결된 문제](../assets/fix.svg)<!-- PAY-xxxx --> 일반 개선 및 최적화. v2.10.2에서 중요한 버그가 수정되었습니다.

## v2.10.2

_2025년 2월 21일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![알려진 문제](../assets/bug.svg)<!-- PAY-xxxx --> 안정성 및 성능에 영향을 줄 수 있는 중요한 버그가 포함되어 있습니다. Adobe에서는 이 버전(v2.10.2)을 사용하지 않고 v2.10.3으로 업그레이드하는 것이 좋습니다.

## v2.10.1

_2025년 2월 5일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새로 만들기](../assets/new.svg)<!-- PAY-5813 --> Adobe Commerce 2.4.8 및 PHP 8.4에 대한 지원이 추가되었습니다.

## v2.10.0

_2024년 12월 13일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새로 만들기](../assets/new.svg)<!-- PAY-5702 --> [!DNL Payment Services]은(는) 이제 구매 없이 보관하기 위한 GraphQL 끝점을 지원하므로 고객이 트랜잭션을 완료하지 않고도 결제 방법을 저장할 수 있습니다.

![새로 만들기](../assets/fix.svg)<!-- PAY-5789 --> [!DNL Payment Services]은(는) 이제 Google Pay를 사용한 [3D 보안 인증](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/payment-services/security-compliance/security#3ds)을 지원하므로 결제 거래 중 가맹점과 고객에 대한 보안이 강화됩니다.

![수정](../assets/fix.svg)<!-- PAY-5703 --> [!DNL Payment Services]은(는) [고객이 자신의 **내 계정**](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/payment-services/payments-checkout/vaulting)에서 직접 카드를 저장할 수 있는 기능을 추가하여 편리성을 개선하고 향후 체크아웃을 간소화합니다. `Vault without purchase functionality might not be 100% compatible with Adobe Commerce 2.4.4 due to a known issue with` [`GraphQL authorization mechanisms`](https://developer.adobe.com/commerce/webapi/graphql/usage/authorization-tokens/).

![수정](../assets/fix.svg)<!-- PAY-5762 --> 주문이 PDP(제품 세부 사항 페이지)에서 시작된 경우 주문 검토 페이지에 쿠폰 코드가 적용되지 않는 문제를 해결했습니다.

![수정](../assets/fix.svg)<!-- PAY-5792 --> [!DNL Payment Services]은(는) 이제 체크아웃 페이지[에 ](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/payment-services/payments-checkout/vaulting)저장된 카드에 대한 설명과 청구 주소를 표시하여 고객이 저장된 결제 방법을 보다 잘 알 수 있도록 합니다.

![수정](../assets/fix.svg)<!-- PAY-5793 --> [!DNL Payment Services]을(를) 사용하면 가맹점이 체크아웃 페이지에서 직접 저장된 카드의 청구 주소를 저장하여 정확하고 완전한 결제 정보를 보장할 수 있습니다.

## v2.9.0

_2024년 11월 7일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새로 만들기](../assets/new.svg)<!-- PAY-5629 --> [!DNL Payment Services]은(는) 이제 **업그레이드된 Apple Pay용 SDK URL**&#x200B;을(를) 지원하므로 Apple Pay를 사용하는 가맹점의 통합이 향상됩니다. 이 기능은 macOS 14 이상과 호환되므로 이전 버전의 macOS을 실행하는 장치에서는 이 기능이 표시되지 않습니다.

![새로 만들기](../assets/new.svg)<!-- PAY-5630 --> **체크아웃**, **제품**, **장바구니** 및 **MiniCart** 페이지를 업데이트하여 **Apple Pay의 업그레이드된 SDK URL**&#x200B;을 지원합니다. 이를 통해 결제 옵션으로 Apple Pay를 제공하는 가맹점을 위한 사용자 환경을 개선할 수 있습니다.

![신규](../assets/new.svg)<!-- PAY-5635 --> 배송 예상 개선 **Apple 결제 주소 기준**&#x200B;으로, 체크아웃 중에 정확한 배송 비용을 확인할 수 있습니다.

![수정](../assets/fix.svg)<!-- PAY-5661 --> 체크아웃 시 여러 **[!DNL Payment Services]문제를 해결했습니다**. 따라서 가맹점과 쇼핑객의 결제 프로세스의 신뢰성이 향상되었습니다.

![수정](../assets/fix.svg)<!-- PAY-5692 --> 빠른 체크아웃에 **스마트 단추**&#x200B;를 사용할 때 **고객의 이름과 성**&#x200B;이 주문에 추가되지 않는 문제를 해결했습니다.

![수정](../assets/fix.svg)<!-- PAY-5712 --> 총 금액이 무료일 때 가맹점이 **소계 결제 옵션을 사용하여 체크아웃을 완료할 수 없는 문제**&#x200B;를 해결했습니다.

## v2.8.1

_2024년 9월 13일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![수정](../assets/fix.svg)<!-- PAY-5644 --> [!DNL Payment Services]에서 여러 범위를 사용할 때 SDK 매개 변수의 캐시 문제를 해결했습니다. 이제 SDK 구성이 단일 키 아래에 있는 대신 각 범위에 대해 별도로 캐시됩니다. 이렇게 하면 각 범위의 캐시가 독립적으로 무효화되므로 여러 범위를 관리할 때 안정성이 향상됩니다.

## v2.8.0

_2024년 9월 13일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새로 만들기](../assets/new.svg)<!-- PAY-5499 --> 이제 [!DNL Payment Services]은(는) Adobe Commerce에서 [추적 번호를 입력](track-shipment.md)할 때 PayPal에 추적 번호 정보를 보낼 수 있습니다.

![수정](../assets/fix.svg)<!-- PAY-5626 --> [!DNL Payment Services]은(는) 고객이 Commerce 체크아웃 페이지를 방문할 때 판매자 레지스트리에 대한 요청 프로세스를 최적화했습니다. 이전에는 각 결제 방법(호스트형 필드, Google 페이, Apple 페이 및 스마트 버튼)에 대해 별도의 요청이 있었습니다. 이러한 개선을 통해 호출 수를 줄여 체크아웃 프로세스 중 성능 및 효율성을 개선합니다.

![수정](../assets/fix.svg)<!-- PAY-5645 --> 이제 [!DNL Payment Services]은(는) 구매자가 결제 페이지에서 사용자 지정 약관을 만든 가맹점에 동의하지 않은 경우 PayPal/Google Pay 팝업이 열리지 않도록 합니다.

![수정](../assets/fix.svg)<!-- PAY-5648 -->  [!DNL Payment Services]이(가) PayPal 포털의 라인 항목 세금 분류와 관련된 문제를 해결했습니다. 주문의 배송비에 세금이 연관되어 있는 경우 세금은 배송비의 일부로 포함되며 PayPal 포털에 표시된 라인 항목 세부 사항에 표시됩니다.

## v2.7.0

_2024년 8월 2일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새로 만들기](../assets/new.svg)<!-- PAY-4844 --> [!DNL Payment Services]은(는) 이제 주문 수준[에서 ](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/payment-services/payments-checkout/manage/line-items)라인 항목 데이터를 지원합니다. 이 기능을 사용하면 판매자가 제품 세부 정보, 수량, 가격(판매세, 할인 및 기타 관련 정보 포함) 등 주문에 있는 항목에 대한 자세한 정보를 볼 수 있습니다.

![새로 만들기](../assets/new.svg)<!-- PAY-5380 --> [!DNL Payment Services]은(는) 더 쉽고 직관적인 온보딩 프로세스를 위해 판매자를 위한 [관리](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/payment-services/configure/configure-admin#general-configuration) 환경의 구성을 개선합니다. 이 기능을 사용하면 판매자가 [!DNL Payment Services] ID를 재설정할 수 있습니다.

![새로 만들기](../assets/new.svg)<!-- PAY-5255 --> [!DNL Payment Services]에 [결제 실패 알림](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/point-of-purchase/checkout/checkout-payment-failed-emails)이 포함되어 있습니다. 이 기능은 가맹점에 결제 실패에 대한 거의 실시간으로 알림을 제공하므로 구매자에게 연락하여 주문을 절약하고 문제 해결을 잠재적으로 개선할 수 있습니다.

![수정](../assets/fix.svg)<!-- PAY-5469 --> **Google 결제 팝업이 Safari에 의해 차단되는 문제를 해결했습니다**. 이제 쇼핑객은 Safari에서 Google 결제 거래를 완료할 수 있습니다.

![수정](../assets/fix.svg)<!-- PAY-5492 --> 판매자가 사용자 지정된 약관을 체크아웃 페이지에 추가할 때 발생하는 문제를 해결했습니다. [빠른 체크아웃](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/payment-services/payments-checkout/payments-options#standard-vs-advanced-payments-experience)을 진행하는 동안 쇼핑객은 이제 문제 없이 체크아웃을 완료할 수 있도록 이 사용 약관에 동의할 수 있습니다.

![수정](../assets/fix.svg)<!-- PAY-5532 --> **InstantPurchase**&#x200B;를 통해 ISPU(매장 내 픽업) 기능을 개선했습니다. 쇼핑객이 **InstantPurchase**&#x200B;를 주문하면 **ISPU 배달 방법**&#x200B;이 더 이상 표시되지 않습니다.

![수정](../assets/fix.svg)<!-- PAY-5606 --> 판매자의 국가가 **독일**(으)로 설정되어 있는 경우 **구성 페이지** 국가 선택기 내의 문제를 해결했습니다.

## v2.6.0

_2024년 6월 4일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![신규](../assets/new.svg)<!-- PAY-4877 --> [!DNL Payment Services]에서 [L2/L3 가격 기능을 지원합니다](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/levels-card-payment-transactions.html). 이 기능은 IC++ 가격이 활성화된 [!DNL Payment Services] 고객에게만 제공됩니다. [!DNL Payment Services]에 대한 L2/L3 처리 데이터를 사용하려면 [!DNL Payment Services] 계정 관리자에게 문의하십시오.

![수정](../assets/fix.svg)<!-- PAY-5455 -->[!DNL Payment Services]을 사용하면 [도메인 연결 파일](https://developer.paypal.com/docs/checkout/apm/apple-pay/#register-your-live-domain)을 다운로드하여 호스팅하지 않고 확장에서 직접 Apple Pay를 사용할 수 있습니다.

## v2.5.0

_2024년 4월 23일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![수정](../assets/fix.svg)<!-- Issue PAY-5396 -->[!DNL Payment Services]은(는) 이제 Adobe Commerce 버전 2.4.7 이상의 [ 매개 변수에 대한 `--db-prefix`Adobe Commerce 지침](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/advanced#install-from-the-command-line)을 지원합니다.

## v2.4.3

_2024년 4월 16일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![수정](../assets/fix.svg)<!-- Issue PAY-5106 --> PayPal과 Adobe Commerce 간 체크아웃 중에 주문 금액 합계를 잘못 채우는 문제를 해결했습니다. 이제 판매자는 주문 시 주문 금액 합계가 정확한지 확인할 수 있습니다.

## v2.4.2

_2024년 4월 11일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새로 만들기](../assets/new.svg)<!-- Issue xxx --> Adobe Commerce 2.4.7에 대한 지원이 추가되었습니다.

## v2.4.1

_2024년 4월 4일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![수정](../assets/fix.svg)<!-- PAY-5322 --> 최신 Adobe Commerce 릴리스의 PCI 호환성 문제를 해결했습니다. 이제 [!DNL Payment Services]이(가) 결제 옵션으로 Adobe Commerce의 요구 사항을 체크아웃하도록 조정되었습니다.

![수정](../assets/fix.svg)<!-- PAY-5323 --> PayLater 및 Venmo가 Adobe Commerce에 올바르게 표시됩니다. 관리자가 PayLater 및 Venmo 전환 옵션을 표시할 수 없는 오류를 수정했습니다.

## v2.4.0

_2024년 3월 20일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![신규](../assets/new.svg)<!-- PAY-4868 --> 가맹점은 관리자를 통해 [의 다른 결제 버튼과 마찬가지로 구매 경험 전체에서 ](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/payments-options.html)Google Pay를 구성[!DNL Payment Services]할 수 있습니다.

![새로 만들기](../assets/new.svg)<!-- PAY-4381 --> [결제 서비스에서 GraphQL을 통해 Google 페이를 지원](https://developer.adobe.com/commerce/webapi/graphql/payment-services/) 가맹점에서 Google 페이 결제 방법을 통해 headless Commerce 경험을 할 수 있도록 허용합니다.

![새로 만들기](../assets/new.svg)<!-- PAY-4878 --> 이제 [!DNL Payment Services] 기본 체크아웃 기능이 Adobe Commerce 및 Magento Open Source 판매자용으로 번들로 제공됩니다.[!DNL Payment Services]은(는) 이제 전 세계 200개 지역에서 비즈니스를 운영하는 가맹점을 지원할 수 있습니다.[!DNL Payment Services] 기본 체크아웃은 셀프 서비스 온보딩에서 직불/신용, PayPal, Venmo(사용 가능한 경우) 및 PayLater(사용 가능한 경우) 옵션을 제공합니다.

![수정](../assets/fix.svg)<!-- PAY-5291 --> 일부 거래에 대한 결제 확인 수신이 지연될 수 있습니다. 이 경우 이제 가맹점은 주문에 대해 업데이트된 결제 상태를 받을 수 있습니다. [결제 서비스는 보류 중인 거래를 감지하고 이러한 거래를 사전에 모니터링하여 보류 중인 상태가 캡처되면 업데이트하여 순서대로 결제 거래의 보류 상태를 감지합니다](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/order-payment-status.html).

## v2.3.4

_2024년 3월 1일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새로 만들기](../assets/new.svg)<!-- PAY-5244 --> 비동기 체크 아웃 호환성을 수정했습니다.

![수정](../assets/fix.svg)<!-- PAY-5253 --> 자격 증명 모음 토큰이 [!DNL Payment Services]에 속하지 않는 경우 삭제할 수 없는 오류를 해결했습니다.

## v2.3.3

_2024년 2월 14일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새로 만들기](../assets/new.svg)<!-- PAY-5048 --> PHP 8.3에 대한 지원을 추가했습니다.

![수정](../assets/fix.svg)<!-- PAY-5048 -->: `is_deleted` 플래그 관련 오류를 해결했습니다. 이제 확장에서 보낸 `Rejected` 상태로 인해 주문이 실패하지 않습니다.

## v2.3.2

_2024년 1월 26일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![REST/GraphQL 성능 문제를 수정](../assets/fix.svg)<!-- PAY-5183 -->했습니다. 이제 API를 통해 가져올 때 신용 카드 버튼이 렌더링됩니다.

## v2.3.1

_2023년 12월 7일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새로 만들기](../assets/new.svg)<!-- PAY-5047 --> 이제 다음 위치에서 신용/직불 카드 브랜드 또는 결제 방법 유형을 사용할 수 있습니다.

- 상점 첫 화면의 고객 주문 페이지
- 구매자에게 전송된 주문 확인 이메일
- Commerce 관리자의 [주문 세부 사항 보기](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/order-management/orders/order-processing.html#view-an-order)에서.

## v2.3.0

_2023년 12월 1일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새로 만들기](../assets/new.svg)<!-- PAY-4381 --> [결제 서비스에서 이제 GraphQL 통합을 지원합니다](https://developer.adobe.com/commerce/webapi/graphql/payment-services/). PayPal 결제 단추, 호스트된 필드 및 Apple Pay에 대한 GraphQL 지원을 통해 [!DNL Payment Services]에서 이제 Headless Commerce 설정을 지원합니다.

## v2.2.1

_2023년 9월 27일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![문제 해결](../assets/fix.svg)<!-- Issue PAY-4870 --> 확장 버전을 최신 릴리스로 보낼 때 Storefront에서 새 헤더 특성을 올바르게 잘못 입력한 문제가 수정되었습니다. 이전에는 Commerce 서비스 커넥터의 `1.3.0` 릴리스에서 `User-Agent header` 확장에서 [!DNL Payment Services]을(를) 확장할 수 없었습니다.

## v2.2.0

_2023년 8월 30일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새로 만들기](../assets/new.svg)<!-- PAY-4638 --> 자동화된 사기 방지 서비스를 제공하는 Signifyd[와의 ](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/security-compliance/fraud-protection.html)통합을 추가했습니다.

![새로 만들기](../assets/new.svg)<!-- PAY-3981 --> [Apple Pay를 PayPal 결제 단추 외부에 있는 별도의 결제 옵션으로 승격](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/payments-options.html?lang=en#apple-pay-button)하여 쇼핑객이 결제 옵션을 볼 수 있도록 하고 가맹점이 Apple Pay의 배치와 스타일을 제어할 수 있도록 합니다.

![새로 만들기](../assets/new.svg)<!-- PAY-4002 --> 결제 아이콘 추가와 같은 스타일 개선 사항을 포함하여 신용카드 필드 체크아웃의 사용자 환경을 개선하여 쇼핑객 인지 부하를 줄이고 전환을 증가시켰습니다.

![새로 만들기](../assets/new.svg)<!-- PAY-4002 --> 가맹점이 특정 결제 옵션의 우선 순위를 지정하기 위해 [결제 옵션의 순서를 정렬](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/configure/settings.html#payment-buttons)할 수 있는 기능을 추가했습니다. 이 기능을 사용하면 체크아웃 대화율이 높아집니다.

![새로 만들기](../assets/new.svg)<!-- PAY-4035 --> 판매자는 이제 [ 관리 홈 페이지에서 사용할 수 있는 새 ](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/transactions.html)트랜잭션 보고서[!DNL Payment Services]를 사용하여 저장소 상태를 효율적으로 모니터링하고 트랜잭션 문제를 식별할 수 있습니다. 보고서는 거래 승인률과 부정적 거래 추세에 대한 자료도 제시한다.

## v2.1.0

_2023년 6월 9일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새로 만들기](../assets/new.svg)<!-- Issue xxx --> Adobe Commerce 2.4.7-beta1에 대한 지원을 추가했습니다.

![새로 만들기](../assets/new.svg)<!-- Issue xxx --> 다음 국가 및 관련 통화에서 [사용 가능 여부](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/overview.html#availability) 추가: 호주, 프랑스, 영국

![새로 만들기](../assets/new.svg)<!-- Issue PAY-4296 --> 관리자 사용자가 고객에 대한 주문을 만들고 관리할 수 있도록 [관리자 역할에 대한 확장된 리소스](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/configure/settings.html#configure-roles)를 추가하고 [!DNL Payment Services]을(를) 판매 메뉴에서 볼 수 있습니다.

![새로 만들기](../assets/new.svg)<!-- Issue PAY-4236 --> 체크아웃 중에 오류가 발생하는 주문에 대해 [자동 무효화를 추가했습니다](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/checkout.html#order-auto-voided-if-error).

![새로 만들기](../assets/new.svg)<!-- Issue PAY-4183 --> 체크아웃 페이지에서 [신용/직불 카드 결제 옵션 단추 표시](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/payments-options.html#debit-or-credit-card-button)하는 기능을 만들었습니다.

## v2.0.0

_2023년 3월 10일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![새로 만들기](../assets/new.svg)<!-- Issue PAY-4152 --> PHP 8.2 및 Adobe Commerce 2.4.6에 대한 지원이 추가되었습니다. PHP 7.x와 호환되지 않습니다.

## v1.6.1

_2023년 3월 10일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.4 이상

![수정](../assets/fix.svg)<!-- Issue PAY-4226 --> 새 [!DNL Payment Services] 판매자가 관리자의 체크아웃을 사용하지 못하는 문제를 해결했습니다.[!DNL Payment Services]은(는) 이전에 새 고객에 존재하지 않는 Commerce 고객 ID를 사용하고 있었습니다.

![수정](../assets/fix.svg)<!-- Issue PAY-4205 --> [PayPal 옵션](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/payments-options.html#paypal-smart-buttons)을 사용하여 체크아웃하는 동안 지정된 배송 주소 상태가 기본 세금 설정의 상태로 바뀌는 문제를 해결했습니다. 이제 고객은 머천트의 세금 설정에서 기본값으로 구성된 상태 이외의 상태로 주문을 출하할 수 있습니다.

![수정](../assets/fix.svg)<!-- Issue PAY-4202 --> 고객이 카드 보관을 사용하여 구매를 완료하거나 저장소 [결제 작업 `Authorize and Capture`을(를) 사용하여 보관된 결제 방법을 삭제할 수 없는 문제를 해결했습니다](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/get-started/production.html#set-payment-services-as-payment-method). 이전에는 고객이 저장된 신용 카드를 사용하거나 수정하려고 할 때 &quot;Provider Vault ID를 찾을 수 없음&quot; 오류가 표시되었습니다.

## v1.6.0

_2023년 2월 17일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.0 이상

![새로 만들기](../assets/new.svg)<!-- Issue PAY-3540 --> 유럽 연합(EU)과 영국에서 거래하는 판매자를 위한 [PCI 3DS 준수 기능](security.md#3ds)을 추가했습니다. 구매자가 신용 카드 발급자를 인증해야 하는 이 추가 보안 계층은 온라인 사기 예방에 도움이 되며 유럽 연합(EU) 규정 준수 규칙의 일부로 필요합니다.

![새로 만들기](../assets/new.svg)<!-- Issue PAY-3609 --> 관리자가 [카드 보관 사용](vaulting.md#use-vaulting-in-the-admin) 기능을 추가했습니다. 이를 통해 판매자는 저장된 결제 방법을 사용하여 관리자에서 고객에 대한 주문을 생성할 수 있습니다.

## v1.5.4

_2023년 1월 29일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.0 이상

![문제 해결](../assets/fix.svg)<!-- Issue PAY-4110 --> 구매자가 제품 페이지, 미니 장바구니 및 장바구니의 결제 단추를 사용하여 주문하지 못하는 문제를 해결했습니다. 이제 구매자가 주문을 성공적으로 완료할 수 있습니다.

## v1.5.3

_2023년 1월 25일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.0 이상

![해결된 문제](../assets/fix.svg)<!-- Issue PAY-4102 --> 이전 버전과 호환되지 않는 알려진 문제에 대한 수정 사항이 릴리스되었습니다. 이 릴리스에서는 서비스 ID 확장 버전을 최신 안정된 버전으로 잠가서 새 [!DNL Payment Services] 설치를 다시 사용하여 Commerce 서비스를 구성할 수 있습니다.

## v1.5.2

_2022년 12월 22일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.0 이상

![문제 해결](../assets/fix.svg)<!-- Issue PAY-3992 --> 결제 방법이 거부되면 [!DNL Payment Services]에서 송장 발행을 개선했습니다.

![해결된 문제](../assets/fix.svg)<!-- Issue PAY-3999 -->[!DNL Payment Services]는 이제 체크아웃 페이지에 대해 [Fire Checkout&#39;s](https://commercemarketplace.adobe.com/swissup-firecheckout.html){target=_blank} 사용자 지정 템플릿을 사용하여 가맹점에 대한 PayPal 결제 단추를 올바르게 표시합니다. 이전에는 미니마트에서 버튼이 간헐적으로 표시되었습니다.

## v1.5.1

_2022년 11월 23일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.0 이상

![새로 만들기](../assets/new.svg)<!-- Issue PAY-3923 -->[!DNL Payment Services]에서는 이제 요청이 사용하지 않는 끝점을 추적, 필터링 또는 사용하지 않도록 설정할 수 있도록 사용자 에이전트 헤더에 버전 번호를 포함합니다.

![문제 해결](../assets/fix.svg)<!-- Issue PAY-3968 -->[!DNL Payment Services]은(는) 이제 결제 단추를 사용하여 제품 페이지에서 주문을 할 때 주문 데이터를 올바르게 표시합니다.

## v1.5.0

_2022년 11월 18일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.0 이상

![새로 만들기](../assets/new.svg)<!-- Issue PAY-3880 --> 이제 구매자는 체크아웃 중에 신용카드 정보를 [저장(저장)할 수 있습니다](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/vaulting.html) 나중에 같은 가맹점 계정 내의 같은 상점이나 다른 상점을 구매할 때 사용할 수 있습니다.

![신규](../assets/new.svg)<!-- Issue PAY-3950 --> 상인이 이제 상점에 대해 [즉시 구매 Commerce 기능](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/point-of-purchase/checkout-instant-purchase.html)을 사용하도록 설정하여 쇼핑객이 체크아웃을 신속하게 할 수 있도록 할 수 있습니다([저장된 신용 카드 정보](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/vaulting.html) 사용).

## v1.4.1

_2022년 10월 14일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.0 이상

![수정](../assets/fix.svg)<!-- Issue PAY-3766 --> 고객의 결제 방법이 거부되면 표시되는 오류 메시지가 더 설명적입니다. 고객이 결제 정보를 다시 입력하고 다시 시도하거나 다른 결제 수단을 시도하거나 거래 거절에 대해 해당 은행에 문의하라고 조언한다.

## v1.4.0

_2022년 9월 30일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.0 이상

![신규](../assets/new.svg)<!-- Issue PAY-784 -->[!DNL Payment Services]에는 [여러 PayPal 비즈니스 계정을 사용](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/configure/settings.html#use-multiple-paypal-accounts)할 수 있도록 판매자 계정을 설정할 수 있는 기능이 포함됩니다. 이를 통해 판매자는 다양한 통화를 사용하여 여러 국가에서 스토어를 운영하거나 비즈니스의 일부로 Adobe Commerce을 사용할 수 있습니다.

![새로 만들기](../assets/new.svg)<!-- Issue PAY-3231 --> 판매자는 [웹 사이트 또는 개별 스토어 조회수 구성에 [!UICONTROL Soft Descriptor]](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/configure/settings.html#add-soft-descriptor)을(를) 추가하여 고객 거래 은행 거래 명세서에 브랜드, 스토어 또는 제품 라인을 설명할 수 있습니다.

![새로 만들기](../assets/new.svg)<!-- Issue PAY-3707 --> [ 설정에서 ](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/configure/settings.html#configure-payment-options)신용 카드 필드와 PayPal 결제 단추를 사용하거나 사용하지 않도록 설정[!DNL Payment Services]합니다.

![해결된 문제](../assets/fix.svg)<!-- Issue PAY-3546 --> 고객이 **[!UICONTROL Edit cart]**&#x200B;을(를) 클릭하면 빈 장바구니를 표시하는 대신 페이지가 장바구니 페이지로 리디렉션되고 업데이트된 항목이 표시됩니다.

## v1.3.1

_2022년 9월 6일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.0 이상

![문제 해결](../assets/fix.svg)<!-- Issue PAY-3663 --> 이제 판매자의 스토어에서 비글로벌 통화로 승인된 주문을 캡처할 때 캡처 프로세스가 완료되고 오류가 표시되지 않습니다.

## v1.3.0

_2022년 8월 9일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.0 이상

![새](../assets/new.svg)<!-- Issue PAY-XX --> 일반 가용성 릴리스—[!DNL Payment Services]은(는) 이제 [및 [!DNL Adobe Commerce] 버전 2.4.0에서 2.4.5 [!DNL Magento Open Source] 까지 지원됩니다.](https://experienceleague.adobe.com/en/docs/commerce-operations/release/product-availability)

![해결된 문제](../assets/fix.svg)<!-- Issue PAY-x --> 이제 Apple Pay가 모바일과 데스크탑에서 Safari 브라우저 v15.5와 호환됩니다.

## v1.2.0

_2022년 6월 29일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.0 이상

![알려진 문제](../assets/bug.svg)<!-- Issue PAY-x --> Apple Pay가 모바일 및 데스크톱의 Safari 브라우저 v15.5와 호환되지 않습니다. Safari 버전 15.5를 사용하는 경우 Apple Pay로 체크아웃을 완료할 수 없습니다.

![이전에 해결된 문제](../assets/fix.svg)<!-- Issue PAY-3264 --> 로그인한 사용자가 계정에 대한 기본 주소가 아닌 청구/배송 주소를 선택한 경우 체크아웃하지 못했습니다. 이제 선택한 청구/배송 주소가 (저장된 기본 주소 대신) 전송되고 체크아웃이 성공적으로 완료되었습니다.

![해결된 문제](../assets/fix.svg)<!-- Issue PAY-3314 --> 체크아웃을 위해 PayPal 결제 단추를 사용하지 않도록 설정하면 오류가 표시되지 않습니다.

![해결된 문제](../assets/fix.svg)<!-- Issue PAY-3330 --> 게스트 사용자가 대시가 포함된 전화 번호를 입력할 때 체크아웃 중에 결제가 더 이상 실패하지 않습니다.

![해결된 문제](../assets/fix.svg)<!-- Issue PAY-3338 PAY-2502 --> Commerce 서비스 자격 증명이 잘못된 경우[!DNL Payment Services]이제 관리자의 [!DNL Payment Services] 홈에서 자격 증명 오류를 표시하여 사용자에게 알립니다.

![알려진 문제](../assets/bug.svg)<!-- Issue PAY-0 --> [!DNL Payment Services]이(가) `commerce-data-export` v101.20 이상과 호환되지 않으므로 [[!DNL Channel manager] 확장](https://experienceleague.adobe.com/docs/commerce-channels/channel-manager/guide-overview.html)과 호환되지 않습니다.

## v1.1.0

_2022년 3월 31일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.0 이상

![새](../assets/new.svg)<!-- Issue PAY-2127 --> 일반 가용성 릴리스—[!DNL Payment Services]은(는) 이제 [및 [!DNL Adobe Commerce] 버전 2.4.0에서 2.4.4 [!DNL Magento Open Source] 까지 지원됩니다.](https://experienceleague.adobe.com/en/docs/commerce-operations/release/product-availability)

![새로 만들기](../assets/new.svg)<!-- Issue PAY-2682 --> 이제 캐나다 상인이 [!DNL Payment Services] 및 [!DNL Adobe Commerce]에 대한 [!DNL Magento Open Source] 확장을 사용할 수 있습니다. 가맹점은 [프랑스어](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/overview.html?lang=fr#carte-de-cr%C3%A9dit-et-devises-accept%C3%A9es) 또는 [영어](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/overview.html#accepted-credit-cards-and-currencies)로 결제 구성을 볼 수 있습니다.

![새로 만들기](../assets/new.svg)<!-- Issue PAY-2681 --> [!DNL Payment Services]은(는) 신용 카드 및 PayPal 거래에 대해 [캐나다 달러(CAD)](introduction.md#accepted-credit-cards-and-currencies)를 지원합니다.

![신규](../assets/new.svg)<!-- Issue PAY-2680 --> 가맹점은 영어 또는 프랑스어로 확장을 [온보딩 [!DNL Payment Services]](onboard.md)할 수 있습니다.

![신규](../assets/new.svg)<!-- Issue PAY-2678 --> 가맹점은 이제 캐나다 달러(CAD)로 [주문 결제 상태](order-payment-status.md) 및 [결제 보고서](payouts.md)의 재무 보고서를 볼 수 있습니다.

![해결된 문제](../assets/fix.svg)<!-- Issue PAY-2710 -->[!DNL Payment Services]이(가) 이제 [PHP 8.1](https://www.php.net/releases/8.1/en.php)과(와) 호환됩니다.

![문제를 해결했습니다](../assets/fix.svg)<!-- Issue PAY-3017 --> 여러 스토어에서 적절한 경고를 표시하도록 샌드박스 모드 경고를 개선했습니다.

![해결된 문제](../assets/fix.svg)<!-- Issue PAY-2742 --> 이제 스토어 보기 수준에서 Venmo와 같은 사용 가능한 결제 방법을 사용하거나 사용하지 않도록 설정할 수 있습니다. 이전에는 웹 사이트당 결제 방법만 구성할 수 있었습니다.

![해결된 문제](../assets/fix.svg)<!-- Issue PAY-2277 --> 이제 선택적으로 [개별 PayPal 결제 단추를 사용하거나 사용하지 않도록 설정](configure-admin.md#payment-buttons)할 수 있습니다.

![해결된 문제](../assets/fix.svg)<!-- Issue PAY-2561 --> 이전에 제거한 제품이 _주문 검토_ 페이지의 장바구니에 표시되지 않습니다.

![알려진 문제](../assets/bug.svg)<!-- Issue PAY-2842 --> 샌드박스 환경에서 결제를 처리할 때 신용 카드 거래 테스트 [PayPal로 실패](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-cc-sandbox-failure.html)할 수 있습니다.

## v1.0.0

_2021년 11월 29일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.0 이상

![새](../assets/new.svg)<!-- Issue PAY-2127 --> 일반 가용성 릴리스—[[!DNL Payment Services]](https://commercemarketplace.adobe.com/magento-payment-services.html)은(는) 이제 [!DNL Adobe Commerce] 및 [!DNL Magento Open Source] 버전 2.4.0에서 2.4.3-p1까지 지원됩니다.

![새로 만들기](../assets/new.svg)<!-- Issue PAY-124 --> [!DNL Payment Services] 및 [!DNL Adobe Commerce]에 대한 [!DNL Magento Open Source] 확장은 [[!DNL Adobe Commerce] 클라우드 인프라](install.md#adobe-commerce-on-cloud-infrastructure) 또는 [온-프레미스](install.md#on-premises) 인스턴스에 대해 설치할 수 있습니다. 이러한 메서드는 명령줄 인터페이스를 사용해야 합니다.

![새로 만들기](../assets/new.svg)<!-- Issue PAY-1986 --> [!DNL Payment Services]은(는) 판매자가 테스트 모드에서 확장을 평가할 수 있도록 하는 [샌드박스 계정](sandbox.md)을 지원합니다.

![새로 만들기](../assets/new.svg)<!-- Issue PAY-666 --> 가맹점은 샌드박스 또는 프로덕션 환경 간 [ 전환을 사용하는 것과 같은 기본 결제 동작을 사용하여 ](configure-admin.md)결제 서비스를 구성[`Authorize and Capture`](production.md#set-payment-services-as-payment-method) 확장을 구성할 수 있습니다.

![새로 만들기](../assets/new.svg)<!-- Issue PAY-780 --> 쇼핑객이 [!DNL Payment Services] 또는 [수동 주문 만들기](create-order.md)를 통해 체크아웃할 수 있습니다.

![새](../assets/new.svg)<!-- Issue PAY-1856 --> [주문 결제 상태](order-payment-status.md) 및 [결제 보고서](payouts.md)를 통해 [!DNL Payment Services]에서 포괄적인 보고를 사용하여 스토어의 주문 및 관련 결제를 명확하게 볼 수 있습니다.

![새로 만들기](../assets/new.svg)<!-- Issue PAY-311 --> [!DNL Payment Services]은(는) 모든 판매자에 맞게 조정된 총 처리 용량을 기반으로 유연한 계층화된 가격을 지원합니다.

![새로 만들기](../assets/new.svg)<!-- Issue PAY-1443 --> [ 확장에 대한 PayPal 결제 단추 및 신용 카드 필드를 ](payments-options.md)사용자 지정[!DNL Payment Services]할 수 있습니다.

![알려진 문제](../assets/bug.svg)<!-- Issue PAY-2473 --> 확장을 설치하는 동안 [잘못된 작성기 키](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-install.html)를 사용하면 사용자가 올바른 [을(를) 사용하여 ](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/authentication-keys)인증`MAGEID`할 수 없습니다.

![알려진 문제](../assets/bug.svg)<!-- Issue PAY-2474 --> [!DNL Payment Services]개의 보고서 [을(를) 즉시 동기화할 수 없습니다](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-report-info-delayed.html).

![알려진 문제](../assets/bug.svg)<!-- Issue PAY-2475 --> 온보딩 중에 해당 계정을 만든 경우 [에 대한 ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-paypal-acct.html)PayPal 샌드박스 계정[!DNL Payment Services]을(를) 확인할 수 없습니다.
