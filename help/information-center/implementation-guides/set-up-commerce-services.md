---
title: Commerce 서비스 설정
description: Commerce 서비스 커넥터를 사용하여 Adobe Commerce을 머천다이징 서비스에 연결하고 Magento Open Source을 결제 서비스에 연결하는 방법을 알아봅니다.
role: Admin, Developer
feature: Integration, Configuration
recommendations: noCatalog
autotag-review: '2026-10-20T11:14:04.410Z'
TQID: 'https://experienceleague.adobe.com/yyUDw1y5CYHxdLlC3bNo0DKK0byamPAKUjK-wwxVEX4'
product_v2:
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
  - id: 4273989f-0bf2-5361-a17a-6909488d18ab
    internal-label: Catalog Service
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: dec06508-d41f-555a-87e8-29e8bcdfa95a
    internal-label: Recommendations
subfeature_v2:
  - id: a1d22079-48b9-5e69-9ee6-eb236068ef34
    internal-label: Search
source-git-commit: ca6bb3543583c865c42b8f4d84f01e27a04f9223
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%
---

# Commerce 서비스 설정

Adobe Commerce on cloud infrastructure 및 온-프레미스 프로젝트는 Commerce 서비스 커넥터를 통해 [!DNL Catalog Service], [!DNL Live Search], [!DNL Product Recommendations] 및 [!DNL Payment Services]과(와) 같은 서비스에 연결합니다. [!DNL Adobe Commerce as a Cloud Service]에서 이 연결은 자동으로 구성됩니다.

Magento Open Source은 [!DNL Payment Services]에 대해 Commerce 서비스 커넥터를 사용합니다. [!DNL Catalog Service], [!DNL Live Search] 및 [!DNL Product Recommendations]은(는) Adobe Commerce이 필요하며 Magento Open Source에 사용할 수 없습니다.

>[!NOTE]
>
>Adobe Commerce Optimizer은 별도의 [!DNL Live Search], [!DNL Catalog Service] 및 [!DNL Product Recommendations] 서비스를 사용하는 대신 기본적으로 카탈로그 및 머천다이징 기능을 제공합니다. 카탈로그를 동기화하기 위해 Commerce 서비스 커넥터가 필요하지 않습니다. [!DNL Payment Services] 및 [!DNL Data Connection]과(와) 같은 Commerce 백엔드의 다른 통합에는 여전히 커넥터가 필요합니다. Optimizer 설정에 대해 [Adobe Commerce Optimizer 사용](enable-aco.md)을(를) 참조하십시오.


## 시작

1. API 키를 가져오고 구성하려면 [Commerce 서비스 커넥터](/help/landing/saas.md) 설명서를 검토하십시오.

1. 커넥터를 통해 사용할 수 있는 개별 서비스에 대해서는 [Adobe Commerce 서비스 안내서](/help/landing/home.md)를 참조하십시오.

## 관련 지침

- [결제 구성](configure-payments.md)
- [AEM Assets 연결](connect-aem-assets.md)
- [Adobe Experience Platform과 통합](integrate-aep.md)
