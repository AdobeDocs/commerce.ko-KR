---
title: 기본 자동 일치
description: 기본 자동 일치 규칙을 사용하여 Adobe Commerce과 AEM Assets 통합 간에 매끄럽게 동기화하여 자산이 올바른 머천다이징 엔티티에 자동으로 연결되는 방법에 대해 알아봅니다.
feature: CMS, Media, Integration
exl-id: 8a18639b-f508-456e-8d22-18e3e0fdd515
source-git-commit: 6640635fca5c53fe4b06b9bbb3120fffc46cb0b8
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# 기본 자동 일치

Commerce용 AEM Assets 통합은 **[!UICONTROL Match by product SKU]** AEM Assets **메타데이터 구성을 기반으로 기본 자동 일치 메커니즘(**)을 제공합니다. 이 규칙을 사용하면 **Adobe Commerce**&#x200B;과(와) **AEM Assets** 간의 원활한 동기화를 통해 자산이 자동으로 올바른 머천다이징 엔터티에 연결되도록 할 수 있습니다.

## 자동 일치 메커니즘 구성

1. Commerce 관리자에서 **[!UICONTROL Store]** > 구성 > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**(으)로 이동합니다.

1. **[!UICONTROL Match by SKU]**&#x200B;을(를) 일치 규칙으로 지정합니다.

   ![기본 자동 일치 규칙](../assets/ootb-matching-rule.png){width="600" zoomable="yes"}

1. AEM Assets에서 에셋 식별에 사용되는 메타데이터 필드 이름을 입력합니다.

   >[!NOTE]
   >
   > 표준 온보딩 프로세스를 따랐다면 이 값을 `commerce:skus`(으)로 설정해야 합니다.

## 자동 일치 메커니즘 작동 방식

**[!UICONTROL Match by product SKU]** 일치 규칙이 Commerce 관리자에 구성된 경우 Commerce 자산 파일은 각 파일에 대해 구성된 자산 메타데이터를 기반으로 AEM Assets에서 Commerce 프로젝트로 자동으로 동기화됩니다. **AEM Assets 작성자** 환경의 AEM **Commerce** 탭에서 메타데이터를 구성합니다.

![예제 메타데이터](../assets/example-metadata.png){width="600" zoomable="yes"}

1. AEM Assets에서 이미지 메타데이터를 업데이트하여 Adobe Commerce 연결 `Commerce=yes`을(를) 추가합니다.

1. 연결된 제품 SKU에 자산을 연결하는 메타데이터([!UICONTROL SKU], [!UICONTROL position] 및 [!UICONTROL role])를 구성합니다.

   >[!NOTE]
   >
   > 자산이 여러 제품에 사용되는 경우 연결된 각 SKU에 대한 메타데이터를 구성합니다.

이 접근 방식을 사용하면 디지털 에셋이 Adobe Commerce에 제대로 연결되고 표시됩니다. 또한 머천다이저와 마케터가 AEM Assets 내에서 직접 역할 및 에셋 위치를 관리할 수 있도록 하여 모든 참여 채널에서 일관되고 중앙 집중식 이미지 선택 및 순서 지정 메커니즘을 제공합니다.
