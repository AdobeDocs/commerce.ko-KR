---
title: AEM Assets 통합 릴리스 노트
description: 모든 AEM Assets 통합 릴리스에 대한 자세한 내용은 릴리스 정보 를 참조하십시오.
feature: CMS, Media, Release Notes
exl-id: 0d639565-812f-481a-afd6-6e6fa54ed70e
source-git-commit: 4f95ca25da819d5c8dfa99e1380edf672f3e0249
workflow-type: tm+mt
source-wordcount: '757'
ht-degree: 0%

---

# AEM Assets 통합 릴리스 노트

이러한 릴리스 노트는 AEM Assets 통합에 대한 모든 릴리스를 설명하며 다음을 포함합니다.

새 기능 ![개](../assets/new.svg)개
![해결된 문제](../assets/fix.svg) 수정 사항 및 개선 사항
![알려진 문제](../assets/bug.svg)알려진 문제

일반 기능 릴리스 버전 외부에서 릴리스된 기능 변경 및 수정 사항에 대해서는 _호스팅된 서비스 업데이트_ 섹션을 검토하십시오.

예정된 릴리스, 제품 지원 및 AEM Assets 통합 확장을 지원하는 Adobe Commerce 버전에 대한 자세한 내용은 Adobe Commerce [릴리스 일정](https://experienceleague.adobe.com/en/docs/commerce-operations/release/planning/schedule) 및 [제품 가용성](https://experienceleague.adobe.com/en/docs/commerce-operations/release/product-availability) 항목을 참조하십시오.

## 호스팅된 서비스 업데이트

이러한 릴리스 노트는 호스팅 서비스에 대한 일반 기능 릴리스 외부에서 발생하거나 릴리스된 기능 변경 사항 및 수정 사항에 대해 설명합니다.

+++호스팅된 서비스 업데이트

_2025년 9월 11일_

![새 문제](../assets/new.svg) [사용자 지정 자동 일치](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/synchronize/custom-match){target=_blank} 끝점을 새 `asset_matches` 특성으로 업데이트했습니다.

_2025년 2월 11일_

![새 문제](../assets/new.svg) 이제 판매자는 제품 및 범주에 대한 이미지를 동기화할 수 있습니다.

+++

## v1.2.11

_2026년 1월 15일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.5 이상 릴리스.

제품 편집 페이지의 ![문제를 해결했습니다](../assets/fix.svg)<!-- Issue ACAP-1180 --> 일반적인 개선 사항. 이제 AEM Assets 통합이 활성화되면 페이지가 올바르게 사전 렌더링됩니다.

## v1.2.10

_2026년 1월 12일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.5 이상 릴리스.

![해결된 문제](../assets/fix.svg)<!-- Issue ACAP-1178 --> 제품에 이미지가 있고 AEM Assets 통합이 활성화되어 있을 때 REST API를 통해 제품 사용자 지정 특성을 업데이트할 수 없는 문제를 해결했습니다. 이제, 제품 사용자 지정 속성은 REST API를 통해 올바르게 업데이트됩니다.

![해결된 문제](../assets/fix.svg)<!-- Issue ACAP-1172 --> 제품 편집 페이지의 관리 UI에서 숨겨진 제품 이미지가 숨겨지지 않은 문제를 해결했습니다. 이제 이미지 가시성 상태가 올바르게 표시됩니다.

![문제 해결](../assets/fix.svg)<!-- Issue ACAP-1170 --> 역직렬화 오류로 인해 AEM Assets의 제품 이미지가 Adobe Commerce으로 동기화되지 않는 문제를 해결했습니다. 이제 모든 이미지 특성(`image`, `small_image` 및 `swatch_image`)이 올바르게 동기화됩니다.

## v1.2.7

_2025년 11월 6일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.5 이상 릴리스.

![문제 해결](../assets/fix.svg)<!-- Issue ACAP-1169 --> **미니 장바구니**, **장바구니**, **체크아웃** 페이지에서 AEM Assets 통합을 활성화한 후 제품 썸네일 이미지가 일관되지 않게 표시되는 문제를 해결했습니다. 이제 페이지를 새로 고친 후에도 제품 이미지가 모든 페이지에서 일관되게 렌더링됩니다.

## v1.2.6

_2025년 10월 24일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.5 이상 릴리스.

![문제 해결](../assets/fix.svg)<!-- Issue ACAP-1163 --> 연속 일괄 제품 업데이트 요청으로 인해 후속 업데이트가 제대로 처리되지 않는 상태 추적 플래그가 남아 있는 문제가 해결되었습니다. 이제 오류가 발생해도 상태가 재설정됩니다.

## v1.2.5

_2025년 10월 22일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.5 이상 릴리스.

![문제 해결](../assets/fix.svg)<!-- Issue ACAP-1161 --> Adobe Commerce 관리에서 기존 이미지 매핑의 위치를 업데이트하면 PHP 유형 오류가 발생하는 문제가 해결되었습니다.

## v1.2.4

_2025년 10월 17일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.5 이상 릴리스.

![문제가 해결되었습니다](../assets/fix.svg)<!-- Issue ACAP-1155 --> 사용자 지정 특성의 전반적인 안정성이 개선되었습니다. 이제 비동기 API를 사용할 때 사용자 지정 특성이 올바르게 업데이트됩니다.

![문제 해결](../assets/fix.svg)<!-- Issue ACAP-1074 --> 이제 기본 링크 URL이 정의된 경우 [제품-자산 동기화](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/store-urls#configure-the-base-url){target=_blank}가 실패하지 않습니다.

## v1.2.3

_2025년 10월 2일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.5 이상 릴리스.

![해결된 문제](../assets/fix.svg)<!-- Issue ACAP-1135 --> 제품 특성을 업데이트하는 문제가 해결되었습니다. 이제 제품 속성이 예상대로 업데이트되며, 업데이트에 실패했을 때 200 응답 대신 적절한 오류가 반환됩니다.

## v1.2.2

_2025년 9월 18일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.5 이상 릴리스.

![해결된 문제](../assets/fix.svg)<!-- Issue ACAP-1110 --> 미니 장바구니, 장바구니 및 체크아웃 페이지의 전반적인 이미지 안정성이 향상되었습니다. 이제 이러한 페이지의 이미지가 제대로 로드됩니다.

## v1.2.0

_2025년 8월 7일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.5 이상 릴리스.

![새 문제](../assets/new.svg)<!-- Issue ACAP-1018 --> 이제 상인은 관리자로부터 Assets 통합을 구성할 때 [시각화 소유자](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/get-started/setup-synchronization){target=_blank}를 선택하여 이미지 및 미디어 에셋의 소스를 선택할 수 있습니다.

![새 문제](../assets/new.svg)<!-- Issue ACAP-1078 --> [사용자 지정 자동 일치](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/synchronize/custom-match){target=_blank} 끝점을 새 `asset_matches` 특성으로 업데이트했습니다. 이 변경 사항으로 고유한 일치 논리를 구현하여 특정 `productSku`과(와) 연결된 모든 자산을 반환할 수 있습니다.

## v1.1.2

_2025년 6월 11일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.5 이상 릴리스.

![새 문제](../assets/new.svg)<!-- Issue ACAP-1041 --> Adobe Commerce 2.4.8 및 PHP 8.4에 대한 지원을 추가했습니다.

## v1.1.0

_2025년 4월 23일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.5 이상 릴리스.

![새 문제](../assets/new.svg)<!-- Issue ACAP-955 --> 이제 AEM 배달 URL 대신 [사용자 지정 도메인 URL](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/get-started/setup-synchronization#optional-configure-the-custom-domain-url)을 사용할 수 있습니다. 판매자가 AEM 대시보드에서 **사용자 지정 도메인 이름**&#x200B;을(를) 설정하는 경우 Commerce에서 이 **사용자 지정 도메인 URL**&#x200B;을(를) 추가해야 합니다.

![문제를 해결했습니다](../assets/fix.svg)<!-- Issue ACAP-987 --> AEM Assets 동기화 프로세스에 대한 전체 로그를 개선했습니다.

## v1.0.22

_2025년 3월 12일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.5 이상 릴리스.

![새로운 문제](../assets/new.svg)<!-- Issue ACAP-xx --> 이제 Assets 선택기에서 제품 범주 및 페이지 빌더에서 생성한 콘텐츠와 AEM Assets 이미지를 매핑할 수 있도록 하려면 [Assets 선택기 IMS 클라이언트 ID](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/get-started/setup-synchronization)가 필요합니다.

## v1.0.20

_2025년 2월 11일_

[!BADGE 지원됨]{type=Informative tooltip="지원됨"} Adobe Commerce 버전 2.4.5 이상 릴리스.

![새로운](../assets/new.svg)<!-- Issue ACAP-xx --> 일반 가용성 릴리스.
