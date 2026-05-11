---
title: Storefront 구성
description: Edge Delivery Services 상점 첫 페이지를 AEM Assets 통합에 연결하는 방법에 대해 알아봅니다.
feature: CMS, Media, Integration
TQID: https://experienceleague.adobe.com/gl0Y2UNs3sYkXE9QYwLtAltyX1dxE699y23ey-y0KUU
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
subfeature_v2:
  - id: ae62cf09-5996-4921-bda8-fbe67b62e470
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
topic_v2:
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 137
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

Edge Delivery Services에서 제공하는 Commerce Storefront와 함께 AEM Assets을 사용하는 방법에 대한 자세한 내용은 *Adobe Commerce Storefront* 설명서의 [AEM Assets 통합](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/aem-assets-configuration/?lang=ko) 주제에 설명된 Storefront 구성을 완료하십시오.
