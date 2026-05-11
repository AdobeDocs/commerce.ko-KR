---
title: Commerce 데이터 유형
description: 수집하여 Experience Platform으로 전송할 수 있는 데이터 유형을 알아봅니다.
role: Admin, Developer
feature: Personalization, Integration
exl-id: 6354963c-f27f-4e69-9ecb-acb4befb7c2a
TQID: https://experienceleague.adobe.com/LXMqOhHAZpUHaCeeU5ioKKXVrkLftospQEPDd9H-MD8
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 339
ht-degree: 2%

---

# Commerce 데이터 유형

[데이터 연결 확장](overview.md)은(는) Commerce 데이터를 Experience Platform에 연결합니다. Experience Platform에서 사용할 데이터는 **경험 이벤트** 클래스에 속하는 시계열 데이터와 **개별 프로필** 클래스에 속하는 레코드 데이터의 두 가지 동작 유형으로 그룹화됩니다.

Experience Platform의 [데이터 동작](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=ko#data-behaviors) 및 [클래스](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=ko#class)에 대해 자세히 알아보세요.

## 시계열 데이터

시계열 데이터는 레코드 주체가 직접 또는 간접적으로 작업을 수행한 시간에 시스템의 스냅샷을 제공합니다. 예를 들어, 쇼핑객이 사이트에서 제품을 탐색할 때 장바구니에 제품을 추가하고, 주문하는 등의 작업을 수행합니다. 클래스가 **경험 이벤트**(으)로 설정된 스키마를 사용하여 시계열 데이터가 Experience Platform에 수집됩니다.

### 캡처된 시계열 데이터

시계열 이벤트가 생성될 때 캡처되는 데이터를 알아보려면 [동작 이벤트](events.md) 및 [백 오피스 이벤트](events-backoffice.md)를 참조하십시오.

### 시계열 이벤트 데이터를 수집하는 데 필요한 스키마

동작 및 백 오피스 시계열 이벤트 데이터를 수집할 수 있는 [스키마를 만드는](update-xdm.md) 방법을 알아봅니다.

## 레코드 데이터

레코드 데이터는 주체의 속성에 대한 정보를 제공합니다. 주제는 조직 또는 개인일 수 있습니다. 예를 들어 사이트의 쇼핑객이 계정을 만들고 이 계정은 레코드 데이터를 생성합니다. 이 데이터는 클래스가 **개인 프로필**(으)로 설정된 스키마를 사용하여 Experience Platform에 수집됩니다. 해당 레코드 데이터를 Adobe의 프로필 관리 및 세분화 서비스로 보낼 수 있습니다. [Real-Time CDP](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=ko).

### 캡처된 프로필 레코드 데이터

프로필 레코드가 생성될 때 캡처된 데이터를 알아보려면 [고객 프로필 레코드 데이터](events-profilerecord.md)를 참조하십시오.

### 프로필 레코드 데이터를 수집하는 데 필요한 스키마

프로필 레코드 데이터를 수집할 수 있는 [스키마를 만드는](profile-data.md) 방법을 알아보세요.
