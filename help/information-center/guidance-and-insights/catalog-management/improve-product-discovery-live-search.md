---
title: Adobe Commerce Live Search를 통해 제품 검색 개선
description: 검색 성능 인사이트 및 의미 체계 검색을 사용하여 구매자가 관련 제품을 찾는 방법에 대해 알아봅니다.
audience: Merchandisers, commerce administrators, and store owners
autotag-review: '2026-10-21T12:57:39.807Z'
TQID: 'https://experienceleague.adobe.com/vUbbKdcd7RFb3YUNNjlW4u7AgtiXJKeZeRs9uJwxYyY'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 4067ab89-2e97-5de1-8d98-de8318461a8d
    internal-label: Products
  - id: 76cfaac4-e563-56dd-8938-708bf8b84956
    internal-label: Attributes
  - id: cdfd3bc1-dc23-5cf0-b965-d3c0c55cde67
    internal-label: Best Practices
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
    internal-label: Catalog management
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: 125c1f49-aefd-5f34-a252-288937f95f6b
    internal-label: Marketing Tools
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
topic_v2:
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
    internal-label: Insights
source-git-commit: f54c816fd23786ec519d5c890bc2664c3dcf8c6f
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 0%
---

# Adobe Commerce Live Search를 통해 제품 검색 개선

<table style="table-layout:auto">
<tr style="border: 0;">
   <td valign="middle" style="vertical-align: middle;"><img alt="산드라 곤잘레스 망가나의 초상화" src="../../assets/guidance-and-insights/live-search-author-avatar-sgonzalezmangana.png" width="96"><br><strong>Sandra Gonzalez Mangana</strong><br><em>고급 제품 관리자</em></td>
</tr>
</table>

*검색 성능 인사이트 및 의미 체계 검색을 통해 구매자가 필요한 제품을 찾을 수 있도록 지원합니다.*

카탈로그에 올바른 제품을 담는 것은 쇼핑 경험의 일부일 뿐입니다. 쇼핑객들은 또한 그들이 자연적으로 사용하는 단어나 문구, 질문을 사용하여 그러한 상품을 찾을 수 있어야 합니다.

Adobe Commerce 라이브 검색은 검색 문제를 발견하고 경험을 구체화하는 데 도움이 되는 검색 성능 인사이트를 제공합니다. 이러한 통찰력을 사용하여 검색 결과가 반환되는지 여부뿐만 아니라 쇼핑객이 어려워하는 위치를 조사합니다.

## 검색 성능에서 신호 찾기

라이브 검색 성능 작업 영역에서 고유 검색, 결과가 없는 검색, 인기 있는 결과, 클릭스루 비율, 전환율 및 평균 클릭 위치와 같은 지표를 검토합니다. 트렌드를 식별하고 주의가 필요한 쿼리 또는 제품을 결정합니다. [성능](https://experienceleague.adobe.com/ko/docs/commerce/live-search/live-search-admin/performance)

![고유 검색, 평균 클릭 위치, 클릭스루 비율, 전환율 및 결과 0을 표시하는 실시간 검색 성능 작업 영역(고유 검색, 결과 0개 및 인기 있는 결과 탭 포함)](../../assets/guidance-and-insights/live-search-performance-dashboard.png){width="800" zoomable="yes"}

*실시간 검색 성능 작업 영역에 검토할 지표가 표시됩니다. 표시된 값은 샘플 데이터입니다.*

다음 신호를 고려하십시오.

- **결과가 없는 검색:** 결과가 없는 쿼리는 카탈로그, 제품 정보 또는 검색 설정의 차이를 가리킬 수 있습니다. 결과 없는 검색을 5% 미만으로 유지하는 것을 목표로 합니다. 이 임계값을 초과하는 속도는 조사할 가치가 있는 신호입니다.
- **낮은 클릭스루 또는 약한 클릭 위치:** 쇼핑객이 필요에 맞지 않는 결과를 보거나 관련 제품이 눈에 잘 띄지 않을 수 있습니다. 참여를 보장하려면 제품 클릭을 유발하는 검색 비율을 최소 50% 이상이어야 합니다.
- **낮은 검색 전환:** 검색이 쇼핑객이 쿼리에서 구매로 이동하는 데 도움이 되는지 여부를 검토합니다. 전환율이 3%를 넘는 경우를 목표로 하십시오.

이를 보편적인 통과/실패가 아닌 벤치마크 및 진단 신호로 취급합니다. 성능은 업계, 카탈로그 복잡성, 고객 행동 및 각 지표를 측정하는 방식에 따라 다릅니다. 스토어에 대한 기준을 설정하고 시간 경과에 따른 성과를 비교합니다. 결과는 카탈로그, 쇼핑객 및 결과 측정 방법에 따라 다를 수 있습니다.

## 정확한 단어뿐만 아니라 쇼핑객의 의도와 일치

쇼핑객들이 항상 카탈로그의 용어를 사용하여 제품을 설명하는 것은 아닙니다. 예를 들어, &quot;하루 종일 서 있기 편한 신발&quot;을 찾는 사람은 &quot;쿠션이 있는 보행 스니커즈&quot;로 묘사된 제품에 관심이 있을 수 있습니다.

시맨틱 검색은 키워드 일치와 함께 의미와 컨텍스트를 사용하므로 쿼리가 카탈로그 문구와 정확히 일치하지 않더라도 자연어 쿼리를 관련 제품에 연결할 수 있습니다. 라이브 검색은 키워드 및 의미 일치를 하나의 검색 경험에 결합합니다. [의미 체계 검색](https://experienceleague.adobe.com/ko/docs/commerce/live-search/live-search-admin/semantic-search)

의미 일치는 탐색적 검색에 도움이 될 수 있지만 관련성은 여전히 카탈로그에서 사용 가능한 제품 및 정보에 따라 다릅니다. 정확한 모델, 사양 또는 호환성 요구 사항이 포함된 검색의 경우 결과가 정확하게 유지되는지 확인합니다.

## 배포에 대한 의미 체계 검색 확인

설정은 사용하는 Adobe Commerce 제품에 따라 다릅니다.

- **Adobe Commerce on cloud infrastructure 또는 온-프레미스:** Adobe Commerce 2.4.4 이상에서 실시간 검색 의미 체계 검색을 사용할 수 있습니다. 관리자에서 마케팅 > SEO 및 검색 > 라이브 검색으로 이동하여 설정 을 열고 의미 체계 검색을 활성화하고 저장합니다. 영어 카탈로그를 지원합니다. [설정—의미 체계 검색](https://experienceleague.adobe.com/ko/docs/commerce/live-search/live-search-admin/settings)
- **Adobe Commerce as a Cloud Service:** 시스템에서 기본적으로 의미 체계 검색을 사용할 수 있습니다. 영어 카탈로그를 지원합니다. [의미 체계 검색](https://experienceleague.adobe.com/ko/docs/commerce/live-search/live-search-admin/semantic-search)
- **Adobe Commerce Optimizer:** 시스템에서 기본적으로 의미 체계 검색을 사용할 수 있습니다. 시맨틱 부스트 및 유사성 임계값과 같은 컨트롤을 선택적으로 조정할 수 있습니다. 설정에는 유사 항목 검색 옵션도 포함됩니다. [의미 체계 검색](https://experienceleague.adobe.com/ko/docs/commerce/optimizer/setup/semantic-search) · [설정—선택적 조정](https://experienceleague.adobe.com/ko/docs/commerce/optimizer/settings)

## 검색 인사이트를 작업으로 전환

지속적인 검토 주기를 사용하여 제품 검색을 개선합니다.

1. **조사할 쿼리를 찾으십시오.** 결과 없는 검색, 자주 찾는 쿼리 및 참여도가 낮은 검색을 검토하십시오.
2. **쇼핑객이 무엇을 요구하는지 확인하세요.** 쿼리가 누락된 제품, 단어 불일치 또는 명확하지 않은 제품 데이터를 가리킬지 여부를 결정합니다.
3. **제품 정보 개선** 제품 속성 및 설명을 쇼핑객이 사용하는 용어에 정확하고 유용하게 사용하십시오. 라이브 검색의 경우 Adobe에서는 적절한 검색 가능한 속성 및 가중치를 설정하고 속성 데이터가 적절한지 확인할 것을 권장합니다. [실시간 검색 모범 사례](https://experienceleague.adobe.com/ko/docs/commerce/live-search/best-practice)
4. **검색 환경을 개선합니다.** 적절한 경우 검색 규칙, 동의어 및 패싯을 사용하여 쇼핑객이 관련 결과를 찾고 좁힐 수 있도록 하십시오. [실시간 검색 모범 사례](https://experienceleague.adobe.com/ko/docs/commerce/live-search/best-practice)
5. **결과를 검토하고 반복합니다.** 변경 후 동일한 쿼리 및 성능 신호를 모니터링한 다음 쇼핑객이 수행하는 작업에 따라 조정합니다.

## 모든 검색 카운트 만들기

검색 쿼리는 쇼핑객이 원하는 것을 나타내는 신호입니다. 검색 성능 인사이트를 관련 제품 정보 및 적절한 검색 기능과 연결하여 고객이 자신의 요구 사항에 맞는 제품을 보다 쉽게 찾을 수 있도록 합니다.

### 자세히 알아보기

- [라이브 검색이란?](../../../live-search/overview.md)
- [라이브 검색 우수 사례](../../../live-search/best-practice.md)
- 클라우드 인프라의 Adobe Commerce에 대한 [의미 체계 검색](../../../live-search/semantic-search.md)
- Adobe Commerce Optimizer용 [의미 체계 검색](../../../optimizer/setup/semantic-search.md)
