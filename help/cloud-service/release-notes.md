---
title: '[!DNL Adobe Commerce as a Cloud Service] 릴리스 정보'
description: ' [!DNL Adobe Commerce as a Cloud Service]의 최신 기능 및 개선 사항에 대해 알아봅니다.'
feature-set: Commerce
feature: App Builder, GraphQL, Integration, Saas
role: Admin, Developer, User, Leader
level: Beginner
badgeSaas: label="SaaS만" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."
exl-id: cf06dec6-8d6b-413e-9977-df88373c188e
source-git-commit: f0f667254bb8b33905543afe83f17428bc3dbdc2
workflow-type: tm+mt
source-wordcount: '1735'
ht-degree: 0%

---

# 릴리스 정보

다음 릴리스 노트에는 [!DNL Adobe Commerce as a Cloud Service]에 대한 업데이트가 포함되어 있습니다.

>[!NOTE]
>
>Adobe Commerce 온-프레미스 또는 Adobe Commerce 온-클라우드 인프라를 사용하는 경우 [Adobe Commerce 릴리스 노트](https://experienceleague.adobe.com/en/docs/commerce-operations/release/notes/overview)를 참조하십시오.

## 2026년 3월 {#latest}

[!BADGE 샌드박스]{type=Caution tooltip="나열된 항목은 현재 샌드박스 환경에서만 사용할 수 있습니다. Adobe은 프로덕션 환경에서 릴리스를 사용하기 전에 예정된 변경 사항을 테스트할 시간을 제공하기 위해 먼저 샌드박스 환경에서 새 릴리스를 사용할 수 있도록 합니다."}

다음 항목은 현재 [!DNL Adobe Commerce as a Cloud Service]의 샌드박스 환경에서 사용할 수 있으며 2026년 3월 9일에 프로덕션 환경으로 릴리스됩니다.

>[!BEGINSHADEBOX]

### App Builder AI 코딩 도구 및 자습서

이제 [AI 코딩 개발자 도구](./migration/coding-tools.md)를 사용하여 새 [!DNL App Builder] 응용 프로그램을 만들고 기존 [!DNL Adobe Commerce] PHP 확장을 [!DNL App Builder] 응용 프로그램으로 변환할 수 있습니다. 다음 튜토리얼을 통해 도구 사용 방법을 확인할 수 있습니다.

* [자습서 사전 요구 사항](./tutorials/tutorial-prerequisites.md)
* [등급 확장 튜토리얼](./tutorials/ratings-extension.md)
* [배송 방법 확장 튜토리얼](./tutorials/shipping-method-extension.md)

### 관리를 통해 App Builder 앱 관리에 액세스

이제 [!DNL Commerce Admin]에 Commerce 인스턴스와 연결된 [개의 앱을 관리하기 위한 통합 셸인 ](https://developer.adobe.com/commerce/extensibility/app-management/){target="_blank"}앱 관리[!DNL App Builder]에 연결되는 메뉴 항목이 포함되어 있습니다. 이 추가는 최신 관리 UI SDK 업데이트를 통해 제공됩니다. <!-- CEXT-5755 -->

### 요청 엔티티 생성 제한 변경

기존에는 홈페이지, 스토어, 스토어 조회수 제한이 50개로 제한됐다. 필요한 경우 [지원 요청](https://experienceleague.adobe.com/home?support-tab=home#support)을 제출하여 이러한 제한을 수정할 수 있습니다. <!-- ACCS-398 -->

### 구조화된 오류 코드로 상점 인증 메시지 사용자 지정

이제 [`generateCustomerToken` GraphQL 돌연변이](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/generate-token/){target="_blank"}이(가) 오류 메시지와 함께 형식화된 오류 코드를 반환하여 상점 앞에 실패 이유별 특정 UI 메시지를 표시할 수 있습니다. 사용 가능한 오류 코드에는 `CUSTOMER_MISSING_EMAIL`, `CUSTOMER_MISSING_PASSWORD`, `CUSTOMER_SIGN_IN_INCORRECT_OR_LOCKED`, `CUSTOMER_ACCOUNT_NOT_CONFIRMED` 및 `CUSTOMER_GENERIC_ERROR`이(가) 포함됩니다. <!-- ACCS-301 -->

### 장바구니 및 위시리스트 비활동에 대한 자동 이메일 미리 알림 보내기

[전자 메일 미리 알림 모듈](https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/communications/email-reminders/email-reminder-rules)&#x200B;(`Magento_Reminder`)이(가) 이제 [!DNL Adobe Commerce as a Cloud Service]에서 활성 상태이므로 가맹점은 장바구니 및 위시리스트 비활성에 따라 고객에게 전자 메일을 트리거하는 자동화된 미리 알림 규칙을 만들 수 있습니다. <!-- CCSAAS-4597 -->

### 범주 삭제 이벤트 웹후크 구독

이제 `observer.catalog_category_delete_before`에서 [!DNL Adobe Commerce as a Cloud Service] 웹후크를 사용할 수 있습니다. 범주를 삭제하기 전에 논리를 실행하는 데 사용합니다. <!-- CEXT-5862 -->

### 등록된 이메일과 함께 수행한 게스트 주문 추적

새로운 선택적 저장소 수준 구성(기본적으로 비활성화됨)을 사용하면 판매자가 등록된 고객 계정과 일치하는 이메일 주소를 사용하여 수행한 게스트 주문을 추적할 수 있습니다. 활성화되면 등록된 이메일과 함께 수행된 게스트 체크아웃 주문에 대한 액세스 권한이 유지되면서 고객의 주문 내역에도 표시됩니다.

이 기능을 사용하려면 **스토어** > 설정 > **구성** > 판매 > **판매** > **게스트 체크아웃**&#x200B;으로 이동하고 **등록된 전자 메일에 대한 게스트 주문 액세스 허용** 설정을 `Yes`(으)로 설정합니다.
<!-- ACCS-289 -->

### 개선 사항 및 버그 수정

이 릴리스에는 다음과 같은 개선 사항, 최적화 및 버그 수정이 포함되어 있습니다.

* 일부 조직 관리자가 테넌트당 권한 없이 테넌트 인스턴스에 잘못 액세스할 수 있는 문제가 수정되었습니다. <!-- ACCS-335 -->

* 공유 카탈로그를 변경할 때 [!DNL Commerce Admin]에서 사용자를 로그아웃할 수 있는 문제를 해결했습니다. <!-- ACCS-318 -->

* 일부 웹후크 필드가 [!DNL Commerce Admin] UI에 잘못 표시되는 문제를 해결했습니다. <!-- CEXT-5874 -->

### 내부(삭제 예정)

다음과 같은 인프라 개선 사항이 포함되어 있습니다.

* [!DNL Adobe Commerce] 코어를 2.4.8-p3에서 2.4.8-p4로 업그레이드했습니다. <!-- CCSAAS-4588 -->

* 게스트 체크아웃 흐름 전체에서 장바구니 견적이 올바르게 연관되고 유지되도록 게스트 체크아웃 세션 처리가 수정되었습니다. <!-- ACCS-261 -->

* 전체 예외 스택 추적을 캡처하도록 GraphQL 오류 로깅을 확장하여 디버깅을 개선했습니다. <!-- ACCS-305 -->

* Company Resolver GraphQL 테스트 세트를 CCSaaS 테스트 환경에 포팅했습니다. <!-- CCSAAS-2122 -->

* PAT devbox CI 빌드의 관리 시나리오 오류를 수정했습니다. <!-- ACCS-351 -->

* PAT 트렌드 빌드에 제품 생성 시나리오가 추가되었습니다. <!-- CCSAAS-4498 -->

* BundleRequisitionList GraphQL 테스트 세트를 CCSaaS 테스트 환경에 포팅했습니다. <!-- CCSAAS-2113 -->

* 피드백 시간을 줄이기 위해 CI에서 GraphQL API 기능 테스트 실행을 병렬화했습니다. <!-- CCSAAS-4607 -->

* 추가 정보 설명서를 업데이트했습니다. <!-- ACCS-404 -->

* CCSaaS 저장소 컨텍스트에 대한 커서 AI 규칙이 확장되었습니다. <!-- PR #1295 -->

* 부실 마이그레이션 파일을 제거했습니다. <!-- PR #1296 -->

* 성능 데이터를 생성하는 동안 템플릿 처리가 비활성화되었습니다. <!-- PR #1297 -->

* 커서 규칙 및 Magento CLI 설명서가 추가되었습니다. <!-- PR #1300 -->

* 개발을 위한 로컬 데이터베이스 도우미 스크립트가 추가되었습니다. <!-- PR #1305 -->

* 커서 보안 코딩 규칙이 도입되었습니다. <!-- PR #1306 -->

* 변경된 파일에서만 실행되도록 CI 정적 분석을 최적화했습니다. <!-- PR #1309 -->

{{accs-release}}

>[!ENDSHADEBOX]

## 2026년 2월 - 릴리스 #2

[!BADGE 프로덕션]{type=Neutral tooltip="나열된 항목은 현재 프로덕션 환경에서 사용할 수 있습니다."}

다음 항목은 2026년 2월 24일에 [!DNL Adobe Commerce as a Cloud Service]의 프로덕션 환경에 릴리스되었습니다.

>[!BEGINSHADEBOX]

### 상거래 이벤트를 사용하여 컨텍스트 필드 보내기

이제 [!DNL Adobe Commerce as a Cloud Service]이(가) 이벤트 페이로드에서 [컨텍스트 필드](https://developer.adobe.com/commerce/extensibility/events/context-fields/)를 지원하므로 기본적으로 이벤트에 포함되지 않은 데이터를 포함할 수 있습니다. <!-- CEXT-5713 -->

### 새 웹후크를 사용하여 견적 항목 저장 이벤트에 가입

이제 `observer.sales_quote_item_save_before`에서 [!DNL Adobe Commerce as a Cloud Service] 웹후크를 사용할 수 있습니다. 견적 항목이 저장되기 전에 논리를 실행하는 데 사용합니다. <!-- ACCS-346 -->

### 개선 사항 및 버그 수정

이 릴리스에는 다음과 같은 개선 사항, 최적화 및 버그 수정이 포함되어 있습니다.

* [!DNL Commerce Admin] 제품 목록에서 표시 문제를 일으킬 수 있는 오류를 해결했습니다. 이제 제품 목록에서 성능을 개선하기 위해 표시되는 공유 카탈로그 수를 제한합니다. <!-- CCSAAS-1242 -->

* 사용자 지정 가능한 기프트 카드를 장바구니에 추가하지 못하는 GraphQL 오류를 수정했습니다. <!-- ACCS-313 -->

{{accs-release}}

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

* [!DNL Storefront Compatibility B2B Package]이(가) `setNegotiableQuoteShippingAddress`(으)로 설정되어 있어도 `save_in_address_book` 돌연변이가 수동으로 입력한 주소를 고객 주소록에 저장하지 않는 `true`의 문제를 해결했습니다. <!-- LYNX-1031 -->

<!-- The above change will also be covered by the B2B changelog published on February 13, 2026. -->

* 자산 역할과 관련된 사용자 지정 특성에서 [!DNL Edge Delivery Services] 값이 손상되어 `no_selection`에서 제품 이미지가 제대로 표시되지 않는 문제를 해결했습니다. <!-- ACAP-1206 -->

* 이름 또는 성 값이 null인 페더레이션 사용자 계정이 Commerce 관리자에 액세스할 수 없는 문제를 해결했습니다. <!-- ACCS-200 -->

* 지역별 IMS 클라이언트 ID를 자동으로 제공하여 자산 선택기 구성을 간소화했습니다. 판매자는 더 이상 제품 범주 이미지를 자산과 매핑하기 위해 자산 선택기를 구성하기 위해 지원 티켓을 제출할 필요가 없습니다. 이제 시스템에서 Commerce 지역을 기반으로 전용 IMS 클라이언트 ID를 자동으로 사용합니다. <!-- ACCS-175 -->

* 다양한 성능 및 최적화 개선 사항. <!-- CCSAAS-4485, CCSAAS-4497, ACCS-196 -->

{{accs-release}}

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

* Released the [B2B Storefront Compatibility Package](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/storefront-compatibility-b2b/). This package enhances the [!DNL Adobe Commerce] B2B GraphQL schema to help improve development on B2B systems. -->

### 외부 배송 추적기에 대한 클릭 가능한 링크

[사용자 지정 추적 URL을 사용](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/delivery/shipping-settings#shipment-tracking-urls)하여 쇼핑객 전자 메일에 포함된 배송 추적 번호를 일반 텍스트에서 클릭 가능한 링크로 변환합니다. 이 기능은 USPS, UPS, FedEx 및 DHL에서 지원됩니다. <!-- See PR #716 in commerce-admin -->

### Google reCAPTCHA Enterprise 지원

[!DNL Adobe Commerce as a Cloud Service] 상점이 이제 [reCAPTCHA Enterprise](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/security/captcha/security-google-recaptcha-enterprise)을(를) 지원합니다. 이 기능은 적응형 위험 분석 및 머신 러닝을 사용하여 인간 사용자를 자동화된 봇과 정확하게 구별하여 고급 봇 보호를 제공합니다. 사이트 보안을 강화하고 사기 행위를 방지하며 스팸 및 남용을 줄여 신뢰할 수 있는 쇼핑 경험을 유지합니다. <!-- CCSAAS-4242 -->

### 인스턴스별 관리자 액세스

이제 Admin Console에서 [사용자에게 개별 ](./user-management.md#add-users) 인스턴스에 액세스 권한을 할당[!DNL Adobe Commerce as a Cloud Service]할 수 있습니다. <!-- CCSAAS-4337 --><!-- See PR #332 -->

### 가시성

[!DNL App Builder]을(를) 사용하면 이제 자동으로 사용할 수 있는 [!DNL Adobe Commerce as a Cloud Service]OpenTelemetry observability[을(를) 사용하여 ](https://developer.adobe.com/commerce/extensibility/observability/) 인스턴스에 대한 더 깊은 가시성을 얻을 수 있습니다. OpenTelemetry는 성능 모니터링, 문제 해결 속도 향상 및 상점 최적화에 도움이 되는 지표, 로그 및 추적을 제공합니다. 이 기능을 통해 시스템 상태에 대한 사전 예방적 통찰력을 확보하고 고객의 안정성을 향상시킬 수 있습니다.

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

* 관리 대시보드에서 `404`데이터 다시 로드&#x200B;[!UICONTROL **단추를 클릭할 때 발생하는**] 오류를 수정했습니다. <!-- CCSAAS-4468 -->

* [!DNL AEM Assets integration]이(가) 활성화되어 있고 제품에 이미지가 있을 때 REST API를 통해 제품 사용자 지정 특성을 업데이트할 수 없는 문제를 해결했습니다. <!-- ACAP-1178 -->

* 다양한 성능 및 최적화 개선 사항.<!-- CCSAAS-4255 --><!-- CCSAAS-4233 --><!-- CCSAAS-4220 --><!-- CCSAAS-4252 --><!-- CCSAAS-4330 --><!-- CCSAAS-3669 --><!-- CCSAAS-4462 -->

{{accs-release}}

>[!ENDSHADEBOX]

## 2025년 11월

>[!BEGINSHADEBOX]

### 향상된 기능

* [사용자 관리](./user-management.md) - Commerce 관리자에 대한 사용자 액세스를 자동으로 업데이트하기 위해 Admin Console에서 **제품 관리자** 역할을 변경했습니다. <!-- CCSAAS-3012 -->

* [GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/uploads) 및 [REST](https://developer.adobe.com/commerce/webapi/rest/modules/s3-uploads)에서 사전 서명된 URL을 사용하여 협상 가능한 견적 첨부 파일뿐만 아니라 고객 및 고객 주소와 연결된 파일 및 이미지를 Amazon S3에 업로드하고 검색하는 기능이 추가되었습니다. REST를 사용하면 카테고리 이미지를 업로드할 수도 있습니다. <!-- CCSAAS-3250 -->

* 고객을 만들고 업데이트하기 위해 `POST /V1/customers`REST API`PUT /V1/customers/{customerId}`에 [ 및 ](https://developer.adobe.com/commerce/webapi/rest/reference/) 끝점을 추가했습니다. 이러한 엔드포인트는 IMS 인증을 필요로 합니다. <!-- CCSAAS-3112 -->

* 쇼핑객 전자 메일 주소와 OTP(일회용 암호)가 필요한 [`exchangeOtpForCustomerToken` 돌연변이](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/exchange-otp-customer-token/)을(를) 추가하고 고객 토큰을 교환으로 받았습니다. 이 돌연변이는 일반적으로 고객이 이메일 또는 전화로 전송된 OTP를 사용하여 인증해야 하는 시나리오에서 사용됩니다.

* 관리자의 [!UICONTROL **전자 메일 주소 저장**] 구성 화면에 정의된 주소에 `example.com`(으)로 끝나는 값이 포함된 경우, Commerce에서는 이 주소로 전자 메일을 보내지 않습니다. 대신 시스템이 이메일이 전송되지 않았다고 기록합니다.  <!-- CCSAAS-3533 -->

#### 사용자 지정 순서 속성

* 이제 관리자 사용자는 관리 패널의 [순서 보기], [편집] 및 [만들기] 화면에서 직접 [사용자 지정 순서 특성](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/order-processing#custom-order-attributes)을 보고 편집할 수 있습니다. 이 향상된 기능은 GraphQL을 통해 만들어진 사용자 지정 주문 데이터의 관리를 개선합니다. <!-- CEXT-5044 -->

>[!ENDSHADEBOX]
