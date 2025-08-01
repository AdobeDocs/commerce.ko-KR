---
title: 검색 성능
description: 검색 성능 페이지에서는 insight에 쇼핑객이 사용하는 검색어를 제공합니다.
badgeSaas: label="SaaS만" type="Positive" url="https://experienceleague.adobe.com/ko/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."
exl-id: 75b43c6f-d876-4379-ad70-5c2a2f29a5ac
source-git-commit: b8b7af1119163589b7d83654b13edae656fea339
workflow-type: tm+mt
source-wordcount: '1737'
ht-degree: 0%

---

# 검색 성능

*검색 성능* 페이지에서는 쇼핑객이 사용하는 검색어에 insight을 제공합니다. 이 정보는 트렌드를 식별하고 클릭스루를 늘리고 전환율을 향상시키는 데 사용할 수 있습니다. [검색 성능] 페이지는 특정 날짜 범위에 대한 검색 측정 단위의 스냅샷을 제공하며 다음 보고서를 포함합니다.

- 고유 검색
- 평균 클릭 위치
- 클릭스루 비율
- 전환율
- 결과 없음 비율

![검색 성능](../assets/search-performance.png){zoomable="yes"}

>[!IMPORTANT]
>
>검색 성능 지표가 표시되지 않으면 검색 이벤트 데이터가 [수집되고](../setup/events/overview.md) 있는지 확인하십시오.

## **카탈로그 보기** 선택

특정 검색 성능 결과를 보려면 [카탈로그 보기](../setup/catalog-view.md)를 선택하십시오.

![카탈로그 보기](../assets/catalog-view.png)

## 보고서 보기

달력을 클릭하고 다음 중 하나를 수행합니다.

- 단일 날짜를 지정하려면 달력에서 날짜를 두 번 클릭합니다.
- 날짜 범위를 지정하려면 달력에서 첫 번째 날짜와 마지막 날짜를 클릭합니다.

>[!NOTE]
>
>날짜 범위는 1년을 초과할 수 없습니다.

검색 성능의 CSV 파일을 생성하려면 **[!UICONTROL Export to CSV]**&#x200B;을(를) 클릭하십시오.

## 검색 성능을 향상시키는 방법

다음 섹션에서는 사이트 검색 기능을 향상시키는 데 사용할 수 있는 전략을 제공하여 전환율을 극대화하는 원활하고 효율적인 쇼핑객 경험을 제공합니다.

검색 결과의 관련성과 유효성을 결정하는 몇 가지 주요 요소는 다음과 같습니다.

- 잘 구조화된 제품 데이터는 검색 알고리즘이 제품을 쿼리에 효과적으로 일치시킬 수 있도록 해줍니다. 낮은 품질의 제품 데이터는 관련성이 낮은 검색 결과를 초래합니다. 머천다이징 전략의 성공에 직접 영향을 주려면 다음을 수행하십시오.
   - 해당 가중치를 사용하여 올바른 [특성을 검색 가능](https://developer.adobe.com/commerce/services/reference/rest/#tag/Metadata)으로 설정합니다.
   - 해당 속성 내의 데이터가 관련성이 있는지 확인하십시오.
- 잘 설계된 검색 경험은 고객과 신뢰를 쌓고, 필요한 것을 찾을 것이라는 자신감을 심어줍니다.
- 검색 규칙은 인기, 새 도착, 프로모션 기준 또는 비즈니스 요구 사항을 충족하는 기타 머천다이징 전략에 따라 특정 제품의 가시성을 높일 수 있으므로 중요합니다.
- 패싯된 탐색을 사용하면 고객이 검색을 구체화하고 관련 결과를 빠르게 얻을 수 있습니다.

### 검색 결과 모니터링

[!DNL Adobe Commerce Optimizer]을(를) 사용하여 검색 결과를 최적화하려면 고유 쿼리, 평균 클릭 위치, 클릭스루 비율, 전환율 및 결과 0과 같은 관련 KPI(주요 성과 지표)를 모니터링하여 쇼핑객이 검색 기능과 상호 작용하는 방법을 이해합니다. 이 데이터는 검색 규칙을 정기적으로 업데이트하고 세분화하는 데 도움이 됩니다.

- **고유 검색** - [!DNL Adobe Commerce Optimizer] 사이트에서 수행된 개별 검색 쿼리 수입니다. 동일한 쇼핑객 또는 다른 쇼핑객에 의해 여러 번 반복되는 경우에도 각 고유 검색은 한 번만 카운트됩니다. 이 지표는 고객이 사용하는 검색어의 다양성을 이해하는 데 도움이 되며 구매자가 원하는 제품 또는 정보에 대한 통찰력을 제공합니다. 고유 검색 추적을 사용하면 다음 작업을 수행할 수 있습니다.

   - 인기 검색 트렌드와 자주 검색된 항목을 식별합니다.
   - 제품 카탈로그 또는 콘텐츠에서 잠재적인 차이를 감지합니다.
   - [동의어](../merchandising/synonyms/overview.md)를 추가하거나 [검색 규칙](../merchandising/rules/overview.md)을 만들거나 업데이트하여 검색 기능을 최적화하십시오.

- **평균 클릭 위치** - 사이트에서 검색 쿼리를 수행한 후 쇼핑객이 클릭한 검색 결과의 평균 위치를 나타냅니다. 이 지표는 검색 결과의 관련성과 유효성에 대한 통찰력을 제공합니다.

  평균 클릭 위치가 낮을수록(1에 가까움) 쇼핑객이 관련 결과를 빠르게 찾는다는 사실을 의미하며 이는 검색 전략이 효과적임을 나타냅니다. 쇼핑객 행동을 이해하고, 원하는 제품을 찾기 위해 스크롤할 의지가 얼마나 되는지를 아는 데 도움이 됩니다. 평균 클릭 위치가 높은 경우 가장 관련성이 높은 결과가 맨 위에 표시되지 않을 수 있으므로 검색 전략을 검토하고 최적화해야 합니다.

- **클릭스루 비율(CTR)** - 검색 쿼리를 수행한 후 검색 결과를 클릭하는 구매자의 비율을 측정합니다. 높은 CTR은 검색 결과가 쇼핑객에게 관련성이 있고, 그들이 찾은 결과를 클릭할 때 매력적이라는 것을 나타냅니다. CTR을 모니터링하면 개선할 영역을 식별하는 데 도움이 될 수 있습니다. 낮은 CTR은 검색 결과가 구매자 의도와 일치하지 않음을 암시하여 검색 규칙을 세분화하거나, 제품 데이터를 개선하거나, 결과 표시를 개선할 필요성을 초래할 수 있습니다.

- **전환율** - 검색 기능이 판매를 촉진하고 비즈니스 목표를 달성하는 데 미치는 효과를 나타냅니다. 이는 쇼핑객 요구를 충족하고 원활한 쇼핑 경험을 용이하게 하는 검색 기능의 전반적인 효과를 반영합니다. 전환율이 높으면 검색 결과가 관련성이 높고 설득력이 있어 구매자가 구매를 완료하게 됩니다. 전환율이 낮은 경우 검색에서 구매까지 검색 관련성, 제품 가용성 또는 전체 쇼핑객 여정과 관련된 문제를 제시할 수 있습니다.

- **결과 제로 비율** - 결과를 반환하지 않는 [!DNL Adobe Commerce Optimizer] 사이트의 검색 쿼리 비율을 측정합니다. 이 지표는 구매자의 검색이 실패하는 빈도를 이해하는 데 중요하며 제품 카탈로그 또는 검색 설정의 잠재적인 격차에 대한 통찰력을 제공할 수 있습니다. 제로 결과율이 높으면 쇼핑객들이 좌절하여 저조한 쇼핑 경험과 잠재 고객 손실로 이어질 수 있습니다. 쇼핑객이 찾고 있는 카탈로그에 누락된 제품 또는 카테고리를 표시하고 재고 및 제품 목록 결정을 안내할 수 있습니다.

  제로 결과율을 줄이기 위해 다음을 수행할 수 있습니다.

   - 정확히 일치하는 항목이 없는 경우 [동의어](../merchandising/synonyms/overview.md)와 같은 대체 검색어 또는 관련 검색어를 제공합니다.
   - 제로 결과 쿼리를 정기적으로 검토하여 패턴을 식별하고 제품 카탈로그 및 검색 설정을 필요한 대로 조정합니다.

다음 방법으로 이 지표 데이터를 사용하여 검색 기능을 최적화할 수 있습니다.

- 검색 결과에서 인기 있는 제품의 등급을 자동으로 더 높게 매기는 규칙을 구현합니다. 자주 클릭하거나 구매하는 제품에 우선 순위를 부여하여 맨 위에 표시할 수 있습니다. 특정 검색 쿼리에 대해 인기 있는 제품 목록을 수동으로 정리하고 이러한 항목이 눈에 잘 띄게 표시되는지 확인하십시오.
- 현재 트렌드가 있거나 최근 인기가 급상승한 제품을 부각시킨다. 이 기능은 특히 계절 행사, 휴일 또는 홍보 기간 동안 효과적일 수 있습니다. 이를 위해 검색 규칙을 설정할 때 사용 사례 및 비즈니스 요구 사항에 더 적합한 지능형 등급을 사용합니다.
- 인기 있는 필터 또는 패싯을 강조 표시합니다. 쇼핑객이 특정 브랜드 또는 가격 범위에 따라 자주 필터링하는 경우 해당 패싯을 고정하여 해당 옵션을 더 두드러지게 만들고 그에 따라 정렬합니다.
- 검색 결과가 0이면 인기 있는 결과 데이터를 사용하여 쇼핑객 참여도가 높은 대체 제품 또는 관련 카테고리를 제안합니다.
- 인기 검색어와 제품 데이터를 분석하여 중요한 키워드를 식별합니다. 이러한 키워드로 제품 검색 가능한 속성을 최적화하여 검색 관련성을 개선합니다.
- 정기적으로 결과 데이터를 분석하여 변화하는 트렌드, 구매자 선호도 및 행동을 파악하고, 상위 검색어를 식별하고, 문제를 감지합니다. 이 피드백 루프를 사용하여 검색 규칙 및 제품 오퍼링을 지속적으로 구체화하고 개선하십시오

## 검색 기능 최적화

검색 기능을 최적화하려면 [동의어 및 철자](../merchandising/synonyms/overview.md)를 사용하여 쇼핑객이 다른 단어를 사용하더라도 제품을 찾을 수 있도록 하고, [패싯](../merchandising/facets/overview.md)을 사용하여 쇼핑객이 검색 결과를 좁힐 수 있도록 합니다.

## 검색 결과 관련성 개선

검색 결과 관련성을 향상시키려면 유효한 [검색 규칙](../merchandising/rules/overview.md)을 구현하고 제품 메타데이터를 사용하여 정확하고 자세한 [특성을 검색할 수 있습니다](https://developer.adobe.com/commerce/services/reference/rest/#tag/Metadata).

### 이미지

구성 가능한 제품의 하위 제품에 올바른 역할이 있는 이미지가 있는지 확인합니다. 상위 또는 하위 제품이 있으면 검색 결과에 이미지가 없을 수 있습니다.

>[!NOTE]
>
>검색 결과에 있는 이미지는 검색어에 따라 다를 수 있습니다. 검색어에 따라 하위 제품이 더 연관성이 있다고 판단되면 상위 제품의 이미지 대신 하위 제품의 이미지가 사용됩니다.

### 제품 메타데이터 활용

정확하고 자세한 제품 [특성이 검색 가능한](https://developer.adobe.com/commerce/services/reference/rest/#tag/Metadata)&#x200B;(으)로 설정되어 있는지 확인하십시오. SKU, 이름 및 카테고리 속성은 기본적으로 검색할 수 있으며 검색에서 제외할 수 없습니다. 최상의 결과를 얻으려면 SKU에 공백을 사용하지 마십시오.

검색 관련성을 높이려면 검색 가능한 각 속성에 가중치를 할당합니다. 가중치가 높은 속성은 검색 결과 내에서 더 높게 표시되어야 합니다. 관련성을 기준으로 정렬하는 것은 검색 가중치와 같은 여러 기준의 영향을 받습니다. 이는 경우에 따라 검색 가중치가 낮은 속성이 검색 가중치가 높은 속성보다 더 많은 관련성을 가질 수 있음을 의미합니다. 다른 기준에는 특정 속성의 일치 수, 검색된 검색어의 위치 및 검색어 전후의 전체 텍스트 구조가 포함될 수 있습니다.

각 제품에 검색 가능한 각 속성 내에 관련 콘텐츠가 있는지 확인합니다. 검색 결과 관련성을 감소시킬 수 있는 콘텐츠로 대량의 콘텐츠가 있는 경우 속성을 검색 가능으로 설정하지 않는 것이 좋습니다.

검색할 제품 속성에 대해 자세히 알아보십시오.

- [검색 가능한 특성을 설정합니다](https://developer.adobe.com/commerce/services/reference/rest/#tag/Metadata)
- [속성에 가중치 할당](https://developer.adobe.com/commerce/services/reference/rest/#tag/Metadata)

## 필드 설명

| 스냅샷 데이터 | 설명 |
|--- |--- |
| 고유 검색 | 지정된 날짜 범위에 대한 총 고유 검색 수입니다. 동일한 구매자가 동일한 쿼리에 대해 여러 검색을 수행하는 경우 한 시간 이상 간격으로 제출되면 고유하다고 간주됩니다. |
| 클릭스루 비율 | 구매자가 제품을 클릭하는 것으로 끝나는 검색의 백분율입니다. 예를 들어, 쇼핑객이 &quot;바지&quot;와 &quot;셔츠&quot;를 검색한 다음 &quot;셔츠&quot; 검색에서 하나의 결과를 클릭하는 경우 클릭스루 비율은 50%입니다. |
| 전환율 | 쇼핑객이 구매한 제품의 비율과 지정된 날짜 범위 동안 쇼핑객이 클릭한 제품 수입니다. 예를 들어, 쇼퍼가 팝오버에서 6개의 제품을 보고, 하나를 클릭한 다음, 구매를 수행하는 경우 상호 작용의 전환율은 100%입니다. <br /><br />전환율은 특정 제품의 보기 수에 영향을 받지 않습니다. 예를 들어 전환율은 쇼핑객이 검색을 사용하지만 제품을 클릭하지 않는 경우 동일하게 유지됩니다. |
| 결과 없음 비율 | 지정된 날짜 범위에 대한 결과를 반환하지 않는 고유 검색의 백분율입니다. 예를 들어, 쇼핑객이 &quot;fjjjfjfjf&quot;를 두 번 검색(결과 없음)하고 &quot;바지&quot;를 한 번 검색(결과 있음)하는 경우 결과 없음 비율은 66.67%입니다. |
| 평균 클릭 위치 | 지정된 날짜 범위에 대한 고유 검색에 따른 평균 클릭스루 비율의 상대적 위치입니다. |

| 보고서 | 설명 |
|--- |--- |
| 결과 없음 | 결과를 반환하지 않는 검색 쿼리와 지정된 날짜 범위 동안 사용한 횟수를 나열합니다. 보고서 제한: 상위 500개 용어 |
| 인기 있는 결과 | 지정된 날짜 범위 동안 가장 많은 보기를 받은 제품의 이름을 나열합니다. 방문 빈도가 높은 결과는 노출 횟수만을 기반으로 계산되며 생성된 클릭 수 또는 매출의 영향을 받지 않습니다. 보고서 제한: 상위 500개 용어 |
| 고유 검색 | 지정된 날짜 범위 동안 사용된 고유한 검색 쿼리를 나열합니다. 보고서 데이터는 고유 검색 스냅샷 데이터와 동일한 방식으로 계산됩니다. 쇼핑객이 동일한 검색 쿼리를 두 번 입력했지만 한 시간 이상 차이가 나는 경우 검색은 두 개의 고유한 검색으로 간주됩니다. 보고서 제한: 상위 500개 용어 |
