---
title: 영업 이메일 템플릿
description: 스토어 픽업 주문 이행 프로세스 중에 고객 및 스토어 관리자와 통신하기 위한 트랜잭션 이메일 템플릿을 구성합니다.
role: Admin
level: Intermediate
feature: Shipping/Delivery, Communications, Configuration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '1233'
ht-degree: 1%

---


# 영업 이메일 템플릿

스토어 이행 은 주문 및 이행 워크플로우를 지원하기 위한 확장된 트랜잭션 이메일 템플릿 세트를 제공합니다. 이 서비스는 고객 및 매장 관리자에게 주문 상태 변경 사항, 매장 내 픽업 주문에 대한 지침 등을 알리는 등 여러 채널에 걸쳐 일관되고 자동화된 커뮤니케이션 및 메시징 기능을 제공합니다.

스토어 이행 이메일 템플릿은 기본 메시지 및 설정으로 구성됩니다. Adobe Commerce의 판매자 관리자는 구성을 관리 및 수정하고 이메일 템플릿을 선택하여 다양한 시나리오에서 고객과 소통할 수 있습니다. 관리자는 템플릿을 구성하고 사용자 정의할 수도 있습니다.

책임자로부터 판매 전자 메일 템플릿을 구성합니다. **[!UICONTROL Stores > Configuration > Sales > Sales Emails]**.

## 이메일 - 일반 설정

<table>
<thead>
<tr>
<th><strong>필드</strong></th>
<th><strong>설명</strong></th>
<th><strong>범위</strong></th>
<th><strong>필수</strong></th>
</tr>
</thead>
<tbody><tr>
<td><strong>비동기 전송</strong></td>
<td>영업 이메일이 비동기적으로 전송되는지 여부를 결정합니다. 옵션: <br/>**`사용 안 함`** - (기본값) 이벤트에 의해 트리거되면 판매 이메일이 전송됩니다. 스토어 픽업에서 가장 빠른 통신 및 응답 시간을 보려면 기본 설정을 사용하십시오. <br/>**'사용'** - 이 옵션을 활성화하면 체크아웃 및 주문 처리 전자 메일 알림을 처리하는 프로세스가 미리 결정된 일정한 간격으로 전송될 백그라운드로 이동합니다.</td>
<td>스토어 뷰</td>
<td>아니요</td>
</tr>
</tbody></table>

## 스토어에서 픽업 준비 주문

<table>
<thead>
<tr>
<th><strong>필드</strong></th>
<th><strong>설명</strong></th>
<th><strong>범위</strong></th>
<th><strong>필수</strong></th>
</tr>
</thead>
<tbody><tr>
<td><strong>활성화됨</strong></td>
<td>이 이메일은 스토어 동료가 주문 선택을 완료하면 고객에게 전송됩니다. 이메일 알림을 비활성화하려면 "아니요"로 설정합니다. 이메일 템플릿이 비활성화된 경우에도 스토어 연결에 의해 주문이 선택되지 않습니다.</td>
<td>스토어 뷰</td>
<td>아니요</td>
</tr>
<tr>
<td><strong>픽업 이메일 발신자를 위한 주문 준비</strong></td>
<td>이메일 알림을 전송할 때 사용되는 발신자 ID입니다.</td>
<td>스토어 뷰</td>
<td>아니요</td>
</tr>
<tr>
<td><strong>주문 픽업 전자 메일 템플릿</strong></td>
<td>등록된 고객에게 알리는 데 사용되는 이메일 메시지 템플릿입니다. 기본 템플릿은 통합에서 제공됩니다.</td>
<td>스토어 뷰</td>
<td>아니요</td>
</tr>
<td><strong>게스트용 픽업 이메일 템플릿 주문 준비</strong></td>
<td>게스트 고객에게 알리는 데 사용되는 이메일 메시지 템플릿입니다. 기본 템플릿은 통합에서 제공됩니다.</td>
<td>스토어 뷰</td>
<td>아니요</td>
</tr>
<tr>
<td><strong>대체 픽업 담당자를 위한 픽업 준비가 된 이메일 템플릿</strong></td>
<td>주문에 이름이 지정된 추가 담당자에게 알리는 데 사용되는 이메일 메시지 템플릿입니다. 기본 템플릿은 통합에서 제공됩니다.</td>
<td>스토어 뷰</td>
<td>아니요</td>
</tr>
<tr>
<td><strong>주문 보내기 픽업 전자 메일 복사 대상</strong></td>
<td>각 알림의 사본을 보낼 이메일 주소를 쉼표로 구분한 목록.</td>
<td>스토어 뷰</td>
<td>아니요</td>
</tr>
<tr>
<td><strong>Send Order Ready For Pickup 이메일 복사 방법</strong></td>
<td>사용할 이메일 복사 방법(카본 복사)입니다.</td>
<td>스토어 뷰</td>
<td>아니요</td>
</tr>
</tbody></table>


## 스토어에서 주문이 선택되었습니다.

<table>
<thead>
<tr>
<th><strong>필드</strong></th>
<th><strong>설명</strong></th>
<th><strong>범위</strong></th>
<th><strong>필수</strong></th>
</tr>
</thead>
<tbody><tr>
<td><strong>활성화됨</strong></td>
<td>이 이메일은 고객이 스토어에서 주문한 물건을 수령했음을 확인하기 위해 고객에게 발송됩니다. 이메일 알림을 비활성화하려면 "아니요"로 설정합니다. 이메일 템플릿을 비활성화해도 고객이 주문을 선택하는 것은 방지되지 않습니다.</td>
<td>스토어 뷰</td>
<td>아니요</td>
</tr>
<tr>
<td><strong>주문이 이메일 발신자에게 전송되었습니다.</strong></td>
<td>이메일 알림을 전송할 때 사용되는 발신자 ID입니다.</td>
<td>스토어 뷰</td>
<td>아니요</td>
</tr>
<tr>
<td><strong>주문이 전자 메일 템플릿으로 선택되었습니다.</strong></td>
<td>등록된 고객에게 알리는 데 사용되는 이메일 메시지 템플릿입니다. 기본 템플릿은 통합과 함께 제공됩니다</td>
<td>스토어 뷰</td>
<td>아니요</td>
</tr>
<td><strong>손님을 위한 주문 전자 메일 템플릿 선택됨</strong></td>
<td>게스트 고객에게 알리는 데 사용되는 이메일 메시지 템플릿입니다. 기본 템플릿은 통합에서 제공됩니다.</td>
<td>스토어 뷰</td>
<td>아니요</td>
</tr>
<tr>
<td><strong>(으)로 이메일 사본 보내기 선택됨</strong></td>
<td>각 알림의 사본을 보낼 이메일 주소를 쉼표로 구분한 목록.</td>
<td>스토어 뷰</td>
<td>아니요</td>
</tr>
<tr>
<td><strong>전송 이(가) 이메일 복사 방법으로 선택되었습니다.</strong></td>
<td>사용할 이메일 복사 방법(카본 복사)입니다.</td>
<td>스토어 뷰</td>
<td>아니요</td>
</tr>
</tbody></table>

## 주문 지연됨

<table>
<thead>
<tr>
<th><strong>필드</strong></th>
<th><strong>설명</strong></th>
<th><strong>범위</strong></th>
<th><strong>필수</strong></th>
</tr>
</thead>
<tbody><tr>
<td><strong>활성화됨</strong></td>
<td>이 이메일은 고객에게 가맹점에서 주문을 처리하거나 선택하는 데 지연되는 것에 대해 통지하기 위해 발송됩니다. 이메일 알림을 비활성화하려면 "아니요"로 설정합니다. 이메일 템플릿을 비활성화해도 주문이 지연되는 것을 방지할 수 없습니다.</td>
<td>스토어 뷰</td>
<td>아니요</td>
</tr>
<tr>
<td><strong>지연된 이메일 보낸 사람 주문
</strong></td>
<td>이메일 알림을 전송할 때 사용되는 발신자 ID입니다.</td>
<td>스토어 뷰</td>
<td>아니요</td>
</tr>
<tr>
<td><strong>지연된 이메일 템플릿 주문</strong></td>
<td>등록된 고객에게 알리는 데 사용되는 이메일 메시지 템플릿입니다. 기본 템플릿은 통합에서 제공됩니다.</td>
<td>스토어 뷰</td>
<td>아니요</td>
</tr>
<td><strong>게스트에 대한 지연된 이메일 템플릿 주문</strong></td>
<td>게스트 고객에게 알리는 데 사용되는 이메일 메시지 템플릿입니다. 기본 템플릿은 통합에서 제공됩니다.</td>
<td>스토어 뷰</td>
<td>아니요</td>
</tr>
<tr>
<td><strong>다음으로 주문 지연 이메일 사본 보내기</strong></td>
<td>각 알림의 사본을 보낼 이메일 주소를 쉼표로 구분한 목록.</td>
<td>스토어 뷰</td>
<td>아니요</td>
</tr>
<tr>
<td><strong>전송 주문 지연 복사 방법</strong></td>
<td>사용할 이메일 복사 방법(카본 복사)입니다.</td>
<td>스토어 뷰</td>
<td>아니요</td>
</tr>
</tbody></table>



## 주문 취소됨

<table>
<thead>
<tr>
<th><strong>필드</strong></th>
<th><strong>설명</strong></th>
<th><strong>범위</strong></th>
<th><strong>필수</strong></th>
</tr>
</thead>
<tbody><tr>
<td><strong>활성화됨</strong></td>
<td>이 이메일은 고객에게 발송되어 고객이 상점에서 주문을 취소했음을 알립니다. 전자 메일 알림을 사용하지 않도록 설정하려면 <code>No</code>(으)로 설정하십시오. 이메일 템플릿이 비활성화되어 있으면 주문이 취소되는 것을 방지할 수 없습니다.</td>
<td>스토어 뷰</td>
<td>아니요</td>
</tr>
<tr>
<td><strong>주문 취소된 이메일 발신자
</strong></td>
<td>이메일 알림을 전송할 때 사용되는 발신자 ID입니다.</td>
<td>스토어 뷰</td>
<td>아니요</td>
</tr>
<tr>
<td><strong>주문 취소된 이메일 템플릿</strong></td>
<td>등록된 고객에게 알리는 데 사용되는 이메일 메시지 템플릿입니다. 기본 템플릿은 통합에서 제공됩니다.</td>
<td>스토어 뷰</td>
<td>아니요</td>
</tr>
<td><strong>게스트에 대해 주문 취소됨</strong></td>
<td>게스트 고객에게 알리는 데 사용되는 이메일 메시지 템플릿입니다. 기본 템플릿은 통합에서 제공됩니다.</td>
<td>스토어 뷰</td>
<td>아니요</td>
</tr>
<tr>
<td><strong>다음으로 주문 취소 이메일 사본 보내기</strong></td>
<td>각 알림의 사본을 보낼 이메일 주소를 쉼표로 구분한 목록.</td>
<td>스토어 뷰</td>
<td>아니요</td>
</tr>
<tr>
<td><strong>전송 주문 취소 복사 방법</strong></td>
<td>사용할 이메일 복사 방법(카본 복사)입니다.</td>
<td>스토어 뷰</td>
<td>아니요</td>
</tr>
</tbody></table>


## 주문이 부분적으로 취소됨

<table>
<thead>
<tr>
<th><strong>필드</strong></th>
<th><strong>설명</strong></th>
<th><strong>범위</strong></th>
<th><strong>필수</strong></th>
</tr>
</thead>
<tbody><tr>
<td><strong>활성화됨</strong></td>
<td>이 이메일은 고객에게 발송되어 상점에서 주문의 일부가 취소되었음을 알립니다. 전자 메일 알림을 사용하지 않도록 설정하려면 <code>No</code>(으)로 설정하십시오. 이메일 템플릿을 비활성화해도 주문이 부분적으로 취소되는 것은 방지되지 않습니다.</td>
<td>스토어 뷰</td>
<td>아니요</td>
</tr>
<tr>
<td><strong>부분적으로 취소된 이메일 발신자 주문
</strong></td>
<td>이메일 알림을 전송할 때 사용되는 발신자 ID입니다.</td>
<td>스토어 뷰</td>
<td>아니요</td>
</tr>
<tr>
<td><strong>부분적으로 취소된 이메일 템플릿 주문</strong></td>
<td>등록된 고객에게 알리는 데 사용되는 이메일 메시지 템플릿입니다. 기본 템플릿은 통합에서 제공됩니다.</td>
<td>스토어 뷰</td>
<td>아니요</td>
</tr>
<td><strong>대체 픽업 연락처에 대해 부분적으로 취소된 이메일 템플릿 주문</strong></td>
<td>주문에 이름이 지정된 추가 담당자에게 알리는 데 사용되는 이메일 메시지 템플릿입니다. 기본 템플릿은 통합에서 제공됩니다.</td>
<td>스토어 뷰</td>
<td>아니요</td>
</tr>
<tr>
<td><strong>게스트에 대한 주문이 부분적으로 취소됨</strong></td>
<td>게스트 고객에게 알리는 데 사용되는 이메일 메시지 템플릿입니다. 기본 템플릿은 통합에서 제공됩니다.</td>
<td>스토어 뷰</td>
<td>아니요</td>
</tr>
<tr>
<td><strong>주문 부분적으로 취소된 이메일 사본 발송 대상</strong></td>
<td>각 알림의 사본을 보낼 이메일 주소를 쉼표로 구분한 목록.</td>
<td>스토어 뷰</td>
<td>아니요</td>
</tr>
<tr>
<td><strong>Send Order 부분적으로 취소된 복사 방법</strong></td>
<td>사용할 이메일 복사 방법(카본 복사)입니다.</td>
<td>스토어 뷰</td>
<td>아니요</td>
</tr>
</tbody></table>

## 배송처 저장소

<table>
<thead>
<tr>
<th><strong>필드</strong></th>
<th><strong>설명</strong></th>
<th><strong>범위</strong></th>
<th><strong>필수</strong></th>
</tr>
</thead>
<tbody><tr>
<td><strong>주문은 납품처 저장 제품 이메일 발신자입니다.</strong></td>
<td>재고를 사용할 수 있을 때까지 머천트 스토어에서 선택할 수 없는 모든 개설 주문의 집계 보고서로 지정된 머천트 담당자에게 전송된 이메일. </br></br> 판매자는 이 보고서를 사용하여 매장 간 재고 이전 또는 보충을 시작하고 관리할 수 있습니다. </br></br>이 알림은 [!DNL Ship-to-Store] 기능을 사용하도록 설정한 경우에만 적용됩니다.
</br></br>이 레이블은 선택한 배송 회사 또는 사용 가능한 배송 방법 레이블에 영향을 주지 않습니다.</td>
<td>스토어 뷰</td>
<td>아니요</td>
</tr>
<tr>
<td><strong>수신자 저장 전자 메일</strong></td>
<td>각 알림의 사본을 보낼 이메일 주소를 쉼표로 구분한 목록.</td>
<td>스토어 뷰</td>
<td>아니요</td>
</tr>
<tr>
<td><strong>이메일 템플릿</strong></td>
<td>수신자에게 알리는 데 사용되는 이메일 메시지 템플릿입니다. 기본 템플릿은 통합에서 제공됩니다.</td>
<td>스토어 뷰</td>
<td>아니요</td>
</tr>
</tbody></table>

>[!NOTE]
>
>미납주문을 허용하는 경우 이러한 주문에 대한 알림을 받으려면 관리자 이메일 주소를 제공해야 합니다. 다음 구성 설정에 주소를 추가합니다. [주문 지연](#order-delayed) 템플릿의 **[!UICONTROL Send Order Delayed Email Copy To]** 및 [스토어로 배달](#ship-to-store) 템플릿의 [!UICONTROL Ship To Store Email Recipients].



