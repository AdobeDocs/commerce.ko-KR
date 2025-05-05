---
title: 주문 결제 상태 보고서
description: 주문 결제 상태 보고서를 사용하여 주문 결제 상태를 확인하고 잠재적 문제를 식별합니다.
role: User
level: Intermediate
feature: Payments, Checkout, Orders
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '2045'
ht-degree: 0%

---

# 주문 결제 상태 보고서

[!DNL Adobe Commerce] 및 [!DNL Magento Open Source]에 대한 [!DNL Payment Services]은(는) 스토어의 [거래](transactions.md), 주문 및 결제를 명확하게 볼 수 있도록 포괄적인 보고를 제공합니다.

두 가지 주문 결제 상태 보고 보기를 사용하여 주문의 결제 상태를 신속하게 볼 수 있습니다.

* **[주문 결제 상태 시각화 보기](#order-payment-status-data-visualization-view)**—주문 결제 상태 보고서 보기에서 일별 집계된 결제 상태를 시각적으로 표시한 차트를 결제 서비스 홈에서 사용할 수 있습니다.
* **[주문 결제 상태 보고서 보기](#order-payment-status-report-view)**—주문 결제 상태에서 모든 거래에 대한 자세한 결제, 인보이스 발행, 배송, 환불 및 분쟁 상태를 보여 주는 보고서를 사용할 수 있습니다.

주문 결제 상태 보기를 통해 주문-현금화 프로세스 흐름 내에서 특정 주문이 어디에 있는지 쉽게 파악할 수 있습니다. 이러한 보고서를 사용하면 결제 상태 및 결제 날짜에 따라 신속하게 주문을 조회하고 잠재적인 문제를 파악할 수 있습니다.

기존 계정 또는 주문 관리 소프트웨어에서 사용할 수 있도록 .csv 파일 형식으로 [주문 결제 상태를 다운로드](#download-order-payment-statuses)할 수 있습니다.

>[!NOTE]
>
>[!DNL Payment Services]에 대해 [온보딩되고 활성화된 라이브 모드](production.md#enable-live-payments)가 없으면 재무 보고서를 볼 수 없습니다.

## 주문 결제 상태 데이터 시각화 보기

주문 결제 상태 데이터 시각화 보기는 결제 서비스 홈에서 사용할 수 있습니다. 자세한 표 형식 [주문 결제 상태 보고서 보기](#order-payment-status-report-view)에서 일별 집계된 결제 상태를 시각적으로 표시합니다.

_관리자_ 사이드바에서 **판매** > **결제 서비스** > _주문_(으)로 이동하여 데이터 시각화 [결제 상태 차트](#statuses-information)를 확인하세요.

![관리자의 페이아웃 데이터 시각화](assets/orderpayment-dataviz.png){width="800" zoomable="yes"}

자세한 표 형식 [주문 결제 상태 보고서 보기](#order-payment-status-report-view)(으)로 이동하려면 **[!UICONTROL View Report]**&#x200B;을(를) 클릭하십시오.

### 일정 기간 상태 사용자 지정

기본적으로 30일 결제 상태가 표시됩니다.

주문 지급 상태 시각화 보기에서 날짜 범위를 선택하여 보려는 지급 상태에 대한 시간대를 사용자 정의할 수 있습니다.

1. _관리자_ 사이드바에서 **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**(으)로 이동합니다. 주문 결제 상태 데이터 시각화 보기가 _주문_ 섹션에 표시됩니다.
1. **[!UICONTROL Range]** 선택기 필터를 클릭합니다.
1. 적용 가능한 날짜 범위(30일, 15일 또는 7일)를 선택합니다.
1. 지정한 날짜의 상태 정보를 봅니다.

### 상태 정보

선택한 날짜 범위에 대한 결제 상태는 주문 결제 상태 데이터 시각화 보기의 왼쪽에 표시됩니다. 선택한 날짜 범위의 날짜가 보기 하단에 표시됩니다. 특정 날짜에 주문이 없는 경우 해당 날짜가 표시되지 않습니다.

주문 결제 상태 데이터 시각화 보기에는 다음 정보가 포함됩니다.

| 데이터 | 설명 |
| ------------ | -------------------- |
| [!UICONTROL Orders] | 지정된 시간대의 주문 금액 범위, Y축의 데이터(왼쪽) |
| 날짜 범위 | 지정된 일정의 날짜 범위, X축의 데이터(하단) |
| 인증됨 | 승인된 주문 |
| 캡처 요청됨 | 주문에 대해 요청된 캡처 |
| 캡처 확인됨 | 주문 캡처 완료됨 |
| 부분 캡처 | 주문이 부분적으로 캡처됨 |
| 캡처 실패 | 주문 캡처 실패 |
| 무효화됨 | 무효화된 주문 |

## 주문 결제 상태 보고서 보기

주문 결제 상태 보고서 보기는 결제 서비스의 홈 보기에서 사용할 수 있습니다. 여기에는 모든 거래에 대한 결제, 송장 발행, 배송, 환불, 분쟁 등의 세부 상태가 포함됩니다.

_관리자_ 사이드바에서 **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]** > _[!UICONTROL Orders]_>**[!UICONTROL View Report]**(으)로 이동하여 자세한 테이블 형식 주문 결제 상태 보고서 보기를 확인하십시오.

![관리자의 결제 상태 트랜잭션 주문](assets/orders-report-data.png){width="800" zoomable="yes"}

이 항목의 섹션에 따라 이 보기를 구성하여 보려는 데이터를 가장 잘 표시할 수 있습니다.

기존 회계 또는 주문 관리 소프트웨어에서 사용할 수 있도록 .csv 파일 형식으로 [지급 트랜잭션을 다운로드](#download-order-payment-statuses)할 수 있습니다.

>[!NOTE]
>
>이 표에 표시된 데이터는 기본적으로 `TRANS DATE`을(를) 사용하여 내림차순(`DESC`)으로 정렬됩니다. `TRANS DATE`은(는) 트랜잭션이 시작된 날짜와 시간입니다.

### 결제 상태 업데이트

특정 결제 방법에는 결제 내용을 캡처하는 데 일정 시간이 필요합니다. 이제 [!DNL Payment Services]에서 다음 순서대로 결제 트랜잭션의 보류 중인 상태를 검색합니다.

* `pending capture`개 트랜잭션을 동기적으로 감지 중
* `pending capture`개 트랜잭션을 비동기적으로 모니터링

>[!NOTE]
>
>주문에서 결제 거래의 대기 상태를 감지하면 아직 결제를 받지 않은 경우 실수로 주문을 배송하지 않습니다. 이는 전자 수표 및 PayPal 거래에 대해 발생할 수 있습니다.

#### 보류 중인 캡처 트랜잭션의 동기 감지

`Pending` 상태의 캡처 트랜잭션을 자동으로 감지하고 이러한 트랜잭션이 검색될 때 주문이 `Processing` 상태로 들어가지 않도록 합니다.

고객 체크아웃 중에 또는 관리자가 이전에 승인된 지급에 대한 송장을 만들 때 [!DNL Payment Services]은(는) `Pending` 상태의 캡처 트랜잭션을 자동으로 감지하고 해당 주문을 `Payment Review` 상태로 전환합니다.

#### 보류 중인 캡처 트랜잭션의 비동기 모니터링

보류 중인 캡처 트랜잭션이 `Completed` 상태로 전환되는 시점을 감지하여 판매자가 영향을 받는 주문 처리를 다시 시작할 수 있도록 하십시오.

이 프로세스가 예상대로 작동하는지 확인하려면 판매자는 새 cron 작업을 구성해야 합니다. 작업이 자동으로 실행되도록 구성되면 판매자의 다른 개입이 필요하지 않습니다.

[cron 작업 구성](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs.html?lang=ko)을 참조하십시오. 구성하고 나면 새 작업이 30분마다 실행되어 `Payment Review` 상태의 주문에 대한 업데이트를 가져옵니다.

가맹점은 주문 결제 상태 보고서 보기를 통해 업데이트된 결제 상태를 확인할 수 있습니다.

### 보고서에 사용된 데이터

[!DNL Payment Services]은(는) 주문 데이터를 사용하여 다른 원본(PayPal 포함)의 결제 데이터와 결합하여 의미 있고 유용한 보고서를 제공합니다.

주문 데이터를 내보내고 결제 서비스에서 유지합니다. [주문 상태를 변경 또는 추가](https://experienceleague.adobe.com/ko/docs/commerce-admin/stores-sales/order-management/orders/order-status#custom-order-status)하거나 [스토어 보기를 편집](https://experienceleague.adobe.com/ko/docs/commerce-admin/stores-sales/site-store/store-views#edit-a-store-view), [스토어](https://experienceleague.adobe.com/ko/docs/commerce-admin/start/setup/store-details#store-information) 또는 웹 사이트 이름을 편집하면 해당 데이터가 결제 데이터와 결합되고 주문 결제 상태 보고서는 결합된 정보로 채워집니다.

이 프로세스에는 두 가지 단계가 있습니다.

1. 관리자의 [인덱스 관리](https://experienceleague.adobe.com/ko/docs/commerce-admin/systems/tools/index-management)에 구성된 방법에 따라 인덱스가 `ON SAVE`(주문 정보 또는 저장소 정보가 변경될 때마다) 또는 `BY SCHEDULE`(사전 구성된 cron 일정에 따라)의 데이터를 변경합니다.

   기본적으로 데이터 인덱싱이 `ON SAVE`에 발생합니다. 즉, 순서, 주문 상태, 스토어 보기, 스토어 또는 웹 사이트의 변경 사항이 있을 때마다 다시 인덱싱 프로세스가 즉시 발생합니다.

1. 인덱스화된 데이터가 결제 서비스로 전송되면 주문 결제 상태 보고서에 채워집니다.

보고 목적으로 내보내고 정렬하는 데이터는 주문 결제 상태 보고서에서 사용하는 데이터뿐입니다.

>[!NOTE]
>
>이 표에 표시된 데이터는 기본적으로 `ORDER DATE`을(를) 사용하여 내림차순(`DESC`)으로 정렬됩니다. `ORDER DATE`은(는) 주문이 만들어진 날짜 타임스탬프입니다.

#### 데이터 내보내기 구성

기본적으로 리인덱싱은 `ON SAVE` 모드에서 수행되지만 `BY SCHEDULE` 모드에서 인덱싱하는 것이 좋습니다. `BY SCHEDULE` 인덱스는 1분의 cron 일정에 따라 실행되며 변경된 데이터는 데이터 변경 후 2분 이내에 주문 상태 보고서에 표시됩니다. 이러한 예약된 리인덱싱은 특히 들어오는 주문량이 많은 경우 각 주문이 아닌 일정에 따라 발생하므로 스토어에 대한 부담을 줄이는 데 도움이 됩니다.

관리자[&#128279;](https://experienceleague.adobe.com/ko/docs/commerce-admin/systems/tools/index-management#change-the-index-mode)에서 인덱스 모드—`ON SAVE` 또는 `BY SCHEDULE`—을(를) 변경할 수 있습니다.

데이터 내보내기를 구성하는 방법은 [명령줄 구성](configure-cli.md#configure-data-export)을 참조하세요.

### 데이터 소스 선택

주문 결제 상태 보고서 보기에서 보고서 결과를 보려는 데이터 원본(**[!UICONTROL Live]** _ 또는 **[!UICONTROL Sandbox]**)을 선택할 수 있습니다.

![데이터 원본 선택](assets/datasource.png){width="300" zoomable="yes"}

_[!UICONTROL Live]_&#x200B;이(가) 선택한 데이터 소스인 경우 프로덕션 모드에서 [!DNL Payment Services]을(를) 사용하는 스토어에 대한 보고서 정보를 볼 수 있습니다._[!UICONTROL Sandbox]_&#x200B;이(가) 선택한 데이터 소스인 경우 샌드박스 모드에 대한 보고서 정보를 볼 수 있습니다.

데이터 소스 선택은 다음과 같이 작동합니다.

* 라이브 모드에서 [!DNL Payment Services]을(를) 사용하는 저장소가 없는 경우 데이터 원본 선택 기본값은 _[!UICONTROL Sandbox]_&#x200B;입니다.
* 라이브 모드에서 [!DNL Payment Services]을(를) 사용하는 저장소(하나 또는 여러 개)가 있는 경우 데이터 원본 선택 기본값은 _[!UICONTROL Live]_&#x200B;입니다.
* 보고서 내보내기는 항상 데이터 소스 선택을 따릅니다.

[!UICONTROL Order Payment Status] 보고서의 데이터 원본을 선택하려면 다음을 수행하십시오.

1. _관리자_ 사이드바에서 **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > **[!UICONTROL Orders]** > **[!UICONTROL View Report]**(으)로 이동합니다.
1. _[!UICONTROL Data source]_&#x200B;선택기 필터를 클릭하고&#x200B;**[!UICONTROL Live]**&#x200B;또는&#x200B;**[!UICONTROL Sandbox]**&#x200B;을(를) 선택합니다.

   선택한 데이터 소스를 기반으로 보고서 결과가 재생성됩니다.

### 주문 날짜 일정 사용자 지정

주문 결제 상태 보고서 보기에서 특정 날짜를 선택하여 보려는 상태 결과의 시간대를 사용자 정의할 수 있습니다. 기본적으로 30일의 주문 결제 상태가 그리드에 표시됩니다.

1. _관리자_ 사이드바에서 **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Orders]_>**[!UICONTROL View Report]**(으)로 이동합니다.
1. _[!UICONTROL Order dates]_&#x200B;일정 선택기 필터를 클릭합니다.
1. 적용 가능한 날짜 범위를 선택합니다.
1. 그리드에서 지정한 일자에 대한 주문 지급 상태를 조회합니다.

### 보고서 정보 필터링

주문 지급 상태 보고서 보기에서 필터 기준을 선택하여 조회할 상태 결과를 필터링할 수 있습니다.

1. _관리자_ 사이드바에서 **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Orders]_>**[!UICONTROL View Report]**(으)로 이동합니다.
1. **[!UICONTROL Filter]** 선택기를 클릭합니다.
1. _결제 상태_ 옵션을 전환하여 선택한 주문 결제 상태에 대한 보고서 결과만 표시합니다.
1. _[!UICONTROL Min Order Amount]_&#x200B;또는 _[!UICONTROL Max Order Amount_]을(를) 입력하여 주문 금액 범위 내에서 보고서 결과를 봅니다.
1. 필터를 숨기려면 **[!UICONTROL Hide filters]**&#x200B;을(를) 클릭합니다.

### 열 표시 및 숨기기

주문 결제 상태 보고서에는 기본적으로 사용 가능한 모든 정보 열이 표시됩니다. 그러나 보고서에 표시되는 열을 사용자 지정할 수 있습니다.

1. _관리자_ 사이드바에서 **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Orders]_>**[!UICONTROL View Report]**(으)로 이동합니다.
1. _열 설정_ 아이콘(![열 설정 아이콘](assets/column-settings.png){width="20" zoomable="yes"})을 클릭합니다.
1. 보고서에 표시되는 열을 사용자 지정하려면 목록에서 열을 선택하거나 선택 취소합니다.

   주문 결제 상태 보고서에는 열 설정 메뉴에서 변경한 사항이 즉시 표시됩니다. 열 기본 설정은 저장되며 보고서 보기에서 멀리 이동하는 경우에도 계속 적용됩니다.

### 상태 보기

주문 지급 상태 보고서 보기에는 각 주문에 대한 포괄적인 지급 상태 정보가 표시됩니다.

기본적으로 30일의 주문 결제 상태가 그리드에 표시됩니다.

주문 날짜, 승인 날짜, 인보이스 발행, 배송, 결제 상태 등 [주문 결제 상태 정보](#column-descriptions)를 보려면 왼쪽과 오른쪽으로 스크롤하십시오.

검색에서 반환되거나 기본 30일 주문 결제 상태에 표시되는 행 수는 주문 날짜 달력 선택기 필터와 함께 주문 결제 상태 보기 그리드 위에 표시됩니다.

#### 지급 상태

지급 상태 열에는 지급의 현재 상태가 표시됩니다. `Capture failed` 결제에는 빨간색 경고 상태가 표시되고 `Voided` 결제에는 회색 경고 상태가 표시됩니다.

#### 환불 상태

환불 상태 열에는 환급의 현재 상태가 표시됩니다. `Capture failed` 결제에는 빨간색 경고 상태가 표시되고 `Voided` 결제에는 회색 경고 상태가 표시됩니다.

### 보고서 데이터 업데이트

주문 결제 상태 보고서 보기에는 보고서 정보가 마지막으로 업데이트된 시간을 보여 주는 _[!UICONTROL Last updated]_&#x200B;타임스탬프가 표시됩니다. 기본적으로 주문 결제 상태 보고서 데이터는 3시간마다 자동으로 새로 고쳐집니다.

주문 지급 상태 보고서 데이터를 수동으로 새로 고쳐 최신 보고서 정보를 볼 수도 있습니다.

1. _관리자_ 사이드바에서 **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Orders]_>**[!UICONTROL View Report]**(으)로 이동합니다.
1. _새로 고침_ 아이콘(![새로 고침 아이콘](assets/refresh-button-med.png){width="20" zoomable="yes"})을 클릭합니다.

   주문 결제 상태 보고서 데이터가 새로 고쳐지고 *[!UICONTROL Update complete]* 확인이 표시되며 최신 정보가 표에 표시됩니다.

### 분쟁 보기

주문 결제 상태 보고서에서 스토어의 주문에 대한 모든 분쟁을 조회하고 PayPal 해결 센터로 이동하여 이에 대한 조치를 취할 수 있습니다.

1. _관리자_ 사이드바에서 **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Orders]_>**[!UICONTROL View Report]**(으)로 이동합니다.
1. **[!UICONTROL Disputes column]**(으)로 이동합니다.
1. 특정 주문에 대한 모든 분쟁을 확인하고 [분쟁 상태](#order-payment-status-information)를 확인하세요.
1. _PP-D-_(으)로 시작하는 분쟁 ID 링크를 클릭하여 [PayPal 해결 센터](https://www.paypal.com/us/cshelp/article/what-is-the-resolution-center-help246)에서 분쟁 세부 정보를 검토하십시오.
1. 필요에 따라 분쟁에 대해 적절한 조치를 취하십시오.

   상태별로 순서 분쟁을 정렬하려면 [!UICONTROL Disputes] 열 머리글을 클릭합니다.

### 주문 결제 상태 다운로드

기본 30일 상태 또는 사용자 정의된 기간을 보는지 여부에 관계없이 주문 결제 상태 보기 그리드에 모든 상태가 표시되는 .csv 파일을 다운로드할 수 있습니다.

1. _관리자_ 사이드바에서 **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Orders]_>**[!UICONTROL View Report]**(으)로 이동합니다.
1. 지난 30일 이외의 다른 기간에 대한 상태를 보려면 [해당 상태에 대한 날짜 범위 기간을 사용자 지정](#customize-dates-timeframe)하세요.
1. _다운로드_(![다운로드 아이콘](assets/icon-download.png){width="20" zoomable="yes"}) 아이콘을 클릭합니다.

주문 결제 상태는 .csv 형식으로 다운로드됩니다.

### 열 설명

주문 결제 상태 보고서에는 다음 정보가 포함됩니다.

| 열 | 설명 |
| ------------ | -------------------- |
| [!UICONTROL Order ID] | Commerce 주문 ID<br> <br>관련 [주문 정보](https://experienceleague.adobe.com/ko/docs/commerce-admin/stores-sales/order-management/orders/orders){target="_blank"}를 보려면 ID를 클릭하세요. |
| [!UICONTROL Order Date] | 주문 날짜 타임스탬프 |
| [!UICONTROL Authorized Date] | 결제 권한 부여의 날짜 타임스탬프 |
| [!UICONTROL Order Status] | 현재 Commerce [주문 상태](https://experienceleague.adobe.com/ko/docs/commerce-admin/stores-sales/order-management/orders/order-status){target="_blank"} |
| [!UICONTROL Invoiced] | 주문 *[!UICONTROL No]*, *[!UICONTROL Partial]* 또는 *[!UICONTROL Yes]*&#x200B;의 송장 상태 |
| [!UICONTROL Shipped] | 주문 배송 상태—*[!UICONTROL No]*, *[!UICONTROL Partial]* 또는 *[!UICONTROL Yes]* |
| [!UICONTROL Order Amt] | 총 주문 금액 |
| [!UICONTROL Cur] | 주문 통화 유형 |
| [!UICONTROL Pay Status] | 특정 주문에 대한 결제 상태 |
| [!UICONTROL Paid Amt] | 주문에서 지불된 금액 |
| [!UICONTROL Cur] | 주문에 대해 지불된 금액의 통화 유형 |
| [!UICONTROL Refund Status] | 주문 환불 상태(예: 반품, RMA 및 대변 메모의 정보)   *[!UICONTROL Requires refund]*, *[!UICONTROL Refund requested]*, *[!UICONTROL Refunded]*, *[!UICONTROL Refund failed]* 또는 *[!UICONTROL Voided]* |
| [!UICONTROL Refund Amount] | 주문에 대한 총 환불 금액 |
| [!UICONTROL Cur] | 주문에 대해 환급한 금액의 통화 유형 |
| [!UICONTROL Disputes] | 주문에 대한 모든 분쟁 상태(분쟁 및 요금 반환의 정보)—*[!UICONTROL Open]*, *[!UICONTROL Waiting for buyer response]*, *[!UICONTROL Waiting for seller response]*, *[!UICONTROL Under review]*, *[!UICONTROL Resolved]* 또는 *[!UICONTROL Other]* |
| [!UICONTROL Payment Method] | 주문에 대한 Commerce 거래에 사용되는 결제 방법 |
| [!UICONTROL Website] | 주문이 접수된 웹 사이트 |
| [!UICONTROL Store] | 주문된 스토어 |
| [!UICONTROL Store View] | 주문이 이루어진 스토어 뷰 |
