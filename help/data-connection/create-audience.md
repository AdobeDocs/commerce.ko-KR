---
title: ' [!DNL Commerce] 이벤트 데이터를 사용하여 Real-Time CDP에서 대상 만들기'
description: ' [!DNL Commerce] 이벤트 데이터를 사용하여 Real-Time CDP에서 대상자를 만드는 방법을 알아봅니다'
role: Admin, Developer
feature: Personalization, Integration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '1040'
ht-degree: 0%

---

# [!DNL Commerce] 이벤트 데이터를 사용하여 Real-Time CDP에서 대상 만들기

[!DNL Commerce] 저장소에서 캡처한 이벤트 데이터를 사용하여 Real-Time CDP에서 대상을 만듭니다. 캡처된 데이터는 검색 행동, 과거 구매, 프로필 속성, 전환 또는 이탈 성향, 충성도 상태, 높은 고객 가치와 낮은 고객 가치 등을 기반으로 합니다.

## 어떤 데이터를 사용해야 합니까?

상점, 백오피스 및 프로필 이벤트의 데이터를 사용하여 Real-Time CDP에서 대상을 만듭니다.

| 데이터 유형 | Storefront 데이터(행동 이벤트) | 백오피스 데이터(서버측 이벤트) | 고객 프로필 및 세그먼트 데이터 |
|---|---|---|---|
| **정의** | 고객이 사이트에서 수행하는 클릭 또는 작업입니다. | 각 주문(과거 및 현재)의 라이프사이클 및 세부 정보에 대한 정보. | 구매자가 누구이며 어떤 세그먼트에 해당하는지 지정합니다. |
| **Adobe Commerce에서 캡처한 이벤트** | [productPageView](events.md#productpageview)<br>[addToCart](events.md#addtocart) | [주문](events.md#completecheckout)<br>[주문](events-backoffice.md#orderplaced)<br>[주문 라인 항목 환불](events-backoffice.md#orderlineitemrefunded)<br>[주문 취소됨](events-backoffice.md#ordercancelled)<br>[주문 내역](connect-data.md#send-historical-order-data) | [createAccount](events.md#createaccount)<br>[editAccount](events.md#editaccount)<br>[프로필 레코드](events-profilerecord.md) |

## 다른 고객들은 어떤 성과를 얻었습니까?

Adobe [!DNL Commerce] 고객은 Real-Time CDP에 내장된 대상을 활성화하고 해당 대상을 [!DNL Commerce] 인스턴스에 배포함으로써 비즈니스에 상당한 영향을 미쳤습니다.

글로벌 다중 브랜드 의류 소매업체:

- 100 만 개의 통합 고객 프로필을 제공하는 신뢰할 수 있는 소스
- 채널 전반에 걸쳐 참여할 수 있는 &quot;고의적인 고객&quot;의 40명 이상의 고유 대상 생성

한 세계적인 음료 회사는 다음을 수집했다:

- 100개국 이상에서 9,800만 개의 고객 프로필

## 시작하겠습니다.

이 문서에서는 다음 방법을 알아봅니다.

- 이벤트가 수집하는 [!DNL Commerce] 데이터를 기반으로 Real-Time CDP에서 대상을 만듭니다.
- [!DNL Commerce] 스토어에 대해 해당 대상자 활성화
- [!DNL Commerce]의 대상자를 사용하여 장바구니 가격 규칙을 알립니다.

>[!IMPORTANT]
>
>[!DNL Commerce] 샌드박스 환경을 사용하여 이 문서에 설명된 작업을 완료하십시오. 이렇게 하면 Experience Platform으로 보내는 상점 및 백오피스 이벤트 데이터가 프로덕션 이벤트 데이터를 희석하지 않습니다.

### 전제 조건

시작하기 전에 다음을 확인하십시오.

- Real-Time CDP을 사용할 수 있도록 프로비저닝되었습니다. 확실하지 않은 경우 프로젝트 및 환경을 관리하는 시스템 통합자나 개발 팀에 문의하십시오.
- [!DNL Commerce]에서 [!DNL Data Connection] 확장을 [설치](install.md) 및 [구성](connect-data.md)했습니다.
- [!DNL Commerce] 이벤트 데이터가 Experience Platform Edge에 도착하는 것을 [확인](connect-data.md#confirm-that-event-data-is-collected)했습니다.

### 1. 대상자 만들기

대상자는 유사한 비헤이비어 또는 특성을 공유하는 고객 집합입니다. 이 연습에서는 상점의 특정 제품에 관심이 있는 사용자에게 자격을 부여하는 대상을 만듭니다.

이 연습을 간소화하려면 [productPageView](events.md#productpageview) 이벤트의 이벤트 데이터를 사용합니다. 이 이벤트는 제품 이름, SKU, 가격 등 조회한 제품에 대한 세부 정보를 캡처합니다.

이 이벤트 데이터를 사용하여 SKU(제품 식별자)가 사이트의 특정 제품과 같고 이벤트가 마지막 날 이내에 발생하는 &quot;제품 보기&quot; 이벤트가 하나 이상 있는 개인을 대상에 포함하도록 지정하십시오. &#x200B;

1. Experience Platform을 열고 왼쪽 탐색 메뉴에서 **[!UICONTROL Audiences]**&#x200B;을(를) 선택합니다.

   ![대상 대시보드](assets/audience-left-rail.png)

1. **[!UICONTROL Create Audience]**&#x200B;을(를) 클릭합니다.

   ![대상 만들기](assets/browse-create-audience.png)

   **세그먼트 빌더** 작업 영역이 표시됩니다.

1. **세그먼트 빌더** 작업 영역에서 **빌드 규칙** 생성 방법을 선택합니다.

   ![규칙 작성](assets/build-rule.png)

   **세그먼트 빌더** 작업 영역에서 대상자에 대한 규칙과 조건을 정의합니다&#x200B;. 이러한 규칙과 조건은 Commerce 스토어의 이벤트 및 프로필 데이터를 기반으로 하며 사용자가 대상자에 적합한지 여부를 결정하는 기준을 정의합니다. 예를 들어 특정 제품을 본 사용자 또는 특정 시간대 내에 구매한 사용자를 포함하는 규칙을 만들 수 있습니다. [세그먼트 빌더](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder) 및 규칙과 조건에 대해 자세히 알아보세요.

1. [이벤트](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder#events) 탭을 선택합니다.

   ![이벤트 탭](assets/audience-events-tab.png)

1. 제품 보기 이벤트 유형을 검색합니다. 그런 다음 **세그먼트 빌더** 작업 영역으로 끌어다 놓습니다.

1. **이벤트** 탭으로 돌아가서 `productListItems` 필드 아래의 데이터 필드인 &quot;SKU&quot;를 검색합니다. **제품 보기** 이벤트 위에 있는 **세그먼트 빌더** 작업 영역으로 끌어다 놓습니다.

   대상을 만들 특정 제품을 지정할 수 있는 **이벤트 규칙** 섹션이 표시됩니다.

   ![SKU 선택](assets/audience-addsku.png)

1. **모든 시간**&#x200B;을 클릭하고 *1* 값을 가진 *마지막에*&#x200B;을(를) 선택하여 시간 간격을 하루로 설정합니다.

   대상을 작성할 때 최근 활동을 캡처하는 시간 간격을 지정할 수 있습니다. 시간 간격을 설정하면 특정 시간대 내의 최근 상호 작용 또는 행동에 따라 사용자를 타깃팅할 수 있습니다.

1. 작업 영역 오른쪽의 **대상 속성** 섹션에서 대상에 대한 이름, 설명 및 평가 메서드를 제공하여 대상 속성을 설정합니다.

1. 대상자를 저장하려면 **[!UICONTROL Save and Close]**&#x200B;을(를) 클릭합니다.

   대상자의 세부 정보가 **대상자** 대시보드에 표시됩니다.

### 2. 대상을 [!DNL Commerce] 대상으로 활성화합니다.

대상을 [!DNL Commerce] 대상에 대해 활성화하여 [!DNL Commerce]에서 사용할 수 있도록 합니다.

>[!IMPORTANT]
>
>[!DNL Commerce]을(를) 데이터를 수신할 수 있는 대상으로 아직 설정하지 않은 경우 [Adobe [!DNL Commerce] 연결](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/personalization/adobe-commerce) 항목을 참조하십시오.

1. 대상자의 **세부 정보** 탭에서 **대상에 활성화**&#x200B;를 클릭합니다.

1. [!DNL Commerce] 대상을 선택하십시오. 그런 다음 **다음**&#x200B;을 클릭합니다.

1. **[!UICONTROL Finish]**&#x200B;을(를) 클릭하여 활성화 프로세스를 완료합니다.

## 3. 대상자 대시보드에서 대상자 보기

[!DNL Commerce]에서 **Real-Time CDP 대상** 대시보드를 사용하여 [!DNL Commerce] 인스턴스에 대해 개인화할 수 있는 모든 [활성](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-edge-personalization-destinations) 대상을 볼 수 있습니다.

**Real-Time CDP 대상** 대시보드에 액세스하려면 _관리자_ 사이드바로 이동한 다음 **[!UICONTROL Customers]** > **[!UICONTROL Real-time CDP Audience]**(으)로 이동하십시오.

대시보드에서 만든 대상자를 찾습니다. 장바구니 가격 규칙 또는 동적 블록에서 사용되고 있지 않습니다. 다음 섹션에서는 대상자를 장바구니 가격 규칙에 연결합니다.

![Real-Time CDP 대상 대시보드](assets/real-time-cdp-dashboard.png)

### 4. 대상자를 기반으로 장바구니 가격 규칙 만들기

이 섹션에서는 새 대상자를 기반으로 장바구니 가격 규칙을 만드는 방법을 보여줍니다.

1. 새 대상이 **Real-Time CDP 대상** 대시보드에 표시되는지 확인하십시오.
1. [장바구니 가격 규칙을 만듭니다](https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/promotions/cart-rules/price-rules-cart-create).
1. 새 대상을 사용하여 장바구니 가격 규칙의 [조건을 설정](https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/promotions/cart-rules/price-rules-cart-create#use-real-time-cdp-audiences-to-set-a-condition)합니다.
1. 제품을 장바구니에 추가할 때 수행할 작업을 [설정](https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/promotions/cart-rules/price-rules-cart-create#step-3-define-the-actions)합니다.
1. 장바구니 가격 규칙을 계속 구성합니다.
1. 샌드박스 인스턴스의 고객 보기로 이동합니다.
1. 대상을 기반으로 한 제품을 장바구니에 추가합니다. 장바구니 가격 규칙이 활성화되어 있습니다.

## 줄바꿈

이 연습에서는 Real-Time CDP에서 대상을 만들고 [!DNL Commerce] 대상에 대해 활성화했습니다. 그런 다음 [!DNL Commerce] 관리자에서 해당 대상자를 기반으로 장바구니 가격 규칙을 만들고 샌드박스 환경에서 규칙을 사용하도록 설정했습니다.
