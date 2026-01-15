---
title: '[!DNL Adobe Commerce as a Cloud Service] 릴리스 정보'
description: ' [!DNL Adobe Commerce as a Cloud Service]의 최신 기능 및 개선 사항에 대해 알아봅니다.'
feature: App Builder, GraphQL, Integration, Saas
role: Admin, Developer, User, Leader
level: Beginner
badgeSaas: label="SaaS만" type="Positive" url="https://experienceleague.adobe.com/ko/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."
exl-id: cf06dec6-8d6b-413e-9977-df88373c188e
source-git-commit: fb4c497c9efc184ffb6bd884cb2f37ad9cc87b02
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 0%

---

# 릴리스 정보

다음 릴리스 노트에는 [!DNL Adobe Commerce as a Cloud Service]에 대한 업데이트가 포함되어 있습니다.

>[!NOTE]
>
>Adobe Commerce 온-프레미스 또는 Adobe Commerce 온-클라우드 인프라를 사용하는 경우 [Adobe Commerce 릴리스 노트](https://experienceleague.adobe.com/ko/docs/commerce-operations/release/notes/overview)를 참조하십시오.

## 2026년 1월 {#latest}

[!BADGE 샌드박스]{type=Caution tooltip="나열된 항목은 현재 샌드박스 환경에서만 사용할 수 있습니다. Adobe은 프로덕션 환경에서 릴리스를 사용하기 전에 예정된 변경 사항을 테스트할 시간을 제공하기 위해 먼저 샌드박스 환경에서 새 릴리스를 사용할 수 있도록 합니다."}

다음 항목은 현재 [!DNL Adobe Commerce as a Cloud Service]의 샌드박스 환경에서만 사용할 수 있습니다. 이 릴리스는 2026년 1월 20일에 프로덕션 환경으로 이전할 예정입니다.

>[!BEGINSHADEBOX]

### 인증 개선 사항

Adobe IMS 관리자 인증에 대한 액세스 토큰은 이제 POST 요청을 통해서만 허용됩니다. <!-- CCSAAS-4421 -->

### B2B 드롭다운

B2B 드롭인 구성 요소는 다음과 같이 변경되었습니다.

* 이제 [!DNL Commerce Storefront on Edge Delivery Services]에 [B2B 끌어 놓기 구성 요소](http://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/?lang=ko)가 포함됩니다. 이제 다음 B2B 드롭인을 사용할 수 있습니다.

   * **회사 관리** - Adobe Commerce 스토어프론트에 대한 회사 프로필 관리 및 역할 기반 권한을 사용하도록 설정합니다.
   * **회사 전환기** - 사용자가 연결된 여러 회사 간에 전환할 수 있는 UI 구성 요소를 제공합니다.
   * **구매 주문** - B2B 트랜잭션에 대한 구매 주문 워크플로, 승인 규칙 및 구매 주문 내역을 관리합니다.
   * **견적 관리** - 견적 요청, 협상 및 승인 워크플로를 통해 B2B 고객에 대해 협상 가능한 견적을 사용하도록 설정합니다.
   * **구매요청 목록** - 반복 구매 및 대량 주문을 위한 구매요청 목록을 만들고 관리하는 도구를 제공합니다.

     >[!NOTE]
     >
     >이 기능이 프로덕션으로 승격되면 B2B 드롭인 구성 요소에 대한 자세한 설명서를 사용할 수 있습니다.

* B2B Storefront 호환성 패키지를 출시했습니다. 이 패키지는 B2B 시스템의 개발을 개선하는 데 도움이 되도록 [!DNL Adobe Commerce] B2B GraphQL 스키마를 향상시킵니다.

<!-- 
* [!DNL Commerce Storefront on Edge Delivery Services] now includes [B2B drop-in components](http://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/?lang=ko). For a complete list of available B2B drop-in blocks, refer to the [storefront documentation](http://experienceleague.adobe.com/developer/commerce/storefront/merchants/b2b-commerce-blocks/).

* Released the [B2B Storefront Compatibility Package](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/storefront-compatibility-b2b/). This package enhances the [!DNL Adobe Commerce] B2B GraphQL schema to help improve development on B2B systems. -->

### 외부 배송 추적기에 대한 클릭 가능한 링크

[사용자 지정 추적 URL을 사용](https://experienceleague.adobe.com/ko/docs/commerce-admin/stores-sales/delivery/shipping-settings#shipment-tracking-urls)하여 쇼핑객 전자 메일에 포함된 배송 추적 번호를 일반 텍스트에서 클릭 가능한 링크로 변환합니다. 이 기능은 USPS, UPS, FedEx 및 DHL에서 지원됩니다. <!-- See PR #716 in commerce-admin -->

### Google reCAPTCHA Enterprise 지원

[!DNL Adobe Commerce as a Cloud Service] 상점이 이제 [reCAPTCHA Enterprise](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/security/captcha/security-google-recaptcha-enterprise)을(를) 지원합니다. 이 기능은 적응형 위험 분석 및 머신 러닝을 사용하여 인간 사용자를 자동화된 봇과 정확하게 구별하여 고급 봇 보호를 제공합니다. 사이트 보안을 강화하고 사기 행위를 방지하며 스팸 및 남용을 줄여 신뢰할 수 있는 쇼핑 경험을 유지합니다. <!-- CCSAAS-4242 -->

### 인스턴스별 관리자 액세스

이제 Admin Console에서 [사용자에게 개별 &#x200B;](./user-management.md#add-users) 인스턴스에 액세스 권한을 할당[!DNL Adobe Commerce as a Cloud Service]할 수 있습니다. <!-- CCSAAS-4337 --><!-- See PR #332 -->

### 가시성

이제 자동으로 사용할 수 있는 [!DNL Adobe Commerce as a Cloud Service]OpenTelemetry 가시성[을 사용하여 &#x200B;](https://developer.adobe.com/commerce/extensibility/observability/) 인스턴스에 대한 더 깊은 가시성을 확보하십시오. OpenTelemetry는 성능 모니터링, 문제 해결 속도 향상 및 상점 최적화에 도움이 되는 지표, 로그 및 추적을 제공합니다. 이 기능을 통해 시스템 상태에 대한 사전 예방적 통찰력을 확보하고 고객의 안정성을 향상시킬 수 있습니다.

### 카탈로그 가격 규칙에 대한 계층 가격 책정

이제 [카탈로그 가격 규칙](https://experienceleague.adobe.com/ko/docs/commerce-admin/catalog/products/pricing/product-price-tier#enable-tier-pricing-for-catalog-price-rules)을 사용하여 계층화된 가격 할인과 카탈로그 규칙 할인을 결합할 수 있습니다. 이 향상된 기능을 통해 판촉 할인을 동시에 적용하면서 대량 구매에 대한 보람을 제공하는 보다 역동적이고 경쟁력 있는 가격 전략을 만들 수 있습니다. 따라서 고객을 유치하고 주문 가치를 높이며 전환을 유도하는 유연성이 향상됩니다.<!-- See PR #708 in commerce-admin -->

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

* 고객을 만들고 업데이트하기 위해 `POST /V1/customers`REST API`PUT /V1/customers/{customerId}`에 [&#x200B; 및 &#x200B;](https://developer.adobe.com/commerce/webapi/rest/reference/) 끝점을 추가했습니다. 이러한 엔드포인트는 관리자 권한이 필요합니다. <!-- CCSAAS-3112 -->

* 쇼핑객 전자 메일 주소와 OTP(일회용 암호)가 필요한 [`exchangeOtpForCustomerToken` 돌연변이](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/exchange-otp-customer-token/)을(를) 추가하고 고객 토큰을 교환으로 받았습니다. 이 돌연변이는 일반적으로 고객이 이메일 또는 전화로 전송된 OTP를 사용하여 인증해야 하는 시나리오에서 사용됩니다.

* 관리자의 [!UICONTROL **전자 메일 주소 저장**] 구성 화면에 정의된 주소에 `example.com`(으)로 끝나는 값이 포함된 경우, Commerce에서는 이 주소로 전자 메일을 보내지 않습니다. 대신 시스템이 이메일이 전송되지 않았다고 기록합니다.  <!-- CCSAAS-3533 -->

#### 사용자 지정 순서 속성

* 이제 관리자 사용자는 관리 패널의 [순서 보기], [편집] 및 [만들기] 화면에서 직접 [사용자 지정 순서 특성](https://experienceleague.adobe.com/ko/docs/commerce-admin/stores-sales/order-management/orders/order-processing#custom-order-attributes)을 보고 편집할 수 있습니다. 이 향상된 기능은 GraphQL을 통해 만들어진 사용자 지정 주문 데이터의 관리를 개선합니다. <!-- CEXT-5044 -->

>[!ENDSHADEBOX]
