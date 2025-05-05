---
title: '[!DNL Store Fulfillment by Walmart Commerce Technologies] 릴리스 정보'
description: 모든 [!DNL Store Fulfillment by Walmart Commerce Technologies] 릴리스에 대한 정보는 릴리스 정보를 검토하십시오.
role: Admin, User, Leader
feature: Shipping/Delivery, Release Notes
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 0%

---

# 릴리스 정보

이 릴리스 노트는 [!DNL Store Fulfillment Services by Walmart Commerce Technologies]의 초기 릴리스에 대해 설명하고 다음을 포함합니다.

새 기능 ![개](../assets/new.svg)개
![해결된 문제](../assets/fix.svg) 수정 사항 및 개선 사항
![알려진 문제](../assets/bug.svg)알려진 문제

릴리스 일정 및 지원에 대한 자세한 내용은 [예정된 릴리스](https://experienceleague.adobe.com/docs/commerce-operations/release/planning/schedule.html)를 참조하세요.

이 확장을 지원하는 Adobe Commerce 버전을 알아보려면 [제품 가용성](https://experienceleague.adobe.com/docs/commerce-operations/release/product-availability.html)을 참조하세요.

## v1.5.0

*2023년 8월 3일*

[!BADGE 지원됨]{type=Informative tooltip="지원됨"}[Adobe Commerce 2.4.4 ~ 2.4.6](https://experienceleague.adobe.com/docs/commerce-operations/release/product-availability.html)&#x200B;(2.4.6-p1, 2.4.5-p3 및 2.4.4-p4 보안 패치 릴리스 포함)

이번 릴리스에는 다음 업데이트가 포함됩니다.

![새로운 기능](../assets/fix.svg) [Adobe Commerce 보안 패치 릴리스](https://experienceleague.adobe.com/docs/commerce-operations/release/notes/security-patches/overview.html) 2.4.6-p1, 2.4.5-p3 및 2.4.4-p4를 지원하도록 확장을 업데이트했습니다.

![새로 만들기](../assets/new.svg)<!-- WMTP-918 --> 판매 전자 메일에 대한 [비동기 전송](sales-emails.md) 구성 옵션에 대한 지원을 추가했습니다. 버전 1.5.0으로 업그레이드하는 판매자는 즉시(기본값) 또는 비동기적으로 이메일을 보낼 수 있습니다.

![새로 만들기](../assets/new.svg)<!-- WMTP-916--> 국제 전화 번호 형식을 지원하도록 [소스 구성](merchant-store-configuration.md)을 업데이트했습니다.

![새로 만들기](../assets/new.svg) 환불 금액이 남은 금액이나 인보이스 발행 금액을 초과하지 않도록 하는 논리를 추가했습니다.

![새로 만들기](../assets/new.svg)<!-- WMTP-882 -->이(가) 이전 버전의 [!DNL Google Maps]과의 호환성을 지원하기 위해 `google.map.LatLng` 개체를 JSON 리터럴로 대체했습니다.

![문제 해결](../assets/fix.svg)<!-- WMTP- --> 특성 범주 충돌을 방지하기 위해 `[!DNL Available for Store Pickup]` 및 `[!DNL Available for Home Delivery]` 제품 특성을 만드는 스크립트를 업데이트했습니다.

![문제 해결](../assets/fix.svg)<!-- WMTP-915 --> 일부 엔터티를 로드하고 저장할 때 무한 루프가 발생하는 호환성 문제를 해결했습니다.

![문제 해결](../assets/fix.svg)<!-- WMTP-921 --> PDP(제품 세부 정보 페이지)에서 장바구니에 항목을 추가할 때 [!DNL Ship to Store] 견적 유효성 검사가 트리거되지 않는 문제를 해결했습니다.

![해결된 문제](../assets/fix.svg)<!-- WMTP- 932 --> 고객이 홈 배달에 적합하지 않은 항목에 대해 홈 배달 방법을 선택할 수 있는 체크아웃 문제를 해결했습니다.

![해결된 문제](../assets/fix.svg) 설치 업데이트:

- &#x200B;<!-- WMTP-880--> [!DNL Store Fulfillment] 확장을 설치할 때 잘못된 웹 사이트 코드가 반환되는 문제를 해결했습니다.

- &#x200B;<!-- WMTP-878--> 설치 중에 데이터 유형을 문자열 유형으로 변환해야 하는 SKU 정수 문제를 해결했습니다.

![문제 해결](../assets/fix.svg)<!-- WMTP-915--> 체크 인 오류 코드 누락으로 인한 오류를 해결했습니다.

![문제 해결](../assets/fix.svg)<!-- WMTP-932 --> 분배 작업 중 부분 거부와 관련된 버그를 수정했습니다.

![새로 만들기](../assets/new.svg)<!-- WMTP-953 --> 상태 매개 변수를 선택적 개체로 사용하도록 Cancel API 끝점을 업데이트했습니다.

![새로 만들기](../assets/new.svg)<!-- WMTP-960 --> 분배 API 끝점에 대한 로깅 세부 정보가 개선되었습니다.

## v1.4.0

*2023년 4월 13일*

[!BADGE 지원됨]{type=Informative tooltip="지원됨"}

![새로 만들기](../assets/fix.svg) [!DNL Store Fulfillment]이(가) 이제 [호환 [!DNL Adobe Commerce] 2.4.4에서 2.4.6](https://experienceleague.adobe.com/docs/commerce-operations/release/product-availability.html)입니다.


## v1.3.0

*2023년 2월 27일*

[!BADGE 지원됨]{type=Informative tooltip="지원됨"}

이번 릴리스에는 다음 업데이트가 포함됩니다.

![새로 만들기](../assets/fix.svg)<!-- WMTP-795 --> 웹 사이트에서 전역 웹 사이트로 시스템 구성 설정의 기본 범위를 변경하여 특정 사이트에 대해 스토어 이행 솔루션을 사용하지 않도록 설정하는 기능을 추가했습니다.

## v1.2.0

*2022년 9월 27일*

[!BADGE 지원됨]{type=Informative tooltip="지원됨"}

이번 릴리스에는 다음 업데이트가 포함됩니다.

![새로 만들기](../assets/fix.svg) [!DNL Store Fulfillment]이(가) 이제 [호환 [!DNL Adobe Commerce] 2.4.4에서 2.4.5](https://experienceleague.adobe.com/docs/commerce-operations/release/product-availability.html)됩니다.


## v1.1.0

*2022년 7월 15일*

[!BADGE 지원됨]{type=Informative tooltip="지원됨"}

안정성: 일반 가용성

![새로 만들기](../assets/fix.svg)<!-- WMTP-731 --> 기본 자동차 제조와 모델 선택을 추가하여 Store Assist 앱에 대한 [체크인 경험 구성](check-in-experience-setup.md)을 간소화했습니다. 이전 버전에서는 자동차 제조와 모델 선택을 가맹점이 수동으로 구성해야 했다.

## v1.0.0

*2022년 3월 4일*

[!BADGE 지원됨]{type=Informative tooltip="지원됨"}

안정성: 일반 가용성

## 스토어 지원 앱

스토어 지원 앱의 새 릴리스에 대한 자세한 내용은 [Apple App Store](https://apps.apple.com/us/app/store-assist-by-walmart/id1609281539){target="_blank"} 또는 [Google Play 스토어](https://play.google.com/store/apps/details?id=com.walmart.faas.storeassist){target="_blank"}에 있는 앱 정보를 참조하십시오.
