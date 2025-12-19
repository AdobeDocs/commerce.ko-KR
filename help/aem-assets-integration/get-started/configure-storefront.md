---
title: Storefront 구성
description: Edge Delivery Services 상점 첫 페이지를 AEM Assets 통합에 연결하는 방법에 대해 알아봅니다.
feature: CMS, Media, Integration
source-git-commit: d426c7878f7a66fe1047673be7c5bf65ae1949a7
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 0%

---


# Storefront 구성

AEM Assets 통합은 Adobe Commerce에서 호스팅되는 이미지를 사용하는 대신 AEM Assets에서 관리되는 제품 이미지를 표시합니다. 이 통합을 통해 Adobe의 CDN(Content Delivery Network)을 통한 고급 최적화, 자르기 및 전달을 비롯한 이미지 관리 기능을 개선할 수 있습니다.

Edge Delivery Services에서 제공하는 Commerce storefront에서 통합을 사용하려면 storefront 구성 파일(`config.json`)을 업데이트하여 `"commerce-assets-enabled": true` 매개 변수를 추가하십시오.

```json
{
  "public": {
    "default": {
      "commerce-assets-enabled": true
    }
  }
}
```

Commerce 드롭인에서 `commerce-assets-enabled` 구성을 자동으로 감지하고 그에 따라 이미지 처리를 조정합니다.

Edge Delivery Services에서 제공하는 Commerce Storefront와 함께 AEM Assets을 사용하는 방법에 대한 자세한 내용은 [Adobe Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/aem-assets-configuration/?lang=ko) 설명서의 *AEM Assets 통합* 주제에 설명된 Storefront 구성을 완료하십시오.
