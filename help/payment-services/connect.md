---
title: 인스턴스 연결
description: API 키 및 개인 키를 사용하여 Commerce 인스턴스를 연결하고 구성에서 데이터 공간을 지정합니다.
feature: Payments, Checkout, Configuration, Saas
exl-id: f2b3be02-e9dd-4bca-b9e4-c80a56bf8691
source-git-commit: 16bd0e7ed1e8982e1571e2593115824a2004b7dc
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 0%

---

# 인스턴스 연결

[!DNL Payment Services]은(는) Commerce 서비스에서 구동되며 SaaS(Software as a Service)로 배포됩니다. API 키 및 개인 키를 사용하여 Commerce 인스턴스를 연결하고 [Commerce 서비스 커넥터](https://experienceleague.adobe.com/docs/commerce/user-guides/saas.html)를 사용하여 구성에 데이터 공간을 지정합니다. **이 연결을 한 번만 설정했습니다.**

>[!VIDEO](https://video.tv.adobe.com/v/3447835)

>[!INFO]
>
> 자세한 내용은 [[!DNL Adobe Commerce] 서비스 커넥터](https://experienceleague.adobe.com/docs/commerce-learn/tutorials/admin/adobe-commerce-services/configure-adobe-commerce-services-connector.html?lang=en) 비디오를 참조하십시오.

* *이미 인스턴스에 연결*&#x200B;한 경우 API 자격 증명을 획득 및 사용하고 Commerce 서비스를 구성하면 [테스트 샌드박스 설정](https://experienceleague.adobe.com/docs/commerce/payment-services/get-started/sandbox.html)을 진행할 수 있습니다.
* *인스턴스에 연결해야 하는 경우* 이 항목에서 [API 자격 증명 가져오기](#obtain-api-credentials) 및 [Commerce 서비스 구성](#configure-commerce-services)에 대한 정보를 참조하십시오.
* 인스턴스가 연결되어 있는지 *확실하지 않은 경우* **시스템** > 서비스 > **Commerce 서비스 커넥터**&#x200B;로 이동하여 [!UICONTROL Sandbox Keys] 및 [!UICONTROL Production Keys] 섹션과 [!UICONTROL SaaS Identifier] 섹션의 *프로젝트* 및 *데이터 공간* 필드를 확인하십시오. 해당 값이 있으면 인스턴스가 연결됩니다.

>[!NOTE]
>
>결제 서비스를 받을 수 있는 모든 가맹점은 하나의 프로덕션 데이터 공간과 두 개의 테스트 데이터 공간을 사용할 수 있습니다.

## API 자격 증명 가져오기

Commerce SaaS 서비스를 사용하려면 샌드박스와 프로덕션에 모두 인스턴스의 API 키(Commerce 공개 API 키 및 개인 키)를 사용해야 합니다. 이 키는 [내 계정 대시보드](https://account.magento.com/customer/account/login)에서 만들고 관리합니다. [한 번에 한 쌍만 활발하게 사용할 수 있지만 Commerce 계정(샌드박스 계정과 프로덕션 계정)에 대해 키 쌍](https://experienceleague.adobe.com/en/docs/commerce-admin/config/services/saas)을 만들 수 있습니다.

>[!NOTE]
>
>[!UICONTROL My Account] 대시보드에 액세스하는 데 도움이 필요하십니까? [Commerce 계정 만들기](https://experienceleague.adobe.com/en/docs/commerce-admin/start/commerce-account/commerce-account-create)를 참조하세요.

공개 API 키가 생성되면 내 계정 대시보드에서 항상 사용할 수 있습니다. 필요에 따라 복사하거나 삭제할 수 있습니다. 샌드박스 또는 프로덕션용 공개 API 키를 만들면 개인 API 키가 표시됩니다. 이 키는 다음 대화 상자에서 복사하거나 저장하는 데만 사용할 수 있으며 나중에 액세스할 수 없습니다.

지정된 API 키 쌍은 환경의 모든 Commerce 서비스에 대해 유효하므로 인스턴스에 대해 Commerce 서비스가 이미 구성되어 있는 경우 API 키 쌍이 Commerce 서비스 커넥터에 이미 있습니다.

API 키가 손실된 경우 새 API 키 쌍은 관리자의 Commerce 서비스 커넥터 구성에 [생성](https://experienceleague.adobe.com/docs/commerce/payment-services/get-started/connect.html#generate-an-api-key-and-private-key) 및 [적용](https://experienceleague.adobe.com/docs/commerce/payment-services/get-started/connect.html#configure-saas-project)되어야 합니다. 잘못된 키가 구성되었거나 구성에 아무 것도 없는 경우, 계정이 확인되지 않았음을 알리는 계정 확인 오류 대화 상자가 결제 서비스에 나타납니다.

[API를 사용하는 사용 가능한 Commerce 서비스 목록](https://experienceleague.adobe.com/en/docs/commerce/user-guides/integration-services/saas#availableservices)을 참조하세요.

샌드박스 또는 프로덕션 환경에 대한 API 키를 생성하는 방법에 대해 알아보려면 [자격 증명](https://experienceleague.adobe.com/docs/commerce/user-guides/saas.html#apikey)을 참조하세요.

>[!IMPORTANT]
>
>API 키 쌍 *및*&#x200B;을(를) 다시 생성하지 않고 활성 프로덕션 인스턴스의 SaaS 식별자 및/또는 데이터 공간을 변경하는 것이 좋습니다. 인스턴스가 수정되면 해당 인스턴스의 데이터가 손실됩니다.

## Commerce 서비스 구성

인스턴스 간에 동일한 API 키를 사용할 수 있지만 각 인스턴스에는 고유한 [SaaS 데이터 공간](https://experienceleague.adobe.com/docs/commerce/user-guides/saas.html#saasenv)이 있어야 합니다.

>[!NOTE]
>
>판매자는 결제 권한에 대해 MageID에 대해 생성된 동일한 키를 사용해야 합니다.

자격 증명을 받았으므로 SaaS 프로젝트 및 Saas 데이터 공간을 구성할 수 있습니다.

1. _관리자_ 사이드바에서 **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]**(으)로 이동합니다.
1. **[!UICONTROL Configure Commerce Services]**&#x200B;을(를) 클릭합니다.

   계정에 대해 Commerce 서비스를 아직 구성하지 않은 경우 이 옵션이 표시됩니다.

   Commerce 서비스 커넥터를 구성하려면 관리자 **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**>**[!UICONTROL Commerce Services Connector]**&#x200B;의 구성 영역으로 이동됩니다.

1. Commerce 서비스를 구성하려면 [SaaS 구성](https://experienceleague.adobe.com/docs/commerce/user-guides/integration-services/saas.html#saasenv)에 설명된 단계를 수행합니다.

   >[!INFO]
   >
   > 자세한 내용은 [[!DNL Adobe Commerce] 서비스 커넥터](https://experienceleague.adobe.com/docs/commerce-learn/tutorials/admin/adobe-commerce-services/configure-adobe-commerce-services-connector.html?lang=en#configuration-faqs) 비디오를 참조하십시오.

## 엔드포인트

[!DNL Payment Services]은(는) [Commerce 서비스 커넥터](https://experienceleague.adobe.com/docs/commerce/user-guides/saas.html)를 사용하여 Commerce 서비스에 연결하고 SaaS로 배포합니다. 이 [!DNL Commerce Services Connector]은(는) 다음 위치의 끝점을 통해 통신합니다.

* 샌드박스 환경용 `commerce-beta.adobe.io`
* `commerce.adobe.io for`(실시간 환경).
