---
title: Inventory management Source 전송
description: Adobe Commerce Inventory management을 사용하여  [!DNL Store Fulfillment solution] 에 대한 주식을 구성합니다. 새 재고를 설정하고 기본 재고에서 재고를 이전하여 Store Fulfillment 솔루션에 필요한 Store Pickup 기능을 사용하도록 구성된 소스에 할당할 수 있습니다.
role: Admin
level: Intermediate
feature: Shipping/Delivery, Inventory, Configuration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---


# Inventory management Source 전송

[!DNL Store Fulfillment] 솔루션은 기본 Adobe Commerce Inventory management을 사용합니다. 기본적으로 [!DNL Commerce] 구성은 모든 웹 인벤토리를 기본 재고에 할당하며, 이 기본 재고는 추가 원본을 할당할 수 없습니다. 웹 사이트에는 단일 재고만 지정할 수 있으므로 판매자는 신규 재고를 구성하고 필요한 경우 기본 출처 재고를 적절한 범위에 지정된 출처로 이전해야 합니다. 그런 다음 출처를 새 재고에 지정할 수 있습니다.

>[!IMPORTANT]
>
>판매자는 그룹 및 번들 제품 유형에 포함된 모든 제품에 대한 기본 소스를 유지 관리해야 합니다. 이러한 제품에는 재고 품목의 최소 수량 임계값을 충족하고 재고 상태가 [!UICONTROL In Stock]인 재고 수량이 필요합니다.

이러한 구성 변경을 통해 다음 세 가지 사항을 달성할 수 있습니다.

1. [인벤토리를 소스로 전송](https://experienceleague.adobe.com/ko/docs/commerce-admin/inventory/quantities/inventory-transfer)하여 기본 재고/원본에서 새 재고/원본으로 인벤토리를 이동합니다.

1. [소스를 일괄 할당](https://experienceleague.adobe.com/ko/docs/commerce-admin/inventory/quantities/bulk-assignment)하여 모든 제품에 대한 새 소스를 추가합니다.

1. [제품 특성에 대한 대량 업데이트를 완료](https://experienceleague.adobe.com/ko/docs/commerce-admin/catalog/product-attributes/create/bulk-product-attribute-update)하여 `Allow Store Pickup` 및 `Allow Home Delivery` 특성을 기존 제품에 추가합니다. 솔루션이 설치되면 속성에 최적의 *기본값* 값이 있습니다. 그러나 이러한 속성은 일괄 updaContes 프로세스를 완료할 때까지 기존 제품에 적용되지 않습니다.

재고는 선택한 출처(소매점 위치 또는 전자 상거래 창고)에서 공제됩니다. 전자 상거래 창고로 사용되는 출처는 매장 픽업 위치와 동일한 재고에 할당되어야 하고 소매 위치보다 우선 순위가 지정되어야 한다. 자세한 내용은 [재고 소스 우선 순위 지정](https://experienceleague.adobe.com/ko/docs/commerce-admin/inventory/stocks/stocks-prioritize-sources)을 참조하십시오.

재고, 재고 및 소스 관리에 대한 자세한 내용은 Adobe Commerce 사용 설명서를 참조하십시오.

- [인벤토리 관리](https://experienceleague.adobe.com/ko/docs/commerce-admin/inventory/introduction)

- [재고 수량 관리](https://experienceleague.adobe.com/ko/docs/commerce-admin/inventory/quantities/quantities-manage)

- [재고 관리](https://experienceleague.adobe.com/ko/docs/commerce-admin/inventory/stocks/stocks-manage)

- [소스 관리](https://experienceleague.adobe.com/ko/docs/commerce-admin/inventory/sources/sources-manage)

- [주식에 대한 소스 우선 순위 지정](https://experienceleague.adobe.com/ko/docs/commerce-admin/inventory/stocks/stocks-prioritize-sources)

- [제품 특성에 대한 대량 업데이트](https://experienceleague.adobe.com/ko/docs/commerce-admin/catalog/product-attributes/create/bulk-product-attribute-update)


>[!IMPORTANT]
>
>재고 및 재고 소스에 대한 구성을 변경하면 통합 시스템에 다운스트림으로 영향을 줄 수도 있습니다. 인벤토리 구성 변경 사항이 이러한 시스템에 미치는 영향을 이해해야 합니다.
