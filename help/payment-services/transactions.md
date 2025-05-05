---
title: 거래 보고서
description: 거래 보고서를 사용하여 거래 승인 비율과 거래 추세를 볼 수 있습니다.
role: User
level: Intermediate
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '1272'
ht-degree: 0%

---

# 거래 보고서

[!DNL Adobe Commerce] 및 [!DNL Magento Open Source]에 대한 [!DNL Payment Services]은(는) 스토어의 거래, 주문 및 결제를 명확하게 볼 수 있도록 포괄적인 보고를 제공합니다.

![트랜잭션 보고서](assets/transactions-report.png){width="700" zoomable="yes"}

거래 보고서는 거래 승인 비율과 부정적인 거래 추세를 볼 수 있도록 하여 점포의 상태를 효과적으로 모니터링하고 거래 문제를 선제적으로 식별하고 해결할 수 있습니다.

상점 및 해당 결제 방법, 결과, 결제 응답 코드 등에 대한 개별 거래를 참조하십시오.

거래 보고서에 제공된 정보는 상인이 사용하기위한 것입니다. 이 정보를 고객 또는 기타 잠재적인 사기범과 공유하지 마십시오. 거래 정보를 사용하여 보안 검사를 우회하거나 과금을 초래하는 주문을 할 수 있습니다.

기존 회계 또는 Order Management 소프트웨어에서 사용할 트랜잭션 보고서를 .csv 파일 형식으로 다운로드할 수 있습니다.

>[!NOTE]
>
>[!DNL Payment Services]에 대해 [온보딩되고 활성화된 라이브 모드](production.md#enable-live-payments)가 없으면 재무 보고서를 볼 수 없습니다.

## 거래 보고서 보기

거래 보고서 보기는 결제 서비스의 거래 보기에서 사용할 수 있습니다. 여기에는 스토어의 거래에 대해 사용 가능한 모든 정보가 포함됩니다.

_관리자_ 사이드바에서 **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]** > _[!UICONTROL Transactions]_>**[!UICONTROL View Report]**(으)로 이동하여 자세한 테이블 형식 트랜잭션 보고서 보기를 확인합니다.

![트랜잭션 보고서 보기](assets/transactions-report-view.png){width="800" zoomable="yes"}

이 항목의 섹션에 따라 이 보기를 구성하여 보려는 데이터를 가장 잘 표시할 수 있습니다.

이 보고서에서 연결된 Commerce 주문 및 PayPal 거래 ID, 거래 금액, 거래당 결제 방법 등을 참조하십시오.

모든 결제 방법이 동일한 세부 정보를 제공하는 것은 아닙니다. 예를 들어 신용 카드 거래는 응답, AVS 및 CCV 코드를 제공하며 거래 보고서에서 카드의 마지막 네 자리를 제공합니다. PayPal 결제 버튼은 제공하지 않습니다.

기존 계정 또는 주문 관리 소프트웨어에서 사용할 수 있도록 .csv 파일 형식으로 [트랜잭션을 다운로드](#download-transactions)할 수 있습니다.

>[!WARNING]
>
> 트랜잭션 보고서에는 [!DNL Payment Services] 외부에서 수행된 캡처가 포함되지 않습니다.

### 데이터 소스 선택

트랜잭션 보고서 보기에서 보고서 결과를 보려는 데이터 원본 **[!UICONTROL Live]** 또는 **[!UICONTROL Sandbox]**&#x200B;을(를) 선택할 수 있습니다.

![데이터 원본 선택](assets/datasource.png){width="300" zoomable="yes"}

_[!UICONTROL Live]_&#x200B;이(가) 선택한 데이터 소스인 경우 프로덕션 모드에서 [!DNL Payment Services]을(를) 사용하는 스토어에 대한 보고서 정보를 볼 수 있습니다._[!UICONTROL Sandbox]_&#x200B;이(가) 선택한 데이터 소스인 경우 샌드박스 모드에 대한 보고서 정보를 볼 수 있습니다.

데이터 소스 선택은 다음과 같이 작동합니다.

* 프로덕션 모드에서 [!DNL Payment Services]을(를) 사용하는 저장소가 없는 경우 데이터 원본 선택 기본값은 _[!UICONTROL Sandbox]_&#x200B;입니다.
* 프로덕션 모드에서 [!DNL Payment Services]을(를) 사용하는 저장소(하나 또는 여러 개)가 있는 경우 데이터 원본 선택 기본값은 _[!UICONTROL Live]_&#x200B;입니다.
* 보고서 내보내기는 항상 데이터 소스 선택을 따릅니다.

[!UICONTROL Transactions] 보고서의 데이터 원본을 선택하려면 다음을 수행하십시오.

1. _관리자_ 사이드바에서 **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Transactions]_>**[!UICONTROL View Report]**(으)로 이동합니다.
1. **[!UICONTROL Data source]**&#x200B;을(를) 클릭하고 **[!UICONTROL Live]** 또는 **[!UICONTROL Sandbox]**&#x200B;을(를) 선택합니다.

   선택한 데이터 소스를 기반으로 보고서 결과가 재생성됩니다.

### 날짜 일정 사용자 지정

트랜잭션 보고서 보기에서 특정 날짜를 선택하여 보려는 트랜잭션의 시간대를 사용자 지정할 수 있습니다. 기본적으로 30일의 트랜잭션이 표에 표시됩니다.

1. _관리자_ 사이드바에서 **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Transactions]_>**[!UICONTROL View Report]**(으)로 이동합니다.
1. **[!UICONTROL Transaction dates]** 일정 선택기 필터를 클릭합니다.
1. 적용 가능한 날짜 범위를 선택합니다.
1. 그리드에서 지정된 날짜에 대한 트랜잭션을 봅니다.

### 보고서 정보 필터링

트랜잭션 보고서 보기에서 필터 기준을 선택하여 보려는 상태 결과를 필터링할 수 있습니다.

1. _관리자_ 사이드바에서 **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Transactions]_>**[!UICONTROL View Report]**(으)로 이동합니다.
1. **[!UICONTROL Filter]** 선택기를 클릭합니다.
1. 선택한 주문 트랜잭션에 대한 보고서 결과를 보려면 _[!UICONTROL Transaction Result]_&#x200B;옵션을 전환하십시오.
1. 거래에 사용된 결제 유형에 대한 보고서 결과를 보려면 _[!UICONTROL Payment Method]_&#x200B;옵션을 전환하십시오.
1. 사용 가능한 경우 사용된 결제 유형에 대한 추가 정보를 보려면 _[!UICONTROL Payment Detail]_&#x200B;옵션을 전환하십시오.
1. 해당 주문 금액 범위 내에서 보고서 결과를 보려면 _최소 주문 금액_ 또는 _최대 주문 금액_&#x200B;을 입력하십시오.
1. 특정 트랜잭션을 검색하려면 _[!UICONTROL Order ID]_&#x200B;을(를) 입력하십시오.
1. 특정 신용 카드 또는 직불 카드를 검색하려면 _[!UICONTROL Card Last Four]_&#x200B;을(를) 도입하십시오.
1. 특정 고객의 모든 트랜잭션을 표시하려면 _[!UICONTROL Customer ID]_&#x200B;을(를) 입력하십시오.
1. 해당 전자 메일에 대한 트랜잭션을 필터링하려면 _[!UICONTROL Customer Email]_&#x200B;을(를) 입력하십시오.
1. 필터를 숨기려면 **[!UICONTROL Hide filters]**&#x200B;을(를) 클릭합니다.

### 열 표시 및 숨기기

트랜잭션 보고서에는 기본적으로 사용 가능한 모든 정보 열이 표시됩니다. 그러나 보고서에 표시되는 열을 사용자 지정할 수 있습니다.

1. _관리자_ 사이드바에서 **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Transactions]_>**[!UICONTROL View Report]**(으)로 이동합니다.
1. **[!UICONTROL Column settings]** 아이콘 ![열 설정 아이콘](assets/column-settings.png){width="20" zoomable="yes"}을 클릭합니다.
1. 보고서에 표시되는 열을 사용자 지정하려면 목록에서 열을 선택하거나 선택 취소합니다.

   트랜잭션 보고서는 열 설정 메뉴에서 변경한 내용을 즉시 표시합니다. 열 기본 설정은 저장되며 보고서 보기에서 멀리 이동하는 경우에도 계속 적용됩니다.

### 보고서 데이터 업데이트

트랜잭션 보고서 보기에는 보고서 정보가 마지막으로 업데이트된 시간을 보여 주는 _[!UICONTROL Last updated]_&#x200B;타임스탬프가 표시됩니다. 기본적으로 거래 보고서 데이터는 3시간마다 자동으로 새로 고쳐집니다.

보고서 데이터를 수동으로 새로 고쳐 최신 보고서 정보를 볼 수도 있습니다.

1. _관리자_ 사이드바에서 **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Transactions]_>**[!UICONTROL View Report]**(으)로 이동합니다.
1. _새로 고침_ 아이콘(![새로 고침 아이콘](assets/refresh-button-med.png){width="20" zoomable="yes"})을 클릭합니다.

   트랜잭션 보고서 데이터가 새로 고침되고 *[!UICONTROL Update complete]* 확인이 표시되며 최신 정보가 표에 표시됩니다.

### 트랜잭션 다운로드

기본 30일 트랜잭션 또는 사용자 정의된 일정 중 어느 것을 보든 트랜잭션 보기 그리드에 모든 트랜잭션이 표시되는 .csv 파일을 다운로드할 수 있습니다.

1. _관리자_ 사이드바에서 **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > **[!UICONTROL Transactions]**(으)로 이동합니다.
1. 지난 30일 이외의 기간에 대한 트랜잭션을 보려면 [상태에 대한 날짜 범위 기간을 사용자 지정](#customize-dates-timeframe)하세요.
1. _다운로드_ ![다운로드 아이콘](assets/icon-download.png){width="20" zoomable="yes"} 아이콘을 클릭합니다.

트랜잭션이 .csv 형식으로 다운로드됩니다.

### 열 설명

트랜잭션 보고서에는 다음 정보가 포함됩니다.

| 열 | 설명 |
| ------------ | -------------------- |
| [!UICONTROL Order ID] | Commerce 주문 ID(성공적인 트랜잭션에 대한 값만 포함하며 거부된 트랜잭션에 대해서는 비어 있음)<br> <br>관련 [주문 정보](https://experienceleague.adobe.com/ko/docs/commerce-admin/stores-sales/order-management/orders/orders){target="_blank"}를 보려면 ID를 클릭하세요. |
| [!UICONTROL PayPal Transaction ID] | 결제 제공자가 제공한 거래 ID. 성공적인 거래에 대한 값만 포함되고 거부된 거래에 대한 대시가 포함됩니다. 이 ID를 클릭하여 PayPal 거래 세부 사항 페이지에 액세스할 수 있습니다. |
| [!UICONTROL Customer ID] | 주문의 Commerce 고객 ID<br> <br>자세한 내용은 [고객 정보](https://experienceleague.adobe.com/ko/docs/commerce-admin/customers/customer-accounts/account-create){target="_blank"} 항목을 참조하십시오. |
| [!UICONTROL Transaction Date] | 트랜잭션 날짜 타임스탬프 |
| [!UICONTROL Payment Method] | 브랜드 및 카드 유형에 대한 정보로 거래에 사용되는 결제 유형. 자세한 내용은 [카드 유형](https://developer.paypal.com/docs/api/orders/v2/#definition-card_type)을 참조하십시오. 결제 서비스 버전 1.6.0 이상에서 사용할 수 있습니다 |
| [!UICONTROL Payment Detail] | 거래에 사용된 결제 유형에 대한 추가 정보를 제공합니다(사용 가능한 경우). |
| [!UICONTROL Card Last Four] | 거래에 사용된 신용 카드 또는 직불 카드의 마지막 4자리 |
| [!UICONTROL Result] | 거래 결과—*[!UICONTROL OK]*(거래 성공), *[!UICONTROL Rejected by Payment Provider]*(PayPal에서 거부), *[!UICONTROL Rejected by Bank]*(카드를 발급한 은행에서 거부) |
| [!UICONTROL Response Code] | 결제 공급자 또는 은행에서 거부 이유를 제공하는 오류 코드. [`Rejected by Bank` 상태](https://developer.paypal.com/docs/api/orders/v2/#definition-processor_response) 및 [`Rejected by Payment Provider` 상태](https://developer.paypal.com/api/rest/reference/orders/v2/errors/)에 대해 가능한 응답 코드 목록 및 설명을 참조하십시오. |
| [!UICONTROL AVS Code] | 주소 확인 서비스 코드, 결제 요청에 대한 프로세서 응답 정보. 자세한 내용은 [가능한 코드 및 설명 목록](https://developer.paypal.com/docs/api/orders/v2/#definition-processor_response)을 참조하세요. |
| [!UICONTROL CVV Code] | 신용 카드 및 직불 카드의 카드 인증 값 코드입니다. 자세한 내용은 [가능한 코드 및 설명 목록](https://developer.paypal.com/docs/api/orders/v2/#definition-processor_response)을 참조하세요. |
| [!UICONTROL Amount] | 거래 주문 금액 |
| [!UICONTROL Currency] | 거래에서 주문에 사용된 통화 |
| [!UICONTROL Type] | [거래에 대한 결제 작업](../payment-services/production.md#set-payment-services-as-payment-method)—`Authorize` 또는 `Authorize and Capture` |

### 오류 응답 코드

_응답 코드_ 열에 트랜잭션과 관련된 특정 오류 또는 성공 코드가 표시됩니다. 표시되는 몇 가지 일반적인 오류 코드는 다음과 같습니다.

* `PAYMENT_DENIED`—사기성으로 의심되어 PayPal에서 거래를 거절했습니다.
* `INTERNAL_SERVER_ERROR`—PayPal에서 트랜잭션을 거부했으며 PayPal 서버 오류가 발생했습니다. 트랜잭션을 다시 시도할 수 있습니다.
* `INSTRUMENT_DECLINED`—선택한 결제 방법별로 PayPal에 의해 고객이 거절되었습니다. 다른 결제 방법으로 거래를 재시도할 수 있습니다.
* `9500`—사기성으로 의심되어 연결된 은행에서 거래를 거절했습니다.
* `5120` - 결제 자금이 부족하여 연결된 은행에서 거래를 거절했습니다.
* `5650`—뱅크에 강력한 고객 인증([3DS](security.md#3ds))이 필요하기 때문에 연결된 뱅크가 거래를 거절했습니다.

실패한 트랜잭션에 대한 자세한 오류 응답 코드는 2023년 6월 1일 이상의 트랜잭션에 사용할 수 있습니다. 2023년 6월 1일 이전에 발생한 거래에 대해 부분 보고서 데이터가 표시됩니다.
