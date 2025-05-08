---
title: ' [!DNL Payment Services]에서 배송 추적'
description: Paypal 판매자 대시보드에 표시되는  [!DNL Payment Services] 배송 및 추적 정보를 사용자 지정합니다.
feature: Payments, Paas, Saas
exl-id: 17aede1f-56ae-441a-b723-3193e865e469
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# [!DNL Payment Services]에서 배송 추적

[!DNL Payment Services]을(를) 통해 판매자는 PayPal 판매자 대시보드에서 배송에 대한 추적 정보를 볼 수 있습니다.

Adobe Commerce의 배송 표에 대한 자세한 내용은 [배송](https://experienceleague.adobe.com/ko/docs/commerce-admin/stores-sales/order-management/shipments){target=_blank} 항목을 참조하십시오.

## 배송 추적이 작동하는 방식

PayPal은 추적 정보를 처리하기 위해 `capture_id`을(를) 받아야 하므로 이 기능은 주문 송장 발행 여부에 따라 달라집니다. 판매자가 캡처 전에 제품을 배송하는 경우 추적 정보가 PayPal로 전송되지 않습니다.

>[!NOTE]
>
> 올바른 품목을 납품과 연관시켜 추적 번호당 납품을 하나 생성하는 것이 좋습니다.

## 추적 번호 추가

다음 지침은 [!DNL Payment Services]을(를) 사용하여 Adobe Commerce에서 선적을 만드는 과정을 안내합니다.

1. _관리자_ 사이드바에서 **[!UICONTROL Sales]** > **[!UICONTROL Orders]**(으)로 이동합니다.

1. 선택한 순서에 대한 **[!UICONTROL Action]** 열에서 **[!UICONTROL View]**&#x200B;을(를) 클릭합니다.

1. **[!UICONTROL Ship]**&#x200B;을(를) 클릭합니다.

1. **[!UICONTROL Payment & Shipping Method]** 블록까지 아래로 스크롤한 다음 **[!UICONTROL Shipping Information]**&#x200B;에서 **[!UICONTROL Add Tracking Number]**&#x200B;을(를) 클릭합니다.

1. **[!UICONTROL Carrier]**&#x200B;을(를) 설정합니다.

1. 게재를 추적하려면 **[!UICONTROL Title]** 및 **[!UICONTROL Number]** 을(를) 입력하십시오.

1. **[!UICONTROL Submit Shipment]**&#x200B;을(를) 클릭합니다.

>[!NOTE]
>
> 또는 배송 모듈을 사용하여 추적 번호 정보를 입력할 수 있습니다. 배송 모듈이 `tracking_number` 필드에 추적 번호 정보를 저장하고 있는지 확인하십시오.

### 서드파티와의 호환성

모든 타사 확장은 [Commerce API](https://developer.adobe.com/commerce/webapi/rest/attributes/#ShipmentRepositoryInterface){target=_blank}를 통해 배송 엔터티를 만들 때 기능과 호환됩니다.
