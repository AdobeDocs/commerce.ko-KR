---
title: 고객 준비 체크리스트
description: 참여, 머신, 소스 및 타겟을 다루는 준비 체크리스트와 함께 Adobe Commerce as a Cloud Service으로의 대량 데이터 마이그레이션을 준비하는 방법에 대해 알아봅니다.
feature: Cloud
badgeSaas: label="SaaS만" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."
role: Developer
level: Intermediate
autotag-review: '2026-07-22T19:19:18.443Z'
TQID: 'https://experienceleague.adobe.com/728hkK-dzIPzyuBhuNyOqEE9FxlVGdVc9R2wIRcXobk'
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: bd989d82-1e15-4534-88db-f1f51dd77ffaid: c1256247-af4b-46d8-9dca-0c654ecfa157id: c32adafa-ed01-4b31-997e-2413013911b0id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
subfeature_v2: id: f8ddfd3b-6194-46e8-a176-0e918039be56
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2: id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 670b6214b28be93a16130552a226a8cadb487324
workflow-type: tm+mt
source-wordcount: 1171
ht-degree: 0%

---

# 고객 준비 체크리스트

{{bulk-data-early-access}}

이 체크리스트를 사용하여 대량 데이터 마이그레이션 도구를 사용하여 [!DNL Adobe Commerce on Cloud] 또는 온-프레미스 인스턴스에서 [!DNL Adobe Commerce as a Cloud Service]&#x200B;(으)로 데이터 마이그레이션을 준비하세요.

마이그레이션 도구는 CDE(Commerce Deployed Engineering) 참여 프로세스의 일부로 배포됩니다. 도구에 대한 액세스는 서명된 CDE 계약에 의해 제어되며, 공개적으로 제공되지 않습니다.

이 체크리스트에서는 도구를 공유하기 전에 준비해야 하는 사항([Stage 1](#stage-1-before-tool-access))과 도구가 있으면 구성 및 실행을 시작할 준비가 된 사항([Stage 2](#stage-2-before-running-the-migration))을 다룹니다. 일부 항목은 Adobe 조정이 필요하므로 Adobe 팀과 일찍 이 체크리스트를 검토하십시오.

## 1단계: 도구 액세스 전

마이그레이션 도구 및 설명서를 제공하기 전에 다음을 완료하거나 확인하십시오.

- **CDE 참여** — 서명된 Commerce 배포 엔지니어링 계약이 있어야 합니다. 도구 액세스는 CDE 라이프사이클의 Deal Sign 단계에서 부여됩니다. Adobe 팀과 협력합니다.
- **범위 지정 설문 조사 완료됨** — CDE 검색 중에 범위 지정 설문 조사를 완료하여 현재 도구 기능으로 마이그레이션이 가능한지 확인하고 데이터 풋프린트와 복잡성을 평가합니다. 계속 진행하기 전에 Adobe 팀과 함께 이 작업이 완료되었는지 확인하십시오.
- **HIPAA 데이터가 확인되지 않음** - 소스 인스턴스에 HIPAA 규제 데이터가 포함되어서는 안 됩니다. 계속하기 전에 이것을 확인하십시오.
- **제공된 IP 주소** — 마이그레이션 도구를 실행할 정적 IP 주소 목록을 Adobe 팀에 제공합니다. Adobe 측에서 네트워크 액세스를 구성하는 데 필요합니다.
- **대상 인스턴스 프로비전됨** — 마이그레이션을 시작하기 전에 대상 [!DNL Adobe Commerce as a Cloud Service] 인스턴스를 프로비전해야 합니다. Adobe 팀과 협력하여 인스턴스가 준비되었는지 확인합니다.

## 2단계: 마이그레이션을 실행하기 전

도구에 액세스할 수 있으면 구성 및 실행을 시작하기 전에 다음 항목을 준비하십시오.

### 마이그레이션 머신

마이그레이션 도구는 전용 점프 상자와 같이 사용자가 제어하는 시스템에서 실행됩니다. 이 컴퓨터는 다음 요구 사항을 충족해야 합니다.

- **[!DNL Docker]및 [!DNL Docker Compose] 설치됨** — 도구는 [!DNL Docker] 기반입니다. `docker`과(와) `docker compose`(또는 레거시 `docker-compose`)이(가) 모두 설치되어 마이그레이션 컴퓨터에서 작업해야 합니다.
- **[!DNL Docker]실행 권한** — 마이그레이션을 실행하는 사용자는 [!DNL Docker] 명령을 실행할 수 있어야 합니다. [!DNL Linux]에서 사용자는 `docker` 그룹에 있어야 합니다. [!DNL macOS] 및 [!DNL Windows]에서 [!DNL Docker Desktop]이(가) 실행 중이고 액세스할 수 있어야 합니다.
- **쓰기 가능한 작업 디렉터리** - 마이그레이션 도구를 추출하는 디렉터리는 마이그레이션 사용자가 완전히 쓸 수 있어야 합니다. 이 도구는 실행 중에 로그, 캐시, [!DNL Composer] 종속성 및 생성된 파일을 기록합니다.
- **충분한 디스크 공간** - 추출된 데이터, [!DNL Docker]개의 이미지 및 로그 출력을 위한 충분한 여유 디스크 공간을 확보하십시오. 공간 요구 사항은 소스 데이터베이스의 크기에 따라 다릅니다.
- **온-프레미스 원본: 마이그레이션 컴퓨터에서 직접 데이터베이스 연결** - 온-프레미스 원본 인스턴스의 경우 마이그레이션 컴퓨터에 원본 데이터베이스에 대한 직접 네트워크 액세스 권한이 있어야 합니다. 이 도구는 온-프레미스 데이터베이스 연결을 자동으로 설정하지 않습니다. 마이그레이션 명령을 실행하기 전에 마이그레이션 시스템에서 호스트, 포트 및 자격 증명에 연결할 수 있는지 확인하십시오.
- **Cloud CLI가 설치되어 있고 SSH 키가 등록됨** — [!DNL Adobe Commerce on Cloud] 원본 인스턴스의 경우 [Cloud CLI](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/dev-tools/cloud-cli/cloud-cli-overview)가 마이그레이션 컴퓨터에 설치되어 있어야 합니다. SSH 공개 키도 계정에 등록해야 합니다. 지침은 [보안 연결 가이드](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/secure-connections)를 참조하세요.

### Source 인스턴스

- **Source 스토어 API 액세스 가능** - 마이그레이션 컴퓨터에서 원본 스토어의 REST 및 GraphQL API에 액세스할 수 있어야 합니다. 소스 URL에 대한 API 트래픽을 차단하는 HTTP 기본 인증 또는 네트워크 제한이 없는지 확인합니다.
- **Source OAuth 자격 증명** - 마이그레이션 도구는 OAuth를 사용하여 원본 스토어를 인증합니다. 소스 [!UICONTROL **관리자**]&#x200B;([!UICONTROL **시스템**] > [!UICONTROL **확장**] > [!UICONTROL Integrations])에서 통합을 만들거나 확인하고 소비자 키, 소비자 암호, 액세스 토큰 및 액세스 토큰 암호가 준비되었습니다.
- **PaaS 소스: Magento Cloud API 토큰** — [!UICONTROL **계정 설정**] > [!UICONTROL **API 토큰**] 아래의 [클라우드 계정 설정](https://accounts.magento.cloud)에서 [!DNL Cloud] API 토큰을 생성합니다. 원본이 [!DNL Adobe Commerce on Cloud] 인스턴스인 경우에만 필요합니다.
- **Source 데이터베이스 자격 증명** — (온-프레미스 전용) `host`, `port`, `user`, `password` 및 `database` 이름의 원본 [!DNL MySQL] 데이터베이스 연결 세부 정보가 준비되었습니다.
- **cron을 일시 중지하는 기능** — 동시 쓰기를 방지하려면 데이터 추출 기간 동안 원본 인스턴스에서 cron을 중지할 수 있어야 합니다.
- **통합 및 백그라운드 작업을 일시 중지하는 기능** — 소스 데이터베이스에 쓰는 모든 타사 통합(ERP, OMS, PIM), 예약된 작업 또는 백그라운드 프로세스를 추출 창에서 일시 중지해야 합니다.
- **유지 관리 모드를 활성화 및 비활성화하는 기능** — (단계별 마이그레이션만 해당) 유지 관리 기간을 사용하여 단계별 마이그레이션을 실행하는 경우 원본 인스턴스에서 유지 관리 모드를 활성화 및 비활성화할 수 있어야 합니다.

### 대상 인스턴스

- **테넌트 ID 및 조직 ID가 확인됨** — 구성하기 전에 Adobe 팀에서 `TARGET_TENANT_ID` 및 `TARGET_ORG_ID`을(를) 가져옵니다.
- **IMS OAuth 서버 간 자격 증명** - 마이그레이션 도구에서 대상으로 인증하는 데 필요합니다. [Adobe Developer Console](https://developer.adobe.com/console/)을(를) 통해 생성되었습니다. 자격 증명을 만드는 데 기본 사용자 액세스 권한이 충분하지 않으므로 Adobe 조직에 대한 [!UICONTROL Developer] 또는 [!UICONTROL Admin] 액세스 권한이 필요합니다. Adobe 팀과 조정하여 올바른 제품 프로필을 선택하고 클라이언트 ID(`ADOBE_IMS_CLIENT_ID`) 및 클라이언트 암호(`ADOBE_IMS_CLIENT_SECRET`)를 준비하십시오.
- **CDMS 끝점 URL** — Adobe 팀에서 제공합니다. 이 값을 유추하지 마십시오. 샌드박스 및 테스트 마이그레이션의 경우 사전 프로덕션 엔드포인트와 라이브 단독형 마이그레이션의 경우 프로덕션 엔드포인트가 모두 필요합니다.
- **소스와 대상 간에 정렬된 핵심 구성** - 저장소 설정 및 시스템 구성과 같은 핵심 구성 데이터는 도구에서 마이그레이션되지 않습니다. 마이그레이션 전에 소스와 일치하도록 타겟에서 수동으로 설정하십시오.
- **B2B 저장소: B2B 기능이 일관되게 구성됨** — 원본이 B2B 사용 가능 저장소인 경우 마이그레이션 전에 관련 B2B [!UICONTROL Admin] 설정이 원본과 대상 모두에서 일관되게 구성되었는지 확인하십시오. 필요한 특정 설정에 대해서는 [마이그레이션 안내서](migration-guide.md)를 참조하십시오.

### 마이그레이션 계획

- **마이그레이션 방법 결정** — 시작하기 전에 사용 사례에 적합한 방법을 결정합니다.
  - 단일 단계 마이그레이션 - 유지 관리 모드가 필요하지 않습니다. 소스가 추출 중에 라이브로 유지될 수 있는 드라이 실행, 개발 또는 샌드박스 환경 또는 모든 마이그레이션에 적합합니다.
  - 다단계 마이그레이션 - 유지 관리 모드가 필요합니다. 데이터 일관성을 보장하기 위해 추출 도중 소스를 동결해야 하는 운영 마이그레이션의 경우 다단계 마이그레이션이 필요합니다.
- **유지 관리 기간 계획** — 다단계 마이그레이션에만 적용됩니다. 유지 관리 창을 미리 계획하고 전달합니다. 추출 및 로드 단계 동안 최종 사용자는 소스 인스턴스를 사용할 수 없습니다.
- **저장소 보기 코드가 확인됨** — 원본 인스턴스에서 저장소 보기 코드(`STORE_CODE`)를 식별합니다. 기본값은 `default`이지만 [!UICONTROL Admin] > [!UICONTROL Stores] > [!UICONTROL All Stores]의 실제 코드와 일치해야 합니다. 잘못된 저장소 코드는 마이그레이션 중 데이터 작업에 영향을 줄 수 있습니다.

모든 항목을 확인한 후에는 [마이그레이션 서비스 액세스 안내서](cdms-access.md)를 통해 서비스 액세스를 확인한 다음 [마이그레이션 안내서](migration-guide.md)에서 구성 및 실행 단계를 시작할 준비가 되었습니다.
