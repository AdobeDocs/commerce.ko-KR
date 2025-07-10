---
title: 로그 보기 및 관리
description: Commerce용 AEM Assets 통합에 대한 로그를 찾고 관리하는 방법에 대해 알아봅니다.
feature: CMS, Media, Integration
badgePaas: label="PaaS만" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce 온 클라우드 프로젝트(Adobe 관리 PaaS 인프라) 및 온프레미스 프로젝트에만 적용됩니다."
exl-id: 9c6c8694-6ded-4cc8-a3ab-d1dfb50e3583
source-git-commit: 202eca18c71a211cbbf1d210be00543049170c3f
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---

# 로그 보기 및 관리

AEM Assets 통합은 Commerce 인스턴스에 다음 로그 파일을 제공합니다.

- `/var/log/aem-assets-integration.log`
- `/var/log/aem-assets-integration-errors.log`

이러한 로그가 너무 커지지 않도록 하려면 시스템 관리자에게 로그 파일 순환 일정을 확인하도록 요청하십시오. 일부 환경에서는 로그가 자동으로 회전하며, 다른 환경에서는 로그 회전을 수동으로 구성해야 합니다.  자세한 내용은 다음 항목을 참조하십시오.

- Adobe Commerce 온-프레미스 설치의 경우 시스템 관리자에게 [로그 순환](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/next-steps/configuration.html#server-settings)을 설정하도록 요청하세요.
- 클라우드 인프라 프로젝트의 Adobe Commerce에 대해서는 [로그 보기 및 관리](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/test/log-locations.html)를 참조하십시오.
