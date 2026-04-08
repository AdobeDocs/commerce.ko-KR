---
title: 머천다이징 규칙 모범 사례
description: 검색, 기본 목록 및 카테고리 페이지에 대한 머천다이징 규칙을 구현하는 모범 사례에 대해 알아봅니다.
role: Admin, Developer
badgeSaas: label="SaaS만" type="Positive" url="https://experienceleague.adobe.com/ko/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 [!DNL Adobe Commerce Optimizer] 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."
exl-id: cc8d0879-c253-4ad4-8e7d-e066dff9112d
source-git-commit: 8abc0593c166a2dd861cfb78674918de1d0744de
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---

# 머천다이징 규칙 모범 사례

전환 및 매출을 최적화하려면 효과적인 **검색 규칙**, 강력한 **기본 목록** 규칙 및 **[범주 규칙](add.md#category-rules)**(베타)을 구현하십시오. 판매 데이터, 재고, 프로모션 및 [지능적인 순위](add.md#intelligent-ranking)를 사용하여 순위를 조정합니다.

**기본 규칙**&#x200B;을(를) 올바르게 설정하는 것이 중요합니다. [기본 규칙](overview.md#default-rule)은(는) 더 이상 특정 검색 규칙이 적용되지 않을 때 검색 결과를 처음에 정렬하는 방법을 결정하므로 검색과 구매 가능성이 향상됩니다. 쇼핑객 요구 사항 및 캠페인과 보조를 맞추도록 정기적으로 검토하십시오.

## 검색 규칙 최적화 팁

- 판매량이 많거나 최근 판매 활동이 많은 제품을 고정하거나 강화합니다.
- 높은 평점과 긍정적인 리뷰가 있는 제품에 우선 순위를 두십시오.
- 재고 항목이 더 높은 등급으로 표시되는지 확인합니다.
- 관련성을 손상시키지 않고 수익 마진이 더 높은 제품의 우선 순위를 약간 지정합니다.
- 판매 중인 제품 또는 특별 프로모션의 일부를 강조하십시오.
- 판촉 기간 중 일자 범위를 사용하여 판촉 또는 판매 기간 중 검색 규칙을 자동으로 설정합니다.
- &quot;추천&quot;, &quot;가장 많이 본 항목&quot; 등과 같은 [지능형 순위](add.md#intelligent-ranking)를 사용하는 개별 구매자 행동을 기반으로 검색 결과를 사용자 지정합니다.
- 항상 &quot;규칙 테스트&quot; 패널을 사용하여 지능형 등급 전략이 다양한 쿼리의 실제 검색 결과에 미치는 영향을 미리 보십시오.

## 카테고리 규칙 팁

>[!IMPORTANT]
>
>카테고리 규칙은 베타 버전입니다.

- 트래픽이 많거나 이윤이 많은 [범주 페이지](add.md#category-rules)에서 **범주 규칙**&#x200B;을 사용하십시오. 조정된 순서는 검색만큼 중요합니다(예: 시즌 컬렉션 또는 주요 부서).
- **지능형 순위**(예: 트렌드, 가장 많이 본 항목)을 쇼핑객이 해당 범주를 검색하는 방법과 맞추십시오. 범주 페이지는 검색 규칙과 같은 방식으로 검색 쿼리 텍스트를 사용하지 않습니다. [지능형 순위](add.md#intelligent-ranking)를 참조하십시오.
- 캠페인 플랜과 일관되게 **pin**, **boost**, **bury**&#x200B;를 적용합니다. 수동 위치는 일반적으로 쇼핑객이 목록에 **기본 정렬**&#x200B;을 사용하는 경우에만 적용됩니다. [수동 순위](add.md#manual-ranking)를 참조하세요.
- 편집기에서 **category** 규칙 흐름을 미리 보고 게시 후 상점에서 검색의 &quot;규칙 테스트&quot; 패널에 사용하는 것과 동일한 규격을 확인합니다.
