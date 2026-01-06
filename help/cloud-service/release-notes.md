---
title: '[!DNL Adobe Commerce as a Cloud Service] 릴리스 정보'
description: ' [!DNL Adobe Commerce as a Cloud Service]의 최신 기능 및 개선 사항에 대해 알아봅니다.'
feature: App Builder, GraphQL, Integration, Saas
role: Admin, Developer, User, Leader
level: Beginner
badgeSaas: label="SaaS만" type="Positive" url="https://experienceleague.adobe.com/ko/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."
exl-id: cf06dec6-8d6b-413e-9977-df88373c188e
source-git-commit: 1ce3b6b6b94b1b4e94c0d34c081dec2884d7f0f8
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 0%

---

# 릴리스 정보

다음 릴리스 노트에는 [!DNL Adobe Commerce as a Cloud Service]에 대한 업데이트가 포함되어 있습니다. 다른 제품에 대한 릴리스 정보는 [Adobe Commerce Optimizer](../optimizer/release-notes.md) 또는 [Adobe Commerce 온-프레미스 및 Adobe Commerce on Cloud](https://experienceleague.adobe.com/ko/docs/commerce-operations/release/notes/overview)를 참조하세요.

[!DNL Adobe Commerce as a Cloud Service]에는 머천다이징 서비스, 결제 서비스 및 확장성 릴리스의 최신 버전이 포함되어 있습니다. 다음 링크를 사용하여 각각에 대한 릴리스 정보를 보십시오.

* 서비스
   * [카탈로그 서비스](../catalog-service/release-notes.md)
   * [라이브 검색](../live-search/release-notes.md)
   * [결제 서비스](../payment-services/release-notes.md)
   * [제품 추천](../product-recommendations/release-notes.md)
   * [SaaS 데이터 내보내기](../data-export/release-notes.md)
* 확장성
   * [관리자 UI SDK](https://developer.adobe.com/commerce/extensibility/admin-ui-sdk/release-notes/)
   * [API Mesh](https://developer.adobe.com/graphql-mesh-gateway/mesh/release)
   * [이벤트](https://developer.adobe.com/commerce/extensibility/events/release-notes/)
   * [웹후크](https://developer.adobe.com/commerce/extensibility/webhooks/release-notes/)

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
