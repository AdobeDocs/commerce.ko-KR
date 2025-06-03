---
title: '[!DNL Adobe Commerce as a Cloud Service] 개요'
description: ' [!DNL Adobe Commerce as a Cloud Service]의 주요 기능 및 이점에 대해 알아봅니다.'
feature: App Builder, GraphQL, Integration, Saas
role: Admin, Architect, Developer, User
exl-id: 1b7e2731-4a10-4c2b-9bfc-8945729ed523
badgeSaas: label="SaaS만" type="Positive" url="https://experienceleague.adobe.com/ko/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."
source-git-commit: 7102feff1364b3b5715b4acd7f4cf013fa783eae
workflow-type: tm+mt
source-wordcount: '1165'
ht-degree: 0%

---

# [!DNL Adobe Commerce as a Cloud Service] 개요

{{accs-early-access}}

[!DNL Adobe Commerce as a Cloud Service]은(는) 기업이 디지털 운영을 제공하고 빠르게 확장하고 혁신을 가속화할 수 있도록 함으로써 유연성, 확장성 및 효율성을 제공합니다. Adobe의 클라우드 기반 인프라는 트래픽, 주문 및 카탈로그 관리에 대한 최대 수요를 충족하도록 리소스를 자동으로 조정합니다.

다음 그래픽에서는 [!DNL Adobe Commerce as a Cloud Service]을(를) 지원하는 제품을 강조합니다.

![[!DNL Adobe Commerce as a Cloud Service] 제품 스택](./assets/product-stack.svg){align="center" zoomable="yes"}

>[!BEGINSHADEBOX]

![정보](assets/Smock_InfoOutline_18_N.svg) [!DNL Adobe Commerce as a Cloud Service] 조기 액세스 프로그램에 참여하려면 [이 양식을 작성](https://forms.office.com/pages/responsepage.aspx?id=Wht7-jR7h0OUrtLBeN7O4WOxhjY2doZPikS2hIbfmL5URFZXTE5TUk9PMUw0OFdOWTBNNlI3UTlNMS4u&amp;route=shorturl)하세요.

>[!ENDSHADEBOX]

## 아키텍처

[!DNL Adobe Commerce as a Cloud Service] 아키텍처에 대한 간략한 소개는 다음 비디오를 참조하십시오. 아키텍처를 설명하는 다이어그램은 비디오 아래에 제공됩니다.

>[!VIDEO](https://video.tv.adobe.com/v/3443274?learn=on&captions=kor)

이 다이어그램은 [!DNL Adobe Commerce as a Cloud Service]과(와) 모든 Adobe Experience Cloud 솔루션 간의 데이터 흐름을 보여 줍니다.

![[!DNL Adobe Commerce as a Cloud Service] 아키텍처 다이어그램](./assets/data-flow.svg){zoomable="yes"}

## Commerce 상점 첫 화면

Edge Delivery Services에서 제공하는 Adobe의 [Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront?lang=ko)을(를) 사용하여 Storefront Builder를 통해 간단한 문서 기반 작성 또는 시각적 편집으로 몇 분 안에 풍부한 경험을 만들 수 있습니다.

Commerce Storefront는 GraphQL API 계층을 통해 모든 머천다이징 서비스 및 데이터를 제공하는 분리된 아키텍처를 통해 전체 헤드리스를 제공합니다. 이 아키텍처를 통해 팀은 Commerce Foundation과 독립적으로 전면을 개발할 수 있으므로 새로운 기술을 통해 새로운 접점을 구축하고 테스트할 수 있는 민첩성을 제공합니다.

>[!NOTE]
>
>[!DNL Adobe Commerce as a Cloud Service]은(는) Luma 상점 전면을 지원하지 않습니다. Adobe Commerce on Cloud 또는 온프레미스에서 마이그레이션하는 경우 전환에 대한 지침은 [기존 상점](https://experienceleague.adobe.com/developer/commerce/storefront/discovery/?lang=ko#existing-storefronts)을 참조하세요.

## 머천다이징 서비스 및 결제 서비스

Adobe은 주요 비즈니스 목표를 지원하는 데 도움이 되는 지능적이고 구성 가능한 머천다이징 서비스 세트를 제공합니다. 또한 이러한 서비스는 규모에 맞게 성능을 최적화하는 데 중요한 API를 제공합니다.

- [실시간 검색](../live-search/overview.md) - 이 AI 기반 검색 도구를 사용하여 쇼핑객에게 보다 스마트하고 빠르며 적절한 결과를 제공합니다.
- [제품 권장 사항](../product-recommendations/overview.md) - 쇼핑객 행동, 인기 트렌드, 제품 유사성 등을 기반으로 AI 기반 권장 사항을 추가합니다.
- [채널 및 정책을 기반으로 하는 머천다이징 서비스](../optimizer/catalog/overview.md)—유연한 데이터 모델링을 통해 크고 복잡한 제품 카탈로그를 관리하여 비즈니스 구조 및 시장 진출 전략에 맞는 뛰어난 성능과 유연한 상거래 카탈로그를 제공합니다. 카탈로그 성능을 최적화하고 전환율을 향상시키려면 [Commerce Optimizer](../optimizer/overview.md)과(와) 함께 사용하십시오.
- [결제 서비스](../payment-services/guide-overview.md)—무이자 결제 할부, 결제 처리, 주문 및 청구서에 대한 단일 보기를 포함한 다양한 결제 방법을 제공하여 고객 만족도를 높입니다.

## 제품 시각화

리치 미디어 콘텐츠를 관리하기 위해 Adobe Experience Manager과 통합된 강력한 DAM(디지털 에셋 관리) 시스템을 사용하여 에셋 관리를 간소화합니다. 또는 [!DNL Adobe Commerce as a Cloud Service] 내의 기본 기능은 디지털 에셋을 저장하고 관리하기 위한 기본 에셋 관리 도구를 제공합니다.

자세한 내용은 [자산 관리](https://experienceleague.adobe.com/ko/docs/commerce-admin/content-design/aem-asset-management/aem-assets-integration)를 참조하세요.

## 개발자 플랫폼

Adobe은 개발자에게 Commerce Foundation 기능을 확장하고 타사 시스템(예: CRM, ERPS 및 PIMS)과 통합하는 애플리케이션을 빌드하는 포괄적인 확장 지점 및 도구를 제공합니다. 이러한 도구를 사용하면 다음과 같은 방법으로 플랫폼의 TCO를 절감할 수 있습니다.

- **확장성**—핵심 소프트웨어와 별도로 응용 프로그램을 확장할 수 있으므로 효율성이 향상되고 업그레이드가 간단해집니다.
- **격리**-격리된 환경은 개발자가 코어 릴리스에 의존하지 않고 임의로 확장을 업그레이드하거나 수정할 수 있음을 의미합니다.
- **기술 독립성**-개발자는 필요에 맞는 기술 스택과 코딩 언어를 선택할 수 있습니다.

>[!TIP]
>
>공급업체가 만든 앱도 [Adobe Exchange](https://exchange.adobe.com/)에 설치할 수 있습니다.

Adobe은 통합 및 사용자 지정을 빌드하기 위한 다음 개발자 도구를 제공합니다.

- [**Adobe Developer App Builder용 API Mesh**](https://developer.adobe.com/graphql-mesh-gateway/) - 여러 API, GraphQL, REST 및 기타 소스를 하나의 쿼리 가능한 GraphQL 엔드포인트로 조정하고 결합합니다.
- [**App Builder**](https://developer.adobe.com/app-builder/docs/overview/) - Commerce 기능을 확장하고 서드파티 솔루션과 통합하는 안전하고 확장 가능한 웹 애플리케이션을 빌드하고 배포합니다.
- [**이벤트**](https://developer.adobe.com/commerce/extensibility/events/)—사용자 지정 이벤트 트리거를 사용하여 다른 확장 가능한 개발 도구와 상호 작용합니다.
- [**Webhooks**](https://developer.adobe.com/commerce/extensibility/webhooks/) - 웹후크를 사용하여 Commerce과 서드파티 시스템 간의 상호 작용을 자동으로 트리거합니다.
- [**관리자 UI SDK**](https://developer.adobe.com/commerce/extensibility/admin-ui-sdk/)—판매자를 위한 새 페이지 및 기능을 사용하여 Commerce 관리자를 사용자 지정하고 개선합니다.
- [**통합 시작 키트**](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/) - 참조 통합, 온보딩 스크립트 및 표준화된 아키텍처를 통해 백오피스 통합을 가속화합니다.

## Commerce 재단

Commerce Foundation은 클라우드 기반 환경에서 Commerce 애플리케이션을 관리하기 위한 안전한 자동 호스팅 플랫폼과 셀프서비스 기능을 제공합니다.

주요 기능은 다음과 같습니다.

- 간소화된 온보딩
- 원활한 업그레이드
- 타사 통합

### 간소화된 온보딩

[!UICONTROL Commerce Cloud Manager] 셀프 서비스 프로비저닝 포털을 사용하여 몇 분 안에 샌드박스 및 프로덕션 인스턴스를 시작합니다. 머천다이징 서비스, Headless Commerce 인스턴스 및 App Builder을 포함하여 필요한 모든 것이 자동으로 구성되고 인스턴스와 통합됩니다.

Commerce 인스턴스를 만들고 관리하는 방법은 [시작하기](getting-started.md)를 참조하세요.

### 원활한 업그레이드

수동 업그레이드 없이도 최신 기능 및 향상된 기능을 이용할 수 있습니다. 새로운 기능과 업데이트를 지속적으로 제공하므로 수동으로 패치할 필요가 없어 TCO가 낮은 최신 기능을 항상 액세스할 수 있습니다.

Adobe Commerce on Cloud의 일반적인 업그레이드 프로세스에는 백업 생성, 인스턴스 복제, 호환성 도구 실행 및 코드 충돌 수정이 포함되었습니다. [!DNL Adobe Commerce as a Cloud Service]에서는 더 이상 필요하지 않습니다. Adobe은 새로운 기능 및 보안 업데이트가 릴리스되면 인앱 알림을 보냅니다. 업데이트가 프로덕션 환경에 자동으로 적용되기 전에 30일 동안 샌드박스 인스턴스의 새 기능을 평가할 수 있습니다.

>[!NOTE]
>
>Adobe은 모든 업데이트에 대해 이전 버전과의 호환성을 보장합니다. 즉, 업데이트를 적용하면 [API 우선 확장성](https://developer.adobe.com/commerce/extensibility/) 모델을 준수하는 기존 기능이나 사용자 지정을 중단하지 않습니다.

### 타사 통합

개발자는 포괄적인 [GraphQL 및 REST API](https://developer.adobe.com/commerce/services/cloud/guides/)를 사용하여 Commerce Foundation을 타사 시스템과 통합하고 Commerce 기능을 확장할 수 있습니다.

<!-- ## Experience Cloud integration

[!DNL Adobe Commerce as a Cloud Service] integrates with all Experience Cloud solutions to deliver [personalized commerce experiences at scale](https://experienceleague.adobe.com/ko/docs/commerce-admin/customers/customers-menu/personalize-scale#customers-menu).

[Data Connection](../data-connection/overview.md) unlocks insights about your shoppers' buying behavior so that you can create personalized shopping experiences across all channels with other Adobe Digital Experience products. -->

## 이점

다음 단원에서는 [!DNL Adobe Commerce as a Cloud Service]이(가) 비즈니스 및 IT 리더에게 제공하는 이점에 대한 정보를 제공합니다.

### 비즈니스 리더

- **매출 성장**: SEO를 향상시키는 고성능 매장을 통해 유기 트래픽을 유도합니다. 풍부한 데이터를 사용하여 전환을 유도하는 개인화된 경험을 만듭니다.
- **확장 작업**: 자동 확장 서비스는 99.9%의 가용성으로 비즈니스의 최대 요구 사항을 충족합니다. 여러 브랜드 및 지역을 롤아웃하고 단일 인스턴스에서 B2B 및 B2C를 지원합니다. 유연한 데이터 모델링을 통해 크고 복잡한 제품 카탈로그를 지원합니다.
- **머천다이저 생산성 향상**: AI 기반 머천다이징 서비스를 사용하여 전환을 개선하십시오. 기본적으로 상점 앞에서 직접 실험하십시오. 간단한 문서 기반 작성 또는 시각적 편집기를 사용하여 몇 분 안에 풍부한 경험을 만들 수 있도록 상점 경험을 관리합니다.
- **총소유비용(TCO)을 절감하고 혁신을 가속화합니다**: 항상 최신 서비스를 통해 새로운 기능에 즉시 액세스할 수 있습니다. 마켓플레이스에서 앱을 쉽게 설치하여 새로운 기능을 활성화합니다. 지루한 유지 관리에서 리소스를 확보하여 새로운 기능 구축에 주력할 수 있습니다.

### IT(정보 기술) 선두 기업

- **빠른 프로비저닝**: 셀프 서비스 프로비저닝을 빠르게 시작할 수 있습니다(분). 모든 서비스는 함께 원활하게 작동하여 더 빠르게 시작할 수 있도록 사전 구성되어 있습니다. 필요에 따라 개발자 실험을 위한 샌드박스를 프로비저닝합니다.
- **낮은 소유 비용**: 항상 최신 서비스를 제공하는 업그레이드되지 않습니다. 자동으로 적용되는 최신 보안 패치를 준수하고 보안을 유지하십시오. 가장 까다로운 워크로드에 맞게 자동으로 확장 가능
- **고성능 상점**: 간단한 문서 기반 작성 또는 시각적 편집기를 사용하여 몇 분 안에 풍부한 경험을 만들 수 있습니다. AI 기반 머천다이징 서비스를 사용하여 전환을 개선하십시오. 상점가에 내장된 네이티브 실험.
- **더 빠른 혁신**: 지루한 유지 관리에서 리소스를 확보하여 비즈니스 가치를 제공하는 새로운 기능 구축에 주력할 수 있습니다. 포괄적인 확장성 및 표준 기반 기술(JavaScript, HTML, CSS 및 로우 코드 도구)을 사용하여 차별화된 경험을 구축할 수 있습니다. 클릭 한 번으로 타사 앱을 설치하여 상거래 플랫폼에 새 기능을 추가합니다.
