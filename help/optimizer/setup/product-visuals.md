---
title: AEM Assets을 사용한 제품 시각화
description: ' [!DNL Adobe Commerce Optimizer]에서 제품 이미지에 AEM Assets을 사용하는 방법에 대해 알아봅니다.'
feature: CMS, Media, Configuration, Integration
role: Admin, Developer
badgeSaas: label="SaaS만" type="Positive" url="https://experienceleague.adobe.com/ko/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 [!DNL Adobe Commerce Optimizer] 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."
source-git-commit: 264658bee09a22cfd55828c6960153cc1239d3fb
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---


# AEM Assets을 사용한 제품 시각화

제품 비주얼을 사용하면 [!DNL Adobe Commerce Optimizer] 판매자가 Adobe Experience Manager(AEM) Assets을 통해 제품 이미지를 관리할 수 있습니다. 이 통합은 카탈로그 계층을 사용하여 AEM Assets의 고품질 제품 이미지를 [!DNL Commerce Optimizer] 카탈로그와 동기화하기 위한 원활한 워크플로를 제공합니다.

>[!NOTE]
>
>**제품 시각적 개체**&#x200B;은(는) [!DNL Adobe Commerce as a Cloud Service] 및 [!DNL Adobe Commerce Optimizer]과(와) 함께 제공된 번들의 이름입니다. [Dynamic Media를 OpenAPI 기능과 결합](https://experienceleague.adobe.com/ko/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/dynamic-media-open-apis-overview) 및 [AEM Assets Prime](https://experienceleague.adobe.com/ko/docs/experience-manager-cloud-service/content/assets/assets-prime).
>
>다른 AEM Assets 라이선스(예: **AEM Assets Ultimate**)를 가진 고객은 동일한 통합을 사용할 수 있습니다. AEM 릴리스만 온보딩 단계에 영향을 주고 라이선스 유형은 영향을 주지 않습니다.

## 주요 이점

* **중앙 집중식 자산 관리**: 엔터프라이즈급 디지털 자산 관리 솔루션인 AEM Assets에서 모든 제품 이미지를 관리합니다.
* **자동 동기화**: AEM Assets에서 에셋을 승인하거나 업데이트할 때 제품 이미지가 자동으로 동기화됩니다.
* **Dynamic Media 게재**: 최적화된 이미지 게재를 위해 OpenAPI 기능이 있는 Dynamic Media를 활용하십시오.
* **카탈로그 레이어**: 제품 이미지가 카탈로그 레이어로 적용되어 기본 카탈로그에 AEM Assets 이미지를 오버레이할 수 있습니다.

## 작동 방식

통합에는 두 개의 독립적인 이벤트 흐름이 있습니다. 두 방법 모두 [Adobe I/O Events](https://developer.adobe.com/events/docs/)을 사용하여 이벤트를 Assets 통합 서비스로 전송하지만 각 방향에서는 고유한 이벤트 공급자를 사용합니다.

* **AEM Assets에서 Assets 통합 서비스로**: 에셋이 승인, 거부 또는 제거되면 이벤트가 Assets 통합 서비스로 전달됩니다. 이 서비스는 `match-by-SKU` 또는 사용자 지정 일치 전략을 사용하여 자산을 제품에 일치시킨 다음 `product-asset` 매핑을 [!DNL Commerce Optimizer]에 보내 제품 계층으로 저장합니다.

* **[!DNL Commerce Optimizer]에서 Assets 통합 서비스로**: [!DNL Commerce Optimizer]에서 제품을 업데이트하면 이벤트가 Assets 통합 서비스로 전달됩니다. 서비스가 일치하는 모든 자산 매핑을 다시 [!DNL Commerce Optimizer]&#x200B;(으)로 동기화합니다.

업데이트된 이미지는 상점 API(카탈로그 서비스, 라이브 검색, 제품 추천)를 통해 사용할 수 있습니다.

### Source 및 레이어 구성

AEM Assets의 이미지는 다음 소스 구성을 사용하는 카탈로그 레이어로 수집됩니다.

> 소스 구성의 예

```json
{
  "source": {
    "locale": "en-US",
    "layer": "AEM-Assets"
  }
}
```

이 구성은 AEM Assets 이미지가 기본 제품 카탈로그에 오버레이로 적용되도록 합니다.

## 사전 요구 사항

제품 비주얼을 활성화하기 전에 [Commerce Optimizer의 필수 구성 요소](../../aem-assets-integration/get-started/configure-aco.md#prerequisites)를 충족하는지 확인하십시오.

## 설정

통합을 사용하려면 [!DNL Commerce Optimizer] 및 AEM Assets 세부 정보를 사용하여 [지원 티켓을 만들기](https://experienceleague.adobe.com/ko/docs/commerce-learn/tutorials/help-and-support/create-a-support-ticket)하십시오. Adobe 지원은 통합을 구성하고 테넌트를 Assets 통합 서비스에 등록합니다.

온보딩 정보는 [Commerce Optimizer용 AEM Assets 구성](../../aem-assets-integration/get-started/configure-aco.md)을 참조하십시오.

### AEM Assets 메타데이터 구성

자동 제품 일치를 활성화하려면 Commerce 메타데이터를 사용하여 AEM Assets에서 자산을 구성합니다.

필요한 메타데이터 필드 및 단계는 [AEM Assets 구성](../../aem-assets-integration/get-started/configure-aco.md#configure-aem-assets-first)을 참조하십시오.

## 제한 사항

제품 비주얼을 사용하기 전에 AEM Assets 데이터가 기본 카탈로그와 병합되는 방식에 영향을 주는 레이어 관련 제한인 [통합 제한](../../aem-assets-integration/get-started/configure-aco.md#limitations)을 검토하십시오.

용량 및 사용량 할당(자산 저장소, Dynamic Media 작업, 사용자 라이선스)에 대해서는 _경계 및 제한 안내서_&#x200B;의 [제품 시각적 개체 제한](../boundaries-limits.md#product-visuals-limits)을 참조하십시오.

## 제품 시각화 사용

통합이 구성된 후 AEM Assets을 통해 제품 이미지를 관리합니다.

### 제품에 이미지 추가

1. AEM Assets 저장소에 이미지를 업로드합니다.

1. Commerce 메타데이터를 에셋에 추가합니다.

   [기본 자동 일치](../../aem-assets-integration/synchronize/default-match.md) 및 [사용자 지정 자동 일치](../../aem-assets-integration/synchronize/custom-match.md)를 참조하십시오.

1. 게재할 자산을 승인합니다. 동기화를 트리거하려면 자산이 **승인됨** 상태여야 합니다.

1. 이미지가 [!DNL Commerce Optimizer]에 자동으로 동기화됩니다.

### AEM-Assets 레이어 적용

상점에 AEM Assets 이미지를 표시하려면 [카탈로그 보기에 `AEM-Assets` 레이어를 할당](catalog-layer.md#assign-the-aem-assets-layer-to-a-catalog-view)하세요.

## 다음과 같음

* [카탈로그 레이어](catalog-layer.md)
* [카탈로그 보기](catalog-view.md)
* [AEM Assets 통합 안내서](../../aem-assets-integration/overview.md)
