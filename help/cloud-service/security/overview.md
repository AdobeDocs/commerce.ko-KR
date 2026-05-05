---
title: 보안 개요
description: Adobe Commerce as a Cloud Service의 보안 기능에 대해 알아봅니다.
role: Admin, Architect, Leader
badgeSaas: label="SaaS만" type="Positive" url="https://experienceleague.adobe.com/ko/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."
source-git-commit: 0343c4f3ecc182145a97e08eca2790bd1512aa27
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 0%

---


# 보안 개요

[!DNL Adobe Commerce as a Cloud Service]은(는) 보안을 핵심으로 하여 설계되었으며, 규모에 관계없이 모든 비즈니스에 엔터프라이즈급 보호, 운영 복원 기능 및 안심할 수 있는 최신 SaaS 기반 상거래 플랫폼을 제공합니다.

기존 PaaS 모델과 달리 SaaS 모델은 수동 패치, 인프라 유지 관리 및 업그레이드 주기 부담을 덜어줍니다. 보안은 Adobe 관리 인프라와 자동화된 배포 파이프라인에서 [!DNL Adobe IMS]을(를) 통한 ID 및 액세스 관리에 이르기까지 플랫폼의 모든 레이어에 임베드됩니다.

[!DNL Adobe Commerce as a Cloud Service]은(는) Adobe의 글로벌 보안 및 규정 준수 프레임워크를 활용하여 ISO 27001, SOC 2 및 GDPR과 같은 업계 표준에 맞게 조정되도록 합니다. 고객은 플랫폼 보안에 대한 Adobe의 역할과 데이터 및 액세스 관리에 대한 고객의 역할을 명확하게 설명하는 [공유 책임 모델](./shared-responsibility.md)을 활용할 수 있습니다.

[!DNL Adobe Commerce as a Cloud Service]은(는) 웹 응용 프로그램 방화벽(WAF), DDoS 완화, 보안 프로비저닝 및 지속적인 취약성 검사와 같은 내장된 보호 기능을 통해 보안을 손상시키지 않고 비즈니스를 빠르게 혁신할 수 있습니다.

이 문서에서는 [!DNL Adobe Commerce as a Cloud Service]의 보안 아키텍처, 운영 안전 장치 및 규정 준수 태세에 대해 간략하게 설명합니다. 이를 통해 고객은 정보에 입각한 결정을 내리고 디지털 상거래 작업을 자신 있게 확장할 수 있습니다.

## CDN(Content Delivery Network) 및 WAF(Web Application Firewall)

### Storefront CDN

판매자는 Adobe 관리 CDN을 배포하거나 Commerce 기반 상점을 보호하기 위해 자체 CDN 솔루션을 구매할 수 있습니다.

>[!IMPORTANT]
>
>고객이 Adobe 관리 CDN을 배포하기로 선택한 경우 CDN 규칙을 구성할 수 없습니다. 고객이 자신의 CDN을 가져와서 Storefrontes를 보호할 때 사용자 지정 캐싱 규칙 또는 WAF 규칙을 구성할 수 있습니다.

### [!DNL API Mesh for Adobe Developer App Builder] CDN

[!DNL API Mesh]의 CDN 계층은 TLS를 종료하고, GraphQL 게이트웨이를 작업자로 실행하고, 전역 에지 캐싱과 자동 DDoS/WAF을 제공하고, `edge‑graph.adobe.io`/`edge‑sandbox‑graph.adobe.io`을(를) 공용 메쉬 끝점으로 노출합니다. 고객은 앞에 고유한 CDN을 추가할 수 있지만, [!DNL API Mesh]의 CDN은 Adobe에서 수정 및 관리되며, 고객은 자신의 WAF 규칙을 구성할 수 없습니다.

[!DNL API Mesh]의 보안 기능에 대한 자세한 내용은 [API Mesh 설명서](https://developer.adobe.com/graphql-mesh-gateway/mesh/security/){target="_blank"}를 참조하세요.

### 백엔드 CDN

기본 제공 CDN은 [!DNL Adobe Commerce as a Cloud Service]을(를) 보호합니다.

[!DNL Adobe Commerce as a Cloud Service] 아키텍처로 인해 판매자가 `na1`, `eu1`, `au1` 또는 기타 지리적 지역과 같은 복합 셀에서 인스턴스를 프로비저닝하면 세 개의 공용 표면이 노출됩니다.

| 표면 | 예제 URL 패턴 |
| --- | --- |
| 관리자 UI | `https://<region>.admin.commerce.adobe.com/<tenant-id>/admin/` |
| 나머지 API | `https://<region>.api.commerce.adobe.com/<tenant-id>/<endpoint>` |
| GRAPHQL API | `https://na1.api.commerce.adobe.com/<tenant_id>/graphql/` |

[!DNL Adobe Commerce as a Cloud Service]이(가) 결합된 WAF 및 CDN을 사용합니다.

- **WAF** - 모든 [!DNL Adobe Commerce as a Cloud Service] 공용 표면에 대한 웹 응용 프로그램 방화벽 보호입니다.
- **CDN** - 정적 자산 및 캐시 가능한 GraphQL 응답에 대한 Edge 캐싱.

WAF 및 CDN은 [!DNL Adobe Commerce as a Cloud Service] 플랫폼에서 관리하며 고객이 구성할 수 없습니다.

### DOS 보호

내장된 CDN 및 WAF은 네트워크 계층과 HTTP 계층 DDoS 보호를 모두 제공합니다. [!DNL Adobe Commerce as a Cloud Service]은(는) 이러한 WAF 또는 DDoS 로그를 판매자에게 직접 노출하지 않습니다.

## 데이터 저장 및 암호화

데이터가 [!DNL App Builder]에 저장되는 경우 판매자는 [!DNL App Builder] [저장소 옵션](https://developer.adobe.com/app-builder/docs/guides/app_builder_guides/storage/)을(를) 참조할 수 있습니다. [!DNL App Builder]은(는) 테넌트 격리를 적용하며 이러한 서비스에 저장된 데이터에 대한 액세스는 작업을 실행하는 런타임 네임스페이스로 제한됩니다. 저장소에 데이터의 암호화가 없습니다.

[!DNL API Mesh]을(를) 사용하는 경우 암호는 메쉬 구성의 `secrets.yaml` 파일에 저장되어야 합니다. [!DNL API Mesh]은(는) AES-256 암호화([https://developer.adobe.com/graphql-mesh-gateway/mesh/advanced/secrets/](https://developer.adobe.com/graphql-mesh-gateway/mesh/advanced/secrets/))를 사용하여 이러한 암호를 암호화합니다.

[!DNL Adobe Commerce as a Cloud Service]에 저장된 모든 데이터는 AES 256비트 암호화를 사용하여 사용하지 않고 암호화되며, 모든 데이터는 전송 중인 TLS 1.2 이상을 사용하여 HTTPS를 통해 암호화됩니다.
