---
title: 카탈로그 이벤트 설정 및 통합 안내서
description: 카탈로그 데이터를 확인하고, Adobe Commerce에 대해  [!DNL Adobe I/O Events] 을(를) 구성하고, 카탈로그 이벤트 유형을 구독하고, 소비자에 대한 게재를 확인하는 방법을 알아봅니다.
level: Intermediate
recommendations: noCatalog
role: Admin, Developer
feature: Services, Catalog Service
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: c32adafa-ed01-4b31-997e-2413013911b0
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 818efacb8dbf63e48cdc83506d228c665d7a8b22
workflow-type: tm+mt
source-wordcount: 1568
ht-degree: 0%

---

# Adobe I/O을 사용하여 카탈로그 이벤트 활성화 및 구성

카탈로그 이벤트는 [!DNL Catalog Service]을(를) 통해 사용 가능한 지원되는 카탈로그 변경 내용을 설명하는 컴퓨터 생성 알림입니다. 이를 통해 다음과 같은 이벤트 기반 워크플로를 사용할 수 있습니다.

* 외부 캐시 또는 서비스를 카탈로그 업데이트와 동기화합니다.
* 제품, 변형, 가격 또는 범주가 변경될 때 다운스트림 프로세스를 트리거합니다.
* 거의 실시간 카탈로그 업데이트가 필요한 Experience Edge 및 [!DNL Edge Delivery Services] 사용 사례를 지원합니다.

[!DNL Adobe Commerce]에서 이벤트 소비자까지의 전체 경로를 보려면 [이벤트 전달 방법 [!DNL Adobe I/O Events]](#event-delivery-through-adobe-io-events)을 참조하세요.

## 지원되는 이벤트 유형 {#supported-event-types}

카탈로그 이벤트는 [!DNL Adobe Developer Console]을(를) 통해 노출된 상점 관련 변경 내용에 중점을 둡니다. 현재 지원되는 구독은 다음과 같습니다.

| 구독 | 이벤트 |
| --- | --- |
| 제품 업데이트 | [!DNL Catalog Service]을(를) 통해 사용 가능한 제품에 대한 제품 만들기, 업데이트 및 변경 내용 삭제 |
| 가격 업데이트 | Storefront 카탈로그 데이터에 영향을 주는 가격 만들기, 업데이트 및 삭제 변경 사항 |

각 이벤트에는 다음이 포함됩니다.

* 변경 유형을 설명하는 이벤트 식별자.
* 인스턴스 ID 및 SKU와 같은 엔티티 및 환경 컨텍스트.
* 변경된 엔티티 및 관련 범위 정보를 설명하는 페이로드입니다.


## 이벤트 페이로드 예

**ProductUpdated 이벤트**

```json
{
  "imsOrgId": "aaa-0",
  "instanceId": "instance-9",
  "eventCode": "productUpdated",
  "sku": "1234",
  "links": [
    {"type":  "variantOf", "sku": "5678"}
   ],
  "scope": [
    { "storeViewCode": "US-us" },
    { "storeViewCode": "FR-fr" },
    { "storeViewCode": "DE-de" }
  ]
}
```

**가격 업데이트 이벤트**

```json
{
  "imsOrgId": "aaa-0",
  "instanceId": "instance-9",
  "eventCode": "priceUpdated",
  "sku": "1234",
  "scope": [
    {
      "websiteCode": "website1",
      "customerGroupCode": "customer-group-code1"
    },
    {
      "websiteCode": "website2",
      "customerGroupCode": "customer-group-code2"
    }
  ]
}
```

## [!DNL Adobe I/O Events]을(를) 통한 이벤트 게재 {#event-delivery-through-adobe-io-events}

[!DNL Adobe I/O Events]이(가) 카탈로그 이벤트를 통합에 제공합니다. 다음 다이어그램은 [!DNL Adobe Commerce]부터 [!DNL Catalog Service] 및 [!DNL Adobe I/O Events]까지의 카탈로그 변경 내용을 구독된 소비자에 대한 높은 수준의 흐름을 보여 줍니다.

![Adobe Commerce에서 카탈로그 서비스 및 Adobe I/O Events을 통해 구독한 소비자로 이어지는 높은 수준의 카탈로그 이벤트 흐름](assets/catalog-service-event-pipeline.png)

다음 단계에서는 각 핸드오프를 자세히 설명합니다.

1. **Adobe Commerce → 카탈로그 서비스**

[!DNL Adobe Commerce]은(는) 지원되는 SaaS 데이터 내보내기 확장 기능을 사용하여 카탈로그 데이터를 [!DNL Catalog Service]에 내보냅니다.

1. **카탈로그 서비스 처리 중**

   * [!DNL Catalog Service]에서 지원되는 카탈로그 변경 내용을 처리하고 이벤트 배달을 준비합니다.

1. **카탈로그 서비스 → Adobe I/O Events**

* 카탈로그 이벤트가 [!DNL Adobe I/O Events]에 게시되었습니다.
* 소비자는 저널링, 웹후크, [!DNL Adobe I/O Runtime], Amazon EventBridge 또는 기타 지원되는 게재 메커니즘을 사용하여 구독합니다.

[!DNL Adobe I/O Events] 제공:

* 구독자당 *최소 한 번 배달*(중복 이벤트가 가능).
* 게재 전반에 걸쳐 주문 보장이 없습니다.

소비자는 중복 이벤트와 순서가 잘못된 배달을 처리해야 합니다. 구현 지침이 필요하면 [Idempotency](#idempotency)을(를) 참조하십시오.

## 사용 사례 {#use-cases}

여러 시나리오에서 카탈로그 이벤트를 사용할 수 있습니다.

### 정적 사이트 및 에지 전달

* 카탈로그 데이터가 변경될 때 카탈로그 페이지 및 상점 조각을 재생성하거나 무효화합니다.
* [!DNL Catalog Service]개의 API를 자주 폴링하지 않도록 합니다.

### 색인 지정 및 캐싱 검색

* 다운스트림 검색 인덱스에서 증분 업데이트를 트리거합니다.
* 제품 또는 카테고리 데이터가 변경될 때 카탈로그의 캐시 레이어 또는 외부 보기를 업데이트합니다.

### 외부 시스템과의 통합

* PIM, 가격 엔진 또는 기타 LOB 시스템과 같은 외부 시스템에 카탈로그 변경 사항을 전달합니다.
* 직접 데이터베이스 액세스 없이 다운스트림 애플리케이션 동기화 유지

### 모니터링 및 가시성

카탈로그 이벤트를 기존 모니터링과 결합(예: [!DNL Grafana] 및 [!DNL Prometheus]):

* 이벤트 처리량 모니터링
* 카탈로그 업데이트 볼륨에서 예외 항목을 탐지합니다.

## 카탈로그 이벤트 활성화 {#enable-catalog-events}

카탈로그 이벤트를 끝까지 활성화하려면 다음 단계를 따르십시오.

>[!PREREQUISITES]
>
>카탈로그 이벤트를 활성화하기 전에 다음을 확인하십시오.
>
>* [!DNL Catalog Service]이(가) 활성화된 지원되는 Adobe Commerce 환경입니다.
>* [Adobe Commerce에 대해  [!DNL Adobe I/O] 연결이 구성되었습니다](https://developer.adobe.com/commerce/extensibility/events/configure-commerce).
>* Commerce 환경이 프로비저닝된 동일한 IMS 조직의 [!DNL Adobe Developer Console]에 대한 액세스 권한.
>* Commerce SaaS 서비스와의 동기화를 확인하려면 관리자의 **[!UICONTROL Data Management Dashboard]**&#x200B;을(를) 사용하십시오.
>* 대시보드 확인에는 제품 권장 사항 v6.0, [!DNL Live Search] v4.1.0+ 또는 [!DNL Catalog Service] v1.17+가 필요합니다. Adobe에서는 Commerce 프로젝트를 이러한 서비스의 지원되는 최신 버전으로 업데이트할 것을 권장합니다. 이전 서비스 버전의 경우 동기화 확인에 [카탈로그 동기화](https://experienceleague.adobe.com/en/docs/commerce/user-guides/data-services/catalog-sync)를 사용하십시오.


>[!NOTE]
>
>카탈로그 이벤트를 사용하려면 먼저 [!DNL Adobe I/O Events]에 대한 Commerce 환경을 구성한 다음 [!DNL Adobe Developer Console]에서 이벤트 구독을 등록하십시오.
>
>구성 후 환경이 [!DNL Adobe Developer Console]에 나타나지 않으면 올바른 IMS 조직에 로그인했는지, 계정에 필요한 액세스 권한이 있는지 확인하십시오. 환경이 여전히 나타나지 않으면 Adobe 지원 센터에 문의하십시오.

### 카탈로그 데이터 확인 {#verify-catalog-data}

구성하기 전에 [!DNL Catalog Service]에 [!DNL Commerce] 인스턴스의 현재 카탈로그 데이터가 있는지 확인하십시오. 카탈로그 이벤트는 [!DNL SaaS Data Export]이(가) 두 단계를 완료하는 데 따라 다릅니다. **둘 다 확인**:

1. Commerce에서 **피드 내보내기 성공**&#x200B;을 확인합니다.

   [!DNL Adobe Commerce] 관리자로부터 [데이터 피드 동기화 상태](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status) 페이지(**[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Feed Sync Status]**)를 열고 각 [!DNL Catalog Service] 피드에 대해 마지막 내보내기 상태가 성공했는지 확인하십시오.

1. [!DNL Adobe Commerce] 관리자로부터 **연결된 Commerce 서비스에 동기화**&#x200B;했는지 확인하십시오.

   [!DNL Adobe Commerce] 관리자로부터 [데이터 관리 대시보드](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard)&#x200B;(**[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Management Dashboard]**)를 열고 동기화된 제품 데이터에 예상 제품이 포함되어 있는지 확인합니다.

### [!DNL Adobe I/O Events] 등록 및 구독 {#register-events}

구독할 Commerce 이벤트를 정의한 다음 프로젝트에 등록합니다.

인스턴스가 선택 목록에 없으면 [!DNL Adobe I/O]에 연결되지 않습니다. 문제를 해결하는 방법은 *Adobe Commerce 개발자* 설명서에서 [연결 구성](https://developer.adobe.com/commerce/extensibility/events/configure-commerce#configure-the-adobe-io-connection)을 참조하십시오. [!DNL Adobe I/O] 

1. [!DNL Adobe Developer Console]에서 Commerce 프로젝트에 사용되는 것과 동일한 IMS 조직에 로그인합니다.

1. Commerce 카탈로그 이벤트에 대한 프로젝트를 만들거나 이벤트 API를 기존 프로젝트에 추가합니다.

   * 위쪽 탐색에서 **[!UICONTROL APIs and services]**&#x200B;을(를) 선택합니다.

   * **[!UICONTROL Browse APIs and services]** 페이지에서 **[!UICONTROL Events]** 탭을 선택합니다.

   * Commerce 카탈로그 이벤트 API를 빠르게 찾습니다. 검색 상자에 _Catalog_&#x200B;을(를) 입력하거나 **[!UICONTROL Commerce]** 제품별로 필터링하십시오.

   * **[!UICONTROL Commerce Catalog Events]** 카드에서 **[!UICONTROL Project]**&#x200B;을(를) 선택합니다.

   ![API 및 서비스 찾아보기 페이지에서 선택한 Commerce 카탈로그 이벤트 공급자](assets/catalog-event-select-provider.png){width="600" zoomable="yes"}

1. 이벤트 등록을 구성합니다.

   이벤트 알림을 받을 Commerce 인스턴스를 선택합니다. **[!UICONTROL Next]**&#x200B;을(를) 선택합니다.

   이벤트 등록 화면에서 ![Commerce 인스턴스 선택됨](assets/catalog-event-registration.png){width="600" zoomable="yes"}

1. 가입할 이벤트를 선택합니다.

   **[!UICONTROL Product Update]** 또는 **[!UICONTROL Price Update]**&#x200B;과(와) 같이 받을 지원되는 이벤트 구독을 선택하십시오. **[!UICONTROL Next]**&#x200B;을(를) 선택합니다.

   ![등록 화면에서 구독하기 위해 선택한 이벤트 범주](assets/catalog-event-subscription.png){width="600" zoomable="yes"}

1. OAuth 서버 간 자격 증명을 추가합니다.

   **[!UICONTROL Credential name]** 입력. **[!UICONTROL Next]**&#x200B;을(를) 선택합니다.

1. **[!UICONTROL Event registration name]** 및 **[!UICONTROL Event registration description]**&#x200B;을(를) 입력하십시오. **[!UICONTROL Next]**&#x200B;을(를) 선택합니다.

1. 최종 등록 화면에서 기본 소비자인 저널링 API를 수락합니다.

   기본 저널링 API 소비자를 사용하면 이벤트 등록을 테스트하고 이벤트가 전달되었는지 확인할 수 있습니다. 이미 Webhook 또는 [!DNL Adobe I/O Runtime] 작업 소비자를 구성한 경우 여기에서 선택하십시오. 그렇지 않으면 나중에 소비자가 준비가 되면 이벤트 등록을 편집합니다.

   ![이벤트 등록 완료 화면에서 저널링 API 소비자 기본값이 선택됨](assets/catalog-event-consumer.png){width="600" zoomable="yes"}

1. **[!UICONTROL Complete registration]**&#x200B;을(를) 선택합니다.

### 이벤트 소비자 구성 {#configure-consumer}

1. 다음과 같이 고객을 구성합니다.

   * 웹후크 엔드포인트
   * [!DNL Adobe I/O Runtime] 작업
   * 다른 지원되는 대상

1. 등록 중에 소비자를 선택하지 않은 경우 이벤트 등록을 편집하여 소비자 세부 정보를 추가합니다.

   * [!DNL Adobe Developer Console]에서 프로젝트를 편집합니다. 그런 다음 만든 이벤트 등록을 선택합니다.

   * 이벤트 등록 세부 정보 페이지에서 **[!UICONTROL Edit Events Registration]**&#x200B;을(를) 선택합니다.

   * 소비자 선택 화면에 도달할 때까지 **[!UICONTROL Next]**&#x200B;을(를) 선택합니다. 그런 다음 구성한 소비자를 선택합니다.

   * 고객을 구성된 대상으로 업데이트합니다. **[!UICONTROL Save configured events]**&#x200B;을(를) 선택합니다.

### 이벤트 흐름 유효성 검사 {#validate-event-flow}

카탈로그 이벤트가 환경에 대해 활성화됩니다. 카탈로그 데이터가 [!DNL Commerce]에서 변경되면 업데이트가 [!DNL Catalog Service]에서 [!DNL Adobe I/O Events]&#x200B;(으)로 이동하고 구독한 소비자가 해당 카탈로그 이벤트를 받습니다. 프로덕션 통합을 빌드하기 전에 [제한 및 모범 사례](#limits-and-best-practices)를 검토하십시오.
1. 제품 이름 업데이트 또는 가격 변경과 같은 간단한 지원 카탈로그 변경을 수행합니다.

1. 다음 결과를 확인합니다.

   * 변경 내용은 [!DNL Catalog Service] API를 통해 표시됩니다.
   * [!DNL Adobe I/O Events] 소비자가 해당 제품 또는 가격 이벤트를 받습니다.


## 제한 사항 및 우수 사례 {#limits-and-best-practices}

카탈로그 이벤트를 기반으로 하는 경우 다음 모범 사례를 따르십시오.

### 멱화능 {#idempotency}

[!DNL Adobe I/O Events]은(는) 동일한 카탈로그 이벤트를 두 번 이상 게재할 수 있으며 단일 제품에 대한 이벤트가 잘못된 순서로 도착할 수 있습니다. 다음을 통해 소비자가 멱등 행렬이 되도록 디자인:

* 버전 또는 타임스탬프 필드에 엔티티 ID 사용.
* 동일한 변경에 대해 중복 알림은 안전하게 무시합니다.

### 처리량 및 배압

높은 업데이트 비율을 가진 큰 카탈로그는 상당한 이벤트 볼륨을 생성할 수 있습니다. 다음을 확인합니다.

* 소비자는 최대 처리량으로 이벤트를 처리할 수 있습니다.
* 필요한 경우 버퍼링, 일괄 처리 또는 큐를 사용합니다.

### 보안 및 격리

* [!DNL Adobe I/O Events]에서 *테넌트 격리*&#x200B;를 적용합니다.
* 조직은 자체 환경 및 자격에 대해서만 이벤트를 받습니다.

### 스키마 진화

카탈로그 이벤트 페이로드는 [!DNL Catalog Service] API와 동일한 개념 모델을 따릅니다. 전달 호환 상태를 유지하려면:

* 가능하면 스키마를 엄격하게 적용하지 마십시오.
* 실패하는 대신 알 수 없는 필드를 무시하십시오.

## 카탈로그 이벤트 문제 해결 {#troubleshoot-catalog-events}

카탈로그 이벤트가 누락되거나 지연된 경우, 다음 단계를 수행하십시오.

1. **카탈로그 서비스 데이터 확인**

   [카탈로그 변경 내용이 저장되었는지 확인하려면  [!DNL Catalog Service] API](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/)를 사용하십시오.

1. **확인[!DNL SaaS Data Export]**

   카탈로그 이벤트에는 [!DNL Catalog Service]의 현재 데이터가 필요합니다. 내보내기 경로의 두 단계 확인:

   * **Commerce에서 피드 내보내기** — [데이터 피드 동기화 상태](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status) 페이지 또는 `var/log/saas-export.log`에서 [!DNL Catalog Service]개의 피드를 [!DNL Commerce]에서 성공적으로 내보냈는지 확인합니다.

   * **연결된 Commerce SaaS 서비스에 동기화** — [데이터 관리 대시보드](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard), [카탈로그 동기화](https://experienceleague.adobe.com/en/docs/commerce/user-guides/data-services/catalog-sync) 또는 내보내기 로그에서 데이터가 [!DNL Catalog Service]에 성공적으로 동기화되었는지 확인합니다.

   내보내기 및 동기화 작업 문제를 해결하려면 [데이터를 SaaS 데이터 내보내기와 동기화](../data-export/data-sync-manage.md) 및 [로깅 및 문제 해결](../data-export/troubleshooting/logging.md)을 참조하십시오.

1. **[!DNL Adobe I/O Events] 구성 유효성 검사**

   다음을 확인합니다.

   * [!DNL Adobe Developer Console]에서 올바른 IMS 조직에 로그인했습니다.
   * **[!UICONTROL Commerce Catalog Events]** 공급자를 사용하도록 설정했습니다.
   * 필요한 **[!UICONTROL Commerce Catalog Events]** 공급자 및 환경이 표시됩니다.
   * 구독이 활성화되었습니다.
   * 엔드포인트, 작업 또는 저널 소비자는 테스트 이벤트를 수신하고 처리할 수 있습니다.

1. **Adobe 지원에 문의**

   지원 티켓을 열 때 **Adobe Commerce 애플리케이션**&#x200B;에 해당하는 문제 원인을 선택하고 다음 정보를 포함하십시오.

   * 카탈로그 서비스 세부 정보(환경, 지역).
   * [!DNL Adobe I/O Events] 구독 세부 정보.
   * 누락된 이벤트의 대략적인 시간 및 설명.

   추가 도움말은 [지원 티켓](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#support-case)을 참조하세요.

>[!MORELIKETHIS]
>
>
>* [온보딩 및 설치](installation.md)
>* [카탈로그 서비스 시작](get-started.md)
>* [데이터를 SaaS 데이터 내보내기와 동기화](../data-export/data-sync-manage.md)
>* [GraphQL API로 카탈로그 데이터 검색](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/){target="_blank"}
>* [[!DNL Catalog Service] 및 API Mesh](mesh.md)
>* [연결 구성 [!DNL Adobe I/O] 2&rbrace;](https://developer.adobe.com/commerce/extensibility/events/configure-commerce#configure-the-adobe-io-connection){target="_blank"}
>* [[!DNL Adobe I/O Events]](https://developer.adobe.com/events/docs/guides/){target="_blank"}
