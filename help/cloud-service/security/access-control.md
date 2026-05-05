---
title: ID 및 액세스 관리
description: Adobe Commerce as a Cloud Service의 ID 및 액세스 관리 기능에 대해 알아봅니다.
role: Admin, Architect, Leader
badgeSaas: label="SaaS만" type="Positive" url="https://experienceleague.adobe.com/ko/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."
source-git-commit: 283e9c8b9dd0812bb19640681d1fdf86f0f7fce1
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 0%

---


# ID 및 액세스 관리

[!DNL Adobe Commerce as a Cloud Service]은(는) Adobe의 엔터프라이즈급 id 인프라를 활용하여 모든 환경에서 안전하고 확장 가능하며 중앙 집중식 액세스 제어를 보장합니다. [!DNL Adobe Commerce as a Cloud Service]의 IAM(Identity and Access Management)은 사용자 프로비저닝을 간소화하고, 최소 권한 액세스를 적용하며, 글로벌 보안 표준 준수를 지원하도록 설계되었습니다.

- **[!DNL Adobe Identity Management Services (IMS)]**: [!DNL Adobe Commerce as a Cloud Service]은(는) [Adobe IMS(Identity Management Services)](https://experienceleague.adobe.com/ko/docs/commerce-admin/start/admin/ims/adobe-ims-integration-overview)을(를) 사용하여 사용자를 인증하고 권한을 관리합니다. 여기에는 페더레이션 ID 공급자 및 [역할 기반 액세스 제어](../user-management.md)에 대한 지원이 포함됩니다.

- **Admin Console 거버넌스**: 관리자는 [!DNL Adobe Admin Console]을(를) 통해 상점 및 백엔드에 대한 액세스를 관리합니다. 권한은 특정 기능 및 역할로 범위를 지정할 수 있으므로 최소 권한 액세스가 보장됩니다.

## Adobe Identity Management 서비스(IMS)

[!DNL Adobe Commerce as a Cloud Service]은(는) [!DNL Adobe Identity Management Services (IMS)]을(를) 사용하여 사용자를 인증하고 플랫폼에서 권한을 관리합니다. IMS는 다음을 제공합니다.

- **페더레이션 ID 지원**: SAML 또는 OIDC를 사용하여 Azure AD 및 Okta와 같은 Enterprise ID 공급자와 통합합니다.
- **SSO(Single Sign-On)**: [!DNL Adobe Commerce] 및 기타 [!DNL Adobe Experience Cloud] 제품에 원활하게 액세스할 수 있습니다.
- **MFA(Multi-Factor Authentication)**: 향상된 보안을 위해 조직 수준에서 적용됩니다.
- **전역 중복성**: ID 데이터는 여러 지역의 부하 분산된 클라우드 인프라에 저장됩니다.

## Admin Console 액세스 제어

[!DNL Adobe Admin Console]은(는) [!DNL Adobe Commerce as a Cloud Service]에 대한 사용자 액세스를 관리하기 위한 중앙 허브입니다.

- **RBAC(역할 기반 액세스 제어)**: 개발자, 관리자 및 분석가와 같은 역할을 기반으로 사용자에게 세분화된 권한을 할당합니다.
- **제품 프로필**: 스테이징 및 프로덕션과 같은 다양한 환경에 대한 액세스 범위를 정의합니다.
- **위임된 관리**: 시스템 관리자 및 제품 관리자는 IT에 관여하지 않고 사용자 액세스를 관리할 수 있습니다.

자세한 내용은 [사용자 관리](https://experienceleague.adobe.com/ko/docs/commerce/cloud-service/user-management)를 참조하십시오.

## API 인증 및 통합 보안

[!DNL Adobe Commerce as a Cloud Service]의 REST API 인증은 표준화된 OAuth 2 프로토콜을 사용하여 Adobe [!DNL Adobe Identity Management Services (IMS)]을(를) 통해 처리됩니다. 이 인증 시스템은 대화식 사용자 기반 워크플로우와 자동화된 서버 간 통합을 모두 지원하므로 다양한 사용 사례에 안전하고 적절한 액세스를 보장합니다.

>[!NOTE]
>
>[!DNL Adobe Commerce]의 PaaS 버전에서 관리 및 통합 토큰 생성 메서드는 SaaS 환경에서 지원되지 않습니다. 대신 OAuth 인증을 통해 IMS 관리 토큰을 받아야 합니다.

- **OAuth 2.0 지원**: 통합 및 타사 서비스를 위한 보안 토큰 기반 인증.
- **범위 API 액세스**: 특정 리소스 및 작업에 대한 API 액세스를 제한합니다.
- **감사 로깅**: 준수 및 문제 해결을 위해 인증 이벤트 및 액세스 변경 사항을 추적합니다.

자세한 내용은 [REST 인증](https://developer.adobe.com/commerce/webapi/rest/authentication/)을 참조하십시오.
