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
source-git-commit: 7f901cec90291e264376e3f93e6ebaaccf7c15f0
workflow-type: tm+mt
source-wordcount: 610
ht-degree: 0%

---

# Storefront 구성

## AEM Assets에서 제품 이미지 표시 활성화 {#enable-product-images}

AEM Assets 통합은 Adobe Commerce 대신 AEM Assets의 제품 이미지를 표시하여 고급 최적화, 자르기 및 CDN 전달을 활성화합니다.

Edge Delivery Services에서 제공하는 Commerce storefront에서 통합을 사용하려면 `"commerce-assets-enabled": true` 매개 변수를 storefront 구성 파일(`config.json`)에 추가하십시오.

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

Edge Delivery Services에서 제공하는 Commerce Storefront와 함께 AEM Assets을 사용하는 방법에 대한 자세한 내용은 *AEM Assets Storefront* 설명서의 [Adobe Commerce 통합](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/aem-assets-configuration/?lang=ko) 항목을 참조하십시오.

>[!TIP]
>
>작성자가 AEM Assets을 검색하여 정적 콘텐츠 페이지에 삽입하려면 [정적 콘텐츠 작성을 위해 AEM Assets을 Da.live에 연결](#connect-aem-assets-authoring)을 참조하십시오.

## 정적 콘텐츠 작성을 위해 AEM Assets을 Da.live에 연결 {#connect-aem-assets-authoring}

>[!NOTE]
>
>이 설정은 AEM Assets 통합 확장과 별개입니다. [Da.live](https://da.live){target="_blank"}에서 제공하는 이 기능을 통해 작성자는 [!UICONTROL Library] 패널 및 [!UICONTROL Content Advisor]을(를) 통해 정적 콘텐츠 페이지(예: 랜딩 페이지 또는 콘텐츠 블록)에 AEM Assets을 검색하고 삽입할 수 있습니다. AEM Assets 통합을 통해 동기화된 제품 이미지는 `commerce-assets-enabled` 설정을 사용하여 별도로 구성됩니다.

다음 단계를 사용하여 AEM Assets을 문서 작성(Da.live) 상점 앞에 연결하면 작성자가 정적 콘텐츠를 편집하는 동안 **[!UICONTROL Content Advisor]**&#x200B;에서 AEM Assets을 검색하고 삽입할 수 있습니다.

>[!NOTE]
>
>자세한 설정 지침은 Da.live 설명서에서 [AEM Assets 설정](https://docs.da.live/administrators/guides/setup-aem-assets){target=_blank} 및 AEM Assets 설명서에서 [Edge Delivery Services에 대한 콘텐츠를 작성하는 동안 AEM Assets 통합](https://experienceleague.adobe.com/ko/docs/experience-manager-cloud-service/content/assets/integrate-aem-assets-edge-delivery-services/integrate-aem-assets-edge-delivery-services){target=_blank}을 참조하십시오.

### 1단계: Da.live에서 사이트 구성 열기

1. [Da.live](https://da.live){target=_blank}에서 상점을 찾아 엽니다.

1. 이동 경로 탐색에서 사이트 이름 옆에 있는 **[!UICONTROL Settings]** 아이콘을 선택하여 사이트 구성 스프레드시트를 엽니다.

### 2단계: AEM 저장소 URL 복사

1. 새 탭에서 [experience.adobe.com](https://experience.adobe.com){target=_blank}(으)로 이동하여 **[!UICONTROL Experience Manager]**(으)로 이동합니다.

1. Adobe Experience Manager Assets을 엽니다. **[!UICONTROL My Authoring]** 섹션으로 이동한 다음 **[!UICONTROL Production]** 환경 옆에 있는 **[!UICONTROL Assets]**&#x200B;을(를) 선택합니다.

1. 브라우저 주소 표시줄에서 `author`(으)로 시작하는 세그먼트를 `.com`(예: `author-p107634-e1009805.adobeaemcloud.com`)까지 복사합니다.

### 3단계: 구성에 저장소 ID 추가

1. 사이트를 구성하려면 Da.live로 돌아가서 사이트 구성에서 **[!UICONTROL data]**&#x200B;을(를) 선택하십시오.

1. 다음과 같이 스프레드시트를 작성합니다.

   | 셀 | 값 |
   |---|---|
   | A1 | `key` |
   | B1 | `value` |
   | A2 | `aem.repositoryId` |
   | B2 | 2단계에서 복사한 URL |

1. **[!UICONTROL Save]**&#x200B;을(를) 선택한 다음 사이트 이름 옆에 있는 뒤로 화살표를 선택하여 사이트 루트로 돌아갑니다.

   >[!NOTE]
   >
   > `author-` 접두사가 있는 호스트가 작성자 계층에서 자산을 찾습니다. 대신 Dynamic Media를 통해 자산을 전달하려면 접두사가 있는 `delivery-` 호스트를 사용하십시오. 모든 `aem.repositoryId` 옵션에 대해서는 [AEM Assets 설치](https://docs.da.live/administrators/guides/setup-aem-assets){target=_blank}를 참조하십시오.

### 4단계: 라이브러리를 통해 AEM Assets 연결

1. 사이트 루트에서 **[!UICONTROL index]** 폴더를 선택하여 엽니다.

1. 편집기에서 **[!UICONTROL Library]** 패널을 열고 **[!UICONTROL AEM Assets]**&#x200B;을(를) 선택합니다.

   **[!UICONTROL Content Advisor]** 팝오버가 열리고 AEM Assets 폴더 및 파일이 표시됩니다.

이제 상점이 AEM Assets에 연결되었습니다. **[!UICONTROL Content Advisor]**&#x200B;에서 직접 자산을 검색하고 삽입할 수 있습니다.

## 관련 설명서

* *AEM Assets Storefront* 설명서의 [Adobe Commerce 통합](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/aem-assets-configuration/?lang=ko){target=_blank}—storefront 구성 및 이미지 처리 동작.

* *AEM Assets* 설명서에서 [Edge Delivery Services에 대한 콘텐츠를 작성하는 동안 AEM Assets을 통합](https://experienceleague.adobe.com/ko/docs/experience-manager-cloud-service/content/assets/integrate-aem-assets-edge-delivery-services/integrate-aem-assets-edge-delivery-services){target=_blank}합니다.

* Da.live 설명서에서 [AEM Assets 설치](https://docs.da.live/administrators/guides/setup-aem-assets){target=_blank} 및 [미디어 작업](https://docs.da.live/authors/guides/adding-media){target=_blank}
