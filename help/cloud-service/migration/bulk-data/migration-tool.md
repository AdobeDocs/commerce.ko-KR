---
title: 대량 데이터 마이그레이션 도구
description: 대량 데이터 마이그레이션 도구를 사용하여 기존 Adobe Commerce on Cloud 인스턴스에서  [!DNL Adobe Commerce as a Cloud Service](으)로 데이터를 마이그레이션하는 방법에 대해 알아봅니다.
feature: Cloud
badgeSaas: label="SaaS만" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."
role: Developer
level: Intermediate
exl-id: 81522de9-df54-4651-b8ed-58956376af86
autotag-review: '2026-07-22T19:18:39.433Z'
TQID: 'https://experienceleague.adobe.com/tkCFabZpBKu-W34wsufHlVIWzCUE8FKm4kK7qZahxBU'
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
subfeature_v2: id: f8ddfd3b-6194-46e8-a176-0e918039be56
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 4c0eca0039bab7d015144dd9ac3885a0b2be0563
workflow-type: tm+mt
source-wordcount: 924
ht-degree: 0%

---

# 대량 데이터 마이그레이션 도구

>[!IMPORTANT]
>
>대량 데이터 마이그레이션 도구는 현재 조기 액세스 상태에 있습니다. 액세스는 CDE(Commerce Deployed Engineering) 참여 프로세스를 통해서만 제공됩니다.

일괄 데이터 마이그레이션 도구를 사용하면 시스템 통합자는 자사 핵심 상거래 데이터를 [!DNL Adobe Commerce on Cloud] 또는 온-프레미스 설치에서 [!DNL Adobe Commerce as a Cloud Service]&#x200B;(으)로 마이그레이션할 수 있습니다.

벌크 데이터 마이그레이션 툴은 시스템 통합자가 자체 마이그레이션 시스템에서 실행하는 Docker 기반 CLI입니다. 소스 인스턴스에 연결하고 자사 핵심 상거래 데이터를 추출하여 Adobe의 마이그레이션 서비스(Commerce 데이터 마이그레이션 서비스)에 업로드하고 완료까지 진행 상황을 모니터링합니다.

모든 명령은 로컬로 실행되므로 마이그레이션이 시작되는 시기, 유지 관리 모드가 적용되는 시기 및 각 단계가 실행되는 시기를 제어할 수 있습니다.

## 마이그레이션 워크플로

이 도구는 다음 단계를 처음부터 끝까지 관리합니다.

- **데이터 추출** — 원본 인스턴스([!DNL Adobe Commerce on Cloud] 또는 온-프레미스)에서 자사 핵심 상거래 데이터를 추출합니다.
- **데이터 로드** — 추출한 데이터를 대상 [!DNL Adobe Commerce as a Cloud Service] 인스턴스로 로드합니다.
- **데이터 무결성 확인** - REST 및 GraphQL API 비교, 레코드 수 유효성 검사를 포함하여 마이그레이션 후 자동 검사를 수행합니다.

>[!NOTE]
>
>현재, 벌크 데이터 마이그레이션 도구는 자사 핵심 상거래 데이터 마이그레이션만 지원합니다. 사용자 지정 데이터 마이그레이션은 현재 지원되지 않습니다. 구성 설정(저장소 설정, 시스템 구성)은 자동으로 마이그레이션되지 않으며 마이그레이션 전에 대상 인스턴스에 독립적으로 설정해야 합니다.

## 아키텍처

벌크 데이터 마이그레이션 도구는 안전하고 효율적인 데이터 마이그레이션을 가능하게 하는 분산 아키텍처를 따릅니다. 이 도구를 사용하면 시스템 통합자가 기존 [!DNL Adobe Commerce on Cloud or on-premises instance]에서 [!DNL Adobe Commerce as a Cloud Service]&#x200B;(으)로 데이터를 마이그레이션할 수 있습니다. 마이그레이션 프로세스에 대한 자세한 내용은 [마이그레이션 개요](../overview.md)를 참조하십시오.

다음 이미지는 대량 데이터 마이그레이션 도구를 사용한 아키텍처 및 전체적인 데이터 흐름에 대해 자세히 설명합니다.

![PaaS에서 SaaS로의 데이터 흐름을 보여 주는 대량 데이터 마이그레이션 도구 아키텍처 다이어그램](../../assets/bulk-data-diagram.png){zoomable="yes"}

### 구성 요소

| 구성 요소 | 역할 |
| --------- | ---- |
| **대량 데이터 마이그레이션 도구** | 시스템 통합자가 마이그레이션 시스템에서 실행하는 Docker 기반 CLI로, 소스에서 스키마 및 데이터를 읽고, 추출된 데이터를 Adobe의 마이그레이션 서비스에 업로드하고, 상태 전환을 유도하여 전체 파이프라인을 조정합니다. |
| **Source 인스턴스(Commerce on Cloud 또는 온-프레미스)** | 마이그레이션 소스. 이 도구는 REST 및 GraphQL API와 SSH 터널([!DNL Adobe Commerce on Cloud]) 또는 데이터 추출을 위한 직접 데이터베이스 연결(온-프레미스)을 통해 연결합니다. |
| **CDMS(Commerce 데이터 마이그레이션 서비스) API** | 마이그레이션을 등록하고 상태 전환을 조정하며 추출된 데이터를 업로드할 수 있는 보안 끝점을 제공하는 Adobe 관리 REST API입니다. 마이그레이션 도구는 `.env` 구성에서 CDMS 끝점 URL 및 IMS 자격 증명을 사용하여 이 API에 연결합니다. |
| **CDMS(Commerce 데이터 마이그레이션 서비스) 작업자** | 추출된 데이터를 대상 인스턴스에 로드하고 로드 후 무결성 확인을 실행하는 Adobe 관리 백그라운드 서비스 |
| **[!DNL Adobe Commerce as a Cloud Service]** | SaaS 기반 버전의 Adobe Commerce 및 마이그레이션 타겟입니다. 로드된 데이터를 수신하고 무결성 확인 중에 사용된 카탈로그, 라이브 검색 및 가격 규칙 서비스를 표시합니다. |

### 데이터 흐름

데이터는 다음 순서로 구성 요소를 통해 이동합니다.

1. 대량 데이터 마이그레이션 도구는 [!DNL Adobe Commerce on Cloud]에 대한 SSH 터널 또는 온-프레미스에 대한 직접 데이터베이스 연결을 통해 원본 인스턴스에서 데이터베이스 스키마와 데이터를 읽습니다.
1. 이 도구는 마이그레이션을 등록하고 CDMS API를 통해 추출된 데이터를 업로드합니다.
1. CDMS 작업자가 데이터를 대상 [!DNL Adobe Commerce as a Cloud Service] 테넌트에 로드합니다.
1. [!DNL Adobe Commerce as a Cloud Service]은(는) 로드된 카탈로그 데이터를 수집하고 카탈로그 색인을 빌드합니다.
1. Commerce 데이터 마이그레이션 서비스(CDMS) 작업자는 다음 서비스에서 데이터베이스 체크섬 비교, REST 및 GraphQL을 통해 로드된 데이터를 확인합니다.

   - **카탈로그**(GraphQL) - 제품 및 범주 데이터.
   - **실시간 검색**(REST) — 검색 색인 수정.
   - **가격 규칙**(REST) - 가격 및 규칙 데이터.

1. 이 도구는 전체에서 마이그레이션 상태를 폴링하고 완료에 대한 최종 마이그레이션 보고서를 검색합니다.


## 참여 라이프사이클

벌크 데이터 마이그레이션 도구에 대한 액세스는 Commerce CDE(Deployed Engineering) 참여를 통해서만 제공됩니다. 이 도구는 공개적으로 액세스할 수 없습니다.

일반적인 참여 라이프사이클은 다음과 같습니다.

1. **CDE 검색** - 초기 범위 지정 호출을 완료하고, 데이터 풋프린트와 복잡성을 평가하고, 범위 지정 설문 조사를 완료합니다.
1. **거래 서명** - 상업적 계약이 적용되었으며 마이그레이션 범위가 확인되었습니다. 이 단계에서는 마이그레이션 도구에 대한 액세스 권한이 부여됩니다.
1. **CDE 공동 혁신 및 지원** - Adobe과 함께 환경에 도구를 설치하고 테스트 마이그레이션을 실행하십시오.
1. **실행** - 프로덕션 전환 마이그레이션을 실행하고 데이터 무결성 확인을 완료합니다.

## 도구 배포

이 도구는 CDE 참여의 일부로 배포됩니다. Adobe 담당자는 다음을 포함하는 도구 패키지를 제공합니다.

- Docker 기반 CLI 및 빌드 구성
- 모든 필수 환경 변수에 대한 설명서가 포함된 `.example.env` 구성 템플릿
- 도구의 아키텍처, 구성 참조, 사용자 정의 변환 및 테스트 프레임워크, 문제 해결 안내서에 대한 포괄적인 기술 문서

자세한 설정 및 운영 지침은 도구 배포 패키지에 포함된 설명서를 참조하십시오.

## 마이그레이션 안내서

다음 페이지에서는 준비에서 실행에 이르기까지 전체 마이그레이션 라이프사이클을 보여줍니다. 마이그레이션 프로세스를 완전히 이해하려면 다음 순서로 검토하십시오.

1. [고객 준비 검사 목록](readiness-checklist.md) - 도구 액세스를 요청하기 전에 참여, 마이그레이션 컴퓨터, 원본 및 대상 사전 요구 사항을 확인하십시오.
1. [마이그레이션 서비스 액세스 확인](cdms-access.md) — 도구에 대한 액세스 권한을 받은 후 Commerce CDMS(데이터 마이그레이션 서비스) API에 대해 네트워크 연결, IMS 인증 및 테넌트 권한 부여를 확인합니다.
1. [대량 데이터 마이그레이션 실행](migration-guide.md) — 도구를 구성하고 네트워크와 인스턴스를 준비하고 마이그레이션을 시작합니다.

전체 구성 참조, 사용자 정의 변환 및 테스트 프레임워크, 문제 해결 지침은 도구 배포 패키지에 포함된 설명서를 참조하십시오.
