---
title: 대량 데이터 마이그레이션 도구
description: Bulk Data Migration Tool을 사용하여 Cloud 인스턴스의 기존 Adobe Commerce에서  [!DNL Adobe Commerce as a Cloud Service](으)로 데이터를 마이그레이션하는 방법에 대해 알아봅니다.
feature: Cloud
badgeSaas: label="SaaS만" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."
role: Developer
level: Intermediate
exl-id: 81522de9-df54-4651-b8ed-58956376af86
source-git-commit: 06bdcfbff5d376064b18bdab3945e7609075b8bc
workflow-type: tm+mt
source-wordcount: '706'
ht-degree: 0%

---

# 대량 데이터 마이그레이션 도구

벌크 데이터 마이그레이션 도구는 PaaS에서 SaaS 환경으로 안전하고 효율적으로 데이터를 마이그레이션할 수 있는 분산 아키텍처를 따릅니다. 이 도구는 솔루션 구현자가 기존 PaaS(Adobe Commerce on Cloud Instance)에서 SaaS([!DNL Adobe Commerce as a Cloud Service])로 데이터를 마이그레이션하도록 도와줍니다. 마이그레이션 프로세스에 대한 자세한 내용은 [마이그레이션 개요](./overview.md)를 참조하십시오.

>[!NOTE]
>
>벌크 데이터 마이그레이션 도구는 자사 핵심 상거래 데이터 마이그레이션만 지원합니다. 사용자 지정 데이터 마이그레이션은 현재 지원되지 않습니다.

다음 이미지는 대량 데이터 마이그레이션 도구를 사용하기 위한 아키텍처 및 주요 구성 요소에 대해 자세히 설명합니다.

![PaaS에서 SaaS로의 데이터 흐름을 보여주는 대량 데이터 마이그레이션 도구 아키텍처 다이어그램](../assets/bulk-data-diagram.png){zoomable="yes"}

## 마이그레이션 워크플로

벌크 데이터 마이그레이션 워크플로우는 다음 단계로 구성됩니다.

1. 마이그레이션을 위한 새 환경을 설정하십시오.
1. 이전 시스템에서 데이터를 복사합니다.
1. 데이터를 새 시스템으로 이동합니다.
1. 새 시스템에서 제품 카탈로그를 사용할 수 있도록 합니다.
1. 데이터가 올바르게 마이그레이션되었는지 확인합니다.

다음 섹션에서는 이러한 단계에 대해 자세히 설명합니다.

## 대량 데이터 마이그레이션 도구 액세스

대량 데이터 마이그레이션 도구의 가용성은 다음과 같습니다.

- **2025년 4분기**(아직 사용 불가) - 대량 데이터 마이그레이션 도구의 초기 릴리스 이후 지원 티켓을 제출하여 액세스할 수 있습니다.
- **2025년 4분기**(아직 사용 불가) - 대량 데이터 마이그레이션 도구가 공개 릴리스된 후 이 페이지에서 액세스할 수 있습니다.

## 대상 환경 만들기

솔루션 구현자(SI)는 마이그레이션을 위한 대상 환경을 만듭니다. 이 환경은 소스 인스턴스에서 마이그레이션된 데이터를 저장합니다.

먼저 [새  [!DNL Adobe Commerce as a Cloud Service] (SaaS) 인스턴스를 만듭니다](../getting-started.md#create-an-instance).

### 추출 도구 구성

추출 도구를 사용하여 소스 인스턴스에서 데이터를 추출합니다.

1. Adobe에서 제공한 링크에서 추출 도구를 다운로드합니다.
1. 추출 도구에서 다음 환경 변수를 설정합니다.
   - 기존 MySQL 데이터베이스에 대한 연결 세부 정보
   - [!DNL Adobe Commerce as a Cloud Service] 인스턴스에 대한 대상 테넌트 ID
   - 다음을 포함한 IMS 자격 증명:
      - 클라이언트 ID
      - 클라이언트 암호
      - IMS 범위
      - IMS URL - 기본 URL. 예: `https://ims-na1.adobelogin.com/`.
      - IMS 조직 ID

   IMS 범위 및 기타 값의 경우 **Adobe Developer Console**&#x200B;의 프로젝트 내에 있는 [자격 증명](https://developer.adobe.com/console/) 섹션에서 OAuth 유형을 선택하십시오. 추출 도구에 포함된 `.example.env` 파일에 자세한 정보가 제공됩니다.

### 데이터 추출

추출 도구를 실행하기 전에 솔루션 구현자는 다음을 사용하여 PaaS 데이터베이스에 대한 SSH 터널을 설정해야 합니다.

```bash
magento-cloud tunnel:open
```

그런 다음 추출 도구를 실행하고

1. PaaS 데이터베이스에 연결하고, 스키마를 분석하고, SaaS 테넌트 스키마 세부 사항과 비교합니다.
1. PaaS와 SaaS 간의 공통 스키마 요소를 기반으로 추출 및 변환 계획을 생성합니다.
1. CDMS(카탈로그 데이터 관리 서비스)를 사용하여 데이터를 추출합니다.

### 데이터 로드

Adobe에서 제공한 데이터 로드 도구를 실행합니다. 이 도구는 다음과 같은 작업을 수행합니다.

1. 마이그레이션 계정을 사용하여 SaaS 테넌트 데이터베이스에 연결합니다.
1. 로드 계획을 생성합니다.
1. 계획을 실행하여 데이터를 SaaS 테넌트 데이터베이스로 일괄적으로 이동합니다.
1. 카탈로그 미디어를 처리하고 타겟 환경에 전송합니다.
1. SaaS Redis 캐시를 플러시하고 테넌트에 대한 데이터베이스 인덱스를 무효화합니다.

### 카탈로그 데이터 수집

데이터가 로드되면 카탈로그 데이터가 SaaS 테넌트 데이터베이스에서 카탈로그 서비스로 자동 전송됩니다.

카탈로그 서비스는 이 데이터를 라이브 검색 및 제품 추천과 공유합니다. 이 프로세스에는 수작업이 필요하지 않습니다. 수집이 완료되면 모든 서비스에서 데이터를 사용할 수 있습니다.

### 데이터 무결성 확인

마이그레이션 후 CDMS는 다음과 같은 자동 데이터 무결성 검사를 수행하여 마이그레이션된 데이터의 정확성과 완전성을 보장합니다.

**API 기반 확인**

확인하는 동안 CDMS는 이전에 실행한 쿼리의 REST 및 GraphQL API 응답과 대상 인스턴스의 해당 레코드를 비교합니다. 모든 불일치는 마이그레이션 상태에 표시됩니다.

**데이터베이스 수준 확인**

확인하는 동안 CDMS는 추출된 레코드의 수를 계산하여 로드된 레코드의 수와 비교합니다.

**주문형 확인(선택 사항)**

모든 시스템 레코드에 대한 포괄적인 확인을 수동으로 트리거할 수도 있습니다.

>[!NOTE]
>
>이 프로세스는 리소스를 많이 사용하며 샌드박스 환경에서만 사용해야 합니다.

전체 확인에는 다음이 포함됩니다.

- 미리 추출된 모든 REST 및 GraphQL API 응답을 사용하여 API 기반 확인 완료
- 불일치가 발견되면 상세 보고서
