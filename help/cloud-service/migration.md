---
title: ' [!DNL Adobe Commerce as a Cloud Service](으)로 마이그레이션'
description: ' [!DNL Adobe Commerce as a Cloud Service](으)로 마이그레이션하는 방법에 대해 알아봅니다.'
exl-id: 9065c92a-f6b2-4464-8ec0-5c549bf78104
source-git-commit: d38066b6db7da5bb029391716063ed098be1f519
workflow-type: tm+mt
source-wordcount: '981'
ht-degree: 0%

---

# [!DNL Adobe Commerce as a Cloud Service]&#x200B;(으)로 마이그레이션

{{accs-early-access}}

[!DNL Adobe Commerce as a Cloud Service]에서는 대부분의 구성을 즉시 제공합니다. 그러나 기존 Adobe Commerce on Cloud 또는 온프레미스 인스턴스에서 마이그레이션하는 경우 특정 구성에 따라 다른 마이그레이션 작업을 수행해야 합니다.

## 마이그레이션 경로

[!DNL Adobe Commerce as a Cloud Service]은(는) 타임라인, 상점 및 사용자 지정에 따라 여러 마이그레이션 경로를 지원합니다.

전체 마이그레이션에 대한 대안으로 [!DNL Adobe Commerce as a Cloud Service]은(는) Commerce Optimizer 또는 증분 접근 방식을 사용하여 단계적 마이그레이션을 지원합니다.

* **증분 마이그레이션** - 이 방법에는 데이터, 사용자 지정 및 통합을 단계적으로 마이그레이션하는 작업이 포함됩니다. 이 방법은 복잡한 사용자 지정 및 데이터를 점차적으로 자신의 속도에 맞게 [!DNL Adobe Commerce as a Cloud Service]&#x200B;(으)로 전환하려는 많은 사용자 지정 기능을 가진 대형 가맹점에 이상적입니다.

![증분 마이그레이션](./assets/incremental.png){width="600" zoomable="yes"}

* **Commerce Optimizer**—이 방법을 사용하면 Commerce Optimizer을 전환 단계로 사용하여 복잡한 사용자 지정 및 데이터를 원하는 속도로 [!DNL Adobe Commerce as a Cloud Service]&#x200B;(으)로 이동하여 반복적으로 마이그레이션할 수 있습니다. Commerce Optimizer은 카탈로그 채널 및 정책으로 구동되는 머천다이징 서비스, Edge Delivery으로 구동되는 Commerce Storefront 및 AEM Assets으로 구동되는 제품 비주얼에 대한 액세스를 제공합니다.

![반복 마이그레이션](./assets/optimizer.png){width="600" zoomable="yes"}

* **전체 마이그레이션**—이 방법에는 모든 데이터, 사용자 지정 및 통합을 한 번에 마이그레이션하는 작업이 포함됩니다. 이 방법은 [!DNL Adobe Commerce as a Cloud Service]&#x200B;(으)로 빠르게 전환하려는 사용자 지정이 거의 없는 소규모 가맹점에 이상적입니다.

다음 표에서는 다양한 상점 및 구성의 마이그레이션 프로세스에 대한 개요를 제공합니다.

|                    | LUMA Storefront | PWA 상점 첫 화면 | Edge Delivery 기반 Commerce Storefront | Headless |
|--------------------|----------------------------------------|----------------------------------------|------------------------------------------------------|----------------------------------------|
| 데이터 마이그레이션 | 필수 | 필수 | 필수 | 필수 |
| 상점 첫 화면 | Edge Delivery 기반의 Commerce Storefront로 마이그레이션 | Edge Delivery 또는 유지 관리를 기반으로 하는 Commerce Storefront로 마이그레이션 | 영향 없음 | 영향 없음 |
| API 메쉬 | 새 메시 작성 | 새 메시 구축 또는 기존 메시 재구성 | 새 메시 구축 또는 기존 메시 재구성 | 새 메시 구축 또는 기존 메시 재구성 |
| 통합 | 통합 시작 키트 활용 | 통합 시작 키트 활용 | 통합 시작 키트 활용 | 통합 시작 키트 활용 |
| 사용자 정의 | App Builder 및 API Mesh로 이동 | App Builder 및 API Mesh로 이동 | App Builder 및 API Mesh로 이동 | App Builder 및 API Mesh로 이동 |
| Assets 관리 | OOTB를 사용하는 경우 마이그레이션 필요 | OOTB를 사용하는 경우 마이그레이션 필요 | OOTB를 사용하는 경우 마이그레이션 필요 | OOTB를 사용하는 경우 마이그레이션 필요 |
| 확장 | App Builder으로 마이그레이션 | App Builder으로 마이그레이션 | App Builder으로 마이그레이션 | App Builder으로 마이그레이션 |

표에서 알 수 있듯이 각 마이그레이션에 대한 완화 기능은 다음과 같이 구성됩니다.

* **데이터 마이그레이션**—제공된 마이그레이션 도구를 사용하여 기존 인스턴스에서 [!DNL Adobe Commerce as a Cloud Service]&#x200B;(으)로 데이터를 마이그레이션합니다.
* **Storefront** - 기존 EDS 및 Headless 스토어프론트는 완화가 필요하지 않지만 LUMA 스토어프론트는 Edge Delivery에서 제공하는 Commerce 스토어프론트로 마이그레이션해야 합니다. PWA Studio 스토어프론트를 Edge Delivery에서 제공하는 Commerce 스토어프론트로 마이그레이션하거나 현재 상태로 유지할 수 있습니다. Adobe은 storefront 마이그레이션을 지원하는 가속기를 제공합니다.
* **[API Mesh](https://developer.adobe.com/graphql-mesh-gateway)**—새 Mesh를 만들거나 기존 Mesh를 수정합니다. Adobe은 이 프로세스를 지원하기 위해 사전 구성된 메쉬를 제공합니다.
* **통합**—모든 통합은 [통합 시작 키트](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/) 또는 [[!DNL Adobe Commerce as a Cloud Service] REST API](https://developer.adobe.com/commerce/services/reference/cloud-service/core-admin/)를 활용해야 합니다.
* **사용자 지정** - 모든 사용자 지정은 App Builder 및 API Mesh로 이동해야 합니다.
* **Assets 관리**—모든 에셋 관리에 마이그레이션이 필요합니다. 이미 AEM Assets을 사용 중인 경우 마이그레이션할 필요가 없습니다.
* **확장**—모든 In-Process 확장을 Out-of-Process 확장으로 다시 만들어야 합니다. 2025년 말까지 Adobe은 빌드 시간을 최소화하기 위해 가장 인기 있는 확장에 대한 액세스를 제공합니다.

## 마이그레이션 단계

현재 Adobe Commerce 인스턴스에서 새 [!DNL Adobe Commerce as a Cloud Service] 인스턴스로 마이그레이션하는 데 주로 다음 단계가 포함됩니다.

* **[준비](#readiness-phase)**—배포를 ACCS로 이동할 준비가 되었는지 확인하는 것으로 시작합니다. 이 단계에서는 ACCS가 도입한 변경 사항도 숙지해야 합니다&#x200B;.
* **[구현](#implementation-phase)** - 다음으로 마이그레이션할 코드, 상점, 확장 및 통합을 준비합니다. 전환을 쉽게 하기 위해 Adobe에서는 [단기 및 장기 반복 접근 방식](#migration-paths)을 모두 사용할 수 있습니다&#x200B;.
* **[Go-Live](#go-live-phase)**—모든 항목이 제대로 되어 있는지 테스트하고 확인한 다음 데이터 마이그레이션을 수행합니다.
* **[Go-Live 후](#post-go-live-phase)** - Adobe과 함께 마이그레이션이 완료된 후 문제를 모니터링하고 필요에 따라 성능을 개선합니다.

### 준비 단계

1. 먼저 [!DNL Adobe Commerce as a Cloud Service] 아키텍처, 확장성 프레임워크 및 상점 기능을 검토하십시오.

   * [Adobe Commerce on Cloud Services 아키텍처](./overview.md) - 플랫폼 아키텍처 및 현재 Adobe Commerce 인스턴스와 어떻게 다른지 검토하십시오.
   * [Adobe Commerce 확장성 프레임워크](https://developer.adobe.com/commerce/extensibility/) - 현재 사용자 지정 내용을 전환하는 방법을 식별합니다.
   * [Edge Delivery에서 제공하는 Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/) - 권장 Storefront 솔루션을 검토하십시오.

1. 사용자 정의 호환성 감사:

   * 현재 사용자 지정 모듈 및 서드파티 통합을 식별합니다.
   * App Builder을 사용하여 다시 구현해야 하는 사용자 지정을 평가합니다.
   * 현재 사용자 정의를 해당 App Builder 확장 기능에 매핑합니다.

1. 상점 요구 사항을 확인하고 Adobe Edge 제공 기능과 일치하는지 확인하십시오.

1. 현재 타사 통합을 검토하고 [!DNL Adobe Commerce as a Cloud Service] 플랫폼과의 API 호환성을 확인합니다.

### 구현 단계

다음 단계에서는 마이그레이션의 개발 및 실행 프로세스에 대해 간략히 설명합니다.

1. [Commerce Cloud 관리자](./getting-started.md#create-an-instance)에서 새 [!DNL Adobe Commerce as a Cloud Service] 인스턴스를 만듭니다.

1. 필요한 앱 및 사용자 지정을 설치합니다. [!DNL Adobe Commerce as a Cloud Service]님이 가장 인기 있는 앱에 액세스할 수 있습니다. 추가 앱 또는 사용자 지정이 필요한 경우 App Builder을 사용하여 이를 다시 구현할 수 있습니다.

1. 다음 GraphQL 기반 상점 중 하나를 설정합니다.

   * [Commerce 상점 만들기](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/)
   * [PWA Studio을 사용하여 사용자 지정 GraphQL 기반 상점을 만드십시오](https://developer.adobe.com/commerce/pwa-studio/)

1. 이전 Commerce 인스턴스에서 ACCS로 데이터를 마이그레이션합니다.

   * 데이터 마이그레이션 도구를 사용하여 기본 Adobe Commerce 데이터를 마이그레이션합니다.
   * 타사 확장 및 사용자 지정 마이그레이션
   * 구성 및 통합 데이터 마이그레이션:
      * [Adobe Commerce 통합 시작 키트](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/)를 사용하여 API Mesh 구성, 타사 서비스 및 시스템 통합을 전송합니다.

### Go-Live 단계

샌드박스 환경을 사용하여 새 [!DNL Adobe Commerce as a Cloud Service] 인스턴스를 시작하기 전에 유효성을 검사하고 테스트하십시오.

* **기능 테스트**—마이그레이션된 데이터, 상점 기능 및 사용자 지정이 원활하게 작동하는지 확인하십시오.

* **성능 테스트**—저장소의 속도와 확장성을 평가하여 전 세계적으로 최적의 성능을 보장합니다.

* **보안 감사** - API 액세스 제어 및 잠재적인 취약점을 포함한 보안 조치를 검토하십시오.

새 [!DNL Adobe Commerce as a Cloud Service] 샌드박스 인스턴스의 유효성을 검사하고 테스트하면 프로덕션 인스턴스를 시작할 수 있습니다.

### Go-Live 후 단계

Go-Live 후 다음 실행 후 활동을 수행합니다.

1. 라이브 후속 작업

   * 트래픽을 새 플랫폼으로 리디렉션하고 성능을 모니터링합니다.
   * 이전 Adobe Commerce 인스턴스를 비활성화합니다.

1. 실행 후 모니터링

   * 모니터링 도구를 사용하여 안정적인 운영을 보장하고 출시 후 문제를 해결할 수 있습니다.
