---
title: 스토어 이행 테스트 및 배포
description: 저장소 이행 기능을 확인하는 테스트 계획입니다. 테스트에서는 재고 동기화 API, 취소된 주문에 대한 엔드 투 엔드 이행 워크플로, 스토어 이행 앱 사용자 관리 및 고객 체크인 경험을 다룹니다.
role: User, Admin
level: Intermediate
feature: Shipping/Delivery, User Account, Roles/Permissions
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '2661'
ht-degree: 0%

---

# Adobe Commerce용 스토어 이행 테스트 및 배포

개발 환경에서 온보딩 프로세스를 완료한 후 프로세스를 시작하여 스토어 이행 솔루션을 테스트하고 프로덕션 환경에 배포할 수 있습니다.

**필수 구성 요소**

정보, 스토어 또는 주문을 테스트하거나 동기화하기 전에 다음 작업을 완료했는지 확인하십시오.

- 스토어 이행 서비스에 대한 [일반 구성](enable-general.md)을(를) 완료했습니다.

- [샌드박스 및 프로덕션 환경에 대한 계정 자격 증명 및 연결 세부 정보 추가 및 확인](connect-set-up-service.md#configure-store-fulfillment-account-credentials)

- 스토어 이행 솔루션에 대한 [Adobe Commerce 통합](connect-set-up-service.md#configure-store-fulfillment-account-credentials)을 사용할 수 있고 인증되었는지 확인하십시오.

## 테스트 준비

테스트 주문을 만들거나 통합 테스트를 수행하려면 먼저 연결 구성을 완료해야 합니다. 테스트하기 전에 스토어 데이터가 동기화되었는지 확인해야 합니다.

1. 스토어 이행 소스 동기화.

   - **[!UICONTROL Stores > Sources]**(으)로 이동합니다.

   - **[!UICONTROL Synchronize Store Fulfillment Sources]**&#x200B;을(를) 선택합니다.

1. 저장소 그리드에서 테스트 주문을 만들기 전에 저장소가 `Synced`(으)로 표시되었는지 확인하십시오.

## 샘플 테스트 계획

소매업체는 배포의 구성 및 테스트 단계에서 스토어 이행 솔루션의 기본 기능을 검증합니다. 이 샘플 테스트 계획은 테스트의 시작 지점을 제공합니다. 요구 사항에 따라 시나리오를 더 추가합니다.

>[!NOTE]
>
>스토어 이행 솔루션에 대한 초기 온보딩을 완료하거나 기존 설치를 업데이트한 후에는 프로덕션에 배포하기 전에 항상 비프로덕션 환경에서 애플리케이션을 테스트하십시오.

이 샘플 테스트 계획은 다음 기능 영역을 다룹니다.

| 기능 영역 | 함수 | 역할 |
|-------------------------------------|------------------------------------------|----------------------------------|
| 재고 및 주문 동기화 | 인벤토리 API 동기화 | Adobe Commerce 관리자 |
| 철저해 | 주문 취소 워크플로우 | 고객, 관리자, 스토어 어소시에이트 |
| 관리자 | Fulfillment 앱 권한 저장 | 관리자 |
| Adobe Commerce 프론트엔드 | 제품 유형 | 고객, 관리자 |
| 프론트엔드 체크 아웃</br>체크 인 양식 | 체크인 경험 | 고객, 관리자 |
| 스토어 지원 앱 | 주문</br>선택</br>단계</br>및 전달 | 스토어 어소시에이트 |

### 인벤토리 API 동기화

이 테스트 계획 섹션에서는 Adobe Commerce과 스토어 이행 솔루션 간에 픽업 소스 및 재고에 대한 업데이트가 올바르게 동기화되는지 확인하기 위한 재고 및 주문 동기화를 다룹니다.

**기능 영역**: 인벤토리 및 주문 동기화</br>
**역할:** 관리자</br>
**테스트 유형:** 모두 양수

<table>
<thead>
<tr>
<th>함수</th>
<th>테스트 시나리오</th>
<th>예상 결과</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>픽업 스톡 소스 추가</strong></td>
<td>새 픽업 스톡 소스를 저장합니다.</td>
<td>실시간 동기화는 5분 이내에 소스 세부 정보를 Walmart GIF 서비스로 전송합니다.</td>
</tr>
<tr>
<td><strong>기존 픽업 스톡 소스 업데이트</strong></td>
<td>기존 픽업 스톡 소스에 대한 업데이트를 저장합니다.</td>
<td>실시간 동기화 작업은 5분 내에 월마트 GIF으로 세부 사항을 전송합니다</td>
</tr>
<tr>
<td><strong>Pickup stock 원본</br><code>Is Synced</code> 상태</strong></td>
<td>기존 픽업 스톡 소스에 대한 업데이트를 저장합니다.</td>
<td>작업이 완료되면 Source 관리 페이지의 <code>Is Synced</code> 열이 <code>No</code>에서 <code>Yes</code>(으)로 업데이트됩니다.</td>
</tr>
<tr>
<td><strong>수정된 재고 예약 프로세스</strong></td>
<td>제품에 대한 새 주문을 생성하여 제출합니다.</td>
<td>그 제품에 대한 판매 가능 수량이 그에 따라 감소합니다.</td>
</tr>
<tr>
<td><strong>새 주문 푸시, API 동기화 - 고객 주문</strong></td>
<td>고객이 매장 픽업 주문을 제출합니다.</td>
<td><ul><li>관리 순서 보기에서 <strong>Adobe Commerce 관리자</strong>가 주문 동기화 상태가 (으)로 업데이트되었음을 확인합니다. <code>Sent</code></li><li>주문 세부 사항 로그에 메시지가 포함됩니다 <code>Order was sent to BOPIS solution for sync, it's not yet acknowledged yet.</code></li></ul></td>
</tr>
<tr>
<td><strong>새 주문 푸시, API 동기화 - 관리자가 주문을 제출함</strong></td>
<td>Adobe Commerce <strong>관리자</strong>가 픽업 주문을 제출합니다.</td>
<td><ul><li>[관리 순서] 보기에서 [동기화 순서] 상태가 <code>Sent</code>(으)로 업데이트됩니다.</li><li>주문 세부 사항 로그에 메시지가 포함됩니다 <code>Order was sent to BOPIS solution for sync, it's not yet acknowledged yet.</code></li></ul></td>
</tr>
<tr>
<td><strong>새 주문 푸시, 예외 대기열<strong></td>
<td>Faa(Fulfillment Service)와의 상호 작용 없이 Adobe Commerce을 통해 이행할 수 있는 Adobe Commerce Admin에서 가상 및 다운로드 가능한 여러 제품을 식별합니다.</td>
<td>이러한 제품은 FaaS와의 다운스트림 충돌을 방지하기 위해 내보내기에서 적절하게 제거되거나 플래그가 지정됩니다.</td>
</tr>
</tbody>
</table>

### 주문 취소 워크플로우

테스트 계획의 이 섹션에는 Adobe Commerce을 통해 취소된 주문에 대한 엔드 투 엔드 워크플로우를 테스트하는 시나리오가 포함되어 있습니다.

**기능 영역:** Adobe Commerce 관리자</br>
**역할:** 전체(관리자, 스토어 연결, 고객)</br>
**테스트 결과 형식:** 모든 시나리오에서 양수

<table style="table-layout:fixed">
<tr>
<th>함수</th>
<th>시나리오</th>
<th>예상 결과</th>
</tr>
<tr>
<td><strong>전체 주문 취소</strong></td>
<td><ol>
<li>주문.</li>
<li>주문이 동기화될 때까지 기다립니다.</li>
<li>송장 전자 메일 수신을 송장 생성(승인 및 캡처하는 경우) 확인</li>
<li>송장 조회에서 주문한 모든 제품을 사용하여 대변 메모를 생성합니다.</li>
</ol>
</td>
<td>
<ul>
<li>주문 내역이 <code>We refunded $X online. Transaction ID: transactionID</code> 및(으)로 업데이트됨 <code>Received Cancel acknowledgment from the BOPIS solution.</code></li>
<li>주문 상태는 <code>Closed</code>입니다. (이제 지불 검토를 설정했습니다.)</li>
<li>Adobe Commerce에서 생성한 대변 메모. (크론이 작동할 때까지 기다립니다.)</li>
<li>모든 항목을 선택한 경우 <code>DISPLAY COMMENT HISTORY</code> 픽업 이메일에 <code>Order is ready for pickup</code>이(가) 표시됩니다(<code>CUSTOMER NOTIFIED</code> 플래그는 <code>true</code>임).</li>
<li>모든 항목을 선택하지 않은 경우 취소 이메일 및 댓글 기록 표시 <code>Order has been canceled - all items were not available</code></li>
<li><code>CUSTOMER NOTIFIED</code> 플래그가 <code>true</code>입니다.)</li>
</ul>
</td>
</tr>
<tr><td><strong>부분 주문 취소<strong></td>
<td>
<ol>
<li>최소 두 가지 이상의 제품을 주문하십시오.</li>
<li>주문이 동기화될 때까지 기다립니다.</li>
<li>송장이 생성되었는지(승인 및 캡처한 경우), 그리고 송장 이메일이 수신되었는지 확인합니다.</li>
<li>거래 해결을 위해 2시간 동안 기다립니다.</li>
<li>송장 조회에서 주문된 제품의 일부만 포함된 대변 메모를 생성합니다.</li>
</td>
<td>
<ul>
<li>주문 내역 업데이트: <code>We refunded $X online. Transaction ID: transactionID</code></li>
<li>주문 내역 업데이트: <code>Order notified as partly canceled at: Date and Hour</code></li>
<li>주문 환불 이메일 수신: <code>$x amount was refunded</code></li>
<li>주문 상태는 <code>Processing</code>입니다.</li>
<li>Adobe Commerce에서 생성된 대변 메모(cron이 작동할 때까지 대기).</li>
<li>일부 항목이 선택되지 않은 경우 nil 선택 또는 환불 섹션이 포함된 [!UICONTROL Ready for Pickup] 전자 메일이 표시되는지 확인하십시오. <code>DISPLAY COMMENT HISTORY</code>이(가) <code>Order is ready for pickup, but some items not available.</code>을(를) 표시합니다.</li>
<li><code>CUSTOMER NOTIFIED</code> 플래그는 <code>true</code>입니다.</li>
</ul>
</td>
</tr>
<td><strong>픽업 준비</br></br>전체 취소</br>(모든 제품이 0수량으로 선택된 상태로 설정됨)</strong></td>
<td>
<ol>
<li>주문하십시오.</li>
<li>주문이 동기화될 때까지 기다립니다.</li>
<li>송장이 생성되었는지(승인 및 캡처한 경우), 그리고 송장 이메일이 수신되었는지 확인합니다.</li>
<li>Postman으로 이동하여 모든 제품이 <code>0 qty</code>과(와) 함께 <code>picked</code>(으)로 설정된 픽업 준비 요청을 실행합니다.</li>
</ol>
</td>
<td>
<ul>
<li>업데이트된 주문 내역: <code>We refunded $X offline</code></li>
<li>주문 상태는 <code>CLOSED</code>입니다.
<li>대변 메모가 생성됩니다. (크론이 작동할 때까지 기다립니다.)</li>
<li>환불 이메일 수신됨: <code>$x amount was refunded</code></li>
<li>주문 취소 이메일이 전송되었습니다.</li>
</ul>
</td>
</tr>
<tr>
<td><strong>픽업 준비 - 일부 취소</strong></br></br><strong>(일부 제품은 선택되었으며 일부는 <code>0 qty</code>(으)로 선택됨)</strong>
</td>
<td>
<ol>
<li>주문하십시오.</li>
<li>주문이 동기화될 때까지 기다립니다.</li>
<li>송장이 생성되었는지(승인 및 캡처한 경우), 그리고 송장 이메일이 수신되었는지 확인합니다.</li>
<li>Postman으로 이동하여 픽업 준비 요청을 실행하고 제품의 일부는 피킹되고 일부는 피킹되며 나머지는 피킹됩니다.</li>
</ol>
</td>
<td>
<ul>
<li><code>Your order is ready for pickup</code> 테이블 [!UICONTROL Ready for Pickup Items]개 및 [!UICONTROL Canceled Items]개 </li>
<li>주문 상태가 픽업 준비되었습니다. </li>
<li>주문 내역 업데이트됨: <code>We refunded $X offline.</code>
<li>주문 내역 업데이트됨: <code>Order notified as partly canceled at: Date and hour</code>
<li>환불 이메일 수신: <code>$x amount was refunded</code>
<li>대변 메모가 생성됩니다. (크론이 작동할 때까지 기다립니다.)</li>
</ul>
</td>
</tr>
<tr>
<td><strong>픽업 준비 - 일부 취소</br></br>일부 제품이 선택되었으며 일부는 <code>0 qty</code>(으)로 선택됨</strong>
</td>
<td><ol>
<li>주문하십시오.</li>
<li>주문이 동기화될 때까지 기다립니다.</li>
<li>송장이 생성되었는지(승인 및 캡처한 경우), 그리고 송장 이메일이 수신되었는지 확인합니다.</li>
<li>Postman으로 이동하여 픽업 준비 요청을 실행하고 제품의 일부는 피킹되고 일부는 피킹되며 나머지는 피킹됩니다.</li>
</ol>
</td>
<td><ul>
<li><code>Your order is ready for pickup</code> 테이블 [!UICONTROL Ready for Pickup Items]개 및 [!UICONTROL Canceled Items]개 </li>
<li>주문 상태가 픽업 준비되었습니다. </li>
<li>주문 내역 업데이트됨: <code>We refunded $X offline.</code>
<li>주문 내역 업데이트됨: <code>Order notified as partly canceled at: Date and hour</code>
<li>환불 이메일 수신: <code>$x amount was refunded</code>
<li>대변 메모가 생성됩니다. (크론이 작동할 때까지 기다립니다.)</li>
</ul>
</td>
</tr>
<tr>
<td><strong>분배됨(분배 중) </br></br>전체 취소(모든 제품이 거부됨으로 설정됨)</strong>
</td>
<td>
<ol>
<li>주문하십시오.</li>
<li>주문이 동기화될 때까지 기다립니다.</li>
<li>송장이 생성되었는지(승인 및 캡처한 경우), 그리고 송장 이메일이 수신되었는지 확인합니다.</li>
<li>Postman으로 이동하여 모든 제품이 피킹됨으로 설정된 상태로 픽업 준비 요청을 실행합니다.</li>
<li>사서함을 열고 픽업 준비 이메일을 찾습니다. 그런 다음 **[!UICONTROL Confirm Arrival]**&#x200B;을(를) 클릭합니다.</li>
<li>체크인.</li>
<li>Postman으로 이동하여 모든 제품이 거부됨으로 설정된 분배됨 요청을 실행합니다.</li>
</ol>
<td><ul>
<li>업데이트된 주문 내역: <code>We refunded $X offline.</code></li>
<li>환불 이메일 수신됨: <code>$x amount was refunded</code></li>
<li>상태가 <code>CLOSED</code>(으)로 설정되었습니다.</li>
<li>대변 메모가 생성되었습니다. (크론이 작동할 때까지 기다립니다.)</li>
</ul>
</td>
</tr>
<tr>
<td><strong>분배됨(분배 중)</br></br>일부 취소</br>(일부 제품은 분배됨, 일부는 거부됨)</strong>
</td>
<td>
<ol>
<li>주문하십시오.</li>
<li>주문이 동기화될 때까지 기다립니다.</li>
<li>송장이 생성되었는지(승인 및 캡처한 경우), 그리고 송장 이메일이 수신되었는지 확인합니다.</li>
<li>Postman으로 이동하여 모든 제품이 피킹됨으로 설정된 상태로 픽업 준비 요청을 실행합니다.</li>
<li>사서함을 엽니다. 픽업 준비 이메일을 찾아 <code>Confirm Arrival</code>을(를) 선택합니다.</li>
<li>체크인.</li>
<li>Postman으로 이동하여 일부 제품은 분배로 설정되고 일부는 거부로 설정된 분배됨 요청을 실행합니다</li>
</ol>
</td>
<td>
<li>업데이트된 주문 내역: <code>We refunded $X offline</code></li>
<li><code>Order notified as partly canceled at: Date and Hour</code>
<li>환불 이메일 수신: <code>$x amount was refunded</code>
<li>주문 상태가 <code>Ready for pickup Dispensed</code>(으)로 설정됨
<li>대변 메모가 생성되었습니다. (크론이 작동할 때까지 기다립니다.)</li>
</td>
</tr>
<tr>
<td> <strong>반환 후 새 RMA(전체)</strong>
</td>
<td>
<ol>
<li>주문하십시오.</li>
<li>주문이 동기화될 때까지 기다립니다.</li>
<li>승인 및 캡처 옵션이 구성된 경우 송장이 생성되었는지, 고객이 송장 이메일을 받았는지 확인합니다.</li>
<li>Postman이 포함된 모든 제품을 선택합니다.</li>
<li>체크인.</li>
<li>분배 해</li>
<li>주문하고 <strong>[!UICONTROL Create returns]을(를) 선택합니다.
<li>RMA를 생성합니다.</li>
</ol>
</td>
<td>
<ul>
<li>RMA가 만들어졌고 주문 보기의 <strong>[!UICONTROL Returns]</b> 탭 아래에 표시됩니다.</li>
<li>고객이 RMA 확인 이메일을 받았습니다.</li>
</ul>
</td>
</tr>
<tr>
<td><strong>반환 후 새 RMA — 부분</strong>
</td>
<td>
<ol>
<li>주문하십시오.</li>
<li>주문이 동기화될 때까지 기다립니다.</li>
<li>송장이 생성되었는지(승인 및 캡처한 경우), 그리고 송장 이메일이 수신되었는지 확인합니다.</li>
<li>Postman이 포함된 모든 제품을 선택합니다.</li>
<li>체크인.</li>
<li>분배 해</li>
<li>주문으로 이동한 다음  <strong>[!UICONTROL Create returns]</strong></li>
<li>주문한 제품의 일부로 RMA를 만듭니다.</li>
</ol>
<td>
<ul>
<li>주문 보기의 <strong>[!UICONTROL Returns]</strong> 탭 아래에 만들어진 RMA가 표시됩니다.</li>
<li>고객이 RMA 확인 이메일을 받았습니다.</li>
<li>RMA를 만든 후 RMA 인증을 받습니다. 관리자로부터 <strong>[!UICONTROL Sales > Returns]</strong>(으)로 이동합니다. 생성한 RMA를 선택하고 승인합니다.</li>
<li>고객이 RMA 인증 확인 이메일을 받았는지 확인합니다.</li>
<li>환불이 거래 및 주문 내역에 추가되었는지 확인합니다.</li>
</ul>
</td>
</tr>
</table>


### Fulfillment 앱 권한 저장

테스트 계획의 이 섹션에서는 스토어 이행 앱 사용자를 위한 계정 관리에 대해 설명합니다.

- 스토어 연결이 Adobe Commerce 관리자에서 만든 새 사용자 계정으로 인증할 수 있는지 확인합니다.
- 기존 계정에 대한 업데이트가 성공적으로 적용되었는지 확인합니다.

**기능 영역:** Adobe Commerce 관리자</br>
**역할:** 관리자, 스토어 연결</br>
**테스트 유형:** 모두 양수

<table style="table-layout:auto">
<tr>
<th>함수</th>
<th>시나리오</th>
<th>예상 결과</th>
</tr>
<tr>
<td><strong>사용자 계정 관리 - 계정 만들기</strong></br></br>
</td>
<td>
<ol>
<li><strong>관리자</strong> — Adobe Commerce 관리자에 로그인합니다.</li>
<li><strong>[!UICONTROL System] &gt; 스토어 이행 앱 권한 &gt; 모든 스토어 이행 앱 사용자로 이동</strong></li>
<li><strong>새 사용자를 추가합니다.</strong></li>
</ol>
<td>
<ul>
<li>계정이 정상적으로 생성되었습니다.</li>
<li>[!UICONTROL Store Fulfillment Users] 대시보드에 새 사용자 계정이 표시됩니다.</li>
<li><strong>스토어 연결</strong> 새 사용자 계정으로 스토어 지원 앱에 로그인합니다.</li>
</ul>
</td>
</tr>
<tr>
<td><strong>사용자 계정 관리 - 기존 사용자 계정 업데이트</strong>
</td>
<td>
<ol>
<li>관리자 계정으로 Adobe Commerce 관리자에 로그인합니다.</li>
<li><strong>[!UICONTROL System] &gt; 스토어 이행 앱 권한 &gt; 모든 스토어 이행 앱 사용자</strong>(으)로 이동합니다.</li>
<li>사용자 계정 목록에서 <strong>[!UICONTROL Edit]</strong>을(를) 선택하여 기존 활성 사용자 계정을 엽니다.
<li><strong>[!UICONTROL Is Active]</strong>을(를) <strong>아니요</strong>(으)로 변경하여 계정을 사용하지 않도록 설정하십시오.</li>
</ol>
</td>
<td>
<ul>
<li><strong>[!UICONTROL Store Fulfillment App Users]</strong> 대시보드에서 업데이트된 계정의 상태가 <strong>[!UICONTROL Inactive]</strong>(으)로 변경되었습니다.</li>
<li>스토어 연결이 비활성 계정 자격 증명으로 스토어 지원 앱에 로그인할 수 없습니다.</li>
</ul>
</td>
</tr>
</table>

## Adobe Commerce 제품 유형

Adobe Commerce 제품 유형에 대한 테스트 시나리오는 고객이 다양한 제품 유형에 대한 올바른 제품, 재고 및 게재 방법 정보를 볼 수 있는지 확인합니다.

- [!UICONTROL Configurable]
- [!UICONTROL Grouped]
- [!UICONTROL Virtual]
- Adobe Commerce 상점 첫 화면의 [!UICONTROL Bundle products].

**기능 영역:** Adobe Commerce 프론트엔드</br>
**역할:** 스토어 지원 앱 사용자(스토어 연결)</br>
**테스트 유형:** 모두 양수

<table style="table-layout:auto">
<tr>
<th>함수</th>
<th>시나리오</th>
<th>댓글</th>
</tr>
<tr>
<td><strong>구성 가능한 제품</strong>
</td>
<td>
<ul>
<li>사용자가 구성 가능한 옵션만 볼 수 있는지, 소스가 활성화되어 있는지, 재고가 지정되어 있는지, 재고에 일부 품목이 있는지(하위 제품 확인) 확인합니다.</li>
<li>다른 저장소를 선택할 때 사용할 수 없는 옵션이 제외된 것으로 표시되는지 확인합니다.</li>
<li>사용자가 다른 저장소를 선택하는 경우 구성 가능한 옵션이 선택 해제되는지 확인합니다.</li>
<li>구성 가능한 제품이 이미 장바구니에 들어 있고 사용자가 다른 스토어를 선택하면 제품이 품절로 표시되는지 확인합니다.</li>
</ul>
</td>
<td></td>
</td>
</tr>
<tr>
<td><strong>그룹화된 제품</strong>
</td>
<td>
<ul>
<li>모든 하위 제품에 포함된 경우 고객에 대해 게재 메서드 및 [!UICONTROL Add to cart] 단추가 비활성화되어 있는지 확인합니다.
<code>qty</code>이(가) <code>0</code>(으)로 설정되었습니다.</li>
<li>하위 제품 중 하나 이상에 <code>qty</code>이(가) 설정되어 있는 경우 고객에 대해 게재 메서드가 활성화되어 있는지 확인하십시오. <code>0.</code></li>
<li>[!UICONTROL Available for Store Pickup]이(가) 활성화된 제품에 대해서만 [!UICONTROL Store Pickup Delivery] 메서드가 표시되고 활성화되어 있는지 확인하십시오. (하위 제품 확인)</li>
</ul>
</td>
<td></td>
</tr>
<tr>
<td><strong>가상 제품</strong>
</td>
<td>
가상 제품이 [!UICONTROL In-store Pickup] 게재 방법을 제공하지 않는지 확인하십시오.
<td></td>
</td>
</tr>
<tr>
<td><strong>제품 번들</strong>
</td>
<td>
<ul>
<li>하나 이상의 하위 제품에 [!UICONTROL Available for Store Pickup]이(가) 비활성화된 경우 고객이 스토어 픽업 배달 옵션을 사용할 수 없는지 확인합니다.</li>
<li>하나 이상의 하위 제품에 [!UICONTROL Available for Home Delivery]이(가) 비활성화된 경우 고객이 홈 게재 옵션을 사용할 수 없는지 확인합니다.</li>
<li>번들의 하위 제품 중 하나 이상이 품절되었는지 확인하고 번들(상위 제품)도 표시됩니다
[!UICONTROL Out of stock] (으)로</li>
</ul>
</td>
<td></td>
</tr>
<tbody>
</table>

## 체크인 경험

이 테스트 계획 섹션에서는 다음 기능에 대한 스토어 픽업 주문 체크인 경험을 다룹니다.

- 대체 픽업 연락처 - [!UICONTROL Alternate Pickup Contact]을(를) 추가하고 스토어 픽업 주문에서 [!UICONTROL Preferred Contact]을(를) 선택하는 워크플로를 확인하십시오.

- 체크인 양식 - 스토어 픽업 주문에 대한 체크인 요청을 제출하는 워크플로우를 확인합니다.

**기능 영역:** 장바구니 체크아웃, 매장 픽업 주문을 위한 체크인 양식</br>
**역할:** 관리자, 고객, 스토어 연결</br>
**테스트 유형:** 모두 양수

### 대체 픽업 연락처


**기능 영역:** 장바구니 체크아웃</br>
**역할:** 고객</br>
**테스트 유형:** 모두 양수

<table style="table-layout:auto">
<tr>
<th>함수</th>
<th>시나리오</th>
<th>예상 결과</th>
</tr>
<tr>
<td><strong>대체 픽업 연락처</br>
체크인<strong>
</td>
<td>
고객이 매장 내 픽업 옵션을 사용하여 주문을 제출합니다.</td>
<td>체크아웃 프로세스 중에 배송 단계에서 [!UICONTROL Alternate Pickup Contact] 옵션이 표시됩니다.
</td>
</tr>
<tr>
<td><strong>대체 픽업 기본 담당자, 체크 인</strong>
<td>
고객이 매장 내 픽업 옵션을 사용하여 주문을 제출합니다. 체크아웃 중에 고객이 [!UICONTROL Alternate Pickup Contact]을(를) 추가합니다.</td>
<td>체크아웃 프로세스 중에 배송 단계에서 [!UICONTROL Preferred Contact] 옵션이 표시됩니다.</td>
</td>
</tr>
<tr>
<td><strong>대체 픽업 연락처 세부 정보, 체크 인</strong>
</td>
<td>
고객이 매장 내 픽업 옵션을 사용하여 주문을 제출합니다. 체크아웃하는 동안 고객은 배송 단계에서 [!UICONTROL Alternate Pickup Contact]을(를) 선택합니다.
</td>
<td>[!UICONTROL First name], [!UICONTROL Last name], [!UICONTROL Phone] 및 [!UICONTROL Email] 연락처 세부 정보를 입력하는 입력 옵션이 고객에게 표시됩니다.</td>
</tr>
<tr>
<td><strong>대체 픽업, 전자 메일 확인</strong>
</td>
<td>고객이 매장 내 픽업 옵션을 사용하여 주문을 제출합니다. 체크아웃 중에 고객은 배송 단계에서 [!UICONTROL Alternate Pickup Contact]을(를) 선택하고 연락처 세부 정보를 추가한 다음 주문을 제출합니다.</td>
<td>고객과 대체 담당자 모두 주문에 대한 체크인 이메일을 받습니다.</td>
</tr>
<td><strong>대체 픽업, 주문 세부 사항</strong></td>
<td>고객이 매장 내 픽업 옵션을 사용하여 주문을 제출합니다. 체크아웃 중에 고객은 배송 단계에서 [!UICONTROL Alternate Pickup Contact]을(를) 선택하고 연락처 세부 정보를 추가한 다음 주문을 제출합니다.</td>
<td>관리자는 저장된 주문에 대한 추가 연락처 정보를 봅니다.</td>
</tr>
<tr>
<td><strong>대체 픽업 연락처, 스토어 연결 주문 보기</strong>
</td>
<td>고객이 매장 내 픽업 옵션을 사용하여 주문을 제출합니다. 체크아웃 중에 고객은 배송 단계에서 [!UICONTROL Alternate Pickup Contact]을(를) 선택하고 연락처 세부 정보를 추가한 다음 주문을 제출합니다.</td>
<td>매장 직원은 FaaS/ChaaS에서 주문에 대한 추가 연락처 정보를 볼 수 있습니다.</td>
</td>
</tr>
</tbody>
</table>

### 체크인 양식


**기능 영역:** 체크 인 양식</br>
**역할:** 고객</br>
**테스트 유형:** 모두 양수

<table style="table-layout:auto">
<tr>
<th>함수</th>
<th>시나리오</th>
<th>예상 결과</th>
</tr>
<tr>
<td><strong>체크 인 작업—요청 제출</strong>
</td>
<td>체크인 양식에서 고객은 모든 필수 필드를 완료한 후 요청을 제출합니다.</td>
<td>고객이 성공 응답을 받습니다.</td>
</tr>
<tr>
<td><strong>체크 인 작업 - 요청 세부 정보 보기</strong></td>
<td>고객이 체크인 요청을 정상적으로 제출했습니다.</td>
<td>주문 상태는 FaaS 시스템에서 업데이트되며 스토어 어소시에이트는 FaaS에서 체크인 요청 세부 사항을 볼 수 있습니다.
</td>
</tr>
<tr>
<td><strong>Check in Action - 요청을 한 번만 제출</strong></td>
<td>고객은 주문에 대한 체크인 요청을 제출한 후 두 번째로 체크인할 링크를 선택합니다.</td>
<td>체크인 양식에서 고객은 양식을 편집하거나 다시 제출할 수 있는 옵션이 표시되지 않습니다.</td>
</tr>
<tr>
<td><strong>체크 인 작업(Check in Action) - 도착 확인</strong></td>
<td>매장 내 픽업 주문은 FaaS에서 픽업 준비가 된 것으로 표시됩니다. 고객이 픽업 준비 이메일을 받고 [!UICONTROL Confirm Arrival]을(를) 선택합니다.</td>
<td>고객은 주문에 대한 체크인 양식을 봅니다.</td>
</tr>
</tbody>
</table>

## 스토어 지원 앱

테스트 계획의 이 섹션에서는 스토어 지원 앱에서 주문, 선택 및 전달 워크플로우를 테스트하기 위한 시나리오를 다룹니다.

**기능 영역:** 스토어 지원 앱</br>
**역할:** 스토어 연결</br>
**테스트 유형:** 모두 양수

<table style="table-layout:auto">
<tr>
<th>함수</th>
<th>시나리오</th>
<th>예상 결과</th>
</tr>
<tr>
<td>
<strong>단일 주문 선택—행복한 경로, 곡선형 선택</strong></td>
<td>단일 및 복수 수량 품목을 피킹합니다. nil 픽이 없고 곡면으로 된 픽업(스테이징 포함)이 있습니다.
</td>
<td>
</td>
</tr>
<tr>
<td><strong>멀티 오더 피킹 - 행복한 경로, 커브사이드 픽업</strong></td>
<td>단일 및 복수 수량 품목. nil 선택 없음, 커브사이드 픽업(스테이징 포함)</td>
<td></td>
</tr>
<tr>
<td><strong>단일 주문 선택—매장 내 수거</strong></td>
<td>단일 및 복수 수량 품목. nil 선택 없음, 매장 내 픽업(스테이징 포함)</td>
<td>
</td>
</tr>
<tr>
<td><strong>멀티 오더 피킹 — 행복한 경로, 매장 내 픽업</strong></td>
<td>단일 및 복수 수량 품목을 피킹합니다. nil 픽이 없고 곡면으로 된 픽업(스테이징 포함)이 있습니다.</td>
<td></td>
</tr>
<tr>
<td><strong>단일 주문 피킹—만족스럽지 않은 경로, 매장 내 픽업</strong></td>
<td>부분 및 간접 피킹 및 매장 내 픽업(스테이징 포함)을 통해 단일 및 다중 수량 품목을 피킹합니다.</td>
</td>
<td></td>
</tr>
<td><strong>다중 주문 피킹 - 경로 커브사이드 픽업이 적합하지 않음</strong></td>
<td>부분 및 간접 피킹 및 매장 내 픽업(스테이징 포함)을 통해 단일 및 다중 수량 품목을 피킹합니다.</td>
<td></td>
</tr>
<td><strong>단일 주문 피킹 - 패스가 좋지 않음, 측면 픽업</strong></td>
<td>부분 및 간접 픽업 및 커브사이드 픽업(스테이징 포함)을 통해 단일 및 다중 수량 품목을 피킹합니다.</strong></td>
</td>
<td></td>
</tr>
<tr><td><strong>주문 - 피킹 전 취소됨</strong></td>
<td></td>
<td></td>
</tr>
<tr>
<td><strong>주문 - 전달 전 취소됨</strong></td>
<td></td>
<td></td>
</tr>
<tr>
<td><strong>주문 - 주문 모듈에서 검색</strong></td>
<td></td>
<td></td>
</tr>
<tr><td><strong>주문 - 핸드오프를 위한 검색 및 수동 체크인</strong></td>
<td></td>
<td></td>
</tr>
<tr><td><strong>주문 배치됨 - 선택되었거나 선택기로 표시된 모든 항목을 사용할 수 없음</strong></td>
<td></td>
<td></td></tr>
<tr><td><strong>번들 품목과 함께 배치된 주문 - 피킹 및 전달</strong></td>
<td></td>
<td></td></tr>
<tr><td><strong>주문 - 거부가 있는 상태로 전달</strong></td>
<td></td>
<td></td></tr>
<tr><td><strong>주문 - 모든 항목의 거부와 함께 전달</strong></td>
<td></td>
<td></td></tr>
</tbody>
</table>

## 배포

솔루션이 구성되고 사양에 맞게 테스트되었는지 확인한 후에는 스테이징에서 프로덕션으로 배포할 준비가 된 것입니다.

배포와 테스트는 인프라와 기능에 따라 다릅니다.

>[!TIP]
>
>클라우드 인프라 프로젝트에서 Adobe Commerce에 대한 배포 지침, 체크리스트 및 모범 사례에 대해서는 Adobe Commerce 개발자 설명서에서 [스토어 배포](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/deploy/staging-production)를 참조하십시오.
