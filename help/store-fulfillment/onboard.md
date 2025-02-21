---
title: 스토어 이행 서비스에 대한 온보딩 개요
description: '[!DNL Live Search] 온보딩 흐름, 시스템 요구 사항, 경계 및 제한 사항.'
role: Admin, Leader
level: Intermediate
feature: Shipping/Delivery, Install
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 0%

---

# 스토어 이행 온보딩 개요

다음 구성 요소를 설정, 구성 및 활성화하여 [!DNL Store Fulfillment for Adobe Commerce by Walmart Commerce Technologies]을(를) 시작합니다.

- **이행 확장 저장**-Adobe Commerce 인스턴스에 이 타사 확장을 설치하고 구성합니다. 설치 후 Commerce 상점 첫 화면에서 [!DNL buys online, pickup in store]&#x200B;(BOPIS) 시나리오를 지원하도록 관리자의 스토어 이행 솔루션을 구성하고 관리할 수 있습니다.

  관리 보기의 ![[!DNL Store Fulfillment Service] 구성](assets/store-fulfillment-admin-home.png)

- **이행 계정 저장**-활성화 프로세스 중에 계정 관리자가 이행 계정을 만들고 계정 정보와 자격 증명을 제공합니다. Adobe Commerce과 스토어 이행 솔루션 간 연결을 활성화하려면 이러한 자격 증명이 필요합니다.

- **스토어 지원 앱** - 스토어 연결을 전체 스토어 이행 워크플로우와 함께 제공하여 모바일 장치에서 BOPI 주문을 관리합니다. Store Associates는 iOS 및 Android™ 디바이스용 Walmart [!DNL Store Assist]을(를) 다운로드하여 설치할 수 있습니다. 앱 온보딩 프로세스는 별도의 프로세스로 Walmart Commerce Technologies 클라이언트 센터에서 관리합니다. 그러나 Adobe Commerce 관리자가 [일부 앱 구성 설정](user-setup.md)을 완료했습니다.

  | 스토어 지원 앱 - 시작 보기 | 스토어 지원 앱 - 모듈 보기 |
  |-------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------|
  | 모바일 장치에서 ![[!DNL Store Assist App Getting Started] 보기](assets/store-assist-get-started-small.png) | 모바일 장치의 ![[!DNL Store Assist App Orders view]](assets/store-assist-orders-small.png) |

## 프로비저닝 단계

- **[!DNL Store Fulfillment for Adobe Commerce by Walmart Commerce Technologies]**&#x200B;에 등록 - [business.adobe.com](https://business.adobe.com/resources/store-fulfillment.html)에서 등록 양식을 작성하거나 Adobe Commerce 계정 관리자에게 도움을 요청하십시오.

- **저장소 이행 요청 시작**-계정 관리자가 제공한 Intake 양식을 완료하여 프로비저닝 프로세스를 시작하는 데 필요한 정보를 제공합니다.

- **스토어 이행 계정 자격 증명을 가져옵니다**-스토어 이행 계정이 만들어지면 스토어 이행 솔루션을 Adobe Commerce과 통합하는 데 필요한 자격 증명을 받게 됩니다.

- **[소스 코드를 다운로드하여  [!DNL Store Fulfillment] 확장](install.md)** 설치

## 온보딩 단계

1. [Adobe Commerce용 스토어 이행 확장 설치](install.md).

1. 책임자가 [솔루션을 사용하도록 설정](enable-general.md)합니다.

1. [Adobe Commerce 관리자에서 스토어 이행 확장을 구성합니다](service-config-settings-overview.md).

1. [제공된 스토어 이행 자격 증명을 사용하여  [!DNL Store Fulfillment] 서비스에 연결합니다](connect-set-up-service.md).

1. [스토어 지원 앱에 대한 사용자 및 역할을 만듭니다](user-setup.md).

1. [원하는 장치에 Walmart의 [!DNL Store Assist] 앱을 다운로드합니다. 이 앱은 Apple 앱(iOS)과 Google Play(Android™)](app-setup.md) 스토어 모두에서 사용할 수 있습니다.

설치, 구성, 온보딩을 완료하고 [!DNL Store Assist] 앱에 액세스한 후에는 [주문 및 테스트 만들기를 시작할 수 있습니다](test-and-deploy.md).
