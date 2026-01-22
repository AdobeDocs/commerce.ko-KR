---
title: 상점 설정
description: 스캐폴딩 도구를 실행하여  [!DNL Adobe Commerce as a Cloud Service] storefront를 설정하는 방법에 대해 알아봅니다.
feature: Storefront
role: Developer
level: Beginner
exl-id: 02928dc4-1777-483e-b0ee-b04fc813864d
badgeSaas: label="SaaS만" type="Positive" url="https://experienceleague.adobe.com/ko/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."
source-git-commit: 0cd9749574460374a8fe875f1eff54f2a4a8d614
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# 상점 설정

[!DNL Adobe Commerce Storefront]&#x200B;(SaaS)에 대해 [!DNL Edge Delivery Services]에서 제공하는 [!DNL Adobe Commerce as a Cloud Service]을(를) 설정하려면 다음 단계를 완료하십시오.

사용자 지정이 가능하고 자세한 설명은 [storefront 설명서](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/?lang=ko)를 참조하세요.

1. [사이트 작성자 도구](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator)를 엽니다.

1. **[!UICONTROL Create New Site (Code & Content)]**&#x200B;을(를) 선택합니다.

1. Storefront 코드 리포지토리를 만들 **[!UICONTROL Github Organization/Username]**&#x200B;을(를) 입력하십시오.

1. **[!UICONTROL Site Name]** 입력.

1. **[!UICONTROL Commerce GraphQL Endpoint (optional)]** 필드에 [!DNL Adobe Commerce as a Cloud Service]&#x200B;(SaaS) GraphQL 끝점을 입력합니다. 이 끝점은 [인스턴스를 만든 후](./getting-started.md#create-an-instance) Commerce Cloud Manager에서 액세스할 수 있습니다.

   또는 [[!DNL API Mesh]](https://developer.adobe.com/graphql-mesh-gateway/mesh/basic)을(를) 사용하는 경우 [!DNL API Mesh] 필드에 **[!UICONTROL Commerce GraphQL Endpoint (optional)]** GraphQL 끝점을 입력합니다. 자세한 내용은 [메쉬 만들기](https://developer.adobe.com/graphql-mesh-gateway/mesh/basic/create-mesh)를 참조하십시오.

1. **[!UICONTROL Create Site]**&#x200B;을(를) 클릭합니다. 화면의 지침에 따라 GitHub 저장소에 대한 액세스 권한을 부여합니다.

프로세스가 완료되면 다음 방법을 사용하여 스토어를 사용자 정의할 수 있습니다.

* 코드 사용자 지정: `https://github.com/<username or org>/<repo name>`
* 콘텐츠 편집: `https://da.live/#/<username or org>/<repo name>`
* 구성 관리: `https://da.live/sheet#/<username or org>/<repo name>/configs-stage`
* 상점 미리 보기: `https://main--<repo name>--<username or org>.aem.page/`

## 다음 단계

자세한 내용은 다음 문서를 참조하십시오.

* [Storefront 콘텐츠 업데이트](./use-cases.md#update-storefront-content)—Storefront의 콘텐츠 및 데이터를 관리하고 표시합니다.
* [상황별 실험](./use-cases.md#contextual-experimentation)—상점에서의 실험을 만들고 관리합니다.
* [변형 생성](./use-cases.md#generate-variations) - 생성 AI를 사용하여 고품질 콘텐츠 생성을 자동화합니다.
* [Adobe Commerce Storefront 설명서](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=ko) - 사이트 콘텐츠를 업데이트하고 Commerce 프론트엔드 구성 요소 및 백엔드 데이터와 통합하는 방법에 대한 자세한 정보를 가져옵니다.
* [구성 서비스](https://www.aem.live/docs/config-service-setup)—저장소 구성을 `config.json`에서 리디렉션 구성 및 오버레이와 같은 고급 사용 사례를 지원하는 구성 서비스를 사용하도록 마이그레이션하는 방법에 대해 알아봅니다.
