---
title: ' [!DNL Adobe Commerce as a Cloud Service]에 대한 가시성'
description: 지표, 로깅 및 추적을 포함하여  [!DNL Adobe Commerce as a Cloud Service]에서 사용할 수 있는 관찰 도구 및 원격 분석 기능에 대해 알아봅니다.
feature: Cloud, Integration
role: Admin, Developer
level: Intermediate
badgeSaas: label="SaaS만" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."
source-git-commit: 3c10ecdea3d06295013c9c6e2d6869afd750a0b9
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 0%

---

# 가시성

가시성은 [!DNL Adobe Commerce as a Cloud Service] 작업의 중요한 요소입니다. 지표, 로깅 및 추적을 비롯한 원격 분석 데이터의 수집, 처리 및 시각화를 포괄하여 애플리케이션 상태를 모니터링하고 성능 문제를 진단하며 상거래 플랫폼 및 통합 시스템의 안정성을 최적화할 수 있습니다.

## [!DNL Adobe Commerce as a Cloud Service]

### 가시성 개요

가시성은 Adobe Commerce 상점 및 연결된 모든 App Builder 애플리케이션의 상태와 성능에 대한 가시성을 제공합니다. 상거래 에코시스템에서 원격 분석 데이터를 수집하여 다음 작업을 수행할 수 있습니다.

* API 응답 시간, 요청 및 오류율, 리소스 사용률과 같은 **지표를 추적하여 실시간 성능 및 스팟 트렌드를 모니터링합니다.**
* 신속한 문제 해결을 위해 애플리케이션, 인프라, CDN 및 통합의 로그를 **중앙 집중화**&#x200B;합니다.
* **추적 요청** 요청이 Commerce 및 연결된 앱을 통해 프런트 엔드에서 이동할 때 엔드투엔드 상태로 전환되어 고객에게 영향을 미치기 전에 병목 지점과 오류를 파악하는 데 도움이 됩니다.

이러한 기능을 함께 사용하면 문제를 신속하게 파악 및 해결하고, 성능을 최적화하고, 고객에게 안정적인 경험을 제공할 수 있습니다. [가시성 개요](https://developer.adobe.com/commerce/extensibility/observability/)에서는 [!DNL Adobe Commerce as a Cloud Service]이(가) OpenTelemetry를 사용하여 이벤트, 웹후크 및 App Builder 응용 프로그램 간에 이 원격 분석 컬렉션을 통합하는 방법을 설명합니다.

![Observability 아키텍처](./assets/observability.png){width="600" zoomable="yes"}

Adobe Commerce은 OpenTelemetry를 통해 다음과 같은 가시성 도구를 지원합니다.

* Elasticsearch
* 그라파나
* 재거
* New Relic
* 프로메테우스
* 스플렁크
* Zipkin

### 구독 구성

[OpenTelemetry 호환 끝점으로 로그, 지표 또는 추적을 라우팅하도록 [!UICONTROL Admin] 또는 REST API를 통해 관찰 구독 구성](https://developer.adobe.com/commerce/extensibility/observability/configuration/). 각 구독은 특정 구성 요소(웹후크, 이벤트 또는 [!UICONTROL Admin UI SDK])를 대상으로 합니다.

### Observability REST API

[Observability REST API](https://developer.adobe.com/commerce/extensibility/observability/api/)에서는 Observability 구독을 프로그래밍 방식으로 만들고, 검색하고, 업데이트하고, 삭제하는 끝점을 제공합니다. 이러한 엔드포인트를 사용하여 인스턴스 간 구성을 자동화합니다.

## Adobe Developer App Builder

### App Builder 계측

[Observability를  [!DNL App Builder]](https://developer.adobe.com/commerce/extensibility/observability/app-builder/)에서 구현하여 추적 컨텍스트를 Commerce의 [!DNL App Builder] 작업으로 전파하면 두 시스템의 로그와 추적이 observability platform에서 상호 연결됩니다. Webhook 기반 및 이벤트 기반 통합을 위한 계측을 다룹니다.

[!DNL App Builder]은(는) CLI 및 Developer Console 액세스를 포함하여 [응용 프로그램 로그 관리](https://developer.adobe.com/app-builder/docs/guides/app_builder_guides/application_logging/logging)를 위한 기본 제공 도구를 제공하며 Splunk, Azure 및 New Relic과 같은 외부 솔루션에 대한 로그 전달을 제공합니다.

### 원격 분석 라이브러리

[`@adobe/aio-lib-telemetry`](https://github.com/adobe/aio-lib-telemetry/blob/main/docs/usage.md) 라이브러리는 App Builder 작업에서 OpenTelemetry 호환 로그 및 추적을 내보내는 데 사용하는 라이브러리입니다. 설치, 구성 및 내보내기 설정을 다룹니다.

### 로컬 개발 및 테스트

배포하기 전에 로컬에서 [가시성 설정을 테스트하십시오](https://developer.adobe.com/commerce/extensibility/observability/local-development/). 시각화 및 터널 전달에 [!DNL Grafana]을(를) 사용하여(예: [!DNL Ngrok]) 개발 컴퓨터의 원격 Commerce 인스턴스에서 원격 원격 원격 분석을 받습니다.

## [!DNL API Mesh]

### API Mesh 로깅

[API Mesh 로깅](https://developer.adobe.com/graphql-mesh-gateway/mesh/advanced/logging/)을 통해 Ray ID를 사용하여 Mesh에서 흐르는 요청을 모니터링하고 디버그할 수 있습니다. 중앙 분석을 위해 로그를 일괄적으로 내보내거나 [!DNL New Relic] 같은 플랫폼에 전달합니다.

## 상점 첫 화면

### CDN 및 Real User Monitoring

CDN 원본을 통한 [프록시 RUM(Real User Monitoring)](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/content-delivery-network/#proxy-rum-through-the-origin-to-avoid-a-tls-handshake) 데이터 수집으로 추가 TLS 핸드셰이크를 제거하고 프런트 엔드 성능 측정을 개선합니다.

## 가시성 비디오

다음 비디오에서는 [!DNL Adobe Commerce as a Cloud Service]의 가시성 제공 기능에 대한 높은 수준의 개요를 제공합니다.

* [App Builder Observability 비디오](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/observability/overview){target="_blank"}
* [API Mesh 비디오](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/extensibility/api-mesh/getting-started-api-mesh){target="_blank"}
