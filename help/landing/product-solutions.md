---
title: Commerce 제품 솔루션
description: 배지를 사용하여 다양한 Adobe Commerce 솔루션(SaaS, PaaS, 온프레미스)에 적용되는 설명서를 식별하는 방법에 대해 알아봅니다.
feature: Paas, Saas
recommendations: noDisplay, noCatalog
hide: true
hidefromtoc: true
exl-id: 5ba1fa65-391f-4af7-8c40-d8314ec9d3e5
source-git-commit: 5e4481dfd7259a07bda58a1e945b086e9f1c1805
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 0%

---

# Adobe Commerce 제품 솔루션

Adobe은 전자 상거래 비즈니스의 요구 사항을 충족하는 몇 가지 솔루션을 제공합니다. [Experience League](https://experienceleague.adobe.com/en/docs/commerce) 및 [Adobe Developer](https://developer.adobe.com/commerce/docs/) 사이트의 Adobe Commerce 설명서는 모든 솔루션을 지원하는 셀프서비스 리소스를 고객에게 제공합니다. 하지만 이렇게 많은 양의 콘텐츠를 탐색하는 것은 지침이 없으면 어려울 수 있습니다.

>[!NOTE]
>
>[!DNL Adobe Commerce as a Cloud Service]&#x200B;(SaaS)에서 사용 가능한 기능 및 이러한 기능이 [!DNL Adobe Commerce on Cloud] 및 [!DNL Adobe Commerce on Premises]&#x200B;(PaaS)와 같은 Adobe Commerce의 다른 버전과 어떻게 일치하는지에 대한 자세한 내용은 [기능 비교](../cloud-service/feature-comparison.md)를 참조하십시오.

## 배지

배지를 사용하면 기존 사이트 탐색 또는 인터넷 검색을 통해 찾은 Commerce 설명서가 사용 중인 Commerce 제품 솔루션과 관련이 있는지 여부를 신속하게 식별할 수 있습니다. 이는 콘텐츠가 하나의 솔루션에만 적용되는 경우 특히 중요합니다.

배지가 표시되면 이는 콘텐츠가 지정된 솔루션에만 적용됨을 의미합니다. 배지가 표시되지 않으면 컨텐츠가 모든 Adobe Commerce 솔루션에 적용됨을 의미합니다.

예를 들어 Adobe Commerce as a Cloud Service을 사용하는 경우 제품 권장 사항 확장 [설치](../product-recommendations/install-configure.md#install-product-recommendations) 및 Commerce 서비스 커넥터 [구성](../product-recommendations/install-configure.md#configure-product-recommendations)에 대한 콘텐츠를 무시해야 합니다. Adobe은 인스턴스를 만들 때 이러한 단계를 자동으로 완료합니다.

### 정의

다음 표는 Adobe Commerce 설명서에 표시되는 배지를 정의합니다.

>[!BEGINSHADEBOX]

![정보](../cloud-service/assets/Smock_InfoOutline_18_N.svg) 여기에 설명된 배지는 특히 Adobe Commerce 설명서에 적용됩니다. 다른 Adobe Experience Cloud 제품에 대한 설명서에서 배지가 사용되는 방식을 나타내지는 않습니다.

>[!ENDSHADEBOX]

#### [!BADGE SaaS만]{type=Positive tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."}

이 배지는 [Adobe Commerce as a Cloud Service](../cloud-service/overview.md) 및 [Adobe Commerce Optimizer](../optimizer/overview.md) 프로젝트에 대한 설명서만 식별합니다. 이러한 프로젝트는 클라우드 기반의 완전 관리 SaaS(Software-as-a-Service) 솔루션에서 호스팅되며, Adobe은 지속적인 업데이트, 보안 모니터링 및 확장성과 같은 대부분의 운영 측면을 담당하므로 고객은 인프라가 아닌 상거래에 집중할 수 있습니다.

#### [!BADGE PaaS만]{type=Informative tooltip="Adobe Commerce 온 클라우드 프로젝트(Adobe 관리 PaaS 인프라) 및 온프레미스 프로젝트에만 적용됩니다."}

이 배지는 [Cloud의 Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/overview) 및 온-프레미스 프로젝트와 관련된 설명서를 식별합니다. Adobe Commerce on Cloud 프로젝트는 사전 프로비저닝된 환경에 모든 Adobe Commerce의 핵심 기능이 포함된 클라우드 기반의 완전 관리 PaaS(platform-as-a-service) 솔루션에서 호스팅됩니다. 온프레미스 프로젝트는 고객 관리 인프라에서 호스팅됩니다.

>[!NOTE]
>
>별도로 언급되지 않는 한, 여기에는 Magento Open Source 코드 베이스에 기반한 자체 호스팅 프로젝트도 포함됩니다.

### 규칙

다음 규칙을 사용하여 각 Adobe Commerce 솔루션에 적용되는 콘텐츠를 이해합니다.

- **페이지 수준 배지**: 페이지 맨 위(페이지 제목 위)에 표시됩니다. 페이지의 _모두_ 콘텐츠가 지정된 솔루션에만 적용됨을 나타냅니다.

- **섹션 수준 배지**: 페이지의 다른 모든 머리글 바로 아래에 표시됩니다(페이지 제목 제외). 해당 섹션의 콘텐츠가 지정된 솔루션에만 적용됨을 나타냅니다.

- **인라인 배지**: 표, 단락, 목록 등 머리글이 아닌 모든 페이지 요소에 표시됩니다. 해당 요소의 콘텐츠가 지정된 솔루션에만 적용됨을 나타냅니다.

>[!NOTE]
>
>배지는 상호 배타적입니다. 즉, 동일한 페이지 또는 섹션에 두 개 이상의 페이지 또는 섹션 수준 배지가 표시되지 않습니다. 그러나 동일한 페이지 또는 동일한 섹션에 여러 인라인 배지가 있을 수 있습니다.
