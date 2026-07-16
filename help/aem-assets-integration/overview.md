---
title: Commerce용 AEM Assets 통합
description: Adobe Experience Manager Assets을  [!DNL Commerce] 인스턴스와 통합하여 Commerce 스토어프론트용 미디어 파일을 만들고 관리하는 방법에 대해 알아봅니다.
feature: CMS, Media, Configuration, Integration
exl-id: f450752a-bef1-419e-ad14-ff8879ab204b
TQID: https://experienceleague.adobe.com/CTDmM7Ox2rQ-55F1BVTg-C8DPBEuEpzFxXGtWpnjXKs
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
subfeature_v2:
  - id: e91a50b1-0b31-436e-9033-00e4776e94cb
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: da3860b0-d637-47df-bef0-273751180266
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 0c2e50338cbf286704239b6d1f628180e85a3bef
workflow-type: tm+mt
source-wordcount: 1081
ht-degree: 1%

---

# Commerce용 AEM Assets 통합

마케팅 예산이 압박을 받는 상황에서 개인화된 콘텐츠에 대한 수요는 빠르게 증가하고 있다. 소매업체와 브랜드는 지역별, 계절별 및 세그먼트별 요구 사항에 따라 제품 이미지의 변형이 필요하다는 요구에 발맞추지 못하고 있습니다.

1,000개의 제품이 있는 retailer을 고려해 보십시오. 서로 다른 지역, 고객 세그먼트 및 개인화 노력을 고려할 때 필요한 디지털 에셋의 수는 크게 확장됩니다. 이러한 상황은 수백만 개에 이르는 압도적인 수의 자산 변동을 초래할 수 있다.

![개요](assets/product-visuals-example.png){width="700" zoomable="yes"}

AEM Assets 통합은 자산 관리 워크플로우를 자동화하여 이 문제를 해결합니다. 통합은 SKU 또는 기타 주요 속성을 기반으로 디지털 에셋을 적절한 Adobe Commerce 제품 및 카테고리에 동적으로 연결합니다. 이 프로세스는 다음을 활성화하여 운영을 간소화하고 효율성을 향상시킵니다.

* **원활한 설치 및 구성** - 머천다이징 팀과 개발자는 익숙한 Adobe 도구 및 워크플로를 사용하여 신속하게 통합을 설정할 수 있습니다.

* **다이내믹 자산 업데이트** - 제품 이미지와 마케팅 자산은 AEM Assets의 최신 변경 사항을 자동으로 반영하므로 상점 전면이 정확하고 관련성이 유지됩니다.

* **간소화된 카탈로그 관리** - 자산 업데이트 및 정리를 자동화하여 수작업을 최소화하고 일관되고 잘 유지 관리되는 제품 카탈로그를 유지합니다.

## 통합 사용 요구 사항

이 통합을 [제품 시각화 또는 AEM Assets](https://experienceleague.adobe.com/ko/docs/commerce/cloud-service/overview#product-visuals-powered-by-aem-assets)와 활용하려면 기업은 다음 요구 사항을 충족해야 합니다.

>[!BEGINTABS]

>[!TAB 제품 시각화]

Adobe Commerce, AEM Assets에서 제공하는 제품 비주얼 및 [AEM Dynamic Media](https://experienceleague.adobe.com/ko/docs/experience-manager-65/content/assets/dynamic/administering-dynamic-media)에 대한 [!BADGE SaaS 전용]{type=Positive url="https://experienceleague.adobe.com/ko/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."}활성 라이선스([!DNL Adobe Commerce as a Cloud Service] 및 [!DNL Adobe Commerce Optimizer]에서 바로 사용 가능).

>[!TAB AEM Assets]

Adobe Commerce, Adobe Experience Manager Assets 및 [AEM Dynamic Media](https://experienceleague.adobe.com/ko/docs/experience-manager-65/content/assets/dynamic/administering-dynamic-media)에 대한 [!BADGE SaaS 전용]{type=Positive url="https://experienceleague.adobe.com/ko/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."}활성 라이선스

[!BADGE PaaS만 해당]{type=Informative tooltip="Adobe Commerce on Cloud 프로젝트에만 적용됩니다(Adobe 관리 PaaS 인프라)."} Adobe Commerce 2.4.5+

* PHP 8.1, 8.2, 8.3 및 8.4

* Composer 2.x

[!BADGE SaaS만]{type=Positive url="https://experienceleague.adobe.com/ko/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."} Adobe Experience Manager이 [Adobe Experience Manager Assets as a Cloud Service](https://experienceleague.adobe.com/ko/docs/experience-manager-cloud-service/content/assets/overview)와(과) 함께 프로비저닝되었습니다.

>[!ENDTABS]

통합을 구성하는 Adobe Commerce 사용자는 AEM Assets 프로젝트가 프로비저닝된 [IMS 조직](https://experienceleague.adobe.com/ko/docs/core-services/interface/administration/organizations#concept_EA8AEE5B02CF46ACBDAD6A8508646255)에 액세스할 수 있어야 합니다.

>[!BEGINSHADEBOX]

## 주요 비즈니스 이점

![확인](assets/icon-check.png) **추가 비용 없음** - 이 통합은 라이선스 요구 사항을 충족하는 판매자에게 무료로 제공됩니다.

![확인](assets/icon-check.png) **공식 Adobe 솔루션** - Adobe에서 개발, 유지 관리 및 완전히 지원하므로 향후 플랫폼 개선 사항에 맞게 안정성과 정렬을 보장합니다.

![확인](assets/icon-check.png) **Adobe 관리 지원 모델** - Adobe은 지원 및 문제 해결을 직접 처리하므로 안정적인 지원과 능률적인 문제 해결을 제공합니다.

![확인](assets/icon-check.png) **Adobe Storefront Builder 기능** - DAM(디지털 에셋 관리) 솔루션을 통해 [Storefront Builder](https://experienceleague.adobe.com/developer/commerce/storefront/merchants/storefront-builder/?lang=ko#userlabs-commerce-genai-product-visuals)에서 이미지, 비디오 및 기타 미디어와 같은 에셋을 사용할 수 있습니다.

>[!ENDSHADEBOX]

## 튜토리얼

Adobe Commerce과 AEM Assets 통합을 설정하고 사용하는 방법에 대해 알아보려면 다음 비디오를 시청하십시오.

>[!BEGINTABS]

>[!TAB 클라우드 또는 온-프레미스 자습서의 Adobe Commerce]

Adobe Commerce과 AEM Assets이 협력하여 콘텐츠 워크플로를 간소화하는 방법에 대해 알아보려면 이 비디오를 시청하십시오.

>[!VIDEO](https://video.tv.adobe.com/v/3447891?captions=kor)

>[!TAB Adobe Commerce as a Cloud Service 자습서]

AEM Assets 통합에서 Adobe Commerce as a Cloud Service을 사용하는 방법을 알아봅니다.

>[!VIDEO](https://video.tv.adobe.com/v/3478140?quality=12&learn=on)

>[!ENDTABS]

## 다음 단계

AEM Assets 통합을 설치하고 구성하는 프로세스는 Adobe Commerce 배포에 따라 다릅니다. 모든 경우에 먼저 AEM Assets을 구성한 다음 Commerce을 여기에 연결합니다.

통합이 AEM Assets 환경에 추가하는 네임스페이스, 메타데이터 스키마 및 **[!UICONTROL Commerce]** 탭을 이해하려면 시작하기 전에 [AEM Assets의 Commerce 메타데이터](metadata.md)를 검토하십시오.

다음 순서로 필요한 단계를 따르려면 배포를 선택합니다.

>[!BEGINTABS]

>[!TAB Adobe Commerce as a Cloud Service]

[!BADGE SaaS만]{type=Positive tooltip="Adobe Commerce as a Cloud Service 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."}

1. Commerce 메타데이터를 지원하려면 [AEM Assets 프로젝트를 구성](get-started/configure-aem.md)하십시오. AEM 릴리스 `2026.5.26309` 이상에서는 [셀프 서비스 온보딩](get-started/configure-aem.md#enable-aem-commerce-self-service)을(를) 사용합니다. 이전 릴리스에서는 `assets-commerce` 패키지를 수동으로 설치하십시오.

1. 자산 선택기와 자동으로 채워진 **[!UICONTROL Program ID]** 및 **[!UICONTROL Environment ID]** 필드를 사용할 수 있도록 [IMS 사용자 권한을 구성](get-started/permissions.md)합니다.

1. [Commerce 관리자에서 통합을 구성](get-started/setup-synchronization.md).

1. 선택 사항입니다. [제품 이미지 표시를 사용하도록 설정](get-started/configure-storefront.md#enable-product-images)하여 Edge Delivery Services에서 제공하는 상점이 AEM 관리 제품 이미지를 렌더링하도록 합니다.

>[!TAB PaaS(클라우드의 Adobe Commerce)]

[!BADGE PaaS만]{type=Informative tooltip="Adobe Commerce on Cloud 프로젝트에만 적용됩니다(Adobe 관리 PaaS 인프라)."}

1. Commerce 메타데이터를 지원하려면 [AEM Assets 프로젝트를 구성](get-started/configure-aem.md)하십시오. AEM 릴리스 `2026.5.26309` 이상에서는 [셀프 서비스 온보딩](get-started/configure-aem.md#enable-aem-commerce-self-service)을(를) 사용합니다. 이전 릴리스에서는 `assets-commerce` 패키지를 수동으로 설치하십시오.

1. 확장을 추가하고 필요한 자격 증명과 연결을 생성하려면 [Adobe Commerce 패키지를 설치](get-started/configure-commerce.md)하십시오.

1. 자산 선택기와 자동으로 채워진 **[!UICONTROL Program ID]** 및 **[!UICONTROL Environment ID]** 필드를 사용할 수 있도록 [IMS 사용자 권한을 구성](get-started/permissions.md)합니다.

1. [Commerce 관리자에서 통합을 구성](get-started/setup-synchronization.md).

1. 선택 사항입니다. [제품 이미지 표시를 사용하도록 설정](get-started/configure-storefront.md#enable-product-images)하여 Edge Delivery Services에서 제공하는 상점이 AEM 관리 제품 이미지를 렌더링하도록 합니다.

>[!TAB Adobe Commerce Optimizer]

[!BADGE SaaS만]{type=Positive tooltip="Adobe Commerce Optimizer 프로젝트에만 적용됩니다."}

[!DNL Adobe Commerce Optimizer] 관리자 구성 UI가 없습니다. Adobe 지원은 온보딩 티켓에서 통합을 구성하므로 먼저 AEM Assets을 준비하십시오.

1. Commerce 메타데이터를 지원하려면 [AEM Assets 프로젝트를 구성](get-started/configure-aem.md)하십시오. AEM 릴리스 `2026.5.26309` 이상에서는 [셀프 서비스 온보딩](get-started/configure-aem.md#enable-aem-commerce-self-service)을(를) 사용합니다. 이전 릴리스에서는 `assets-commerce` 패키지를 수동으로 설치하십시오.

1. 테넌트 ID, AEM 프로그램 ID, AEM 환경 ID, 일치하는 규칙, 레이어 및 로케일을 사용하여 [온보딩 지원 티켓을 제출합니다](get-started/configure-aco.md#onboarding).

1. 티켓에 등록한 동일한 로케일과 레이어로 [카탈로그 보기를 구성](get-started/configure-aco.md#onboarding)합니다.

1. 선택 사항입니다. [제품 이미지 표시를 사용하도록 설정](get-started/configure-storefront.md#enable-product-images)하여 Edge Delivery Services에서 제공하는 상점이 AEM 관리 제품 이미지를 렌더링하도록 합니다.

   전체 절차, 제한 사항 및 레이어 지침을 보려면 [Commerce Optimizer용 AEM Assets 구성](get-started/configure-aco.md)을 참조하십시오.

>[!ENDTABS]

## 지원

정보가 필요하거나 이 안내서에서 다루지 않는 질문이 있는 경우 AEM Assets 통합 영업 담당자에게 문의하거나 [지원 티켓](https://experienceleague.adobe.com/ko/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#support-case)을 만들어 추가 도움을 받으십시오.
