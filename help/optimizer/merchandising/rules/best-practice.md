---
title: 머천다이징 규칙 모범 사례
description: 스토어에서 머천다이징 규칙을 구현하기 위한 모범 사례에 대해 알아봅니다.
role: Admin, Developer
badgeSaas: label="SaaS만" type="Positive" url="https://experienceleague.adobe.com/ko/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."
exl-id: cc8d0879-c253-4ad4-8e7d-e066dff9112d
source-git-commit: f966a3f6f59c28e9f394d5eb7e41aaef1a992fec
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 0%

---

# 머천다이징 규칙 모범 사례

전환율과 매출을 최적화하려면 효과적인 검색 규칙을 구현해야 합니다. [머천다이징 규칙](add.md#intelligent-ranking)을 사용하여 판매 데이터, 재고 수준 및 프로모션을 기반으로 제품 순위를 조정합니다.

기본 검색 규칙을 잘 생각해 내는 것이 중요합니다. [기본 규칙](overview.md#default-rule)은(는) 검색 결과가 처음에 정렬되어 쇼핑객에게 표시되는 방식을 결정하므로 전체 경험이 향상되고 구매 가능성이 높아집니다. 이 규칙을 정기적으로 모니터링 및 조정하면 쇼핑객의 요구 사항과 비즈니스 목표를 효과적으로 지속적으로 충족할 수 있습니다.

## 검색 규칙 최적화 팁

- 판매량이 많거나 최근 판매 활동이 많은 제품을 고정하거나 강화합니다.
- 높은 평점과 긍정적인 리뷰가 있는 제품에 우선 순위를 두십시오.
- 재고 항목이 더 높은 등급으로 표시되는지 확인합니다.
- 관련성을 손상시키지 않고 수익 마진이 더 높은 제품의 우선 순위를 약간 지정합니다.
- 판매 중인 제품 또는 특별 프로모션의 일부를 강조하십시오.
- 판촉 기간 중 일자 범위를 사용하여 판촉 또는 판매 기간 중 검색 규칙을 자동으로 설정합니다.
- &quot;추천&quot;, &quot;가장 많이 본 항목&quot; 등과 같은 [지능형 순위](add.md#intelligent-ranking)를 사용하는 개별 구매자 행동을 기반으로 검색 결과를 사용자 지정합니다.
- 항상 &quot;규칙 테스트&quot; 패널을 사용하여 지능형 등급 전략이 다양한 쿼리의 실제 검색 결과에 미치는 영향을 미리 보십시오.
