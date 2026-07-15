---
title: AEM Assets의 Commerce 메타데이터
description: AEM Assets 통합이 Commerce 작성 환경에 추가하는 AEM Assets 네임스페이스, 메타데이터 스키마 및 대체 텍스트에 대해 알아봅니다.
feature: CMS, Media, Integration
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: da3860b0-d637-47df-bef0-273751180266
source-git-commit: 0c2e50338cbf286704239b6d1f628180e85a3bef
workflow-type: tm+mt
source-wordcount: 749
ht-degree: 0%

---

# AEM Assets의 Commerce 메타데이터

Commerce 메타데이터는 AEM Assets과 Commerce 간의 계약입니다. Commerce에 대한 에셋, 에셋이 속한 제품 및 에셋을 사용하거나 표시하는 방법을 Commerce에 알려줍니다. 이 메타데이터를 사용하면 AEM Assets 통합에서 자산 파일을 올바르게 매핑하고 동기화할 수 있습니다.

Commerce 메타데이터를 사용하면 다음 기능을 사용할 수 있습니다.

* `commerce:isCommerce` 필드를 통해 **자산을 Commerce 적격 자산으로 표시**.
* `commerce:skus` 필드를 통해 **자산을 하나 이상의 제품 SKU와 연결**&#x200B;합니다.
* **에셋이 `commerce:roles` 및 `commerce:positions` 필드를 통해 Commerce에 표시되는 방식을 정의합니다**.
* `commerce:altTextStoreViews` 및 `commerce:altTextValues` 필드를 통해 **스토어 보기에서 입력한 Commerce 전용 대체 텍스트를 추가**&#x200B;합니다.
* **[!UICONTROL Commerce]** 탭 및 스키마 양식을 통해 **AEM Assets 속성 UI에 이러한 필드를 표시합니다**.

>[!IMPORTANT]
>
>**Commerce 전용 대체 텍스트** 기능은 아직 [셀프 서비스 온보딩](get-started/configure-aem.md#enable-aem-commerce-self-service)을 통해 사용할 수 없습니다. 현재 `assets-commerce` 사용자 지정 코드 패키지를 배포하는 경우에만 제공됩니다([assets-commerce 패키지를 수동으로 설치](get-started/configure-aem.md#install-the-assets-commerce-package-manually) 참조). 향후 AEM 릴리스에 대한 기본 지원이 예정되어 있습니다.

AEM 프로젝트에서 이러한 리소스를 구성하려면 [AEM Assets 프로젝트 구성](get-started/configure-aem.md)을 참조하십시오. 이 항목의 나머지 부분에서는 메타데이터 제공 방법에 대해 설명합니다.

## AEM Commerce assets-commerce 패키지 콘텐츠

Adobe은 Experience Manager Assets as a Cloud Service 구성에 Commerce 네임스페이스 및 메타데이터 스키마 리소스를 추가할 수 있는 `assets-commerce` AEM Commerce 코드 패키지를 제공합니다.

이 패키지 코드는 AEM Assets 작성 환경에 다음 리소스를 추가합니다.

* Commerce 관련 속성을 식별하기 위한 [사용자 지정 네임스페이스](https://github.com/ankumalh/assets-commerce/blob/main/ui.config/jcr_root/apps/commerce/config/org.apache.sling.jcr.repoinit.RepositoryInitializer~commerce-namespaces.cfg.json), `Commerce`입니다.

   * Adobe Commerce 프로젝트와 연결된 Commerce 자산에 태그를 지정하는 레이블이 `Eligible for Commerce`인 사용자 지정 메타데이터 형식 `commerce:isCommerce`입니다.

   * **[!UICONTROL Product Data]** 속성을 추가할 사용자 지정 메타데이터 형식 `commerce:skus` 및 해당 UI 구성 요소입니다. 제품 데이터에는 Commerce 에셋을 제품 SKU와 연결하는 메타데이터 속성이 포함됩니다.

     ![사용자 지정 제품 데이터 UI 컨트롤](assets/aem-commerce-sku-metadata-fields-from-template.png){width="600" zoomable="yes"}

   * Commerce에서 에셋이 시각화되는 방식을 보여 주는 사용자 지정 메타데이터 형식 `commerce:roles` 및 `commerce:positions` 특성입니다.

   * 편집자가 각 Commerce 스토어 보기 코드에 대해 대체 텍스트를 입력할 수 있도록 대체 텍스트 다중 필드(_[!UICONTROL Alt texts]_) 메타데이터입니다. 다중 필드는 두 개의 인덱스 정렬 `String[]` 속성에서 유지됩니다.

      * `commerce:altTextStoreViews` — 각 행의 보기 코드를 저장합니다.
      * `commerce:altTextValues` — `commerce:altTextStoreViews`의 각 항목과 동일한 인덱스에서 대체 텍스트와 일치합니다.

     [외부 선택기](synchronize/custom-match.md){target=_blank}를 사용하는 App Builder 구현은 자산 페이로드를 변환할 때 이러한 속성을 가로챌 수 있습니다. 따라서 카탈로그에서 제품 이미지가 지정되거나 범위가 지정되는 방식은 변경되지 않습니다. [AEM Assets 메타데이터의 지역화된 대체 텍스트](#localized-alt-text-in-aem-assets-metadata)를 참조하십시오.

* Commerce 자산에 태그를 지정할 `Eligible for Commerce` 및 `Product Data` 필드가 포함된 Commerce 탭이 있는 메타데이터 스키마 양식입니다. 이 양식은 AEM Assets UI에서 `roles` 및 `position` 필드를 표시하거나 숨기는 옵션도 제공합니다.

  AEM Assets 메타데이터 스키마 양식에 대한 ![Commerce 탭](assets/assets-configure-metadata-schema-form-editor.png){width="600" zoomable="yes"}

* 초기 에셋 동기화를 지원하기 위해 [샘플 Commerce 에셋이 태그되고 승인되었습니다](https://github.com/ankumalh/assets-commerce/blob/main/ui.content/src/main/content/jcr_root/content/dam/wknd/en/activities/hiking/equipment_6.jpg/.content.xml) `equipment_6.jpg`. 승인된 Commerce 자산만 AEM Assets에서 Adobe Commerce으로 동기화할 수 있습니다.

>[!NOTE]
>
> **AEM Commerce 패키지 코드**&#x200B;에 대한 자세한 내용은 GitHub의 [readme](https://github.com/ankumalh/assets-commerce) 페이지를 참조하십시오.

## AEM Assets 메타데이터의 현지화된 대체 텍스트

_[!UICONTROL Alt texts]_&#x200B;다중 필드는 적격 이미지를 편집할 때&#x200B;**[!UICONTROL Commerce]**&#x200B;탭의 AEM Assets 에셋 메타데이터 편집기에서 사용할 수 있습니다.

>[!IMPORTANT]
>
> 스토어별 보기 동작은 대체 텍스트에만 적용됩니다. AEM Assets 통합은 Adobe Commerce 스토어 보기당 다른 제품 이미지를 동기화하지 않습니다. AEM의 제품 이미지는 이 릴리스 전과 동일한 갤러리 할당 동작으로 Commerce에 계속 동기화됩니다.

다중 필드에는 Commerce 스토어 보기당 하나의 행이 포함됩니다. 각 행에는 두 개의 입력이 있습니다.

* **[!UICONTROL Store View Code]** — 저장소 보기 식별자(예: `default` 또는 `en_US`).

* **[!UICONTROL Alt Text]** — 255자로 제한된 해당 스토어 보기에 대한 대체 텍스트입니다.

저장소 보기를 추가할 행을 더 추가하려면 **[!UICONTROL Add]**&#x200B;을(를) 선택하십시오. 행을 제거하려면 해당 행에서 **[!UICONTROL Delete]** 아이콘을 선택하여 제거합니다.

![저장소 보기 코드와 대체 텍스트 입력이 있는 다중 필드](assets/commerce-metadata-alt-texts-multifield.png){width="600" zoomable="yes"}

저장할 때, 행에 빈 _[!UICONTROL Store View Code]_&#x200B;이(가) 있거나 두 행이 동일한 저장소 보기 코드를 사용하는 경우(대/소문자 구분 안 함) 클라이언트측 유효성 검사가 제출을 차단합니다.

대체 텍스트 항목은 JCR 자산 메타데이터에서 두 개의 인덱스 정렬 `String[]` 속성으로 유지됩니다.

* `commerce:altTextStoreViews`: 각 행에 대한 보기 코드를 저장합니다.
* `commerce:altTextValues`: `commerce:altTextStoreViews`의 각 항목과 동일한 인덱스에 있는 대체 텍스트와 일치합니다.

이러한 에셋이 Adobe Commerce과 동기화되면 일치하는 스토어 보기 코드에 대해 스토어별 보기 대체 텍스트가 제품 미디어 갤러리에 작성됩니다. 기본 이미지 매핑이 변경되지 않았습니다.
