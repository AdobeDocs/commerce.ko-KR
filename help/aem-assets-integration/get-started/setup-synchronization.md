---
title: 통합 구성
description: Adobe Commerce 프로젝트와 Experience Manager Assets 프로젝트를 연결하여 이 두 시스템 간에 에셋을 동기화하는 방법에 대해 알아봅니다.
feature: CMS, Media
exl-id: 3533d010-926f-4d78-935c-98a9b7040d27
source-git-commit: 86e8876af21da3df0ec5e940113f19593b2f6d0a
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 0%

---

# 통합 구성

Commerce을 AEM Assets 인스턴스에 연결하고 에셋 동기화를 위한 일치 전략을 선택하여 통합을 구성합니다.

AEM Assets 프로젝트를 식별한 후 Adobe Commerce과 AEM Assets 간에 자산을 동기화하기 위한 일치 규칙을 선택합니다.

* **[!UICONTROL Match by product SKU]** - 에셋이 올바른 제품과 연결되어 있는지 확인하기 위해 에셋 메타데이터의 SKU와 [Commerce 제품 SKU](https://experienceleague.adobe.com/ko/docs/commerce-operations/implementation-playbook/glossary#sku)가 일치하는 기본 규칙입니다.

* **[!UICONTROL Custom match]** - 사용자 지정 일치 논리가 필요한 더 복잡한 시나리오 또는 특정 비즈니스 요구 사항에 대한 일치 규칙. 사용자 지정 일치를 구현하려면 Adobe Developer App Builder에서 자산과 제품의 일치 방법을 정의하는 사용자 지정 코드를 개발해야 합니다. 자세한 내용은 곧 제공될 예정입니다.

초기 설정의 경우 기본 *제품별 일치 sku* 규칙을 사용하십시오.

## 사전 요구 사항

* [AEM Assets 프로젝트 구성](configure-aem.md)

* [!BADGE PaaS만 해당]{type=Informative tooltip="Adobe Commerce on Cloud 프로젝트에만 적용됩니다(Adobe 관리 PaaS 인프라)."} [Adobe Commerce 패키지를 설치하여](configure-commerce.md) 확장을 추가하고 확장을 사용하는 데 필요한 자격 증명과 연결을 생성합니다.

* [Dynamic Media Open API 활성화](https://experienceleague.adobe.com/ko/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/dynamic-media-open-apis-overview#enable-dynamic-media-open-apis) 주제에 설명된 단계를 따릅니다. 지원 팀에 대한 다음 정보를 포함하십시오.

   * **[!UICONTROL AEM Program ID]**
   * **[!UICONTROL Adobe Commerce URL]**
   * **[!UICONTROL AEM Environment ID]**,
   * Commerce에 연결할 AEM Assets 제작 환경에 대한 **[!UICONTROL IMS Org ID]**.

## 연결 구성

1. [AEM Assets 작성 환경](https://experienceleague.adobe.com/ko/docs/experience-manager-cloud-service/content/sites/authoring/quick-start) 프로젝트 및 환경 ID를 가져옵니다.

   1. AEM Cloud Manager을 열고 **[!UICONTROL Assets]**&#x200B;을(를) 선택합니다.

   1. URL <br>`https://author-p[Program ID]-e[EnvironmentID].adobeaemcloud.com/`에서 프로젝트 및 환경 ID를 복사하여 저장합니다.

1. Commerce 관리자에서 AEM Assets 통합 구성을 엽니다.

   1. **[!UICONTROL Store]** > 구성 > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**(으)로 이동합니다.

      ![AEM Assets 통합을 통해 통합 사용](../assets/aem-assets-view.png){width="600" zoomable="yes"}

1. AEM Assets 환경 **[!UICONTROL Program ID]** 및 **[!UICONTROL Environment ID]**&#x200B;을(를) 입력하십시오.

   *[!UICONTROL Use system value]*&#x200B;에서 선택 항목을 제거하여 구성 값을 편집합니다.

1. **[!UICONTROL Asset Selector IMS Client ID]** 입력.

   자산 선택기에 대한 자세한 내용은 [자산 수동으로 선택](../synchronize/asset-selector-integration.md)을 참조하세요.

1. [!BADGE PaaS만 해당]{type=Informative tooltip="Adobe Commerce on Cloud 프로젝트에만 적용됩니다(Adobe 관리 PaaS 인프라)."} Commerce과 자산 일치 서비스 간 요청을 인증하기 위해 [[!UICONTROL Commerce integration]](configure-commerce.md#add-the-integration-to-the-commerce-environment)을(를) 선택합니다.

1. AEM Assets에서 사용할 Commerce 통합을 선택하려면 **[!UICONTROL Commerce integration]**&#x200B;을(를) `assets-integration`(으)로 설정하십시오.

1. Commerce이 AEM Assets에서 들어오는 업데이트를 수락하도록 하려면 **[!UICONTROL Synchronization enabled]**&#x200B;을(를) `Yes`(으)로 설정하십시오.

   통합을 활성화한 후 에셋 일치 기준을 지정하는 추가 구성 옵션을 사용할 수 있습니다.

1. **[!UICONTROL Asset matching rule]** 드롭다운에서 자산 동기화에 대한 자산 일치 규칙 중 하나를 선택합니다.

   * **[!UICONTROL Match by SKU]**&#x200B;기본 자동 일치[에 대해 ](../synchronize/default-match.md)을(를) 선택하십시오.
   * **[!UICONTROL Custom match]**&#x200B;사용자 지정 자동 일치[에 대해 ](../synchronize/custom-match.md)을(를) 선택하십시오([Adobe Developer App Builder](https://experienceleague.adobe.com/ko/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder) 필요).

1. 기본적으로 [ 필드 ](configure-aem.md#configure-metadata)에 Commerce 제품 SKU에 대해 정의된 **[!UICONTROL Match by product SKU attribute name]** AEM Assets 메타데이터 필드 이름`commerce:skus`을(를) 추가합니다.

1. 업데이트를 적용하고 자산 동기화를 시작하려면 **[!UICONTROL Save Config]**&#x200B;을(를) 선택하십시오.

   구성 업데이트는 초기 동기화 프로세스를 트리거하여 Commerce에서 AEM Assets의 수신 업데이트를 수락할 수 있습니다. 동기화에 필요한 시간은 에셋의 볼륨과 특정 구성에 따라 다릅니다. 통합은 자동화된 프로세스를 활용하여 동기화에 필요한 시간을 최소화합니다.

### 동기화 SLA

통합은 다음과 같은 동기화 성능 수준을 보장합니다.

* `< 5 minutes for 99% of updates`

* `< 30 minutes for 99.9% of updates`

이렇게 하면 제품 페이지에 항상 최신 이미지가 표시되므로 상점 컨텐츠가 정확하고 시각적으로 매력적입니다.

### 시각화 소유자 구성

**시각화 소유자** 설정은 통합에서 제품 이미지를 제공하는 시스템을 결정합니다.

* Adobe Commerce - Commerce에서 호스팅된 이미지를 사용합니다.
* AEM Assets - AEM에서 동기화된 이미지를 사용합니다.

관리자는 해당 소유자에게 사용 가능한 이미지를 표시하지만 나머지 이미지는 회색으로 표시되며 **hidden** 레이블과 함께 표시됩니다.

이미지 표시 동작에 대한 자세한 내용은 [이미지 세부 정보 설정](https://experienceleague.adobe.com/ko/docs/commerce-admin/catalog/products/digital-assets/product-image#set-image-details){target=_blank} 항목을 참조하십시오.

>[!TIP]
>
> Commerce에서 AEM Assets으로 마이그레이션하는 동안 끊어진 이미지 링크를 방지하려면 **시각화 소유자**&#x200B;를 Commerce으로 설정하십시오. 모든 제품이 AEM Assets과 성공적으로 동기화되면 AEM Assets 소유자로 전환하여 전환을 완료합니다. 이를 통해 프로세스 전체에서 지속적인 이미지 가용성을 보장합니다.

1. **[!UICONTROL Store]** > 구성 > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**(으)로 이동합니다.

   ![AEM Assets 통합 시각화 소유자 기능](../assets/visualization-owner-detail.png){width="400" zoomable="yes"}

1. 이미지를 표시할 **시각화 소유자** 원본을 선택하십시오.

1. 업데이트를 적용하고 자산 동기화를 시작하려면 **[!UICONTROL Save Config]**&#x200B;을(를) 클릭하십시오.

### 선택 사항입니다. 사용자 정의 도메인 URL 구성

AEM Assets as a Cloud Service 프로젝트가 [사용자 지정 도메인 이름](https://experienceleague.adobe.com/ko/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name){target=_blank}(으)로 구성된 경우 Commerce용 AEM Assets 통합에서 사용할 수 있도록 도메인 이름을 Commerce 저장소 구성에 추가해야 합니다.

1. **[!UICONTROL Store]** > 구성 > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**(으)로 이동합니다.

   ![AEM Assets 통합을 통해 통합 사용](../assets/aem-assets-view.png){width="700" zoomable="yes"}

1. **사용자 지정 도메인 URL**&#x200B;을(를) **[!UICONTROL Asset Custom Domain]** 필드에 추가하십시오.

1. 업데이트를 적용하고 자산 동기화를 시작하려면 **[!UICONTROL Save Config]**&#x200B;을(를) 클릭하십시오.

## 다음 단계

[Commerce 에셋 관리](../manage-assets.md)
