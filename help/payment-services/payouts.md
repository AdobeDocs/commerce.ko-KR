---
title: 지급 보고서
description: 지급 보고서를 사용하여 재무 조정을 위해 결제 금액, 처리 수량 및 거래 레벨에 대한 상세 보고를 완전히 투명화합니다.
role: User
level: Intermediate
exl-id: f3f99474-cd28-4c8f-b0ea-dca8e014b108
feature: Payments, Checkout, Paas, Saas
source-git-commit: a0f9ddbf3d0f291855cb51fd70a782c48b8efc6c
workflow-type: tm+mt
source-wordcount: '1303'
ht-degree: 0%

---

# 지급 보고서

[!DNL Payment Services] 및 [!DNL Adobe Commerce]에 대한 [!DNL Magento Open Source]은(는) 스토어의 거래, 주문 및 결제를 명확하게 볼 수 있도록 포괄적인 보고를 제공합니다.

사용 가능한 두 가지 지급 보고 보기를 통해 모든 지급 횟수에 대한 자세한 정보를 볼 수 있습니다.

* **[지급 데이터 시각화 보기](#payouts-data-visualization-view)** - 지급 서비스 홈에서 사용할 수 있는 차트로, 지급 보고서 보기에서 일별 집계된 금액을 시각적으로 표시한 것입니다.
* **[지급 보고서 보기](#payouts-report-view)** - 모든 트랜잭션에 대한 자세한 지급 정보를 보여 주는 지급에서 사용할 수 있는 보고서

지급 조회는 종합적인 지급 정보를 한눈에 표시하므로, 지급 금액, 처리 수량 및 재무 조정을 위한 거래 수준에 대한 상세한 보고를 완전히 투명하게 확인할 수 있습니다.

기존 회계 또는 주문 관리 소프트웨어에서 사용할 수 있도록 .csv 파일 형식으로 [지급 트랜잭션을 다운로드](#download-transactions)할 수 있습니다.

>[!NOTE]
>
>지급 보고서는 캡처된 주문(결제 작업이 [`Authorize and Capture`](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/get-started/production.html#set-payment-services-as-payment-method)&#x200B;(으)로 설정됨) 또는 [이(가) `Invoiced`](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/invoices#create-an-invoice)&#x200B;(으)로 표시된 주문만 표시합니다.

## 지급액 데이터 시각화 보기

지급 데이터 시각화 보기는 결제 서비스 홈에서 사용할 수 있습니다. 자세한 테이블 형식 [일시 중단 보고서 보기](#payouts-report-view)에서 일별 집계된 금액을 시각적으로 표시한 것입니다.

_관리자_ 사이드바에서 **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**(으)로 이동하여 크레딧 대 차변 데이터 시각화 차트와 시간 경과에 따른 이동 평균을 확인하십시오.

![관리자의 페이아웃 데이터 시각화](assets/payouts-report.png){width="800" zoomable="yes"}

자세한 표 형식 **[!UICONTROL View Report]**&#x200B;지급 보고서 보기[(으)로 이동하려면 &#x200B;](#payouts-report-view)을(를) 클릭하십시오.

### 트랜잭션 일정 사용자 지정

기본적으로 30일의 트랜잭션이 표시됩니다.

지급액 데이터 시각화 보기에서 날짜 범위를 선택하여 보려는 지급액 트랜잭션에 대한 기간을 사용자 정의할 수 있습니다.

1. _관리자_ 사이드바에서 **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**(으)로 이동합니다. 지급액 데이터 시각화 보기가 지급액 섹션에 표시됩니다.
1. **[!UICONTROL Range]** 선택기 필터를 클릭합니다.
1. 적용 가능한 날짜 범위(30일, 15일 또는 7일)를 선택합니다.
1. 지정한 날짜에 대한 거래 정보를 봅니다.

### 거래 정보

선택한 날짜 범위에 대한 거래 금액은 지급액 데이터 시각화 보기의 왼쪽에 표시됩니다. 선택한 날짜 범위의 날짜가 보기 하단에 표시됩니다. 특정 날짜에 지급이 없는 경우 해당 날짜가 표시되지 않습니다.

일시 중단 데이터 시각화 보기에는 다음 정보가 포함됩니다.

| 데이터 | 설명 |
| ------------ | -------------------- |
| [!UICONTROL Transaction amount] | 지정된 시간대의 거래에 대한 금액 범위, Y축의 데이터(왼쪽) |
| 날짜 범위 | 지정된 일정의 날짜 범위, X축의 데이터(하단) |
| 크레딧 | 지정된 일정의 결제 |
| 차변 | 지정된 시간대에 대한 차변(환불) |
| 이동 평균 | 지정된 시간대의 각 날짜에 대한 평균 지급액 표시 |
| 범위에 대한 네트 | 지정된 기간(범위)에 대한 순 지급액 |

## 지급 보고서 보기

지급 보고서 보기는 지급 서비스의 지급 보기에서 사용할 수 있습니다. 여기에는 스토어의 지불에 대해 사용 가능한 모든 정보가 포함됩니다.

_관리자_ 사이드바에서 **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]** > _[!UICONTROL Payouts]_>**[!UICONTROL View Report]**(으)로 이동하여 자세한 테이블 형식 지불/수혜금 보고서 보기를 확인하십시오.

![관리자의 페이아웃 트랜잭션](assets/payouts-report-new.png){width="800" zoomable="yes"}

이 항목의 섹션에 따라 이 보기를 구성하여 보려는 데이터를 가장 잘 표시할 수 있습니다.

이 보고서에서 연결된 Commerce 주문 및 거래 ID, 거래 금액, 거래당 결제 방법 등을 모두 참조하십시오.

기존 회계 또는 주문 관리 소프트웨어에서 사용할 수 있도록 .csv 파일 형식으로 [지급 트랜잭션을 다운로드](#download-transactions)할 수 있습니다.

>[!NOTE]
>
>이 표에 표시된 데이터는 기본적으로 `DESC`을(를) 사용하여 내림차순(`TRANS DATE`)으로 정렬됩니다. `TRANS DATE`은(는) 트랜잭션이 시작된 날짜와 시간입니다.

### 데이터 소스 선택

일시 중단 보고서 보기에서 보고서 결과를 보려는 데이터 원본(**[!UICONTROL Live]** 또는 **[!UICONTROL Sandbox]**)을 선택할 수 있습니다.

![데이터 원본 선택](assets/datasource.png){width="300" zoomable="yes"}

_[!UICONTROL Live]_&#x200B;이(가) 선택한 데이터 소스인 경우 프로덕션 모드에서 저장소에 대한 보고서 정보를 볼 수 있습니다._[!UICONTROL Sandbox]_&#x200B;이(가) 선택한 데이터 소스인 경우 샌드박스 모드에서 보고서 정보 저장소를 볼 수 있습니다.

데이터 소스 선택은 다음과 같이 작동합니다.

* 라이브 모드에 있는 저장소가 없는 경우 데이터 원본 선택 기본값은 _[!UICONTROL Sandbox]_&#x200B;입니다.
* 라이브 모드에 하나 이상의 저장소가 있는 경우 데이터 원본 선택 기본값은 _[!UICONTROL Live]_&#x200B;입니다.
* 보고서 내보내기는 항상 데이터 소스 선택을 따릅니다.

주문 지급 상태 보고서에 대한 데이터 출처를 선택하려면

1. _관리자_ 사이드바에서 **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]** > _[!UICONTROL Payouts]_>**[!UICONTROL View Report]**(으)로 이동합니다.
1. **[!UICONTROL Data source]**&#x200B;을(를) 클릭하고 **[!UICONTROL Live]** 또는 **[!UICONTROL Sandbox]**&#x200B;을(를) 선택합니다.

   선택한 데이터 소스를 기반으로 보고서 결과가 재생성됩니다.

### 트랜잭션 보기

기본적으로 30일의 트랜잭션이 표시됩니다.

검색에서 반환되거나 기본 30일 거래에서 표시되는 행 수는 거래 날짜 달력 선택기 필터와 함께 지급 보기 그리드 위에 표시됩니다.

트랜잭션 날짜, 참조 ID, 송장 번호 및 결제 방법 세부 정보를 포함하여 일별 보고서에서 [각 지급 트랜잭션에 대한 정보](#column-descriptions)를 보려면 왼쪽과 오른쪽으로 스크롤하십시오.

#### 트랜잭션 일정 사용자 지정

지급 보고서 보기에서 특정 날짜를 입력하거나 날짜 선택기에서 날짜 범위를 선택하여 보려는 지급 거래에 대한 기간을 사용자 정의할 수 있습니다.

1. _관리자_ 사이드바에서 **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]** > _[!UICONTROL Payouts]_>**[!UICONTROL View Report]**(으)로 이동합니다.
1. _[!UICONTROL Transaction dates]_&#x200B;일정 선택기 필터를 클릭합니다.
1. 적용 가능한 날짜 범위를 선택합니다.
1. 그리드에서 지정된 날짜에 대한 지급 상태를 봅니다.

### 열 표시 및 숨기기

지급 보고서 보기에는 기본적으로 사용 가능한 대부분의 정보 열이 표시됩니다. 그러나 보고서에 표시되는 열을 사용자 지정할 수 있습니다.

1. _관리자_ 사이드바에서 **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Payouts]_>**[!UICONTROL View Report]**(으)로 이동합니다.
1. _열 설정_ 아이콘(![열 설정 아이콘](assets/column-settings.png){width="20" zoomable="yes"})을 클릭합니다.
1. 보고서에 표시되는 열을 사용자 지정하려면 목록에서 열을 선택하거나 선택 취소합니다.

   일시 중지 보고서 보기에는 열 설정 메뉴에서 변경한 사항이 즉시 표시됩니다. 열 환경 설정이 저장되며 보고서 보기에서 나가면 적용됩니다.

### 트랜잭션 다운로드

지급액 보기 그리드에 표시되는 모든 트랜잭션이 들어 있는 .csv 파일을 다운로드할 수 있습니다.

1. _관리자_ 사이드바에서 **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]** > _[!UICONTROL Payouts]_>**[!UICONTROL View Report]**(으)로 이동합니다.
1. [트랜잭션에 대한 날짜 범위 일정 사용자 지정](#customize-transactions-timeframe).
1. _다운로드_( ![다운로드 아이콘](assets/icon-download.png){width="20" zoomable="yes"} ) 아이콘을 클릭합니다.

지급 트랜잭션은 .csv 형식으로 다운로드됩니다.

### 열 설명

지급 보고서에는 다음 정보가 포함됩니다.

| 열 | 설명 |
| ------------ | -------------------- |
| [!UICONTROL Provider] | 결제 제공자 |
| [!UICONTROL Provider trans] | 거래 ID |
| [!UICONTROL Trans date] | 트랜잭션이 시작된 날짜 및 시간 |
| [!UICONTROL Type] | 트랜잭션 유형—*[!UICONTROL PAYMENT]*, *[!UICONTROL BONUS]*, *[!UICONTROL CHARGEBACK]*, *[!UICONTROL CORRECTION]*, *[!UICONTROL CURRENCY_CONVERSATION]*, *[!UICONTROL DEPOSIT]*, *[!UICONTROL DISBURSEMENT]*, *[!UICONTROL DISPUTE]*, *[!UICONTROL FEES]*, *[!UICONTROL HOLD]*, *[!UICONTROL HOLD_RELEASE]*, *[!UICONTROL INCENTIVES]*, *[!UICONTROL OTHERS]*, *[!UICONTROL RECOUP]*, *[!UICONTROL REFUND]*, *[!UICONTROL REVERSAL]*, *[!UICONTROL WITHDRAWAL]* <br> <br>자세한 내용은 [트랜잭션 유형](#transaction-types)을 참조하세요. |
| [!UICONTROL Status] | 현재 트랜잭션 상태—*[!UICONTROL SUCCESS]*, *[!UICONTROL DENIED]*, *[!UICONTROL PENDING]* |
| [!UICONTROL Code] | 대변(*CR*) 또는 차변(*DR*)을 나타내는 거래 코드 |
| [!UICONTROL Reference ID] | 이 이벤트와 관련된 원래 거래 ID |
| [!UICONTROL Invoice] | 거래의 송장 ID(주문당 하나) |
| [!UICONTROL Commerce order] | Commerce 주문 ID <br> <br>관련 [주문 정보](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/orders)를 보려면 ID를 클릭하십시오. |
| [!UICONTROL Commerce trans] | Commerce 거래 ID |
| [!UICONTROL Pay method] | 신용 카드 유형—*[!UICONTROL BANK]*, *[!UICONTROL PAYPAL]*, *[!UICONTROL CREDIT_CARD]* 및 관련 카드 공급자(예: *Visa* 또는 *MasterCard*) |
| [!UICONTROL TRANS AMT] | 거래 금액 |
| [!UICONTROL CUR] | 거래 금액에 대한 통화 단위 |
| [!UICONTROL PENDING] | 아직 지불되지 않은 금액 |
| [!UICONTROL CUR] | 보류 중인 금액에 대한 통화 단위 |
| [!UICONTROL SELLER AMT] | 고객 <br>(으)로부터 송금 금액 <br>판매자 계정에서 나가는 자금은 대시(-) 접두사를 표시합니다. |
| [!UICONTROL CUR] | 판매자 금액에 대한 통화 단위 |
| [!UICONTROL PARTNER FEE] | 트랜잭션 <br>과(와) 연결된 파트너 수수료 <br>파트너 수수료 계정에서 나가는 자금은 대시(-) 접두사를 표시합니다. |
| [!UICONTROL CUR] | 파트너 비용에 대한 통화 단위 |
| [!UICONTROL PROV FEES] | 트랜잭션 <br>과(와) 연계된 수수료 <br>공급자 수수료 계정에서 이동하는 자금은 대시(-) 접두사를 표시합니다. |
| [!UICONTROL CUR] | 제공업체 수수료에 대한 통화 단위 |
| [!UICONTROL FEE %] | 수수료로 청구된 거래 금액의 백분율 |
| [!UICONTROL FIXED FEE] | 고정 공급자 수수료 금액 |
| [!UICONTROL CHBK FEE] | 거래 <br>에 연결된 비용 청구 수수료 <br>대시(-) 접두사는 비용 산출 비용이 반전되었음을 나타냅니다. |
| [!UICONTROL CUR] | 비용 청구 요금에 대한 통화 단위 |
| [!UICONTROL HOLD AMT] | 보류 중 또는 보류 해제 금액 <br> <br>대시(-) 접두사는 보류 중인 자금이 출시되고 있음을 나타냅니다. |
| [!UICONTROL CUR] | 보류 금액에 대한 통화 단위 |
| [!UICONTROL RECOUP AMT] | 회수 계정 <br>에서 회수된 금액 <br>수금 계정에서 나가는 자금은 대시(-) 접두사를 표시합니다. |
| [!UICONTROL CUR] | 배상 금액에 대한 통화 단위 |

### 거래 유형

이러한 거래 유형은 지급금 거래에서 유의할 수 있다.

| 보고서 | 설명 |
| ------------ | -------------------- |
| [!UICONTROL PAYMENT] | 주문하기 위해 구매자와 판매자 간에 돈이 이동했다 |
| [!UICONTROL AUTH] | 인증 및 인증 무효 트랜잭션 |
| [!UICONTROL BONUS] | — |
| [!UICONTROL CHARGEBACK] | 차지백 수수료 및 차지백 수수료 취소 거래 |
| [!UICONTROL CORRECTION] | — |
| [!UICONTROL CURRENCY_CONVERSION] | — |
| [!UICONTROL DEPOSIT] | — |
| [!UICONTROL DISBURSEMENT] | — |
| [!UICONTROL DISPUTE] | — |
| [!UICONTROL FEES] | 파트너 수수료, 결제 수수료 및 수수료 취소 거래 |
| [!UICONTROL HOLD] | — |
| [!UICONTROL HOLD_RELEASE] | — |
| [!UICONTROL INCENTIVES] | — |
| [!UICONTROL OTHERS] | — |
| [!UICONTROL RECOUP] | 은행 또는 손실 계좌에서 배상 |
| [!UICONTROL REFUND] | — |
| [!UICONTROL REVERSAL] | — |
| [!UICONTROL WITHDRAWAL] | — |
