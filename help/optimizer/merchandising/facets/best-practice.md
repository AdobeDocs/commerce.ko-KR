---
title: Facet 모범 사례
description: 스토어에서 패싯을 구현하기 위한 모범 사례에 대해 알아봅니다.
role: Admin, Developer
badgeSaas: label="SaaS만" type="Positive" url="https://experienceleague.adobe.com/ko/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."
source-git-commit: 3131cc27a25d1bf958071b973f1d4bf1a68be152
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 0%

---


# Facet 모범 사례

필터 및 패싯 기능은 [!DNL Adobe Commerce Optimizer] 사이트의 중요한 구성 요소이며, 쇼핑객이 검색 결과의 범위를 좁히고 제품을 보다 효율적으로 찾을 수 있도록 하여 쇼핑객 경험을 향상시키도록 설계되었습니다. 이 기능은 쇼핑객들이 특정 기준을 적용하여 방대한 상품 카탈로그를 분류할 수 있도록 도와주며, 쇼핑 프로세스를 더 빠르고, 더 쉽고, 더 만족스럽게 만듭니다. 효과적이고 구매자 친화적인 필터 및 패싯을 구현하여 고객이 필요한 것을 빠르고 효율적으로 정확하게 찾을 수 있도록 지원함으로써 만족도와 전환율을 높일 수 있습니다.

## 패싯 최적화 팁

- 제목, 카테고리, 브랜드, 가격 범위, 색상 및 크기와 같은 제품에 가장 관련성이 높고 유용한 특성을 결정하고 [동적 패싯](type.md)으로 설정합니다. 
- 카탈로그에서 일관되고 제품에 관련성이 높은 제품 속성을 설정하고 정렬하여 쇼핑객의 관련성과 필터링 기능을 개선합니다.
- 패싯 레이블을 이해하기 쉽고 사이트 간에 일관되게 지정해야 합니다. 예를 들어 &quot;비용&quot; 대신 &quot;가격 범위&quot;를 사용합니다.
- 패싯의 수를 가장 중요한 패싯으로 제한하여 구매자의 과몰을 방지하십시오. 옵션이 너무 많으면 의사 결정 피로가 발생할 수 있습니다. 기본적으로 [!DNL Adobe Commerce Optimizer]은(는) 패싯으로 구성된 최대 100개의 특성과 각 패싯 내에서 반환되는 30개의 버킷으로 제한됩니다. [패싯 제한](../../boundaries-limits.md#catalog-views-and-policies)에 대해 자세히 알아보세요. 
- 구매자가 여러 필터 기준을 동시에 선택하여 결과를 구체화할 수 있습니다. 예를 들어 쇼핑객에게 &quot;빨간색&quot;과 &quot;파란색&quot; 색상을 모두 선택하도록 합니다.
- 구매자가 예상할 수 있는 검색 결과를 파악할 수 있도록 각 패싯 옵션 옆에 사용 가능한 제품 수를 표시합니다.
- 접을 수 있는 패싯 섹션을 구현하여 특히 모바일 장치에서 인터페이스를 깔끔하고 관리할 수 있도록 합니다.
- 쇼핑객이 개별 패싯 또는 선택한 모든 필터를 쉽게 재설정하여 새 검색을 시작할 수 있도록 합니다.
- 경합할 속성이 많은 경우 속성을 하나의 &quot;meta-attribute&quot;로 결합하는 것이 좋습니다. 예를 들어, 신발은 일반적으로 숫자 크기를 가지지만 셔츠는 일반적으로 &quot;S/M/L/XL&quot; 크기를 갖습니다. 이 두 가지 유형의 크기를 하나의 검색 가능한 속성으로 결합할 수 있습니다.
