---
title: 벌크 데이터 마이그레이션 도구
description: 벌크 데이터 마이그레이션 도구를 사용하여 기존 Adobe Systems Commerce on Cloud 인스턴스 데이터를 마이그레이션하는 [!DNL Adobe Commerce as a Cloud Service] 방법을 알아봅니다.
feature: Cloud
badgeSaas: label="SaaS만 해당" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Systems Commerce as a Cloud Service 및 Adobe Systems Commerce Optimizer 프로젝트에만 적용됩니다(Adobe Systems 관리 SaaS 인프라)."
role: Developer
level: Intermediate
exl-id: 81522de9-df54-4651-b8ed-58956376af86
source-git-commit: e582ce85b58b57922a8cdd63dbe32bd0f08c64f9
workflow-type: tm+mt
source-wordcount: '706'
ht-degree: 0%

---

# 대량 데이터 마이그레이션 도구

대량 데이터 마이그레이션 도구 PaaS에서 SaaS 환경으로 안전하고 효율적인 데이터 마이그레이션을 가능하게 하는 분산 아키텍처를 따릅니다. 이 도구는 솔루션 구현자가 기존 Adobe Systems Commerce on Cloud 인스턴스(PaaS)에서 SaaS로 데이터를 마이그레이션하는 데 [!DNL Adobe Commerce as a Cloud Service] 도움이 됩니다. 마이그레이션 프로세스에 대한 자세한 내용은 마이그레이션 개요를[&#x200B; 참조하세요](./overview.md).

>[!NOTE]
>
>벌크 데이터 마이그레이션 도구 지원 퍼스트 파티 핵심 상거래 데이터 마이그레이션만 사용자 지정 데이터 마이그레이션은 현재 지원되지 않습니다.

다음 이미지는 대량 데이터 마이그레이션 도구 사용하기 위한 아키텍처 및 주요 구성 요소에 대해 자세히 설명합니다.

![PaaS에서 SaaS 데이터 흐름을 보여주는 대량 데이터 마이그레이션 도구 아키텍처 다이어그램](../assets/bulk-data-diagram.png){zoomable="yes"}

## 마이그레이션 작업 과정

대량 데이터 마이그레이션 작업 과정 은 다음 단계로 구성됩니다.

1. 마이그레이션을 위한 새 환경을 설정합니다.
1. 이전 시스템에서 데이터를 복사합니다.
1. 데이터를 새 시스템으로 이동합니다.
1. 새 시스템에서 제품 카탈로그를 사용할 수 있도록 합니다.
1. 데이터가 올바르게 마이그레이션되었는지 확인합니다.

다음 섹션에서는 이러한 단계에 대해 자세히 설명합니다.

## 대량 데이터 마이그레이션 도구 액세스

대량 데이터 마이그레이션 도구 사용 가능 여부는 다음과 같습니다.

- **2026** 년 1분기(아직 사용할 수 없음) - 대량 데이터 마이그레이션 도구의 초기 릴리스 후에는 지원 티켓을 제출하여 액세스할 수 있습니다.
- **2026** 년 1분기(아직 사용할 수 없음) - 대량 데이터 마이그레이션 도구 공개 후 이 페이지 에서 액세스할 수 있습니다.

## 타겟 환경 만들기

솔루션 구현자(SI)는 마이그레이션을 위한 타겟 환경을 만듭니다. 이 환경은 소스 인스턴스 에서 마이그레이션된 데이터를 저장합니다.

[먼저 새 [!DNL Adobe Commerce as a Cloud Service] (SaaS) 인스턴스](../getting-started.md#create-an-instance) 생성.

### 추출 도구 구성

추출 도구 도구를 사용하여 소스 인스턴스에서 데이터를 추출합니다.

1. Adobe Systems 제공 링크 에서 추출 도구 를 다운로드합니다.
1. 추출 도구 내에서 다음 환경 변수를 설정하십시오.
   - 기존 MySQL 데이터베이스에 대한 연결 세부 정보
   - 인스턴스에 대한 타겟 테넌트 ID입니다 [!DNL Adobe Commerce as a Cloud Service]
   - 다음을 포함한 IMS 자격 증명:
      - 클라이언트 ID
      - 클라이언트 시크릿
      - IMS 범위
      - IMS URL - 기본 URL입니다. 예를 들어, `https://ims-na1.adobelogin.com/`.
      - IMS 조직 ID

   IMS 범위 및 기타 값의 경우 Adobe Systems 개발자 콘솔&#x200B;**에서 프로젝트**&#x200B;내의 자격 증명[&#x200B; 섹션에서 OAuth 유형을 &#x200B;](https://developer.adobe.com/console/)선택합니다. 자세한 정보는 추출 도구 중에 포함된 파일에서 확인할 `.example.env` 수 있습니다.

### 데이터 Extract

추출 도구 실행 전에 솔루션 구현자는 다음을 사용하여 PaaS 데이터베이스에 대한 SSH 터널을 설정해야 합니다.

```bash
magento-cloud tunnel:open
```

그런 다음 추출 도구 실행:

1. PaaS 데이터베이스에 연결하고, 해당 스키마를 분석하고, SaaS 테넌트 스키마 세부 정보와 비교합니다.
1. PaaS와 SaaS 간의 공통 스키마 요소를 기반으로 추출 및 변환 계획을 생성합니다.
1. CDMS(카탈로그 데이터 관리 서비스)를 사용하여 데이터를 Extract.

### 데이터 로드

Adobe Systems 에서 제공하는 데이터 로드 도구 를 실행합니다. 이 도구 기능은 다음과 같습니다.

1. 마이그레이션 계정 사용을 사용하여 SaaS 테넌트 데이터베이스에 연결합니다.
1. 적재 계획을 생성합니다.
1. 계획을 실행하여 데이터를 일괄적으로 SaaS 테넌트 데이터베이스로 이동합니다.
1. 카탈로그 미디어 처리 및 타겟 환경으로 전송.
1. SaaS Redis 캐시를 플러시하고 테넌트에 대한 데이터베이스 인덱스를 무효화합니다.

### 카탈로그 데이터 수집

데이터가 로드된 후 카탈로그 데이터는 SaaS 테넌트 데이터베이스에서 카탈로그 서비스로 자동으로 흐릅니다.

카탈로그 서비스는 이 데이터를 Live Search 및 Product 추천와 공유합니다. 이 프로세스에는 수동 개입이 필요하지 않습니다. 수집이 완료되면 모든 서비스에서 데이터를 사용할 수 있습니다.

### 데이터 무결성 확인

마이그레이션 후 CDMS는 마이그레이션된 데이터의 정확성과 완전성을 보장하기 위해 다음과 같은 자동 데이터 무결성 검사를 수행합니다.

**API 기반 검증**

검증하는 동안 CDMS는 이전에 실행된 쿼리의 REST 및 GraphQL API 응답을 타겟 인스턴스의 해당 레코드와 비교합니다. 모든 불일치는 마이그레이션 상태에서 볼 수 있습니다.

**데이터베이스 수준 확인**

확인하는 동안 CDMS는 추출된 레코드의 수를 계산하고 해당 수를 로드된 레코드의 양과 비교합니다.

**주문형 확인(선택 사항)**

또한 모든 시스템 레코드에 대한 포괄적인 확인을 수동으로 트리거할 수 있습니다.

>[!NOTE]
>
>이 프로세스는 리소스를 많이 사용하므로 샌드박스 환경에서만 사용해야 합니다.

전체 확인에는 다음이 포함됩니다.

- 사전 추출된 모든 REST 및 GraphQL API 응답을 사용한 모든 앱 API 기반 검증
- 발견된 불일치에 대한 자세한 보고서
