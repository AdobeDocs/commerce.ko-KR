---
title: 여러 웹 사이트 및 범위 구성
description: 여러 웹 사이트 및 스토어 범위에 대한 재고 및 게재 방법을 구성합니다.
role: Admin
level: Experienced
feature: Shipping/Delivery, Inventory, Configuration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---

# 여러 웹 사이트 및 범위 구성

여러 웹 사이트, 스토어 및 스토어 보기에 맞게 몇 가지 요소에 대해 [범위](https://experienceleague.adobe.com/ko/docs/commerce-admin/start/setup/websites-stores-views#scope-settings)를 설정할 수 있습니다.

- 범위당 [재고 관리](https://experienceleague.adobe.com/ko/docs/commerce-admin/inventory/stocks/stocks-manage)

- 범위당 [!DNL Delivery Methods] 관리

웹 사이트 또는 스토어 범위에 재고를 할당할 수 있습니다. 그런 다음 저장소 소스를 업데이트하여 사용 가능한 게재 방법(홈 게재, 저장소 픽업)을 설정합니다.

구성을 정상적으로 업데이트하면 Adobe Commerce 상점 첫 화면의 PDP(제품 세부 사항 페이지)에 있는 상점 픽업 옵션은 상점 선택을 허용하는 재고 소스에서 사용 가능한 제품에 대해서만 선택할 수 있습니다.

## 매장 내 픽업 설정 관리

관리자의 [배달 메서드 구성](enable-general.md#delivery-methods)에서 각 웹 사이트 또는 스토어 범위에 대해 [!UICONTROL In-Store Pickup] 옵션을 활성화하거나 비활성화합니다.

1. **[!UICONTROL Stores > Configuration]**(으)로 이동합니다.

1. 구성할 범위(저장할 웹 사이트)를 선택합니다.

1. 범위를 선택한 상태에서 **[!UICONTROL Sales > Delivery Methods]**(으)로 이동합니다.

1. **[!UICONTROL In-Store Pickup]** 배달 메서드를 사용하지 않도록 설정하거나 사용하도록 설정합니다.

또한 이 섹션에서 전체적으로 커브사이드 또는 매장 내 픽업을 사용할 수 있는지 여부를 관리할 수도 있습니다.

스톡 소스당 [!UICONTROL In-Store Pickup] 및 [!UICONTROL Delivery Method] 설정을 관리합니다. 구현에 비해 완벽한 유연성을 제공하기 위해 다양한 다른 구성이 존재합니다.
