---
title: '[!DNL Data Connection] 소개'
description: ' [!DNL Data Connection] 확장을 사용하여 Adobe Commerce 데이터를 Adobe Experience Platform과 통합하는 방법을 알아봅니다.'
recommendations: noCatalog
exl-id: 660f9337-cad8-47fb-a959-0770f0fd813c
TQID: https://experienceleague.adobe.com/-wfkGM2isTVmAaJokndxVy0-UtZ4pM9msYXmh2IE-Hc
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: c4147b6e-073b-4d3c-9ab1-d60f2f4434ef
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
  - id: fd2e3797-f2ea-4b36-a9af-52acf5e90513
source-git-commit: 5ba5dfa23580b5eefa8271277e78c6ea67879b90
workflow-type: tm+mt
source-wordcount: 1373
ht-degree: 1%

---

# [!DNL Data Connection] 소개

>[!IMPORTANT]
>
>Experience Platform 커넥터의 이름이 [!DNL Data Connection]&#x200B;(으)로 변경되었습니다.

[!DNL Data Connection] 확장은 Adobe Commerce 웹 인스턴스를 Adobe Experience Platform 및 Edge Network에 연결합니다. 모바일 앱 개발자의 경우 Adobe Experience Platform Mobile SDK과 Commerce을 함께 사용하여 Commerce 데이터를 캡처하고 Experience Platform으로 보냅니다. [자세히 알아보기](./mobile-sdk-epc.md)

다중 웹 사이트 판매자는 Experience Platform 샌드박스 선택을 포함하여 웹 사이트별로 적용 가능한 [!DNL Data Connection] 설정을 구성할 수 있습니다. 전역 필드와 웹 사이트 범위 필드는 [Commerce 데이터를 Adobe Experience Platform에 연결](connect-data.md#configuration-scope)을 참조하십시오.

Commerce 스토어에는 풍부한 데이터가 있습니다. 쇼핑객이 사이트에서 제품을 검색하고, 보고, 최종적으로 구매하는 방법에 대한 정보는 보다 개인화된 쇼핑 경험을 만들 수 있는 기회를 보여줄 수 있습니다. 해당 데이터는 장바구니 가격 규칙 및 동적 블록과 같은 기본 Commerce 기능을 알릴 수 있지만 데이터는 Commerce 인스턴스에 격리된 상태로 유지됩니다.

Adobe Experience Platform은 Commerce 스토어의 데이터로 하이드레이션될 때 해당 데이터를 Edge Network을 통해 다른 Adobe DX 제품에 배포하여 구매자의 구매 행동에 대한 통찰력을 확보할 수 있는 기술 제품군을 제공합니다. 이러한 심층적인 통찰력을 통해 모든 채널에서 보다 개인화된 쇼핑 경험을 만들 수 있습니다.

다음 이미지는 [!DNL Data Connection] 확장을 설치하고 구성할 때 Commerce 데이터가 저장소에서 다른 Adobe DX 제품으로 흐르는 방식을 보여 줍니다.

![데이터가 Experience Platform Edge로 이동하는 방법](assets/commerce-edge.png)

위의 이미지에서 행동, 백오피스 및 고객 프로필 데이터는 SDK, API 및 소스 커넥터를 사용하여 Experience Platform Edge로 전송됩니다. 확장이 데이터 공유 복잡성을 처리하므로 이러한 부분이 어떻게 작동하는지 완전히 이해할 필요는 없습니다. 이벤트 데이터가 에지에 있으면 다운스트림 Adobe DX 제품(예: [Real-Time CDP](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html), [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html), [Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/analyze/admin-overview/analytics-overview.html) 및 [Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html))에서 사용할 수 있습니다. 안내식 예제는 [Adobe Journey Optimizer을 사용하여 포기한 장바구니 전자 메일을 보내기](using-ajo.md) 및 [Commerce 이벤트 데이터를 사용하여 Real-Time CDP에서 대상 만들기](create-audience.md)를 참조하십시오.

## Experience Platform 데이터를 다시 Commerce으로 가져오기

[!DNL Data Connection] 확장을 사용하여 Commerce 데이터를 Experience Platform에 보내는 것은 Commerce의 데이터 공유 기능의 한 부분입니다. 선택적 확장인 반대쪽은 [Audience Activation](https://experienceleague.adobe.com/docs/commerce-admin/customers/audience-activation.html)입니다. 이 확장을 사용하면 Real-Time CDP에서 대상을 작성하고 이러한 대상을 Commerce 스토어에 배포하여 장바구니 가격 규칙, 관련 제품 규칙 및 동적 블록을 알릴 수 있습니다.

높은 수준에서 Commerce 스토어에서 Experience Platform으로 그리고 Audience Activation 확장을 통해 다시 이동하는 데이터 흐름은 다음과 같습니다.

![[!DNL Data Connection] 흐름](assets/data-connection.png)

Commerce에서 Experience Platform으로, Experience Platform에서 Commerce으로 연결을 설정한 후에도 데이터가 계속 흐릅니다. 업그레이드에서 다시 연결할 필요가 없는 한 다시 연결할 필요가 없습니다.

## 개념

이 두 시스템 간에 데이터를 공유하려면 몇 가지 개념을 이해해야 합니다.

- **데이터 형식** — [!DNL Data Connection]은(는) 브라우저에서 **동작(상점)** 데이터, Commerce 서버에서 **백 오피스** 데이터 및 **프로필** 데이터를 수집합니다. 관리자가 storefront 컬렉션 **Storefront 이벤트**&#x200B;에 레이블을 지정합니다. 전체 분류법은 [Commerce 데이터 유형](data-ingestion.md)을 참조하십시오.

- **동작(상점 첫 화면) 데이터** — `addToCart`, `pageView`, `startCheckout` 및 `completeCheckout`과 같은 사이트의 쇼핑객 상호 작용에서 캡처됩니다. [상점 이벤트](events.md#storefront-events)를 참조하세요.

- **사무실 뒷면 데이터** — [`orderPlaced`](events-backoffice.md#orderplaced) 및 [`orderShipped`](events-backoffice.md#ordershipmentcompleted)과(와) 같은 [주문 상태](events-backoffice.md#order-status) 이벤트를 포함하여 Commerce 서버에서 캡처됩니다. [이전 사무실 이벤트](events-backoffice.md)를 참조하세요.

- **프로필 레코드** — 구매자 프로필이 Commerce에서 만들어질 때 전송된 스냅숏 데이터입니다. [프로필 레코드](events-profilerecord.md) 및 [프로필 레코드 스키마 업데이트](profile-data.md)를 참조하세요.

- **프로필 이벤트** — 서버의 프로필 라이프사이클 변경에 대한 시계열 이벤트입니다. [고객 프로필 이벤트](events-backoffice.md#customer-profile-events)를 참조하세요.

- **Experience Platform 및 Edge Network** - 대부분의 Adobe DX 제품에 대한 데이터 웨어하우스 Experience Platform으로 전송된 데이터는 Experience Platform Edge Network을 통해 Adobe DX 제품에 전파됩니다. 예를 들어 Journey Optimizer을 시작하고, Edge에서 특정 Commerce 이벤트 데이터를 검색하고, Journey Optimizer에서 포기한 장바구니 이메일을 작성할 수 있습니다. 그러면 Journey Optimizer 스토어에 구매하지 않은 카트가 있는 경우 Commerce에서 해당 이메일을 보낼 수 있습니다. [Experience Platform 및 Edge Network](https://experienceleague.adobe.com/docs/platform-learn/data-collection/web-sdk/overview.html)에 대해 자세히 알아보세요.

- **스키마** - 스키마는 전송 중인 데이터 구조를 설명합니다. Experience Platform에서 Commerce 데이터를 수집하려면 먼저 데이터의 구조를 설명하는 스키마를 구성하고 각 필드 내에 포함될 수 있는 데이터 유형에 대한 제약 조건을 제공해야 합니다. 스키마는 기본 클래스와 0개 이상의 스키마 필드 그룹으로 구성됩니다. 스키마는 모든 Adobe DX 제품이 읽을 수 있는 XDM 구조를 사용합니다. 스키마는 Experience Platform으로 전송된 데이터를 모든 DX 제품에서 이해할 수 있도록 합니다. [스키마](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html)에 대해 자세히 알아보세요.

- **데이터 집합** - 데이터 수집을 위한 저장소 및 관리 구성으로서, 일반적으로 스키마(열)와 필드(행)를 포함하는 테이블입니다. 데이터 세트에는 저장하는 데이터의 다양한 측면을 설명하는 메타데이터도 포함됩니다. Adobe Experience Platform에 성공적으로 수집된 모든 데이터는 데이터 세트 내에 포함됩니다. [데이터 세트](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/overview.html)에 대해 자세히 알아보세요.

- **데이터스트림** - Adobe Experience Platform에서 다른 Adobe DX 제품으로 데이터를 이동할 수 있는 ID입니다. 이 ID는 특정 Adobe Commerce 인스턴스 내의 특정 웹 사이트에 연결되어야 합니다. 이 데이터 스트림을 만들 때 위에서 만든 XDM 스키마를 지정합니다. [데이터스트림](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html)에 대해 자세히 알아보세요.

## 지원되는 아키텍처

[!DNL Data Connection] 확장은 다음 아키텍처에서 사용할 수 있습니다.

- PHP/Luma
- [PWA Studio](https://developer.adobe.com/commerce/pwa-studio/integrations/adobe-commerce/aep/)
- [AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/integrations/aep.html)

>[!BEGINSHADEBOX]

## 사전 요구 사항

[!DNL Data Connection] 확장을 사용하려면 다음 항목이 있어야 합니다.

- Adobe Commerce 2.4.4 이상
- Adobe ID 및 조직 ID
- [ACDL(Adobe Client Data Layer)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/client-data-layer/overview.html), 상점 이벤트 데이터를 수집하는 데 필요
- 다른 Adobe DX 제품에 대한 자격.

>[!ENDSHADEBOX]

## 확장 활성화 {#enable-extension}

높은 수준에서 [!DNL Data Connection] 확장을 활성화하려면 다음 단계를 수행해야 합니다.

1. [!DNL Data Connection] 확장을 [설치](install.md)합니다.
1. Adobe 계정에 [로그인](https://helpx.adobe.com/manage-account/using/access-adobe-id-account.html)하고 조직 ID를 확인하려면 [확인](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html#concept_EA8AEE5B02CF46ACBDAD6A8508646255)하세요. 조직 ID 는 공급된 Experience Cloud 회사와 연결된 ID입니다. 이 ID는 24자의 영숫자 문자열과 `@AdobeOrg`(포함 필수)로 구성됩니다.
1. Experience Platform의 데이터 수집에 대한 [권한이 있는지 확인](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html).
1. 수집 및 전송할 수 있는 [데이터 형식](data-ingestion.md)을 검토하십시오.
1. Commerce 관련 필드 그룹으로 [시계열 이벤트 스키마](update-xdm.md) 또는 [프로필 레코드 데이터 스키마](profile-data.md)를 만들거나 업데이트하십시오.
1. 만들거나 업데이트한 스키마를 기준으로 [데이터 집합을 만듭니다](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html#create-a-dataset). 이 데이터 세트에는 Experience Platform Edge으로 전송된 Commerce 데이터가 포함되어 있습니다.
1. [데이터 스트림을 만들고](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html) Commerce 관련 필드 그룹이 포함된 XDM 스키마를 선택합니다.
1. [Commerce 서비스에 연결](../landing/saas.md).
1. [Adobe Experience Platform에 연결](connect-data.md).

이 안내서의 나머지 부분에서는 이러한 모든 단계를 보다 자세히 안내하므로 Commerce 스토어에서 Adobe DX 제품의 강력한 기능을 최대한 활용하여 속도를 높일 수 있습니다.

>[!NOTE]
>
>모바일 개발자의 경우 Adobe Experience Platform Mobile SDK을 Commerce과 [통합](./mobile-sdk-epc.md)하는 방법에 대해 알아보십시오.

## HIPAA 준비

[!DNL Data Connection] 확장을 사용하면 [!DNL Commerce] 백 오피스 데이터를 Experience Platform과 공유하고 HIPAA 준수를 유지할 수 있습니다. [자세히 알아보기](hipaa-readiness.md)

## 대상자

이 안내서는 Commerce 스토어를 풍요롭게 하고 개인화하여 고객의 쇼핑 경험을 향상시키고자 하는 Adobe Commerce 판매자를 위해 설계되었습니다.

## 지원

이 안내서에서 다루지 않는 정보가 필요하거나 질문이 있는 경우 다음 리소스를 사용하십시오.

- [도움말 센터](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/overview.html){target="_blank"}
- [지원 티켓](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket){target="_blank"} — 추가 지원을 받으려면 티켓을 제출합니다.
