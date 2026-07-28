---
title: 대량 데이터 마이그레이션 실행
description: CLI를 사용하여 Adobe Commerce PaaS 또는 온프레미스 인스턴스에서 Adobe Commerce as a Cloud Service으로 대량 데이터 마이그레이션을 구성하고 실행하는 방법에 대해 알아봅니다.
feature: Cloud
badgeSaas: label="SaaS만" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."
role: Developer
level: Intermediate
autotag-review: '2026-07-22T19:19:07.600Z'
TQID: 'https://experienceleague.adobe.com/z9659Vnf2JLxJ4U5p3tEEjurj5Mg3bfKj68Gheq2AXY'
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: bd989d82-1e15-4534-88db-f1f51dd77ffaid: c1256247-af4b-46d8-9dca-0c654ecfa157id: c32adafa-ed01-4b31-997e-2413013911b0id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
subfeature_v2: id: f8ddfd3b-6194-46e8-a176-0e918039be56
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2: id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 670b6214b28be93a16130552a226a8cadb487324
workflow-type: tm+mt
source-wordcount: 2802
ht-degree: 0%

---

# 대량 데이터 마이그레이션 실행

{{bulk-data-early-access}}

이 안내서는 대량 데이터 마이그레이션 도구를 사용하여 [!DNL Adobe Commerce] PaaS 또는 온-프레미스 설치에서 [!DNL Adobe Commerce as a Cloud Service]&#x200B;(으)로 데이터 마이그레이션을 실행하기 위한 단계별 운영 참조입니다. 실제 구성 값 및 환경별 세부 정보는 설정에 따라 다릅니다.

시작하기 전에 [고객 준비 검사 목록](readiness-checklist.md)의 모든 항목을 완료했는지 확인하고 [마이그레이션 서비스 액세스 안내서](cdms-access.md)를 통해 API 액세스를 확인했습니다.

>[!NOTE]
>
>도구 배포 패키지의 일부로 도구의 아키텍처, 내부 디자인, 데이터 변환 프레임워크 및 무결성 테스트 프레임워크에 대한 포괄적인 기술 설명서가 제공됩니다.

## 사전 요구 사항

- 마이그레이션을 실행하는 컴퓨터에 **[!DNL Docker]** 및 **[!DNL Docker Compose]**&#x200B;이(가) 설치되어 있어야 합니다.
- 마이그레이션을 실행하는 사용자는 `docker` 및 `docker compose`(또는 기존 `docker-compose`) 명령을 실행할 수 있는 권한이 있어야 합니다. [!DNL Linux]에서 사용자는 `docker` 그룹에 있어야 합니다. [!DNL macOS] 및 [!DNL Windows]에서 [!DNL Docker Desktop]이(가) 실행 중이고 액세스할 수 있어야 합니다. 마이그레이션 CLI가 [!DNL Docker]을(를) 반복적으로 호출하고 여기에 권한 오류가 있으면 실행이 차단됩니다.
- 마이그레이션을 실행하기 전에 핵심 구성은 소스와 타겟 간에 일관되어야 합니다. 저장소 설정 및 시스템 구성과 같은 핵심 구성 데이터는 이 도구에 의해 마이그레이션되지 않습니다. 타겟에서 독립적으로 설정하고 마이그레이션 전에 소스와 정렬합니다.

## 도구 패키지 설정

대량 데이터 마이그레이션을 위한 환경 설정:

>[!VIDEO](https://video.tv.adobe.com/v/3496121)

1. `ccsaas-migration-tools.tar.gz`의 내용을 추출합니다.

1. `bin/console`이(가) 있는 추출된 `ccsaas-migration-tools` 폴더에서 모든 명령을 실행합니다.

1. 로그, 캐시, [!DNL Composer] 및 생성된 파일에 대해 폴더에 쓸 수 있는지 확인하십시오.

   이 도구는 일관되게 읽고 쓸 수 있도록 해당 디렉터리 아래의 모든 파일 및 하위 폴더의 소유권을 마이그레이션을 실행하는 운영 체제 사용자로 변경합니다. 예를 들어, [!DNL Linux]에서: `chown -R <user>:<group> <project-root>`.

1. 예제 파일(`.example.env`에서 `.env`으로, `.my.cnf.example`에서 `.my.cnf`으로)을 복사하여 프로젝트 루트에 `.env` 및 `.my.cnf` 파일을 만든 다음 다음 다음 섹션에 설명된 값을 입력하십시오.

### 예제 구성 파일

저장소 루트의 `.example.env` 및 `.my.cnf.example` 파일이 구성의 시작점입니다. 각 파일을 작업 이름으로 복사하고 필요한 값을 입력합니다.

| 예제 파일 | 복사 위치: | 대상 |
| --- | --- | --- |
| `.example.env` | `.env` | 지원되는 모든 환경 변수(성능, CDMS, IMS, 대상 SaaS, 소스 URL 인증, OAuth 및 선택적 PaaS 값(`id=`이(가) `.my.cnf`에 설정된 경우 `MAGENTO_CLOUD_CLI_TOKEN`)의 주석이 있는 목록입니다. `.env` 파일에서 전체 변수 목록을 사용할 수 있습니다. |
| `.my.cnf.example` | `.my.cnf` | 온-프레미스 [!DNL MySQL] 및 PaaS(`id=project:environment`)에 대한 `[section]` 레이아웃을 참조합니다. `[section]` 이름은 `.env`의 `SOURCE_CONNECTION_NAME`과(와) 일치해야 합니다. 필드에는 PaaS에 대한 `user`, `password`, `host`, `port`, `database` 및 `id=`이(가) 포함됩니다. |

## 환경 파일 구성

프로젝트 루트의 `.env` 파일이 마이그레이션 및 추출 구성입니다. 소스 및 타겟 URL, OAuth, 원격 CDMS 연결, SaaS 및 IMS 인증 및 기타 스위치를 비롯한 CLI 파이프라인을 구동합니다.

>[!NOTE]
>
>URL에 후행 슬래시를 포함하지 마십시오. 예를 들어 `https://example.com/` 대신 `https://example.com`을(를) 사용합니다.

`.env` 파일을 편집하고 적어도 다음 값을 올바르게 설정하십시오. 지원되는 변수의 전체 목록을 보려면 `.example.env`의 인라인 주석을 참조하십시오.

```shell-session
SOURCE_INSTANCE_URL=https://<source-host>
SOURCE_INSTANCE_GRAPHQL_URL=https://<source-host>/graphql
SOURCE_INSTANCE_REST_URL=https://<source-host>/rest
SOURCE_INSTANCE_CONSUMER_KEY=<consumer_key>
SOURCE_INSTANCE_CONSUMER_SECRET=<consumer_secret>
SOURCE_INSTANCE_ACCESS_TOKEN=<access_token>
SOURCE_INSTANCE_ACCESS_TOKEN_SECRET=<access_token_secret>
```

### 소스 OAuth 자격 증명 구성

>[!VIDEO](https://video.tv.adobe.com/v/3496142)

이 네 가지 값은 마이그레이션 도구에서 소스 스토어 API로의 요청에 서명합니다. 다운로드하려면 원본 [!UICONTROL Admin]을(를) 열고 [!UICONTROL **시스템**] > [!UICONTROL **확장**] > [!UICONTROL **통합**]&#x200B;(으)로 이동하세요. 통합을 만들거나 연 다음 값을 `.env`에 복사합니다.

```shell-session
SOURCE_INSTANCE_CONSUMER_KEY=<consumer_key>
SOURCE_INSTANCE_CONSUMER_SECRET=<consumer_secret>
SOURCE_INSTANCE_ACCESS_TOKEN=<access_token>
SOURCE_INSTANCE_ACCESS_TOKEN_SECRET=<access_token_secret>
```

### Cloud CLI 토큰 설정

>[!NOTE]
>
>[!DNL Adobe Commerce on Cloud]개의 원본 인스턴스에만 적용됩니다. 이 도구는 `.my.cnf`에서 자동으로 원본 형식을 검색합니다. `SOURCE_CONNECTION_NAME` 섹션에 `id=` 줄이 포함된 경우(예: `id=project:production`) 원본은 [!DNL Adobe Commerce on Cloud]이고 `MAGENTO_CLOUD_CLI_TOKEN`이(가) 필요합니다. `id=`이(가) 없는 온-프레미스 원본의 경우 이 토큰이 필요하지 않으며 터널 설정을 건너뜁니다.

1. `https://accounts.magento.cloud`(으)로 이동하여 로그인합니다.

1. 프로필 이미지를 클릭하고 [!UICONTROL **계정 설정**]&#x200B;을 선택합니다.

1. [!UICONTROL **API 토큰**] 섹션으로 이동합니다.

1. [!UICONTROL **API 토큰 만들기**]&#x200B;를 선택하고 수사적 이름을 지정한 다음 생성된 토큰을 복사합니다.

1. `.env`에서 토큰 설정:

   ```text
   MAGENTO_CLOUD_CLI_TOKEN=<your_magento_cloud_api_token>
   ```

>[!NOTE]
>
>Cloud CLI를 처음 사용하는 경우 SSH 공개 키도 계정에 추가해야 합니다. 지침은 [보안 연결 가이드](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/secure-connections)를 참조하세요.

### Commerce 관리 설정 정렬

마이그레이션 전에 소스와 타겟 간에 다음 설정이 일치하는지 확인하십시오.

>[!NOTE]
>
>원활한 마이그레이션을 위해 [!DNL Adobe]은(는) 대상 인스턴스의 모든 핵심 구성을 소스와 일치시키는 것을 권장합니다.

### 대상 SaaS 및 IMS 자격 증명 구성

>[!VIDEO](https://video.tv.adobe.com/v/3496167)

대상의 [!DNL Adobe Commerce as a Cloud Service] IMS 및 API 설정입니다. 사용자 환경에 대한 테넌트 ID, 조직 ID, IMS OAuth 서버 간 자격 증명 및 올바른 IMS 호스트가 필요합니다. 조직, 테넌트 및 프로필 액세스를 위해 Adobe 팀과 협력합니다. 중요한 값을 유추하거나 추정하지 마십시오.

#### IMS 자격 증명 생성

[Adobe Developer Console](https://developer.adobe.com/console/)을(를) 사용합니다. 프로젝트를 만들려면 Adobe 조직에 대한 [!UICONTROL Developer] 또는 [!UICONTROL Admin] 액세스 권한이 필요합니다. 기본 사용자 로그인으로 API를 추가할 수 없습니다.

1. 프로젝트를 만들거나 기존 프로젝트를 연 다음 [!UICONTROL Add API]을(를) 선택하십시오.

1. [!UICONTROL **Adobe Commerce as a Cloud Service**]&#x200B;을(를) 선택하고 계속합니다.

1. 인증 유형으로 [!UICONTROL **OAuth 서버 간**]&#x200B;을(를) 선택하고 계속합니다.

1. Adobe 팀에서 이 테넌트에 대해 예상하는 제품 프로필을 선택한 다음 [!UICONTROL **구성된 API 저장**]&#x200B;을 선택합니다.

1. 프로젝트 사이드바에서 [!UICONTROL **OAuth 서버 간**]&#x200B;(또는 [!UICONTROL **자격 증명**])을 연 다음 클라이언트 ID와 클라이언트 암호를 `.env`에 `ADOBE_IMS_CLIENT_ID` 및 `ADOBE_IMS_CLIENT_SECRET`(으)로 복사하십시오.

IMS 토큰 끝점(`ADOBE_IMS_URL`)은 자격 증명의 환경과 일치해야 합니다.

| 계층 | 일반 `ADOBE_IMS_URL` |
| --- | --- |
| QA 또는 스테이징 | `https://ims-na1-stg1.adobelogin.com` |
| 사전 프로덕션 또는 프로덕션 | `https://ims-na1.adobelogin.com` |

>[!NOTE]
>
>이러한 URL의 `na1`은(는) 대상 인스턴스가 프로비저닝된 지역을 나타냅니다. 인스턴스가 다른 지역에서 프로비저닝된 경우 이를 적절한 지역 식별자로 대체합니다.

`ADOBE_IMS_META_SCOPES`은(는) 해당 자격 증명에 프로비전된 범위와 일치해야 합니다. `.example.env` 파일에 쉼표로 구분된 전체 범위 문자열이 참조로 포함되어 있습니다. Adobe에서 지시한 경우에만 변경합니다.

#### [!DNL Adobe I/O] 자격 증명을 환경 파일에 매핑

[!DNL Developer Console]에서 OAuth 서버 간 값은 다음 JSON 구조에 해당하는 클라이언트 ID 및 클라이언트 암호로 표시됩니다.

```json
{
  "client_id": "xxxxxxxxxxxxxxxxxxxxxxxxxxx",
  "client_secret": "xxxxxxxxxxxxxxxxxxxxxxxxxxx"
}
```

`.env`에 매핑합니다(자리 표시자 예).

```shell-session
TARGET_ORG_ID=<org_id>@AdobeOrg
ADOBE_IMS_URL=https://ims-na1.adobelogin.com
ADOBE_IMS_CLIENT_ID=xxxxxxxxxxxxxxxxxxxxxxxxxxx
ADOBE_IMS_CLIENT_SECRET=xxxxxxxxxxxxxxxxxxxxxxxxxxx
ADOBE_IMS_META_SCOPES=AdobeID,openid,additional_info.projectedProductContext
```

SaaS API 호스트는 사전 프로덕션 및 프로덕션마다 다릅니다. `TARGET_INSTANCE_REST_URL` 및 `TARGET_INSTANCE_GRAPHQL_URL`은(는) 프로덕션 전 또는 프로덕션으로 마이그레이션과 동일한 Commerce API 환경을 사용해야 합니다. 한 계층을 다른 계층의 CDMS 또는 테넌트와 혼합하지 마십시오.

| 환경 | `TARGET_INSTANCE_*_URL`의 일반 호스트 |
| --- | --- |
| 사전 프로덕션 또는 샌드박스 | `https://na1-sandbox.api.commerce.adobe.com/{tenantId}` |
| 프로덕션 | `https://na1.api.commerce.adobe.com/{tenantId}` |

>[!NOTE]
>
>이러한 URL의 `na1`은(는) 대상 인스턴스가 프로비저닝된 지역을 나타냅니다. 인스턴스가 다른 지역에서 프로비저닝된 경우 이를 적절한 지역 식별자로 대체합니다.

```shell-session
TARGET_TENANT_ID=<tenant_id>
TARGET_ORG_ID=<org_id>@AdobeOrg
ADOBE_IMS_URL=https://ims-na1.adobelogin.com
ADOBE_IMS_CLIENT_ID=<client_id>
ADOBE_IMS_CLIENT_SECRET=<client_secret>
ADOBE_IMS_META_SCOPES=AdobeID,openid,additional_info.projectedProductContext
TARGET_INSTANCE_REST_URL=https://na1-sandbox.api.commerce.adobe.com/{tenantId}
TARGET_INSTANCE_GRAPHQL_URL=https://na1-sandbox.api.commerce.adobe.com/{tenantId}/graphql
```

프로덕션 SaaS 호스트의 경우 `TARGET_INSTANCE_*` URL에서 `na1-sandbox`을(를) `na1`(으)로 바꾸십시오. 이전 표에 표시된 대로 해당 계층에 대해 일치하는 `ADOBE_IMS_URL`을(를) 사용합니다.

### CDMS 엔드포인트 설정

마이그레이션 대상 환경과 일치하는 CDMS API 호스트에 마이그레이션 도구를 지정합니다. `.env`에서 `CDMS_HOST`(및 일반적으로 `CDMS_PORT=443`)을(를) 설정합니다. 운영 전 또는 운영 호스트 중 하나만 사용하고 둘 다 사용하지 마십시오.

| 환경 | 사용 시기 | `CDMS_HOST` |
| --- | --- | --- |
| 사전 프로덕션 | 비프로덕션 CDMS의 사전 프로덕션 또는 샌드박스 스타일 실행 | `https://commerce-data-migration-service-preprod-external.adobe.io` |
| 프로덕션 | 라이브 프로덕션 마이그레이션 또는 전환 | `https://commerce-data-migration-service-prod-external.adobe.io` |

실행과 일치하는 블록을 설정하거나 주석 처리를 제거합니다.

```shell-session
# Pre-production CDMS
CDMS_HOST=https://commerce-data-migration-service-preprod-external.adobe.io
CDMS_PORT=443

# Production CDMS (use for prod cutover only)
# CDMS_HOST=https://na1.api.commerce.adobe.com
# CDMS_PORT=443
```

### 스토어 코드 설정

`STORE_CODE`은(는) 원본 인스턴스 REST API 호출, 가상 테스트 고객 생성 및 데이터 정리를 위해 마이그레이션 도구에서 사용하는 저장소 보기 코드입니다. 또한 로드 단계 중에 `x-store-code` 헤더로 전송됩니다.

`STORE_CODE`의 기본값은 `.example.env`의 `default`입니다. 소스 인스턴스의 기본 스토어 보기 코드와 일치하는지 확인합니다. 확인하려면 원본 [!UICONTROL Admin]에서 [!UICONTROL **스토어**] > [!UICONTROL **모든 스토어**]&#x200B;(으)로 이동하여 사용해야 하는 스토어 보기에 대한 [!UICONTROL **코드**] 열을 확인합니다. 표시된 코드가 `default`이(가) 아니면 `.env`에서 `STORE_CODE`을(를) 업데이트하여 일치시키십시오.

## 데이터베이스 연결 파일 구성

>[!VIDEO](https://video.tv.adobe.com/v/3496152)

`.my.cnf` 파일은 마이그레이션 도구의 추출 측에 [!DNL MySQL] 연결 설정을 제공합니다. 프로젝트 루트의 `.my.cnf`에 `.my.cnf.example`을(를) 복사하여 만드십시오. 섹션 이름은 `.env`의 `SOURCE_CONNECTION_NAME`과(와) 일치해야 합니다.

온-프레미스 또는 자체 호스팅 소스의 경우:

```ini
[<connection-name>]
user=<db_user>
password='<db_password>'
host=<db_host>
port=3306
database=<db_name>
```

>[!NOTE]
>
>마이그레이션 도구를 실행하는 컴퓨터는 원본 데이터베이스에 대한 직접 네트워크 액세스 권한이 있어야 합니다. 이 도구는 온-프레미스 연결을 자동으로 설정하거나 확인하지 않습니다. 마이그레이션 명령을 실행하기 전에 마이그레이션 시스템에서 호스트, 포트 및 자격 증명에 연결할 수 있는지 확인하십시오.

[!DNL Adobe Commerce on Cloud] 소스의 경우:

```ini
[<connection-name>]
id=<project_id>:<environment>
```

`id=` 필드는 원본이 PaaS이고 `MAGENTO_CLOUD_CLI_TOKEN`을(를) 사용하여 터널 설정을 트리거함을 도구에 알려줍니다. `project_id` 및 `environment` 값은 [!DNL Cloud Console] 또는 `magento-cloud project:list` 및 `magento-cloud environment:list` 명령을 통해 사용할 수 있습니다.

## 네트워크 및 인스턴스 준비

스토어 앞에 있는 HTTP 기본 인증은 API 및 도구 트래픽을 차단할 수 있습니다. 마이그레이션에 사용되는 소스 URL에 대해 비활성화되어 있거나 도구의 경로가 허용되어 REST 및 GraphQL 요청이 스토어에 도달할 수 있는지 확인하십시오.

### 추출 중 소스 데이터베이스 안정성 유지

이 툴은 소스 데이터베이스에서 데이터를 추출하지만 다른 프로세스는 이 데이터 소스에 쓰지 않아야 합니다. 동시 쓰기로 인해 스냅샷이 일치하지 않을 수 있습니다.

- 소스 및 `bin/magento` 또는 다른 작성기를 실행하는 운영 체제 스케줄러에서 추출 기간 동안 cron을 중지하거나 추출 중에 실행할 수 없는지 확인하십시오.
- 동일한 데이터베이스에 쓰는 ERP, OMS, PIM, 사용자 정의 작업 및 서드파티 API와 같은 다른 통합을 검토합니다. 추출 실행 중에 테이블을 변경하지 않도록 추출 창에 대한 쓰기를 일시 중지하거나 차단합니다.
- 유지 관리 모드와 터널 또는 데이터베이스 액세스를 보완합니다. 이를 통해 상점 및 API 트래픽을 줄일 수 있습니다. Cron 및 통합은 명시적으로 제어해야 하는 별도의 쓰기 소스입니다.

### 대상

마이그레이션 전에 대상 카탈로그를 지워야 하는 경우 중복 카탈로그 충돌과 대량 삭제 시간 초과를 방지하기 위해 [!UICONTROL Admin]의 제품을 한 번에 200개씩 작은 배치로 삭제하십시오.

## 마이그레이션 구축 및 실행

쓰기 권한이 있는 추출된 프로젝트 디렉토리에서 작업합니다.

### SSH를 통해 세션 유지

SSH를 통해 연결하는 경우, 삭제된 네트워크는 셸을 죽이고 긴 마이그레이션을 방해할 수 있습니다. GNU `screen` 명령은 서버에서 세션을 사용 가능하도록 유지합니다.

```bash
screen -S migration          # new session named "migration"
# run ./bin/console commands here; when you want to disconnect without stopping work:
# press Ctrl+A, release, then press d   # detach
screen -ls                   # list sessions
screen -x migration          # reattach to "migration"
```

서버에서 사용할 수 있는 경우 `tmux`을(를) 사용할 수도 있습니다.

### 도커 이미지 빌드

PHP, CLI 및 종속성을 포함하는 `bin/console`에서 사용하는 [!DNL Docker] 이미지를 빌드합니다. 첫 번째 실행 전에 또는 Dockerfile 또는 기본 이미지 변경 후에 이 작업을 실행합니다.

```bash
./bin/console build
```

### 지원 서비스 시작

로컬 테스트 데이터베이스와 같은 도구에 대한 [!DNL Docker Compose] 지원 서비스를 시작하고 `.env`에서 활성화된 경우 선택적 로컬 서비스를 시작합니다. 정확한 서비스는 구성에 따라 다릅니다. 빌드 성공 후 셸, 마이그레이션 또는 단계 명령 전에 이 작업을 실행합니다.

```bash
./bin/console start
```

### CLI 컨테이너 초기화

CLI 컨테이너를 한 번 시작하면 진입점이 탑재된 프로젝트에 대해 필요한 경우 [!DNL Composer] 설치와 같은 설치를 완료할 수 있습니다. 새 환경에서 첫 번째 마이그레이션이 실행되기 전에 이 작업을 한 번 실행합니다.

```bash
./bin/console shell
exit
```

### 마이그레이션 실행

이 도구는 두 가지 마이그레이션 접근 방식을 지원합니다. 사용 사례에 맞는 항목을 선택합니다.

#### 단일 단계 마이그레이션

소스 인스턴스에는 유지 관리 모드가 필요하지 않습니다. 단일 명령으로 전체 마이그레이션 파이프라인을 실행합니다.

```bash
./bin/console migration
```

이 명령은 모든 파이프라인 단계를 다음 순서로 끝에서 끝까지 자동으로 실행합니다.

1. **구성 확인** — 환경 변수 및 도구 설정의 유효성을 검사합니다.
1. **환경 초기화** — [!DNL Docker] 서비스를 시작하고, 클라우드 터널(해당되는 경우)을 열고, 단위 테스트를 실행합니다.
1. **통합 테스트 및 CDMS 초기화** - 통합 테스트를 실행하고 CDMS API 연결을 초기화합니다.
1. **마이그레이션 만들기** — CDMS에 마이그레이션을 등록하고 대상 스키마 분석을 기다립니다. 마이그레이션 ID가 `.migration_id`에 저장됩니다.
1. **기능 테스트 및 테스트 데이터 생성** — 기능 테스트를 실행하고 무결성 확인을 위해 소스에서 합성 테스트 데이터를 생성합니다(활성화된 경우).
1. **데이터 추출** — 원본 인스턴스에서 데이터를 추출합니다.
1. **대상에 로드** — 추출한 데이터를 대상 [!DNL Adobe Commerce as a Cloud Service] 인스턴스로 로드합니다. 스테이징 보기는 소스에서 정리되고, 소스 테스트 데이터는 로드와 동시에 REST를 통해 제거됩니다.
1. **데이터 무결성 확인** — 체크섬 확인을 트리거하고 로컬 API 확인 테스트를 실행합니다. 결과가 기록되고 실패해도 파이프라인이 중지되지 않습니다.
1. **Test data cleanup on target** — 대상 인스턴스에서 합성 테스트 데이터를 제거합니다.
1. **결과 처리** — 마이그레이션 요약을 생성하고 필요한 경우 저장소에서 아티팩트를 다운로드합니다.

유지 관리 창이 필요하지 않은 경우 이 옵션을 사용합니다. 이 창은 일반적으로 엔드 투 엔드 드라이 실행, 개발 또는 샌드박스 환경 또는 추출 중에 소스가 라이브로 유지될 수 있는 모든 마이그레이션에 사용됩니다.

>[!WARNING]
>
>고정 소스가 필요한 경우(예: 추출 중에 새 주문이나 데이터 변경이 발생하지 않아야 하는 프로덕션 마이그레이션) 이 옵션을 사용하지 마십시오. 대신 단계별 마이그레이션을 사용하십시오. 이 명령을 단계별 유지 관리 워크플로의 단계로 사용하지 마십시오.

#### 유지 관리 모드를 사용한 다단계 마이그레이션

추출 중에 데이터 일관성을 유지하려면 소스 인스턴스에 유지 관리 모드가 필요합니다. 마이그레이션은 순서대로 실행해야 하는 개별 단계로 분할됩니다.

>[!NOTE]
>
>두 개의 다른 CLI가 포함됩니다. `./bin/console` 명령은 마이그레이션 도구 프로젝트 루트에서 실행됩니다. `bin/magento maintenance:*` 명령은 원본 [!DNL Adobe Commerce] 응용 프로그램 서버에서 SSH를 통해 설치 루트로 실행되거나 [!UICONTROL Admin]을(를) 통해 실행됩니다. 이 도구는 사용자를 대신하여 [!DNL Magento] 유지 관리 명령을 실행하지 않습니다.

| 단계 | 운영자 | Source 주 |
| --- | --- | --- |
| 1. `migration:before-maintenance` | 도구 | 라이브 — 아직 유지 관리를 활성화하지 않음 |
| &#x200B;2. 유지 관리 모드 활성화 | 수동 | 고정으로 전환 |
| 3. `migration:during-maintenance` | 도구 | 고정 — 이 단계에서 유지 관리를 비활성화하지 않음 |
| &#x200B;4. 유지 관리 모드 비활성화 | 수동(조건부) | 소스 인스턴스를 라이브로 전환 |
| &#x200B;5. `migration:cleanup` (선택 사항) | 도구 | Live — 유지 관리를 해제해야 합니다. |

**1단계 — 유지 관리 전(소스가 라이브)**

소스 인스턴스가 라이브이고 트래픽을 수락하는 동안 실행됩니다. 소스에 대한 REST 및 GraphQL 액세스를 완전히 사용할 수 있어야 합니다. 이 단계가 완료되기 전에 유지 관리 모드를 활성화하지 마십시오.

서버 루트로 돌아가서 다음을 실행합니다.

```bash
./bin/console migration:before-maintenance
```

1. **구성 확인** — 환경 변수 및 도구 설정의 유효성을 검사합니다.
1. **환경 초기화** — [!DNL Docker] 서비스를 시작하고 PaaS 클라우드 터널(해당되는 경우)을 열고 단위 테스트를 실행합니다.
1. **통합 테스트 및 CDMS 초기화** - 통합 테스트를 실행하고 CDMS API 연결을 초기화합니다.
1. **마이그레이션 만들기** — CDMS에 마이그레이션을 등록하고 대상 스키마 분석을 기다립니다. 마이그레이션 ID가 `.migration_id`에 저장됩니다.
1. **기능 테스트** — 라이브 소스에 대해 기능 테스트를 실행합니다.
1. **테스트 데이터 생성** — 무결성 확인을 위해 소스에서 합성 테스트 고객 및 주문을 만듭니다(활성화된 경우).

**2단계 — 유지 관리 모드 사용(수동)**

소스에서 유지 관리 모드를 활성화하고 예약된 작업, 서드파티 통합, 주문 처리 및 미디어 에셋 동기화를 포함하여 데이터베이스에 기록되거나 데이터베이스에 영향을 주는 모든 작업을 일시 중지합니다.

소스 Commerce 서버(설치 루트)에서 다음을 실행합니다.

```bash
bin/magento maintenance:enable
```

**3단계 — 유지 관리 중(원본이 동결됨)**

유지 관리 모드에서 소스 인스턴스로 를 실행합니다. 소스는 이 단계의 전체 기간 동안 고정된 상태를 유지해야 합니다. **단계 3**&#x200B;이(가) 성공적으로 완료될 때까지 유지 관리 모드를 비활성화하지 마십시오.

```bash
./bin/console migration:during-maintenance
```

1. **클라우드 터널 설정** — [!DNL Adobe Commerce on Cloud] 소스 인스턴스의 경우 클라우드 터널을 다시 열고 데이터베이스 연결을 확인합니다. 온-프레미스 인스턴스에 대해 자동으로 건너뜀
1. **데이터 추출** — 고정된 소스 인스턴스에서 데이터를 추출합니다.
1. **준비 보기 정리** - 직접 데이터베이스 연결을 사용하여 원본에서 준비 보기를 제거합니다(유지 관리 모드에서 안전).
1. **대상에 로드** — 추출한 데이터를 대상 [!DNL Adobe Commerce as a Cloud Service] 인스턴스에 로드하고 완료될 때까지 대기합니다.
1. **데이터 무결성 확인** — CDMS 체크섬 확인을 트리거하고 로컬 API 확인 테스트를 실행합니다. 결과가 기록되고 실패해도 파이프라인이 중지되지 않습니다.
1. **Test data cleanup on target** — 대상 인스턴스에서 합성 테스트 데이터를 제거합니다.
1. **결과 처리** — 마이그레이션 요약을 생성하고 필요한 경우 저장소에서 아티팩트를 다운로드합니다.

**4단계 — 유지 관리 모드 비활성화(수동, 조건부)**

이 단계에서는 유지 관리 모드를 비활성화하여 소스 인스턴스에 대한 트래픽을 다시 활성화합니다. 정리 단계는 REST를 통해 소스와 통신하며 유지 관리 모드가 아직 활성 상태인 경우 `HTTP 503`과(와) 함께 실패하기 때문에 정리 단계를 실행하기 전에 필요합니다.

소스 Commerce 서버에서 다음을 실행합니다.

```bash
bin/magento maintenance:disable
```

**5단계 — 정리(선택 사항, 원본은 라이브여야 함)**

**단계 1**&#x200B;에서 만든 가상 테스트 고객 및 주문을 REST를 통해 원본 인스턴스에서 제거합니다. 이 단계는 유지 관리 모드가 비활성화된 후에만 실행할 수 있습니다.

>[!NOTE]
>
>테스트 데이터가 만들어지지 않았으므로 `SKIP_TEST_DATA_CREATION=true`이(가) `.env`에 설정된 경우 이 단계를 건너뜁니다.

서버 루트로 돌아가서 다음을 실행합니다.

```bash
./bin/console migration:cleanup
```

1. **데이터베이스 연결 설정** — [!DNL Adobe Commerce on Cloud] 원본 인스턴스의 경우 클라우드 터널을 다시 엽니다. 온-프레미스 인스턴스의 경우 직접 데이터베이스 연결을 설정하고 확인합니다.
1. **Source REST 정리** — REST API를 통해 소스에서 합성 테스트 고객 및 주문을 제거합니다.

## 마이그레이션 다시 시작 또는 다시 실행

마이그레이션 도구는 프로젝트 루트의 `.migration_id` 파일을 사용하여 진행 상황을 추적합니다. 이 파일은 새 마이그레이션이 시작될 때 자동으로 만들어지며 현재 마이그레이션 식별자를 기록합니다.

### 실패 후 다시 시작

마이그레이션 실행이 실패하거나 중단되는 경우 처음부터 다시 시작하지 않고 동일한 명령을 다시 실행하여 마지막으로 성공한 단계(추출, 로드 또는 확인)에서 다시 시작하십시오. 이미 완료된 단계는 자동으로 건너뜁니다.

>[!IMPORTANT]
>
>`migration:during-maintenance` 단계를 다시 시작하면 원본이 계속 유지 관리 모드로 유지되어야 합니다. 소스를 유지 관리에서 제외했거나 실행 사이에 데이터가 변경된 경우 다시 시작된 마이그레이션은 일관되지 않은 결과를 생성할 수 있습니다.

### 새 마이그레이션 시작

이전 실행을 무시하고 완전히 새로운 마이그레이션을 시작하려면 다음 마이그레이션을 시작하기 전에 `.migration_id` 파일을 삭제하십시오.

```bash
rm .migration_id
```

`.migration_id`이(가) 있고 이전 마이그레이션이 이미 완료된 경우 도구에서 마이그레이션이 이미 완료되었다는 메시지를 인쇄하고 파일을 삭제하도록 권장합니다.

## 로그 검토 및 디버그

모든 마이그레이션 로그는 프로젝트 루트의 `logs/` 디렉터리에 기록되며 타임스탬프가 지정된 하위 디렉터리로 구성됩니다.

```text
logs/
  2026-03-23_14-30-00/     ← one directory per run
    index.log              ← main pipeline log (start here)
    ...
```

- `index.log`은(는) 주 파이프라인 오케스트레이션 로그입니다. 단계가 실패하면 0이 아닌 코드로 종료된 스크립트와 그 이유를 표시합니다.
- `09b_run_load.log` 및 `11_verify_data_integrity_local.log`과(와) 같은 단계별 로그에는 각 단계에 대한 자세한 출력이 포함되어 있습니다.
