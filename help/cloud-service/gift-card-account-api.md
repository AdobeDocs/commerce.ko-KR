---
title: 기프트 카드 계정 REST 엔드포인트
description: 기프트 카드 계정 REST API를 사용하여  [!DNL Adobe Commerce as a Cloud Service]에서 프로그래밍 방식으로 기프트 카드 계정을 만들고, 업데이트하고, 삭제하고, 쿼리하는 방법에 대해 알아봅니다.
role: Admin, Developer
level: Experienced
badgeSaas: label="SaaS만" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."
source-git-commit: 160180d9d779514f6faee3c7de46531ebf191c7d
workflow-type: tm+mt
source-wordcount: '807'
ht-degree: 0%

---

# 기프트 카드 계정 API

{{accs-sandbox-experimental}}

기프트 카드 계정 REST 엔드포인트는 장바구니 또는 견적 수준이 아닌 계정 수준에서 기프트 카드 계정을 프로그래밍 방식으로 관리합니다. 이 API를 사용하여 기프트 카드 계정을 생성, 검색, 업데이트 및 삭제하거나 JSON 가져오기 엔드포인트를 통해 기프트 카드 계정을 일괄적으로 프로비저닝할 수 있습니다.

이러한 엔드포인트는 다음을 위해 설계되었습니다.

* 기프트 카드 프로그램을 관리하는 관리자
* 타사 통합: ERP, CRM 및 마케팅 플랫폼과 같은 외부 시스템에서 기프트 카드 프로비저닝
* 벌크 기프트 카드 생성을 위한 자동화된 워크플로

## 인증

모든 엔드포인트에는 관리자 또는 통합 전달자 토큰이 필요합니다. 토큰은 `Magento_GiftCardAccount::giftcardaccount` ACL(액세스 제어 목록) 리소스를 포함하는 역할에 연결되어야 합니다.

대량 가져오기 작업의 경우 역할에는 `Magento_ImportExport::import_api` ACL 리소스도 포함되어야 합니다.

## 웹 사이트 및 스토어 컨텍스트

웹 사이트 및 저장소 보기 값은 요청 본문이 아닌 HTTP 요청 헤더에서 확인됩니다. 각 요청에 다음 헤더 중 하나를 전달합니다.

* `Store: <store_view_code>`
* `Magento-Website-Code: <website_code>`

API는 이러한 헤더에서 웹 사이트를 자동으로 확인합니다. REST 요청 페이로드에 `website_id`을(를) 포함하지 마십시오.

>[!NOTE]
>
>대량 가져오기 끝점은 예외입니다. 가져오기는 대량으로 작동하며 특정 웹 사이트를 대상으로 할 수 있으므로 가져오기 페이로드의 각 행에 명시적 `website_id` 값이 필요합니다.

## REST API 참조

API는 `/V1/giftcardaccounts` ACL 리소스로 보호되는 `Magento_GiftCardAccount::giftcardaccount` 아래에 다음 작업을 표시합니다.

| 방법 | URL | 설명 |
|--------|-----|-------------|
| POST | `/rest/V1/giftcardaccounts` | 기프트 카드 계정 만들기 |
| GET | `/rest/V1/giftcardaccounts` | 계정 나열(searchCriteria 지원) |
| GET | `/rest/V1/giftcardaccounts/:id` | ID로 계정 가져오기 |
| GET | `/rest/V1/giftcardaccounts/code/:code` | 코드로 계정 가져오기 |
| PUT | `/rest/V1/giftcardaccounts/:id` | 계정 업데이트(병합 의미) |
| DELETE | `/rest/V1/giftcardaccounts/:id` | 계정 삭제 |

### 필드 참조

| 필드 | 유형 | 유효한 값 | REST 만들기 | 가져오기 |
|---|---|---|---|---|
| `code` | 문자열 | 최대 255자 | 필수 | 필수 |
| `balance` | 부동 | >= 0 | 필수 | 필수 |
| `status` | int | `0`(사용 안 함), `1`(사용) | 선택 사항이며 기본값은 `1`입니다. | 선택 사항이며 기본값은 `1`입니다. |
| `state` | int | `0`(사용 가능), `1`(사용됨), `2`(상환됨), `3`(만료됨) | 선택 사항이며 기본값은 `0`입니다. | 선택 사항이며 기본값은 `0`입니다. |
| `is_redeemable` | int | `0` 또는 `1` | 선택 사항이며 기본값은 `1`입니다. | 선택 사항이며 기본값은 `1`입니다. |
| `date_expires` | 문자열 | `YYYY-MM-DD` 또는 null | 선택 사항 | 선택 사항 |
| `date_created` | 문자열 | `YYYY-MM-DD` | 자동 설정 | 선택 사항, 생략된 경우 자동 설정 |
| `website_id` | int | 유효한 웹 사이트 ID | 승인되지 않음(헤더에서 자동 해결됨) | 필수 |

### 기프트 카드 계정 만들기

중복 코드 검색을 사용하여 새 기프트 카드 계정을 만듭니다.

| 항목 | 값 |
|---|---|
| **메서드** | `POST` |
| **URL** | `/V1/giftcardaccounts` |

**요청 본문:**

```json
{
  "giftcardAccount": {
    "code": "GIFT-1234-ABCD",
    "balance": 100.00,
    "status": 1,
    "state": 0,
    "is_redeemable": 1,
    "date_expires": "2027-12-31"
  }
}
```

**응답(200):**

```json
{
  "account_id": 42,
  "code": "GIFT-1234-ABCD",
  "balance": 100,
  "status": 1,
  "state": 0,
  "is_redeemable": 1,
  "date_expires": "2027-12-31",
  "date_created": "2026-03-12"
}
```

### ID로 기프트 카드 계정 검색

| 항목 | 값 |
|---|---|
| **메서드** | `GET` |
| **URL** | `/V1/giftcardaccounts/:id` |

**응답(200):**

단일 기프트 카드 계정 개체를 반환합니다.

### 코드로 기프트 카드 계정 검색

| 항목 | 값 |
|---|---|
| **메서드** | `GET` |
| **URL** | `/V1/giftcardaccounts/code/:code` |

>[!IMPORTANT]
>
>기프트 카드 코드가 순전히 숫자인 경우(예: `12345`) `/V1/giftcardaccounts/12345`에 대한 요청이 코드 경로가 아닌 ID 경로와 일치합니다. 코드가 숫자일 수 있는 경우 코드 기반 조회에 항상 `/V1/giftcardaccounts/code/12345`을(를) 사용하십시오.

**응답(200):**

단일 기프트 카드 계정 개체를 반환합니다.

### 검색 기준이 있는 기프트 카드 계정 나열

| 항목 | 값 |
|---|---|
| **메서드** | `GET` |
| **URL** | `/V1/giftcardaccounts` |

검색 기준을 쿼리 매개 변수로 전달합니다. 다음 예제에서는 `status`이(가) `1`인 기프트 카드 계정을 반환합니다(활성화됨).

```text
GET /V1/giftcardaccounts?searchCriteria[filterGroups][0][filters][0][field]=status&searchCriteria[filterGroups][0][filters][0][value]=1&searchCriteria[pageSize]=10&searchCriteria[currentPage]=1
```

**응답(200):**

```json
{
  "items": [
    {
      "account_id": 42,
      "code": "GIFT-1234-ABCD",
      "balance": 100,
      "status": 1,
      "state": 0,
      "is_redeemable": 1,
      "date_expires": "2027-12-31",
      "date_created": "2026-03-12"
    }
  ],
  "search_criteria": { ... },
  "total_count": 1
}
```

### 기프트 카드 계정 업데이트

병합 의미 체계를 사용하여 기존 기프트 카드 계정을 업데이트합니다. 요청의 null이 아닌 필드만 적용됩니다. `code` 필드를 변경할 수 없습니다. 다른 코드를 전달하면 유효성 검사 오류가 반환됩니다.

| 항목 | 값 |
|---|---|
| **메서드** | `PUT` |
| **URL** | `/V1/giftcardaccounts/:id` |

**요청 본문:**

```json
{
  "giftcardAccount": {
    "balance": 75.00,
    "status": 1
  }
}
```

**응답(200):**

업데이트된 기프트 카드 계정 개체를 반환합니다.

### 기프트 카드 계정 삭제

| 항목 | 값 |
|---|---|
| **메서드** | `DELETE` |
| **URL** | `/V1/giftcardaccounts/:id` |

**응답(200):**

```json
true
```

## JSON을 통한 대량 가져오기

엔터티 형식이 `POST /V1/import/json`인 `giftcardaccount`을(를) 사용하여 기프트 카드 계정을 일괄적으로 프로비전할 수 있습니다. 이 끝점에는 기프트 카드 계정 ACL 외에 `Magento_ImportJsonApi::import_api` ACL(액세스 제어 목록) 리소스가 필요합니다.

### 지원되는 동작

| 비헤이비어 | 설명 |
|---|---|
| `append` | 새 기프트 카드 계정을 만듭니다. 코드가 이미 있으면 해당 행이 실패하고 나머지 행에서 가져오기를 계속합니다. |
| `replace` | 코드로 기프트 카드 계정을 업데이트하고 삽입합니다. 코드가 없는 경우 계정을 만들고, 없는 경우 바꿉니다. |
| `delete` | 코드로 기프트 카드 계정을 제거합니다. |

### 요청 예

```json
{
  "source": {
    "entity": "giftcardaccount",
    "behavior": "append",
    "validation_strategy": "validation-stop-on-errors",
    "allowed_error_count": "10",
    "items": [
      {
        "code": "BULK-001",
        "balance": 50.00,
        "website_id": 1,
        "status": 1,
        "state": 0,
        "is_redeemable": 1,
        "date_expires": "2027-06-30"
      },
      {
        "code": "BULK-002",
        "balance": 25.00,
        "website_id": 1
      }
    ]
  }
}
```

### 가져오기 동작 세부 정보

* 가져오기 페이로드의 각 행에는 요청 헤더에서 웹 사이트를 유추하는 REST 끝점과 달리 명시적 `website_id`이(가) 필요합니다.
* 각 행은 독립적으로 검증됩니다. 잘못된 행은 동일한 배치의 유효한 행에 영향을 주지 않고 행당 오류를 생성합니다.
* 동일한 배치 내의 중복 코드는 트랜잭션 롤백을 일으키지 않고 행별 오류로 탐지 및 보고됩니다.
* 성능을 위해 데이터베이스에 직접 쓰기를 가져오고 공급업체 모델의 저장 주기를 건너뜁니다. 가져오기를 수행하는 동안 잔고 변경 내역 항목은 생성되지 않습니다.
* REST 만들기 작업에서 지난 만료 날짜를 거부합니다. 가져오기는 과거 데이터 마이그레이션을 지원하기 위해 과거 만료 날짜를 디자인에 의해 허용합니다.

## 오류 처리

API는 표준 HTTP 상태 코드를 반환합니다.

| 상태 코드 | 조건 |
|---|---|
| `400` | 유효성 검사 오류입니다. 필수 필드 누락, 잘못된 값 또는 REST 생성 시 만료 날짜가 지났습니다. |
| `401` | 전달자 토큰이 누락되었거나 잘못되었습니다. |
| `403` | 토큰에 필수 ACL 리소스가 없습니다. |
| `404` | 기프트 카드 계정을 찾을 수 없습니다. |
| `409` | 기프트 카드 코드를 복제합니다. |

입력 유효성 검사에는 필수 필드, 값 범위(상태는 `0` 또는 `1`이어야 하며, 상태는 `0`-`3`이어야 하고, 잔액은 음수가 아니어야 함), 날짜 형식 및 형식 안전성이 포함됩니다. 숫자 필드의 숫자가 아닌 값은 거부됩니다.
