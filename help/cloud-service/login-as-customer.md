---
title: 일회성 코드를 사용하여 고객으로 로그인
description: ' [!DNL Adobe Commerce as a Cloud Service]에서 고객 OTC로 로그인 기능을 사용하여 고객 인증을 위한 일회용 코드를 생성하는 방법을 알아봅니다.'
role: Admin
level: Intermediate
badgeSaas: label="SaaS만" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."
source-git-commit: 2de1006ad3cee936d114bcf1b9a98b43a54d8c76
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 0%

---

# 고객으로 로그인

{{accs-sandbox-experimental}}

관리자 사용자는 고객 OTC(1회 코드)로 로그인 기능을 사용하여 고객에 대한 단기간 단일 사용 코드를 생성할 수 있습니다. 이 코드는 GraphQL을 통해 고객 액세스 토큰으로 교환할 수 있으므로 판매자 지원 쇼핑 시나리오에 대해 암호가 없는 **고객으로 로그인** 워크플로우를 사용할 수 있습니다.

고객으로 로그인은 다음 구성 요소로 구성됩니다.

* **관리자 UI** - 고객 편집 페이지에서 관리자는 고객으로 직접 로그인하지 않고 OTC(일회용 코드)를 요청할 수 있습니다.
* **REST API** - 관리 스크립트 및 서드파티 통합에 유용한 OTC 생성을 위한 프로그래밍 종단점입니다.
* **GraphQL API** - 상점 또는 헤드리스 상거래 흐름을 위한 고객 액세스 토큰으로 OTC를 교환하는 돌연변이.

## 관리자로부터 1회 코드 생성

고객 OTC로 로그인 은 고객 편집 페이지의 표준 고객 로그인 단추를 [!UICONTROL **고객 로그인 OTC 가져오기**] 단추로 바꿉니다. 생성된 일회성 코드는 판매자 지원 쇼핑을 위해 상점 또는 GraphQL과 함께 사용할 수 있습니다.

>[!NOTE]
>
>주문, 송장, 배송 및 대변 메모 페이지에서 **고객으로 로그인** 단추를 사용할 수 없습니다.

### 사전 요구 사항

고객으로 로그인 기능을 사용하기 전에 다음 요구 사항을 충족해야 합니다.

* **관리자 권한** - 관리자로 로그인하려면 관리자 사용자의 관리자 역할에서 `Magento_LoginAsCustomer::login` ACL(액세스 제어 목록) 권한을 활성화해야 합니다.

* **고객 동의** - 고객은 `login_as_customer_assistance_allowed` 확장 특성을 **2**(으)로 설정해야 합니다. 이는 관리자의 **고객 편집** 페이지에서 구성하거나 고객을 만들거나 편집할 때 GraphQL을 통해 구성할 수 있습니다.

  ![고객 편집 페이지의 고객 동의 확장 특성 구성](./assets/customer-consent-attribute.png){width="600" zoomable="yes"}

* **고객 확장으로 로그인** - 고객 확장으로 로그인이 비활성화되어 있으면 고객 로그인 기능을 사용할 수 없습니다. 확장이 활성화되었는지 확인하려면 [!UICONTROL **스토어**] > [!UICONTROL **구성**] > [!UICONTROL **고객**] > [!UICONTROL **고객으로 로그인**] > [!UICONTROL **확장 활성화**]&#x200B;로 이동하십시오.

### 일회용 코드 요청(OTC)

1. [!UICONTROL **고객**]&#x200B;(으)로 이동하여 편집 페이지를 열 고객을 선택하십시오.

1. 고객 편집 페이지에서 [!UICONTROL **고객 로그인 OTC 가져오기**]&#x200B;를 클릭합니다.

   ![고객 편집 페이지의 고객 로그인 OTC 가져오기 단추](./assets/get-customer-login-otc-button.png){width="600" zoomable="yes"}

1. [!UICONTROL **이유**]&#x200B;(필수)를 입력하고 [!UICONTROL **요청**]&#x200B;을(를) 클릭합니다.

   이유 필드가 있는 ![OTC 요청 양식](./assets/otc-reason-modal.png){width="600" zoomable="yes"}

   >[!NOTE]
   >
   >**이유** 필드는 필수입니다. OTP 생성 플로우로 전달되며 향후 감사 및 이벤트 로깅 기능에서 사용하도록 예약됩니다.

1. 생성된 OTC가 모달에 표시됩니다. 고객 인증을 위해 이 코드를 `generateCustomerToken` 또는 `exchangeOtpForCustomerToken` GraphQL 돌연변이와 함께 사용하십시오.

   ![생성된 OTC가 모달에 표시됨](./assets/otc-generated-code.png){width="300" zoomable="yes"}

>[!IMPORTANT]
>
>생성된 일회용 코드 OTC는 기본적으로 30초 동안 유효하며 한 번 사용 후 무효화됩니다. [지원 티켓](https://experienceleague.adobe.com/home?support-tab=home#support)을 제출하여 TTL을 구성할 수 있습니다.

일회용 코드가 생성되면 상점으로 이동하여 다음 자격 증명을 사용하여 로그인하면 일회용 코드를 사용할 수 있습니다.

* **이메일**: 고객의 이메일 주소
* **암호**: 생성된 일회용 코드(OTC)

## REST API를 사용하여 일회용 코드 생성

POST `V1/customer/:customerId/otp` 끝점은 고객을 위한 OTC를 체계적으로 생성하는 방법을 제공합니다. 이 기능은 OTC 발급을 일관되게 트리거해야 하는 관리 UI, 스크립트 또는 서드파티 통합에 유용합니다.

### REST 계약

| 항목 | 값 |
|---|---|
| **메서드** | POST |
| **URL** | `/rest/V1/customer/:customerId/otp` |
| **인증** | 관리 토큰(전달자). 필수 ACL: `Magento_LoginAsCustomer::login`. |
| **요청 본문** | 선택적 `reason` 필드가 있는 JSON. 감사 및 로깅에 사용됩니다. |
| **성공 응답** | HTTP 200, `otp`이(가) 있는 JSON(32자 16진수 문자열). |
| **오류 응답** | 표준 웹 API 오류(예: 401, 403). 고객에 대해 고객 지원으로 로그인 이 비활성화된 경우 이 500 또는 매핑된 예외로 표시될 수 있습니다. |

### 요청 예

```text
POST /rest/V1/customer/:customerId/otp
Content-Type: application/json
```

```json
{"reason": "Support session"}
```

### 응답 예

```json
{"otp": "a1b2c3d4e5f6789012345678abcdef01"}
```

## GraphQL을 사용하여 고객 토큰에 대한 일회성 코드 교환

(관리 UI 또는 REST API에서) OTC를 생성한 후 다음 GraphQL 돌연변이 중 하나를 사용하여 고객 액세스 토큰으로 교환합니다.

### `generateCustomerToken` 돌연변이

`generateCustomerToken(email, password)` 돌연변이는 고객 토큰을 반환합니다. `password` 인수는 다음 순서로 평가됩니다.

1. **고객 암호(기본값)** - 고객의 계정 암호입니다.
1. **고객 암호 재설정 토큰(1회 사용)** - **암호 찾기**&#x200B;의 유효한 토큰(예: `requestPasswordResetEmail` 돌연변이). 처음 사용 시 사용됨.
1. **관리자가 생성한 OTC(1회성 코드)** - REST API 또는 관리자 UI를 통해 고객을 위해 관리자가 생성한 코드. 일회성 사용, 단기(기본적으로 30초).

**스키마:**

```graphql
type Mutation {
  generateCustomerToken(email: String!, password: String!): CustomerToken
}

type CustomerToken {
  token: String!
}
```

**예: 관리자 OTC로 로그인**

```graphql
mutation GenerateCustomerToken($email: String!, $password: String!) {
  generateCustomerToken(email: $email, password: $password) {
    token
  }
}
```

변수(OTC를 `password`(으)로 사용):

```json
{
  "email": "customer@example.com",
  "password": "<admin-generated-OTC>"
}
```

**예: 암호를 사용하여 로그인**

```graphql
mutation GenerateCustomerToken($email: String!, $password: String!) {
  generateCustomerToken(email: $email, password: $password) {
    token
  }
}
```

변수:

```json
{
  "email": "customer@example.com",
  "password": "CustomerPassword123"
}
```

**예: 암호 재설정 토큰을 사용하여 로그인**

고객이 암호 재설정을 요청한 후(예: `requestPasswordResetEmail`) 이메일 링크를 통해 받은 재설정 토큰을 `password`의 `generateCustomerToken`(한 번 사용)로 사용할 수 있습니다.

```graphql
mutation GenerateCustomerToken($email: String!, $password: String!) {
  generateCustomerToken(email: $email, password: $password) {
    token
  }
}
```

변수(`password`(으)로 재설정 토큰 사용):

```json
{
  "email": "customer@example.com",
  "password": "<reset-password-token-from-email-link>"
}
```

**응답 예:**

```json
{
  "data": {
    "generateCustomerToken": {
      "token": "<customer-access-token>"
    }
  }
}
```

### `exchangeOtpForCustomerToken` 돌연변이

`exchangeOtpForCustomerToken` 돌연변이는 관리자가 생성한 암호 재설정 토큰 또는 OTP를 고객 액세스 토큰으로 교환합니다. 성공적으로 교환한 후 OTP가 무효화됩니다(1회 사용). 이 끝점은 reCAPTCHA 구성을 준수합니다.

**스키마:**

```graphql
type Mutation {
  exchangeOtpForCustomerToken(
    email: String!
    otp: String!
  ): CustomerToken
}

type CustomerToken {
  token: String!
}
```

**예제 요청:**

```graphql
mutation ExchangeOtpForCustomerToken($email: String!, $otp: String!) {
  exchangeOtpForCustomerToken(email: $email, otp: $otp) {
    token
  }
}
```

변수:

```json
{
  "email": "customer@example.com",
  "otp": "<one-time-password>"
}
```

**응답 예:**

```json
{
  "data": {
    "exchangeOtpForCustomerToken": {
      "token": "<customer-access-token>"
    }
  }
}
```

### 돌연변이 요약

| 돌연변이 | 사용 사례 |
|---|---|
| `generateCustomerToken(email, password)` | 단일 진입점: 고객 암호, 암호 재설정 토큰, 관리자 OTC 또는 OTP(암호/재설정 후 시도). |
| `exchangeOtpForCustomerToken(email, otp)` | OTP 또는 암호 재설정 토큰 교환. OTP(또는 암호 재설정 토큰)는 사용 후 사용됩니다. |

암호 재설정 토큰과 관리자 OTC가 모두 `password`에 `generateCustomerToken` 인수로 전달됩니다. 확인자가 토큰 유형을 감지하고 그에 따라 확인합니다.
