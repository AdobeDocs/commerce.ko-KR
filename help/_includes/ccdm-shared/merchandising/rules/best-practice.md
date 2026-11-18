---
source-git-commit: e3be9274ca8db80d3559b24a5c8be36f5d61b2ba
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 0%
---
<!--
SOURCE OF TRUTH: Edit this file in the commerce.en repo:
https://github.com/Adobe-Enterprise-Docs/commerce.en/blob/main/help/_includes/ccdm-shared/merchandising/rules/best-practice.md

This content is shared by the Adobe Commerce Optimizer Guide (commerce.en) and the
Merchandising Services with CCDM Guide (commerce-admin.en). Changes made in commerce.en
are synced automatically to commerce-admin.en, so do not edit the copy in that repo.
This includes related images in help/assets/ccdm-shared/.
-->

# 머천다이징 규칙 모범 사례

전환 및 매출을 최적화하려면 효과적인 **검색 규칙**, 강력한 **기본 목록** 규칙 및 **[범주 규칙](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/add#rule-types)**&#x200B;을 구현하십시오. 판매 데이터, 재고, 프로모션 및 [지능적인 순위](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/add#intelligent-ranking)를 사용하여 순위를 조정합니다.

[검색 비표시 규칙](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/overview#search-suppression-rules)은(는) 일치하는 구매자 쿼리가 제품을 0으로 반환해야 하는 경우에만 사용합니다. 제품에 다른 순위가 필요한 경우에는 사용하지 않습니다.

**기본 규칙**&#x200B;을(를) 올바르게 설정하는 것이 중요합니다. [기본 규칙](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/overview#default-rule)은(는) 더 이상 특정 검색 규칙이 적용되지 않을 때 검색 결과를 처음에 정렬하는 방법을 결정하므로 검색과 구매 가능성이 향상됩니다. 쇼핑객 요구 사항 및 캠페인과 보조를 맞추도록 정기적으로 검토하십시오.

## 검색 규칙 최적화 팁

- 판매량이 많거나 최근 판매 활동이 많은 제품을 고정하거나 강화합니다.
- 높은 평점과 긍정적인 리뷰가 있는 제품에 우선 순위를 두십시오.
- 재고 항목이 더 높은 등급으로 표시되는지 확인합니다.
- 관련성을 손상시키지 않고 수익 마진이 더 높은 제품의 우선 순위를 약간 지정합니다.
- 판매 중인 제품 또는 특별 프로모션의 일부를 강조하십시오.
- 판촉 기간 중 일자 범위를 사용하여 판촉 또는 판매 기간 중 검색 규칙을 자동으로 설정합니다.
- &quot;추천&quot;, &quot;가장 많이 본 항목&quot; 등과 같은 [지능형 순위](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/add#intelligent-ranking)를 사용하는 개별 구매자 행동을 기반으로 검색 결과를 사용자 지정합니다.
- **없음** 이외의 지능형 전략을 선택한 경우 규칙당 **[지능형 순위 증폭](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/add#intelligent-ranking-boost)**&#x200B;을(를) 조정하고 **규칙을 테스트**&#x200B;한 후 게시하십시오.
- 항상 &quot;규칙 테스트&quot; 패널을 사용하여 지능형 등급 전략이 다양한 쿼리의 실제 검색 결과에 미치는 영향을 미리 보십시오.

## 카테고리 규칙 팁

- 트래픽이 많거나 이윤이 많은 **범주 페이지**&#x200B;에서 [범주 규칙](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/add#rule-types)을 사용하십시오. 조정된 순서는 검색만큼 중요합니다(예: 시즌 컬렉션 또는 주요 부서).
- **지능형 순위**(예: 트렌드, 가장 많이 본 항목)을 쇼핑객이 해당 범주를 검색하는 방법과 맞추십시오. 범주 페이지는 검색 규칙과 같은 방식으로 검색 쿼리 텍스트를 사용하지 않습니다. [지능형 순위](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/add#intelligent-ranking)를 참조하십시오. **없음** 이외의 지능형 메서드의 경우 **[지능형 순위 증폭](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/add#intelligent-ranking-boost)** 및 범주 미리 보기를 사용하여 해당 범주 규칙에 대한 동작 강도를 조정합니다.
- 캠페인 플랜과 일관되게 **pin**, **boost**, **bury**&#x200B;를 적용합니다. 수동 위치는 일반적으로 쇼핑객이 목록에 **기본 정렬**&#x200B;을 사용하는 경우에만 적용됩니다. [수동 순위](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/add#manual-ranking)를 참조하세요.
- 편집기에서 **category** 규칙 흐름을 미리 보고 게시 후 상점에서 검색의 &quot;규칙 테스트&quot; 패널에 사용하는 것과 동일한 규격을 확인합니다.

## 제외 모범 사례 및 사용 사례 검색 {#search-suppression-best-practices}

검색 비표시 규칙은 해당 조건과 일치하는 쿼리에 대한 결과를 차단하므로 상점 첫 페이지에는 제품이 없는 검색 결과 페이지가 표시됩니다. 규칙 편집기는 제외 규칙에 대한 미리 보기를 제공하지 않습니다. 제한을 충족하는 가장 좁은 조건을 사용한 다음 [검색 비표시 규칙 만들기 및 관리](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/add#search-suppression-rules)를 따르십시오. 규칙이 활성화되면 상점 첫 화면에서 일치하는 검색과 일치하지 않는 검색을 확인합니다. 상점 첫 화면의 실제 무결과 프레젠테이션을 확인합니다.

| 사용 사례 | 제안된 구성 | 확인할 사항 |
| --- | --- | --- |
| 검색 규정 준수 | 영향을 받는 카탈로그 보기에 규칙 범위를 지정하고 제한된 검색어와 일치시키십시오. | 준수 팀과 조건을 확인합니다. 검색 억제만으로는 범주 탐색, 머천다이징 페이지, 권장 사항 또는 직접 제품 URL을 통한 액세스가 차단되지 않습니다. |
| 브랜딩 제한 사항 | 제한된 브랜드 이름을 더 긴 쿼리 내에서 차단해야 하는 경우 **쿼리 포함**&#x200B;을 사용합니다. | 규칙이 활성화되면 합법적인 검색이 제외되지 않도록 유사한 텍스트가 포함된 관련되지 않은 상점 첫 번째 쿼리를 확인하십시오. |
| 특정 검색어가 결과를 반환하지 않도록 방지 | 제품을 반환하지 않아야 하는 정확한 구문에 대해서는 **Query is**&#x200B;을(를) 사용하십시오. | 관련 구문을 별도로 확인합니다. 정확한 일치 조건은 해당 구문이 포함된 모든 쿼리를 차단하지 않습니다. |
| 쿼리 접두사 또는 접미사에 대한 제한 사항 | 제한된 텍스트의 위치가 문제가 될 때 **쿼리 시작** 또는 **쿼리 종료**&#x200B;를 사용합니다. | 규칙이 활성화되면 텍스트의 시작, 중간 및 끝에 있는 상점 첫 번째 쿼리를 확인하여 의도한 범위를 확인합니다. |
| 임시 검색 제한 사항 | 제한 시간 제한에 대한 시작 및 종료 날짜를 설정합니다. | 일정 및 활성화됨 상태를 확인하고 제한이 종료된 후에도 규칙이 계속 필요한지 여부를 검토합니다. |

- 각 규칙에 수사적 이름을 지정하고 해당 설명에 제한 이유를 기록하십시오.
- 변경 사항을 게시하기 전에 쿼리 조건을 검토하십시오. 규칙이 활성화되면 차단해야 하는 storefront 쿼리와 여전히 제품을 반환해야 하는 쿼리를 확인하십시오. 캐시된 쿼리 결과는 새로 고치는 데 최대 15분이 걸릴 수 있습니다.
- 상점 첫 화면의 결과 없음 상태를 검토하고 쇼핑객이 상점 첫 화면의 도움을 받는 경우 쿼리를 수정하거나 범주를 탐색하는 등 탐색을 계속할 수 있는 유용한 방법을 찾도록 하십시오.
- 쿼리 제외를 제품 수준 제외의 대용으로 사용하지 마십시오. 검색 결과, 검색 제안 및 자동 완성에서 제품을 제외하려면 수동 제외 또는 **기본 검색 규칙**&#x200B;에서 **숨기기** 작업과 함께 **특성 기반 머천다이징 이벤트**&#x200B;를 사용하십시오.
- 활성 제외 규칙을 정기적으로 검토하십시오. 더 이상 필요하지 않은 규칙을 비활성화하거나 제한이 변경될 때 편집하고 게시합니다.
