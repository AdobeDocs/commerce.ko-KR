---
title: 빈 공간
description: Void를 사용하면 구매 금액에 대한 승인이 차단되거나 보류된 신용 카드 또는 직불 카드 계정의 자금을 확보할 수 있습니다.
feature: Payments, Checkout
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 0%

---

# 빈 공간

[!DNL Payment Services]을(를) 사용하면 기존 Commerce 기능을 사용하여 트랜잭션을 무효화할 수 있습니다. Void를 사용하면 구매 금액에 대한 승인이 차단되거나 보류된 신용 카드 또는 직불 카드 계정의 자금을 확보할 수 있습니다.

>[!NOTE]
>
>지급이 아직 수집되지 않은 경우에만 거래를 무효화할 수 있습니다.

판매 시점에 펀드만 승인하도록 스토어가 [구성](https://experienceleague.adobe.com/en/docs/commerce-admin/config/sales/payment-methods/payment-methods#payment-actions){target="_blank"}된 경우(캡처하지 않음) 스토어에서 구매하면 Commerce 관리자에서 `Processing` 상태의 주문이 발생합니다.

송장이 발행되지 않은 주문을 [취소](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/point-of-purchase/assist/customer-account-create-order){target="_blank"}할 수도 있습니다. 해당 취소 프로세스의 일부로 캡처되지 않은 승인도 무효화됩니다.

>[!NOTE]
>
>주문을 취소하면 공백도 생성되지만, 주문을 취소하면 취소가 트리거되지 않습니다.

주문의 기본 단계에 대한 자세한 내용은 핵심 사용 안내서에서 [주문 워크플로](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/order-processing){target="_blank"} 항목을 참조하십시오.

무효 기능과 주문 트랜잭션을 무효화하는 방법에 대해 알아보려면 핵심 사용 안내서에서 [주문 처리](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/order-processing#process-an-order){target="_blank"}를 참조하십시오.
