---
title: 앱 설정
description: 온라인 구매, 스토어 주문 픽업을 위한 전체 스토어 이행 워크플로우 및 프로세스를 관리하려면  [!DNL Store Assist] 앱을 설정하십시오.
level: Intermediate
role: Admin
feature: Shipping/Delivery, Configuration, Tools and External Services
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 0%

---

# 앱 설정

Store Assist는 Walmart Commerce Technologies에서 제공하는 서비스별 주문 처리(Fulfillment-as-a-Service) 플랫폼 앱입니다. 앱은 [!DNL buy online, pick up in store]&#x200B;(BOPI) 주문을 처리하는 매장 내 처리 기능을 제공합니다. 스토어 어시스트를 통해 스토어 제휴자는 고객이 주문한 품목을 확인하고, 정확한 품목을 더 빨리 선택하며, 고객에게 매장 내 또는 커브사이드 픽업 배송에 대한 이행된 주문을 설정할 수 있습니다.

Store Assist 앱은 주문 세부 사항에서 시간을 선택하는 데 이르기까지 모든 주문 및 고객 정보를 수신하고 데이터를 모바일 장치를 통해 온라인으로 협력사에 저장할 수 있도록 합니다. 앱에는 다음과 같은 이행 활동과 Store Associates를 지원할 수 있는 [!UICONTROL Pick], [!UICONTROL Stage], [!UICONTROL Handoff] 및 [!UICONTROL Orders] 모듈이 포함되어 있습니다.

- 주문 납품 일자 및 시간을 지정합니다.
- 주문 픽업을 위해 고객이 도착하면 알림을 받습니다.
- 고객에게 전달할 스테이지 주문.
- 할당된 저장소 위치의 모든 주문에 대한 주문 상태를 추적합니다.

>[!NOTE]
>
>[스토어 지원 이행 워크플로](store-assist-modules.md) 항목을 검토하여 스토어 지원 앱에 대해 자세히 알아보세요.

## 스토어 지원 앱 구성

스토어 지원 앱에는 두 가지 유형의 구성이 필요합니다.

- [사용자 계정, 사용자 역할, 리소스 권한을 관리](user-setup.md) 및 [체크인 프로세스 중에 고객이 자동차 제조와 모델을 선택](check-in-experience-setup.md)할 수 있는 Adobe Commerce 관리 시스템 설정입니다.

- Store Assist 앱 인터페이스를 사용자 지정하는 프론트엔드 구성 설정 및 다음을 포함한 기타 설정:

   - **스토어 지원 앱 브랜딩**—회사 로고와 색상으로 앱 사용자 인터페이스를 사용자 지정합니다.

   - **기본 지침 업데이트** - 스토어 지원 선택, 준비, 전달 및 주문 모듈의 지침을 사용자 지정하여 스토어 구성원이 회사의 이행 워크플로우의 각 단계를 진행할 수 있도록 합니다.

   - **지역화**—앱에 사용할 수 있는 언어를 선택합니다. 날짜 및 시간 형식을 선택하고 기본 측정 단위 및 기본 통화를 선택합니다.

   - **비활성 시간**—로그아웃하기 전에 앱이 비활성 상태여야 하는 시간을 지정합니다.

   - **저장소에서 취소**—저장소에서 주문을 취소할 수 있는지 여부와 취소 권한이 있는 역할을 지정합니다

   - **주문 정리 기간**—선택한 주문이 다시 입고되기 전에 스테이징에 남아 있는 [예상 픽업 리드 타임](enable-general.md#delivery-method-title-configuration)을(를) 지정합니다(예: 3일). 기본값은 7일입니다. 이 구성이 켜져 있으면 이 시간이 만료되면 주문이 자동으로 취소됩니다. 품목은 재입고되고 판매자는 취소 이메일을 받습니다.

   - 앱 지침(선택, 스테이징, 전달)에서 모든 항목을 사용자 지정합니다.

   - **알림 피킹**—고객이 주문한 후 피킹 프로세스를 시작하기 위해 푸시 알림을 보낼지 여부를 지정합니다.

   - **알림 체크 인**—주문 픽업을 위해 체크인 프로세스 중에 푸시 알림을 보낼지 여부를 지정합니다. 체크인 후, 고객 대기 시간이 지정된 기간을 초과한 후에. 또는 알림을 비활성화합니다.

   - **처리 프로세스** - Store Associate가 고객에게 주문을 전달할 때 선택적 프로세스를 활성화합니다. 예를 들어 고객 서명이 필요하거나 담당자에게 고객 ID를 확인하라는 메시지를 표시합니다.

   - **전달 시 항목 거부 사용**—주문 전달 중에 고객이 주문 항목을 반환하거나 취소할 수 있도록 허용합니다.

  Walmart Commerce Technologies Client Services 팀과 함께 스토어 지원 앱에 대한 프론트엔드 구성을 완료합니다.

## 앱 다운로드 및 설치

Store Assist 앱을 설정하고 구성한 후 Store Associates는 모바일 장치에서 Store Assist 앱을 다운로드하여 설치하고 로그인할 수 있습니다.

- 모바일 장치가 스토어 이행 솔루션에 대한 [하드웨어 및 소프트웨어 요구 사항](solution-requirements.md#store-assist-app-requirements)을 충족하는지 확인하십시오.

- [Apple App Store](https://apps.apple.com/us/app/store-assist-by-walmart/id1609281539){target="_blank"} 또는 [Google Play 스토어](https://play.google.com/store/apps/details?id=com.walmart.faas.storeassist){target="_blank"}에서 스토어 지원 앱을 다운로드합니다.

- Store Associates에서 로그인하려면 다음 정보가 필요합니다.

   - 저장소 지원 계정과 연결된 **[!UICONTROL Company name]**

   - **지원 계정 자격 증명 저장**—계정의 사용자 이름 및 암호 자격 증명입니다.

  Adobe Commerce 관리자는 관리 저장소 설정에서 [매장 내 픽업](merchant-store-configuration.md#pickup-location-configuration)을(를) 사용하도록 설정한 모든 저장소 위치에 대해 [!DNL Store Assist app] 사용자 계정을 만들고 관리할 수 있습니다.
