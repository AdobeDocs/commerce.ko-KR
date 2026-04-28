---
title: '[!DNL Adobe Commerce as a Cloud Service] 릴리스 정보'
description: ' [!DNL Adobe Commerce as a Cloud Service]의 최신 기능 및 개선 사항에 대해 알아봅니다.'
feature-set: Commerce
feature: App Builder, GraphQL, Integration, Saas
role: Admin, Developer, User, Leader
level: Beginner
badgeSaas: label="SaaS만" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."
exl-id: cf06dec6-8d6b-413e-9977-df88373c188e
source-git-commit: aad22963d5519bd5a1d353b2e411bb011fea56fa
workflow-type: tm+mt
source-wordcount: '3289'
ht-degree: 0%

---

# 릴리스 정보

다음 릴리스 노트에는 [!DNL Adobe Commerce as a Cloud Service]에 대한 업데이트가 포함되어 있습니다.

>[!NOTE]
>
>Adobe Commerce 온-프레미스 또는 Adobe Commerce 온-클라우드 인프라를 사용하는 경우 [Adobe Commerce 릴리스 노트](https://experienceleague.adobe.com/en/docs/commerce-operations/release/notes/overview)를 참조하십시오.

## 2026년 4월 - 릴리스 #3 {#latest}

[!BADGE 프로덕션]{type=Neutral tooltip="나열된 항목은 현재 프로덕션 환경에서 사용할 수 있습니다."}

<!-- [!BADGE Sandbox]{type=Caution tooltip="The items listed are currently only available in Sandbox environments. Adobe makes new releases available in Sandbox environments first to provide time to test upcoming changes before the release is available on Production environments."} -->

다음 항목은 2026년 4월 27일에 프로덕션 환경에 릴리스되었습니다.

>[!BEGINSHADEBOX]

### 개선 사항 및 버그 수정

이 릴리스에는 다음과 같은 개선 사항, 최적화 및 버그 수정이 포함되어 있습니다.

* 상태가 할당된 구성된 모든 주문 상태를 검색하기 위해 `GET /V1/order-statuses` REST API 끝점을 추가했습니다. <!-- CEXT-6100 -->

* 주문, 장바구니, 송장, 메모 및 회사와 같은 엔터티에 대한 `custom_attributes`이(가) REST 스키마에 표시되지 않는 문제를 해결했습니다. <!-- CCSAAS-4818 -->

* 비동기 대량 API 소비자의 중복 메시지 처리 오류(`MessageLockException`)를 해결했습니다. <!-- CCSAAS-4805 -->

* 이제 필터 옵션에 대해 제품 특성을 사용하도록 설정한 경우 [!DNL Commerce Admin] 제품 표에서 부터/까지 범위 필터로 제품 특성 번호를 렌더링합니다. <!-- ACCS-761 -->

* [!DNL AEM Assets]을(를) 사용할 때 장바구니 포기 알림 이메일에 제품 이미지가 표시되지 않는 문제를 해결했습니다. <!-- ACCS-798 -->

* 다운로드 가능한 제품에 파일, 샘플 또는 링크를 추가할 때 잘못된 &quot;최대 업로드 크기&quot; 오류가 표시되는 문제를 해결했습니다. <!-- ACCS-813 -->

* 여러 공유 카탈로그에 할당된 제품을 저장하면 오류가 발생하는 문제를 해결했습니다. <!-- ACCS-788 -->

* 주문 내역 쿼리가 느려지고 주문이 많은 회사에서 데이터베이스 메모리 부족 오류가 발생할 수 있는 문제를 해결했습니다. <!-- ACCS-808 -->

* 가져오기 파일 유효성 검사가 실패할 수 있는 문제를 해결했습니다. <!-- CCSAAS-4364 -->

* [!DNL Adobe Commerce as a Cloud Service] 관리에서 지원되지 않으므로 **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**&#x200B;의&#x200B;**[!UICONTROL Catalog]**&#x200B;섹션에서&#x200B;**[!UICONTROL Recently Viewed/Compared Products]**&#x200B;구성을 제거했습니다. <!-- ACCS-793 -->

{{accs-release}}

>[!ENDSHADEBOX]

## 2026년 4월 - 릴리스 #2

[!BADGE 프로덕션]{type=Neutral tooltip="나열된 항목은 현재 프로덕션 환경에서 사용할 수 있습니다."}

<!-- [!BADGE Sandbox]{type=Caution tooltip="The items listed are currently only available in Sandbox environments. Adobe makes new releases available in Sandbox environments first to provide time to test upcoming changes before the release is available on Production environments."} -->

다음 항목은 2026년 4월 16일에 프로덕션 환경에 릴리스되었습니다.

>[!BEGINSHADEBOX]

### 웹후크를 사용하여 사용자 정의 견적 합계 구현

이제 [!DNL Adobe Commerce as a Cloud Service]에서 `plugin.magento.out_of_process_totals_collector.api.get_total_modifications.execute` [webhook](https://developer.adobe.com/commerce/extensibility/webhooks/)을(를) 사용할 수 있습니다. 프로세스 외부 확장성을 통해 사용자 정의 견적 합계 수정 사항을 구현하는 데 사용합니다. <!-- CEXT-5896 -->

### 재사용 가능한 이메일 미리 알림 규칙(실험적)

>[!IMPORTANT]
>
>이 기능은 실험적인 기능이며 Adobe Commerce 고객 성공 관리자에게 문의하거나 지원 티켓을 만들어 활성화해야 합니다.

[전자 메일 미리 알림 규칙](https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/communications/email-reminders/email-reminder-rules#rule-repeatability)은(는) 이제 원래 트리거 조건이 더 이상 적용되지 않은 후에 동일한 규칙을 고객에게 다시 적용할 수 있도록 하는 선택적 규칙 재사용 가능성 설정을 지원합니다.

예를 들어 고객이 장바구니를 포기하고, 구매를 완료하고, 나중에 새 장바구니를 포기하는 경우 규칙이 다시 트리거될 수 있습니다. 이 설정이 없으면 원래 트리거를 지우는 고객은 동일한 규칙의 향후 일치에서 영구적으로 제외됩니다.

### 결제 서비스 거래 보고서 보기

[[!DNL Payment Services]](https://experienceleague.adobe.com/en/docs/commerce/payment-services/get-started/production)을(를) 활성화한 경우 이제 [!DNL Commerce Admin]에서 [대시보드 UI](../payment-services/payments-home.md)을(를) 사용할 수 있으며, 결제 거래를 보고 관리하기 위해 [거래 보고서](../payment-services/reporting.md#transactions-report-view)에 액세스할 수 있습니다. <!-- PAY-6510 -->

### 개선 사항 및 버그 수정

이 릴리스에는 다음과 같은 개선 사항, 최적화 및 버그 수정이 포함되어 있습니다.

* 공유 카탈로그 회사 할당 페이지에서 관리 UI SDK에 큰 공유 카탈로그를 사용할 때 발생할 수 있는 500 오류를 수정했습니다. <!-- CCSAAS-4783 -->

* 고객이 회사에 할당되기 전에 해당 주문이 이루어진 경우 회사 고객이 자신의 주문을 볼 수 없었던 문제를 수정했습니다. <!-- ACCS-746 -->

{{accs-release}}

>[!ENDSHADEBOX]

## 2026년 4월

[!BADGE 프로덕션]{type=Neutral tooltip="나열된 항목은 현재 프로덕션 환경에서 사용할 수 있습니다."}

다음 항목은 2026년 4월 1일에 프로덕션 환경에 릴리스되었습니다.

>[!BEGINSHADEBOX]

### 제품에 파일 추가

[!DNL Adobe Commerce as a Cloud Service]은(는) 이제 파일 형식 제품 특성을 사용하여 [제품에 파일 추가](./product-files.md)를 지원합니다. REST API를 통해 프로그래밍 방식으로 제품 편집 페이지에서 수동으로 파일을 업로드하거나, 외부 URL을 CSV로 제공하여 대량으로 파일을 업로드할 수 있습니다. <!-- ACCS-535, ACCS-565 -->

### GraphQL을 통해 가격 및 스톡 경고 구독 상태 확인

새 GraphQL 쿼리 [`isSubscribedProductAlertStock`](https://developer.adobe.com/commerce/webapi/graphql/schema/products/queries/is-subscribed-product-alert-stock/){target="_blank"} 및 [`isSubscribedProductAlertPrice`](https://developer.adobe.com/commerce/webapi/graphql/schema/products/queries/is-subscribed-product-alert-price/){target="_blank"}을(를) 통해 상점 첫 화면에서 쇼핑객이 이미 제품에 대한 주식 또는 가격 알림을 구독했는지 여부를 확인할 수 있습니다. <!-- ACCS-334 -->

### 음수 값을 지원하는 숫자 제품 속성 만들기

새 `numeric` [제품 특성 입력 형식](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/attributes-input-types)을(를) 사용하면 판매자는 음수 값을 지원하는 10진수 특성을 만들 수 있습니다. <!-- ACCS-600 -->

### 하나의 GraphQL 요청에서 여러 양식에 대한 쿼리 reCAPTCHA 구성

[`recaptchaFormConfigs` 쿼리](https://developer.adobe.com/commerce/webapi/graphql/schema/store/queries/recaptcha-form-configs/)은(는) 단일 요청에서 여러 양식 유형에 대한 구성 세부 정보를 반환할 수 있습니다. <!-- ACCS-628 -->

### 새 B2B 권한으로 모든 회사 주문 보기

새 `view_all_company_orders` [회사 역할](https://developer.adobe.com/commerce/webapi/rest/b2b/roles/)을(를) 사용하면 B2B 회사 고객은 관리자 사용자가 만든 이전 주문을 포함하여 회사 내의 모든 주문을 볼 수 있습니다. <!-- ACCS-675 -->

### 개선 사항 및 버그 수정

이 릴리스에는 다음과 같은 개선 사항, 최적화 및 버그 수정이 포함되어 있습니다.

* 이제 적용 가능한 사용자 지정 특성을 사용하여 주문 및 회사 REST API 결과를 필터링할 수 있으며, 회사 범위 주문 검색과 같은 시나리오를 지원합니다. <!-- ACCS-633 -->

* 브라우저 개발자 콘솔에 나타날 수 있는 오류를 해결했습니다. <!-- CCSAAS-4650 -->

* 주문 댓글이 있는 손님 주문을 취소할 때 발생할 수 있는 오류를 수정했습니다. <!-- ACCS-674 -->

* 연관된 품목이 많은 그룹화된 제품을 구매요청 목록에 추가할 때 발생할 수 있는 오류를 수정했습니다. <!-- ACCS-627 -->

>[!ENDSHADEBOX]

## 2026년 3월 - 릴리스 #2

[!BADGE 프로덕션]{type=Neutral tooltip="나열된 항목은 현재 프로덕션 환경에서 사용할 수 있습니다."}

다음 항목은 2026년 3월 24일에 프로덕션 환경에 릴리스되었습니다.

>[!BEGINSHADEBOX]

### 일회용 코드를 사용하여 고객으로 로그인

이제 관리자는 [!DNL Commerce Admin] 및 REST API를 통해 고객 가장에 대해 [일회성 코드](https://experienceleague.adobe.com/en/docs/commerce-admin/customers/customer-accounts/manage/login-as-customer)을(를) 생성할 수 있습니다. `generateCustomerToken` 또는 `exchangeOtpForCustomerToken` GraphQL 돌연변이를 통해 일회성 코드를 고객 액세스 토큰으로 교환할 수 있으므로 판매자 지원 쇼핑 시나리오에 대해 암호 없는 &quot;고객으로 로그인&quot; 흐름이 가능합니다. <!-- ACCS-404 -->

API를 사용하여 이 기능을 구현하는 방법에 대한 지침은 [REST API](https://developer.adobe.com/commerce/webapi/rest/saas-integrations/login-as-customer/) 및 [GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/generate-token/) 설명서를 참조하십시오.

### REST API를 통해 기프트 카드 계정 관리

이제 REST API를 통해 [기프트 카드 계정](https://developer.adobe.com/commerce/webapi/rest/saas-integrations/gift-card-accounts/)을 만들고, 업데이트하고, 삭제하고, 쿼리할 수 있습니다. 또한 `/V1/import/json` 끝점을 통해 JSON 대량 가져오기 지원을 사용할 수 있으므로 서드파티 통합에서 기프트 카드를 프로그래밍 방식으로 동기화할 수 있습니다. <!-- ACCS-476 -->

### REST API를 통해 트랜잭션 이메일 트리거

새 REST API 끝점(`POST /V1/custom-email/send`)을 사용하면 전자 메일 템플릿 ID, 받는 사람 전자 메일 및 템플릿 변수를 지정하여 요청 시 [트랜잭션 전자 메일을 트리거](https://developer.adobe.com/commerce/webapi/rest/saas-integrations/custom-email/)할 수 있습니다. API는 복잡한 이메일 콘텐츠에 대한 템플릿 변수로 중첩된 배열을 지원합니다. <!-- ACCS-325, ACCS-481 -->

### Out-of-process 배송 요금 웹후크 구독

이제 [!DNL Adobe Commerce as a Cloud Service]의 관리 웹후크 목록에서 `plugin.out_of_process_shipping_methods.api.shipping_rate_repository.get_rates` 웹후크를 사용할 수 있습니다. [사용자 지정 배송 방법](https://developer.adobe.com/commerce/extensibility/starter-kit/checkout/shipping-use-cases/#shipping-methods)을 구현하는 데 사용합니다. <!-- ACCS-478 -->

### 제품 속성을 통해 PDF 및 기타 파일 업로드

새 &quot;file&quot; [특성 입력 형식](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/attributes-input-types)을(를) 사용하면 PDF와 같은 파일을 개별 제품에 업로드할 수 있는 특성 집합을 만들 수 있습니다. [!UICONTROL **스토어**] > [!UICONTROL **구성**] > [!UICONTROL _카탈로그_] > [!UICONTROL **제품 파일 특성**]&#x200B;으로 이동하여 허용되는 파일 확장명과 최대 파일 크기를 구성할 수 있습니다. <!-- ACCS-535, ACCS-565 -->

### 회사 사용자 지정 속성 구성

이제 관리자는 [!DNL Commerce Admin]의 회사 편집 페이지에서 회사 사용자 지정 특성을 관리할 수 있습니다. [!DNL Adobe Commerce as a Cloud Service]의 관리 UI에서 사용자 지정 특성을 구성, 저장 및 확인할 수 있습니다.

회사 사용자 지정 특성을 구성하려면 [!UICONTROL **고객**] > [!UICONTROL **회사**]&#x200B;(으)로 이동하고 회사를 선택하여 편집 페이지를 엽니다. 그런 다음 [!UICONTROL **사용자 지정 특성**] 탭을 선택하여 새 특성을 추가합니다.
<!-- ACCS-294 -->

### GraphQL을 통해 가격 및 주식 알림 구독

이제 EDS 상점 전면이 [가격 및 재고 알림](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/configuration/product-alerts/alert-setup)과(와) 함께 작동합니다. <!-- ACCS-334 -->

또한 가격 및 재고 경고를 구독하거나 구독 취소하는 몇 가지 새로운 GraphQL 돌연변이가 있습니다.

+++새로운 GraphQL 돌연변이

```graphql
mutation {
  subscribeProductAlertStock(input: { sku: "ADB111" }) {
    success
    message
  }
}
```

```graphql
mutation {
  unsubscribeProductAlertStock(input: { sku: "ADB111" }) {
    success
    message
  }
}
```

```graphql
mutation {
  unsubscribeProductAlertStockAll {
    success
    message
  }
}
```

```graphql
mutation {
  subscribeProductAlertPrice(input: { sku: "ADB112" }) {
    success
    message
  }
}
```

```graphql
mutation {
  unsubscribeProductAlertPrice(input: { sku: "ADB115" }) {
    success
    message
  }
}
```

```graphql
mutation {
  unsubscribeProductAlertPriceAll {
    success
    message
  }
}
```

+++

### 개선 사항 및 버그 수정

이 릴리스에는 다음과 같은 개선 사항, 최적화 및 버그 수정이 포함되어 있습니다.

* [!UICONTROL Sales] > [!UICONTROL View Orders] 회사 역할이 이제 예상대로 작동합니다. <!-- ACCS-604 -->

* 이제 REST API를 통해 `last_login_at` 고객 확장 특성을 사용할 수 있으므로 통합에서 각 고객의 최신 로그인 날짜를 검색할 수 있습니다. <!-- ACCS-555 -->

* [!DNL AEM Assets] 통합 양식 제안 문제를 해결했습니다. <!-- ACCS-209 -->

* 공유 카탈로그 그리드에 대한 대량 회사 할당 및 할당 해제 작업으로 인해 오류가 발생하는 문제를 해결했습니다. <!-- CCSAAS-4614 -->

* 동일한 제품을 다른 수량 또는 사용자 지정 가격으로 장바구니에 다시 추가할 때 사용자 지정 장바구니 가격이 덮어쓰기되는 문제가 해결되었습니다. <!-- ACCS-529 -->

* 이제 구매요청 목록 품목 UID가 장바구니 및 위시리스트 품목 UID와 일치합니다. <!-- ACCS-349 -->

* 대형 공유 카탈로그에서 발생할 수 있는 제품 편집 페이지 시간 제한을 수정했습니다. <!-- CCSAAS-4657 -->

* 관리자 통합을 위해 GET `/V1/directory/countries` 및 GET `/V1/directory/countries/:countryId` REST API 끝점을 다시 활성화하여 클라이언트가 유효한 국가 및 지역 데이터를 조회할 수 있도록 합니다. <!-- ACCS-518 -->

* 사용자에게 큰 공유 카탈로그가 있을 때 REST API에서 발생할 수 있는 시간 초과 문제를 해결했습니다. <!-- ACCS-4657 -->

* 차단된 B2B 회사가 여전히 장바구니에 제품을 추가할 수 있는 문제를 해결했습니다. <!-- ACCS-552 -->

* 고객 또는 회사 그리드에 대량의 데이터가 있는 경우 오류를 방지하기 위해 내보내기 단추를 더 이상 사용할 수 없습니다. <!-- ACCS-320 -->

* 첨부 파일 크기가 올바르게 표시되지 않던 문제를 수정했습니다. <!-- ACCS-566 -->

* [!DNL Commerce Admin]에서 &quot;File&quot; 특성 유형을 만들고 삭제하는 문제를 해결했습니다. <!-- ACCS-605, ACCS-606 -->

>[!ENDSHADEBOX]


## 2026년 3월 - 릴리스 #1

[!BADGE 프로덕션]{type=Neutral tooltip="나열된 항목은 현재 프로덕션 환경에서 사용할 수 있습니다."}

다음 항목은 2026년 3월 9일에 [!DNL Adobe Commerce as a Cloud Service]의 프로덕션 환경에 릴리스되었습니다.

>[!BEGINSHADEBOX]

### App Builder AI 코딩 도구 및 자습서

이제 [AI 코딩 개발자 도구](https://developer.adobe.com/commerce/extensibility/developer-agent/){target="_blank"}를 사용하여 새 [!DNL App Builder] 응용 프로그램을 만들고 기존 [!DNL Adobe Commerce] PHP 확장을 [!DNL App Builder] 응용 프로그램으로 변환할 수 있습니다. 다음 튜토리얼을 통해 도구 사용 방법을 확인할 수 있습니다.

* [자습서 사전 요구 사항](./tutorials/tutorial-prerequisites.md)
* [등급 확장 튜토리얼](./tutorials/ratings-extension.md)
* [배송 방법 확장 튜토리얼](./tutorials/shipping-method-extension.md)

### 관리를 통해 App Builder 앱 관리에 액세스

이제 [!DNL Commerce Admin]에 Commerce 인스턴스와 연결된 [!DNL App Builder]개의 앱을 관리하기 위한 통합 셸인 [앱 관리](https://developer.adobe.com/commerce/extensibility/app-management/){target="_blank"}에 연결되는 메뉴 항목이 포함되어 있습니다. 이 추가는 최신 관리 UI SDK 업데이트를 통해 제공됩니다. <!-- CEXT-5755 -->

### 요청 엔티티 생성 제한 변경

기존에는 홈페이지, 스토어, 스토어 조회수 제한이 50개로 제한됐다. 필요한 경우 [지원 요청](https://experienceleague.adobe.com/home?support-tab=home#support)을 제출하여 이러한 제한을 수정할 수 있습니다. <!-- ACCS-398 -->

### 구조화된 오류 코드로 상점 인증 메시지 사용자 지정

이제 [`generateCustomerToken` GraphQL 돌연변이](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/generate-token/){target="_blank"}이(가) 오류 메시지와 함께 형식화된 오류 코드를 반환하여 상점 앞에 실패 이유별 특정 UI 메시지를 표시할 수 있습니다. 사용 가능한 오류 코드에는 `CUSTOMER_MISSING_EMAIL`, `CUSTOMER_MISSING_PASSWORD`, `CUSTOMER_SIGN_IN_INCORRECT_OR_LOCKED`, `CUSTOMER_ACCOUNT_NOT_CONFIRMED` 및 `CUSTOMER_GENERIC_ERROR`이(가) 포함됩니다. <!-- ACCS-301 -->

### 장바구니 및 위시리스트 비활동에 대한 자동 이메일 미리 알림 보내기

[전자 메일 미리 알림 모듈](https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/communications/email-reminders/email-reminder-rules)&#x200B;(`Magento_Reminder`)이(가) 이제 [!DNL Adobe Commerce as a Cloud Service]에서 활성 상태이므로 가맹점은 장바구니 및 위시리스트 비활성에 따라 고객에게 전자 메일을 트리거하는 자동화된 미리 알림 규칙을 만들 수 있습니다. <!-- CCSAAS-4597 -->

### 범주 삭제 이벤트 웹후크 구독

이제 [!DNL Adobe Commerce as a Cloud Service]에서 `observer.catalog_category_delete_before` 웹후크를 사용할 수 있습니다. 범주를 삭제하기 전에 논리를 실행하는 데 사용합니다. <!-- CEXT-5862 -->

### 등록된 이메일과 함께 수행한 게스트 주문 추적

새로운 선택적 저장소 수준 구성을 사용하면 등록된 고객 계정과 일치하는 이메일 주소를 사용하여 주문한 경우 고객이 수행한 게스트 주문을 [추적](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/point-of-purchase/checkout/checkout-guest#allow-guest-order-access-for-registered-emails)할 수 있습니다. <!-- ACCS-289 -->

### 개선 사항 및 버그 수정

이 릴리스에는 다음과 같은 개선 사항, 최적화 및 버그 수정이 포함되어 있습니다.

* 일부 조직 관리자가 테넌트당 권한 없이 테넌트 인스턴스에 잘못 액세스할 수 있는 문제가 수정되었습니다. <!-- ACCS-335 -->

* 공유 카탈로그를 변경할 때 [!DNL Commerce Admin]에서 사용자를 로그아웃할 수 있는 문제를 해결했습니다. <!-- ACCS-318 -->

* 일부 웹후크 필드가 [!DNL Commerce Admin] UI에 잘못 표시되는 문제를 해결했습니다. <!-- CEXT-5874 -->

>[!ENDSHADEBOX]

## 2026년 2월 - 릴리스 #2

[!BADGE 프로덕션]{type=Neutral tooltip="나열된 항목은 현재 프로덕션 환경에서 사용할 수 있습니다."}

다음 항목은 2026년 2월 24일에 [!DNL Adobe Commerce as a Cloud Service]의 프로덕션 환경에 릴리스되었습니다.

>[!BEGINSHADEBOX]

### 상거래 이벤트를 사용하여 컨텍스트 필드 보내기

이제 [!DNL Adobe Commerce as a Cloud Service]이(가) 이벤트 페이로드에서 [컨텍스트 필드](https://developer.adobe.com/commerce/extensibility/events/context-fields/)를 지원하므로 기본적으로 이벤트에 포함되지 않은 데이터를 포함할 수 있습니다. <!-- CEXT-5713 -->

### 새 웹후크를 사용하여 견적 항목 저장 이벤트에 가입

이제 [!DNL Adobe Commerce as a Cloud Service]에서 `observer.sales_quote_item_save_before` 웹후크를 사용할 수 있습니다. 견적 항목이 저장되기 전에 논리를 실행하는 데 사용합니다. <!-- ACCS-346 -->

### 개선 사항 및 버그 수정

이 릴리스에는 다음과 같은 개선 사항, 최적화 및 버그 수정이 포함되어 있습니다.

* [!DNL Commerce Admin] 제품 목록에서 표시 문제를 일으킬 수 있는 오류를 해결했습니다. 이제 제품 목록에서 성능을 개선하기 위해 표시되는 공유 카탈로그 수를 제한합니다. <!-- CCSAAS-1242 -->

* 사용자 지정 가능한 기프트 카드를 장바구니에 추가하지 못하는 GraphQL 오류를 수정했습니다. <!-- ACCS-313 -->

>[!ENDSHADEBOX]

## 2026년 2월 - 릴리스 #1

[!BADGE 프로덕션]{type=Neutral tooltip="나열된 항목은 현재 프로덕션 환경에서 사용할 수 있습니다."}

다음 항목은 2026년 2월 10일에 [!DNL Adobe Commerce as a Cloud Service]의 프로덕션 환경에 릴리스되었습니다.

>[!BEGINSHADEBOX]

### 배송 방법 사용자 지정 및 관리 보고서 보기

[!DNL Commerce Admin]에 다음과 같은 기능이 개선되었습니다.

* 배송 주소 사용자 지정 특성을 포함하도록 [배송 웹후크 페이로드](https://developer.adobe.com/commerce/extensibility/starter-kit/checkout/shipping-use-cases/#payload)를 프로세스 외부에서 개선했습니다. 이 변경으로 판매자는 사용자 정의 배송 방법을 구현할 수 있습니다. <!-- ACCS-235 -->

* [고객](https://experienceleague.adobe.com/en/docs/commerce-admin/start/reporting/customer-reports), [마케팅](https://experienceleague.adobe.com/en/docs/commerce-admin/start/reporting/marketing-reports), [제품](https://experienceleague.adobe.com/en/docs/commerce-admin/start/reporting/product-reports) 및 [판매](https://experienceleague.adobe.com/en/docs/commerce-admin/start/reporting/sales-reports)에 대한 보고서를 포함하는 관리 보고서에 대한 액세스 권한을 추가했습니다. <!-- CCSAAS-3085 -->

>[!NOTE]
>
>[!DNL Adobe Commerce as a Cloud Service]에서 사용할 수 없는 보고서는 PaaS로만 레이블 지정([!BADGE PaaS만]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce 온 클라우드 프로젝트(Adobe 관리 PaaS 인프라) 및 온프레미스 프로젝트에만 적용됩니다."})됩니다.

### REST API를 통해 사용자 지정 송장 금액 캡처

이제 Invoice API가 확장 특성을 사용하여 [사용자 지정 캡처 양](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/invoices#custom-capture-amounts)을 지원합니다. <!-- ACCS-186, ACCS-197, ACCS-143 -->

>[!NOTE]
>
>법적 제한으로 인해 사용자 정의 캡처 금액은 북미(NA) 지역 및 결제 오버캡처가 허용된 기타 지역에서만 사용할 수 있습니다.

### 개선 사항 및 버그 수정

이 릴리스에는 다음과 같은 개선 사항, 최적화 및 버그 수정이 포함되어 있습니다.

* API 또는 가져오기를 통해 만든 모든 사용자 지정 쿠폰을 표시하도록 쿠폰 그리드 필터를 수정했습니다. <!-- CCSAAS-4509 -->

* `save_in_address_book`이(가) `true`(으)로 설정되어 있어도 `setNegotiableQuoteShippingAddress` 돌연변이가 수동으로 입력한 주소를 고객 주소록에 저장하지 않는 [!DNL Storefront Compatibility B2B Package]의 문제를 해결했습니다. <!-- LYNX-1031 -->

<!-- The above change will also be covered by the B2B changelog published on February 13, 2026. -->

* 자산 역할과 관련된 사용자 지정 특성에서 `no_selection` 값이 손상되어 [!DNL Edge Delivery Services]에서 제품 이미지가 제대로 표시되지 않는 문제를 해결했습니다. <!-- ACAP-1206 -->

* 이름 또는 성 값이 null인 페더레이션 사용자 계정이 Commerce 관리자에 액세스할 수 없는 문제를 해결했습니다. <!-- ACCS-200 -->

* 지역별 IMS 클라이언트 ID를 자동으로 제공하여 자산 선택기 구성을 간소화했습니다. 판매자는 더 이상 제품 범주 이미지를 자산과 매핑하기 위해 자산 선택기를 구성하기 위해 지원 티켓을 제출할 필요가 없습니다. 이제 시스템에서 Commerce 지역을 기반으로 전용 IMS 클라이언트 ID를 자동으로 사용합니다. <!-- ACCS-175 -->

* 다양한 성능 및 최적화 개선 사항. <!-- CCSAAS-4485, CCSAAS-4497, ACCS-196 -->

>[!ENDSHADEBOX]

## 2026년 1월

[!BADGE 프로덕션]{type=Neutral tooltip="나열된 항목은 현재 프로덕션 환경에서 사용할 수 있습니다."}

다음 항목은 2026년 1월 20일에 [!DNL Adobe Commerce as a Cloud Service]의 프로덕션 환경에 릴리스되었습니다.

>[!BEGINSHADEBOX]

### B2B 드롭다운

B2B 드롭인 구성 요소는 다음과 같이 변경되었습니다.

* 이제 [!DNL Commerce Storefront on Edge Delivery Services]에 [B2B 끌어 놓기 구성 요소](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/)가 포함됩니다. 이제 다음 B2B 드롭인을 사용할 수 있습니다.

   * **[회사 관리](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/company-management/)** - Adobe Commerce 상점에 대한 회사 프로필 관리 및 역할 기반 권한을 사용하도록 설정합니다.
   * **[회사 전환기](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/company-switcher/)** - 사용자가 연결된 여러 회사 간에 전환할 수 있는 UI 구성 요소를 제공합니다.
   * **[구매 주문](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/purchase-order/)** - B2B 트랜잭션에 대한 구매 주문 워크플로, 승인 규칙 및 구매 주문 내역을 관리합니다.
   * **[견적 관리](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/quote-management/)** - 견적 요청, 협상 및 승인 워크플로를 통해 B2B 고객을 위해 협상할 수 있는 견적을 사용하도록 설정합니다.
   * **[구매요청 목록](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/requisition-list/)** - 반복 구매 및 대량 주문을 위한 구매요청 목록을 만들고 관리하는 도구를 제공합니다.

* B2B Storefront 호환성 패키지를 출시했습니다. 이 패키지는 B2B 시스템의 개발을 개선하는 데 도움이 되도록 [!DNL Adobe Commerce] B2B GraphQL 스키마를 향상시킵니다.

<!-- 
* [!DNL Commerce Storefront on Edge Delivery Services] now includes [B2B drop-in components](http://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/). For a complete list of available B2B drop-in blocks, refer to the [storefront documentation](http://experienceleague.adobe.com/developer/commerce/storefront/merchants/b2b-commerce-blocks/).

* Released the [B2B Storefront Compatibility Package](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/storefront-compatibility-b2b/). This package enhances the [!DNL Adobe Commerce] B2B GraphQL schema to help improve development on B2B systems. 
-->

### 외부 배송 추적기에 대한 클릭 가능한 링크

[사용자 지정 추적 URL을 사용](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/delivery/shipping-settings#shipment-tracking-urls)하여 쇼핑객 전자 메일에 포함된 배송 추적 번호를 일반 텍스트에서 클릭 가능한 링크로 변환합니다. 이 기능은 USPS, UPS, FedEx 및 DHL에서 지원됩니다. <!-- See PR #716 in commerce-admin -->

### Google reCAPTCHA Enterprise 지원

[!DNL Adobe Commerce as a Cloud Service] 상점이 이제 [reCAPTCHA Enterprise](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/security/captcha/security-google-recaptcha-enterprise)을(를) 지원합니다. 이 기능은 적응형 위험 분석 및 머신 러닝을 사용하여 인간 사용자를 자동화된 봇과 정확하게 구별하여 고급 봇 보호를 제공합니다. 사이트 보안을 강화하고 사기 행위를 방지하며 스팸 및 남용을 줄여 신뢰할 수 있는 쇼핑 경험을 유지합니다. <!-- CCSAAS-4242 -->

### 인스턴스별 관리자 액세스

이제 Admin Console에서 [사용자에게 개별 [!DNL Adobe Commerce as a Cloud Service] 인스턴스에 액세스 권한을 할당](./user-management.md#add-users)할 수 있습니다. <!-- CCSAAS-4337 -->
<!-- See PR #332 -->

### 가시성

[!DNL App Builder]을(를) 사용하면 이제 자동으로 사용할 수 있는 [OpenTelemetry observability](https://developer.adobe.com/commerce/extensibility/observability/)을(를) 사용하여 [!DNL Adobe Commerce as a Cloud Service] 인스턴스에 대한 더 깊은 가시성을 얻을 수 있습니다. OpenTelemetry는 성능 모니터링, 문제 해결 속도 향상 및 상점 최적화에 도움이 되는 지표, 로그 및 추적을 제공합니다. 이 기능을 통해 시스템 상태에 대한 사전 예방적 통찰력을 확보하고 고객의 안정성을 향상시킬 수 있습니다.

>[!NOTE]
>
>OpenTelemetry 가시성을 사용하려면 [!DNL App Builder] 또는 기타 OOPE(Out-of-Process Extensibility) 서비스를 사용해야 합니다.

### 카탈로그 가격 규칙에 대한 계층 가격 책정

이제 [카탈로그 가격 규칙](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/pricing/product-price-tier#enable-tier-pricing-for-catalog-price-rules)을 사용하여 계층화된 가격 할인과 카탈로그 규칙 할인을 결합할 수 있습니다. 이 향상된 기능을 통해 보다 역동적이고 경쟁력 있는 가격 전략을 수립하고 일괄 구매에 대한 보상을 제공하는 동시에 판촉 할인을 적용할 수 있습니다. 따라서 고객을 유치하고 주문 가치를 높이며 전환을 유도하는 유연성이 향상됩니다.<!-- See PR #708 in commerce-admin -->

### 개선 사항 및 버그 수정

이 릴리스에 포함된 다음과 같은 선택된 개선 사항, 최적화 및 버그 수정 사항:

* 파일을 S3에 업로드할 때 발생할 수 있는 오류를 해결했습니다. <!-- CCSAAS-4189 -->

* Commerce 관리자에 로그인하거나 REST API에 액세스할 때 발생할 수 있는 `User is not entitled to access this instance` 오류를 해결했습니다. <!-- CCSAAS-4324 -->

* 뉴스레터 템플릿 그리드에서 뉴스레터를 미리 보거나 큐에 추가할 때 발생하는 오류를 수정했습니다. <!-- CCSAAS-4398 -->

* 관리 대시보드에서 [!UICONTROL **데이터 다시 로드**] 단추를 클릭할 때 발생하는 `404` 오류를 수정했습니다. <!-- CCSAAS-4468 -->

* [!DNL AEM Assets integration]이(가) 활성화되어 있고 제품에 이미지가 있을 때 REST API를 통해 제품 사용자 지정 특성을 업데이트할 수 없는 문제를 해결했습니다. <!-- ACAP-1178 -->

* 다양한 성능 및 최적화 개선 사항.
<!-- CCSAAS-4255 -->
<!-- CCSAAS-4233 -->
<!-- CCSAAS-4220 -->
<!-- CCSAAS-4252 -->
<!-- CCSAAS-4330 -->
<!-- CCSAAS-3669 -->
<!-- CCSAAS-4462 -->

>[!ENDSHADEBOX]

## 2025년 11월

>[!BEGINSHADEBOX]

### 향상된 기능

* [사용자 관리](./user-management.md) - Commerce 관리자에 대한 사용자 액세스를 자동으로 업데이트하기 위해 Admin Console에서 **제품 관리자** 역할을 변경했습니다. <!-- CCSAAS-3012 -->

* [GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/uploads) 및 [REST](https://developer.adobe.com/commerce/webapi/rest/saas-integrations/s3-uploads)에서 사전 서명된 URL을 사용하여 협상 가능한 견적 첨부 파일뿐만 아니라 고객 및 고객 주소와 연결된 파일 및 이미지를 Amazon S3에 업로드하고 검색하는 기능이 추가되었습니다. REST를 사용하면 카테고리 이미지를 업로드할 수도 있습니다. <!-- CCSAAS-3250 -->

* 고객을 만들고 업데이트하기 위해 [REST API](https://developer.adobe.com/commerce/webapi/rest/reference/)에 `POST /V1/customers` 및 `PUT /V1/customers/{customerId}` 끝점을 추가했습니다. 이러한 엔드포인트는 IMS 인증을 필요로 합니다. <!-- CCSAAS-3112 -->

* 쇼핑객 전자 메일 주소와 OTP(일회용 암호)가 필요한 [`exchangeOtpForCustomerToken` 돌연변이](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/exchange-otp-customer-token/)을(를) 추가하고 고객 토큰을 교환으로 받았습니다. 이 돌연변이는 일반적으로 고객이 이메일 또는 전화로 전송된 OTP를 사용하여 인증해야 하는 시나리오에서 사용됩니다.

* 관리자의 [!UICONTROL **전자 메일 주소 저장**] 구성 화면에 정의된 주소에 `example.com`(으)로 끝나는 값이 포함된 경우, Commerce에서는 이 주소로 전자 메일을 보내지 않습니다. 대신 시스템이 이메일이 전송되지 않았다고 기록합니다.  <!-- CCSAAS-3533 -->

#### 사용자 지정 순서 속성

* 이제 관리자 사용자는 관리 패널의 [순서 보기], [편집] 및 [만들기] 화면에서 직접 [사용자 지정 순서 특성](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/order-processing#custom-order-attributes)을 보고 편집할 수 있습니다. 이 향상된 기능은 GraphQL을 통해 만들어진 사용자 지정 주문 데이터의 관리를 개선합니다. <!-- CEXT-5044 -->

>[!ENDSHADEBOX]
