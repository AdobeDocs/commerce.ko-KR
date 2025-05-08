---
title: 환불
description: 관리자의  [!DNL Payment Services] 주문에 대한 환불을 대변 메모 프로세스의 일부로 만듭니다.
exl-id: 2b3721a1-9c9d-4e3f-ab7d-5bd61573dcb4
feature: Payments, Checkout, Paas, Saas
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---

# 환불

[!DNL Payment Services]개 주문에 대한 환불이 대변 메모 프로세스의 일부로 관리자에 생성됩니다. 대변 메모는 고객이 전액 또는 일부 환불을 위해 지불해야 하는 금액을 표시하는 문서로, 구매 시 적용하거나 고객에게 직접 환불할 수 있습니다. [인보이스 발행](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/invoices#create-an-invoice){target="_blank"}된 주문에 대해서만 대변 메모를 발행할 수 있습니다.

자세한 내용 및 대변 메모를 발행하고 인쇄하는 방법에 대한 자세한 내용은 핵심 사용 안내서의 [대변 메모](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/credit-memos/credit-memos){target="_blank"}를 참조하십시오.

PayPal 또는 신용 카드로 처리된 주문의 경우 다음을 수행할 수 있습니다.

* 주문금액 전액을 환불해 주세요
* 주문의 일부 금액(또는 복수 부분 금액) 환불
* 특정 주문 항목의 금액보다 적은 금액을 환불합니다.

자세한 내용은 핵심 사용 안내서의 [대변 메모 발급](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/credit-memos/credit-memo-create){target="_blank"}을 참조하십시오.

>[!NOTE]
>
>나머지 주문 금액(최초 금액에서 기존 환불 합계를 뺀 금액)을 초과하는 주문에 대해 부분 환불을 시도하거나 전체 주문 금액보다 큰 금액에 대해 환불을 실행하는 경우 PayPal 또는 신용카드 처리 주문에 오류가 발생합니다.

[!UICONTROL Payment Settings] 구성의 [!UICONTROL Payment Action] 설정(`Authorize` 또는 `Authorize and Capture`)은 주문에 대한 [기본 환불 워크플로](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/credit-memos/credit-memos#refund-workflow){target="_blank"}를 결정합니다.

자세한 내용은 _대변 메모 발급_&#x200B;의 [결제 작업 설정 섹션](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/credit-memos/credit-memo-create#payment-action-setting){target="_blank"}을 참조하세요.
