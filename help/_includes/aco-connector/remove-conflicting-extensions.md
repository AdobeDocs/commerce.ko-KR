---
source-git-commit: a3ade1a31d3c2905b601f71bda118de89c43cf59
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 27%
---

# 충돌하는 확장 제거

다음 확장이 설치되어 있는 경우 [!DNL Adobe Commerce Optimizer Connector for B2B]을(를) 설치하기 전에 해당 확장을 제거하십시오.

* [!DNL Adobe Commerce Live Search] (`magento/live-search`)
* [!DNL Adobe Commerce Product Recommendations] (`magento/product-recommendations`)
* [!DNL Adobe Commerce Catalog Service] (`magento/catalog-service`, `magento/catalog-service-installer`)
* **[!UICONTROL Data Management Dashboard]** (`magento-catalog-sync-admin`)

이러한 확장과 연결된 데이터는 여전히 Commerce 데이터베이스에서 사용할 수 있습니다. 그러나 커넥터를 사용하도록 설정한 경우 [!DNL Commerce Optimizer]&#x200B;(으)로 내보내지 않습니다. 커넥터를 사용하도록 설정한 후 이러한 확장에서 제공하는 Adobe Commerce 검색 및 머천다이징 기능을 구현하려면 [[!DNL Commerce Optimizer] 관리 UI](https://experienceleague.adobe.com/en/docs/commerce/optimizer/overview#quick-tour)에서 구성하십시오.

>[!IMPORTANT]
>
>커넥터를 사용하기 전에 이러한 확장을 제거하지 않으면 구성 화면이 손상되고 [!DNL Commerce Optimizer]에 데이터가 중복되며 401 또는 403 인증 오류가 발생합니다.