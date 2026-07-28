---
title: 마이그레이션 서비스 액세스 확인
description: Commerce 데이터 마이그레이션 서비스 API에 대한 엔드 투 엔드 액세스를 확인하고 네트워크 연결 가능성, IMS 인증 및 테넌트 인증을 확인하는 방법을 알아봅니다.
feature: Cloud
badgeSaas: label="SaaS만" type="Positive" url="https://experienceleague.adobe.com/ko/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."
role: Developer
level: Intermediate
autotag-review: '2026-07-22T19:18:53.554Z'
TQID: 'https://experienceleague.adobe.com/csDq2Bbha2IieqxsDDG0iS1IHhAJ02fD-cwd8KFIsSk'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
  - id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
subfeature_v2:
  - id: f8ddfd3b-6194-46e8-a176-0e918039be56
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 670b6214b28be93a16130552a226a8cadb487324
workflow-type: tm+mt
source-wordcount: 452
ht-degree: 1%

---

# 마이그레이션 서비스 액세스 확인

{{bulk-data-early-access}}

이 안내서를 사용하여 사용자 환경에서 Commerce CDMS(데이터 마이그레이션 서비스) API에 대한 엔드 투 엔드 액세스를 확인합니다. 호출이 성공하면 이그레스 IP(IP 허용 목록에 추가), IMS 인증 및 테넌트 권한 부여에서 네트워크 연결 여부를 동시에 확인합니다.

[고객 준비 검사 목록](readiness-checklist.md)의 모든 항목을 완료한 후 [마이그레이션 안내서](migration-guide.md)에 설명된 마이그레이션을 실행하기 전에 이 안내서를 완료하십시오.

## 사전 요구 사항

- [Adobe Developer Console](https://developer.adobe.com/console/)에서 만든 OAuth 2.0 서버 간 자격 증명(클라이언트 ID 및 클라이언트 암호)입니다.
- `<org>@AdobeOrg` 형식의 IMS 조직 ID입니다. 조직이 대상 테넌트를 소유해야 합니다.
- 대상 `tenantId`, 22자 영숫자 IMS 테넌트 ID입니다.
- CDMS 게이트웨이용 Adobe에 의해 허용 목록에추가된으로 제출된 아웃바운드 이그레스 IP 주소입니다. IP 주소 또는 해당 상태가 확실하지 않은 경우 Adobe 팀과 협력합니다.
- [환경 및 지역별 서비스 호스트](#service-hosts-by-environment-and-region) 테이블의 지역별 서비스 호스트입니다.

## IMS 액세스 토큰 생성

`client_credentials` 부여와 함께 OAuth 2.0 서버 간 자격 증명을 사용하여 액세스 토큰을 생성합니다. 이 단계의 IMS 호스트는 모든 데이터 영역에 대해 동일합니다. CDMS 호스트만 지역별 변경.

```bash
curl -X POST "https://ims-na1.adobelogin.com/ims/token/v3" \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -H "x-org-id:<your-org-id>@AdobeOrg" \
  -d "grant_type=client_credentials" \
  -d "client_id=<your-ims-client-id>" \
  -d "client_secret=<your-ims-client-secret>" \
  -d "scope=AdobeID,openid,read_organizations,additional_info.projectedProductContext,additional_info.roles,adobeio_api,read_client_secret,manage_client_secrets"
```

## 목록 마이그레이션 API 호출

다음 요청은 테넌트에 대한 마이그레이션 목록을 검색하고 이전 단계의 액세스 토큰이 필요합니다. [환경 및 지역별 서비스 호스트](#service-hosts-by-environment-and-region) 테이블에서 해당 지역의 호스트를 선택합니다. `-i` 플래그는 HTTP 상태 줄 및 응답 헤더를 인쇄하므로 결과를 확인할 수 있습니다.

```bash
curl -i "https://<host>/<tenantId>/v1/migrations" \
  -H "Authorization: Bearer <your IMS access token>"
```

## 응답 해석

| HTTP 코드 | 의미 | 예제 응답 본문 |
| --- | --- | --- |
| 200 | 성공. 연결, 인증 및 테넌트 권한 부여가 모두 전달되었습니다. 응답 본문에는 테넌트에 대한 마이그레이션 목록이 포함되어 있습니다. | `{"migrations":[...]}` |
| 401 | 누락되었거나 잘못된 전달자 토큰, 서비스에 도달하기 전에 거부됨. [토큰을 다시 생성](#generate-an-ims-access-token)합니다. | 다양함(게이트웨이 생성) |
| 403 | 인증된 사용자는 이 테넌트에 대한 마이그레이션 권한이 없습니다. | `{"error":"access_denied","message":"You do not have permission to access this tenant"}` |
| 500 | 내부 서버 오류. | `{"error":{"message":"Internal Server Error","status":500}}` |

>[!NOTE]
>
>요청 시간이 초과되거나 연결이 거부되고 HTTP 상태가 반환되지 않는 경우 이그레스 IP가 허용 목록에추가된이 아니거나 잘못된 호스트를 사용하고 있을 수 있습니다. 다음 표에서 지역 호스트 및 허용 목록에추가된 IP를 확인합니다.

## 환경 및 지역별 서비스 호스트

| 지역 또는 환경 | 호스트 |
| --- | --- |
| 샌드박스 또는 사전 프로덕션 | `https://na1-sandbox.api.commerce.adobe.com` |
| 북아메리카 | `https://na1.api.commerce.adobe.com` |
| 유럽 | `https://eu1.api.commerce.adobe.com` |
| 인도 | `https://in1.api.commerce.adobe.com` |
| 영국 | `https://uk1.api.commerce.adobe.com` |
| 오스트레일리아 및 뉴질랜드 | `https://au1.api.commerce.adobe.com` |

## 다음 단계

액세스를 확인한 후 [마이그레이션 안내서](migration-guide.md)로 이동하여 환경 구성 및 마이그레이션 실행을 시작합니다.
