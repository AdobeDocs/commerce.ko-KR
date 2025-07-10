---
title: Commerce용 AEM Assets 통합
description: Adobe Experience Manager Assets을  [!DNL Commerce] 인스턴스와 통합하여 Commerce 스토어프론트용 미디어 파일을 만들고 관리하는 방법에 대해 알아봅니다.
feature: CMS, Media, Configuration, Integration
exl-id: f450752a-bef1-419e-ad14-ff8879ab204b
source-git-commit: 9e6f8ae86b28577e2b2c675dbf274c762abe9f3f
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 0%

---

# Commerce용 AEM Assets 통합

마케팅 예산이 압박을 받는 상황에서 개인화된 콘텐츠에 대한 수요는 빠르게 증가하고 있다. 소매업체와 브랜드는 지역별, 계절별 및 세그먼트별 요구 사항에 따라 제품 이미지의 변형이 필요하다는 요구에 발맞추지 못하고 있습니다.

1,000개의 제품이 있는 retailer을 고려해 보십시오. 속성 변형을 인수분해하기 전이라도 서로 다른 지역, 고객 세그먼트 및 개인화 노력을 고려할 때 필요한 디지털 에셋의 수는 크게 확장됩니다. 이로 인해 수백만 개에 이르는 압도적인 수의 에셋 변형이 발생할 수 있다.

![개요](assets/product-visuals-example.png){width="700" zoomable="yes"}

AEM Assets 통합은 자산 관리 워크플로우를 자동화하여 이 문제를 해결합니다. 이 통합을 통해 제품 이미지 및 마케팅 컨텐츠와 같은 디지털 에셋이 SKU 또는 기타 주요 속성을 기반으로 Adobe Commerce의 제품 및 카테고리를 비롯한 적절한 머천다이징 엔티티에 동적으로 연결됩니다. 이 프로세스는 다음을 활성화하여 운영을 간소화하고 효율성을 향상시킵니다.

* **원활한 설치 및 구성** - 머천다이징 팀과 개발자는 익숙한 Adobe 도구 및 워크플로를 사용하여 신속하게 통합을 설정할 수 있습니다.

* **다이내믹 자산 업데이트**-제품 이미지 및 마케팅 자산은 AEM Assets의 최신 변경 사항을 자동으로 반영하므로 상점 전면이 정확하고 관련성이 유지됩니다.

* **간소화된 카탈로그 관리**-자산 새로 고침 및 정리를 자동화하여 수작업을 최소화하고 일관되고 잘 유지 관리되는 제품 카탈로그를 유지합니다.

## 통합 사용 요구 사항

제품 비주얼이나 AEM Assets과 이러한 통합을 활용하려면 기업은 다음 요구 사항을 충족해야 합니다.

>[!BEGINTABS]

>[!TAB 제품 시각화]

Adobe Commerce, AEM Assets에서 제공하는 제품 비주얼 및 [!BADGE AEM Dynamic Media]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."}에 대한 [SaaS 전용](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/assets/dynamic/administering-dynamic-media)활성 라이선스([!DNL Adobe Commerce as a Cloud Service] 및 [!DNL Adobe Commerce Optimizer]에서 바로 사용 가능).

>[!TAB AEM Assets]

Adobe Commerce, Adobe Experience Manager Assets 및 [!BADGE AEM Dynamic Media]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."}에 대한 [SaaS 전용](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/assets/dynamic/administering-dynamic-media)활성 라이선스

[!BADGE PaaS만 해당]{type=Informative tooltip="Adobe Commerce on Cloud 프로젝트에만 적용됩니다(Adobe 관리 PaaS 인프라)."} Adobe Commerce 2.4.5+

* PHP 8.1, 8.2, 8.3 및 8.4

* Composer 2.x

[!BADGE SaaS만]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."} Adobe Experience Manager이 [Adobe Experience Manager Assets as a Cloud Service](https://experienceleague.adobe.com/ko/docs/experience-manager-cloud-service/content/assets/overview)와(과) 함께 프로비저닝되었습니다.

>[!ENDTABS]

통합을 구성하는 Adobe Commerce 사용자는 AEM Assets 프로젝트가 프로비저닝된 [IMS 조직](https://experienceleague.adobe.com/en/docs/core-services/interface/administration/organizations#concept_EA8AEE5B02CF46ACBDAD6A8508646255)에 액세스할 수 있어야 합니다.

>[!BEGINSHADEBOX]

## 주요 비즈니스 이점

![확인](assets/icon-check.png) **추가 비용 없음**-이 통합은 라이선스 요구 사항을 충족하는 판매자에게 무료로 제공됩니다.

![확인](assets/icon-check.png) **공식 Adobe 솔루션** Adobe에서 개발, 유지 관리 및 완전히 지원하여 안정성과 향후 플랫폼 개선 사항에 맞게 조정할 수 있습니다.

![확인](assets/icon-check.png) **Adobe 관리 지원 모델**-지원 및 문제 해결은 Adobe에서 직접 처리하므로 안심하고 문제를 해결할 수 있습니다.

![확인](assets/icon-check.png) **Adobe Storefront Builder 기능**-DAM(디지털 에셋 관리) 솔루션을 사용하면 [Storefront Builder](https://experienceleague.adobe.com/developer/commerce/storefront/merchants/storefront-builder/#userlabs-commerce-genai-product-visuals)에서 이미지, 비디오 및 기타 미디어와 같은 에셋을 사용할 수 있습니다.

>[!ENDSHADEBOX]

이 비디오를 통해 Adobe Commerce과 AEM Assets이 함께 콘텐츠 워크플로를 간소화하는 방법에 대해 알아보십시오.

>[!VIDEO](https://video.tv.adobe.com/v/3447837)

## 다음 단계

Experience Manager Assets과 Commerce 통합을 활성화하는 3단계 프로세스입니다.

1. [Commerce 메타데이터를 지원하도록 AEM Assets 프로젝트를 구성합니다](get-started/configure-aem.md).

1. [!BADGE Paa만]{type=Informative tooltip="Adobe Commerce on Cloud 프로젝트에만 적용됩니다(Adobe 관리 PaaS 인프라)."} [Adobe Commerce 패키지 설치](get-started/configure-commerce.md).

1. [통합을 구성](get-started/setup-synchronization.md)합니다.

## 지원

정보가 필요하거나 이 안내서에서 다루지 않는 질문이 있는 경우 AEM Assets 통합 영업 담당자에게 문의하거나 [지원 티켓](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket)을 만들어 추가 도움을 받으십시오.
