---
title: 의미 체계 검색
description: 설정에서  [!DNL Adobe Commerce Optimizer] 의 AI 의미 체계 검색을 사용하도록 설정합니다. 속성 설정 또는 Storefront 변경이 필요하지 않습니다.
role: Admin, User
recommendations: noCatalog
badgeSaas: label="SaaS만" type="Positive" url="https://experienceleague.adobe.com/ko/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 [!DNL Adobe Commerce Optimizer] 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."
source-git-commit: 015f88e540fe5bf7acc4469d7c91b4f606709809
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 0%

---

# 의미 체계 검색

시맨틱 검색은 AI를 활용해 쇼핑객이 정확하게 입력하는 단어뿐만 아니라 어떤 의미를 갖는지 파악한다. &quot;해변 결혼식 드레스&quot; 또는 &quot;하루 종일 서 있기 편한 신발&quot;과 같은 쿼리는 카탈로그에서 정확한 문구를 사용하지 않는 경우에도 관련 제품을 반환할 수 있습니다.

[!DNL Adobe Commerce Optimizer]은(는) 키워드 일치와 의미 체계 일치를 하나의 검색 경험에 결합합니다. 상점 첫 화면에서 별도의 키워드 및 의미 체계 모드를 관리하지 않습니다. 관리자의 [설정](../settings.md#advanced-search) 작업 영역으로 이동하여 의미 체계 검색을 관리하고 선택적으로 **[!UICONTROL Advanced search]** 탭에서 고급 컨트롤을 조정합니다.

## 이점

- **빈 검색 페이지 수 감소** — 구매자는 단어가 카탈로그 텍스트와 정확히 일치하지 않으면 제품을 찾습니다.
- **더 나은 의도 일치** — 자연어, 설명 쿼리는 유용한 결과를 반환합니다.
- **더 적은 동의어 유지 관리** — 일반적인 단어 변형(예: 소파와 소파)은 종종 수동 동의어 목록 없이 처리됩니다.
- **상점 또는 개발자 작업 없음** — 의미 체계 검색은 기본적으로 활성화되어 있으며 테마 코드, 드롭인 또는 API 변경이 필요하지 않습니다.

## 작동 방식

의미 체계 검색이 활성화된 경우 [!DNL Adobe Commerce Optimizer]은(는) 시스템에서 선택한 사전 정의된 카탈로그 특성(예: 제품 이름 및 설명)을 사용하여 기존의 키워드 검색과 함께 쿼리 의미를 해석합니다. 관리자에서 속성을 선택하거나 우선 순위를 지정하지 않습니다.

For example:

- &#39;가죽 소파&#39;를 검색하면 &#39;가죽 소파&#39;라는 라벨이 붙은 제품들이 반환될 수 있다.
- &#39;스프링드레스&#39;는 상품명에 &#39;스프링&#39;이 없어도 계절에 맞는 드레스를 연출할 수 있다.
- &quot;트레일 러닝용 신발&quot;은 오프로드 또는 하이킹 신발로 설명된 제품과 일치할 수 있습니다.

## 의미 체계 검색을 활성화하면 어떻게 됩니까?

의미 체계 검색은 기존 [!DNL Adobe Commerce Optimizer] 검색 구성과 함께 작동합니다. 키워드 검색을 바꾸거나 스토어프론트를 다시 구성하지 않습니다.

의미 체계 검색이 활성화된 경우:

- 기존 [머천다이징 규칙](../merchandising/rules/overview.md), [동의어](../merchandising/synonyms/overview.md), [패싯](../merchandising/facets/overview.md), 부스트 및 필터가 계속 적용됩니다.
- 시맨틱 검색은 AI 기반의 쇼퍼 의도 이해를 더해 키워드 매칭과 함께 결과 관련성을 향상시킵니다.
- 사전 정의된 카탈로그 속성은 자동으로 색인화됩니다. 속성을 선택하거나 별도의 구성을 게시하지 않습니다.

## 관리자의 의미 체계 검색 관리

적절한 영어 카탈로그에 대해 의미 체계 검색이 **기본적으로 활성화됨**&#x200B;입니다. 설정을 확인하거나 변경하려면 **[!UICONTROL Settings]** > **[!UICONTROL Advanced search]**(으)로 이동하십시오.

1. 관리자의 **[!UICONTROL Settings]**(으)로 이동합니다.
1. **[!UICONTROL Advanced search]** 탭에서 **[!UICONTROL Enable semantic search]**&#x200B;을(를) 검토합니다.

   활성화되면 검색은 의미와 컨텍스트를 기반으로 제품과 일치하므로 더 연관성 있는 결과를 생성하고, 빈 검색 페이지를 줄이며, 전환을 향상시킬 수 있습니다.

1. 토글 또는 조정 컨트롤을 변경하려면 **[!UICONTROL Save]**&#x200B;을(를) 클릭합니다.

   색인화가 완료된 후 검색 결과가 업데이트됩니다. 중간 크기의 카탈로그의 경우 색인화는 최대 30분이 소요될 수 있습니다. 수백만 개의 제품이 포함된 대규모 카탈로그의 경우 몇 시간이 걸릴 수 있습니다.

>[!NOTE]
>
> 의미 체계 검색은 **영어** 카탈로그에서만 사용할 수 있습니다. **[!UICONTROL Language]**&#x200B;을(를) 영어가 아닌 카탈로그로 변경하면 **[!UICONTROL Enable semantic search]**&#x200B;이(가) 자동으로 비활성화됩니다.

저장한 후 별도의 구성을 게시하거나 상점 설정을 변경할 필요가 없습니다.

## 활성화 후 유효성 검사

시맨틱 검색이 활성화되고 색인화가 완료되면 Adobe에서 검색 성능의 유효성을 검사하는 것이 좋습니다. [검색 성능](../manage-results/search-performance.md) 페이지에서 비즈니스에 중요한 지표를 검토하고 쿼리를 테스트할 수 있습니다.

1. **고유 검색** 보고서에서 가장 많이 검색된 용어를 검토하십시오.
1. 상점 첫 화면의 **0개 결과** 보고서에서 기록된 0개 결과 쿼리를 테스트합니다.
1. 활성화 전후의 동일한 쿼리에 대한 검색 결과를 비교합니다.
1. 클릭스루 비율, 전환율 및 결과 0을 포함한 검색 전환 및 참여 지표를 모니터링합니다.

## 선택적 조정

**[!UICONTROL Advanced search]** 탭에서 의미 체계 검색을 사용하도록 설정한 후 검색이 작동하는 방식을 조정할 수 있습니다.

- **[!UICONTROL Semantic boost]** — 의미 기반 일치가 순위에 영향을 미치는 정도를 늘리거나 줄입니다. 예를 들어 의미 체계 검색을 통해 검색된 제품 일치가 결과 끝에 표시된다고 가정해 보겠습니다. 증폭을 추가하면 결과에서 더 높게 이동합니다.
- **[!UICONTROL Similarity threshold]** — 제품이 나타나기 전에 일치가 얼마나 가까워야 하는지 설정합니다. 값이 낮을수록 더 많은 결과가 표시되고, 값이 높을수록 더 적은 일치 항목이 표시됩니다.
- **[!UICONTROL Fuzzy search]** 및 **[!UICONTROL Fuzzy search similarity threshold]** — 쿼리에 작은 맞춤법 차이가 있을 때 구매자가 제품을 찾을 수 있도록 지원합니다.

컨트롤 설명 및 단계별 지침은 [고급 검색](../settings.md#advanced-search)을 참조하세요.

## 우수 사례

- 명확하고 설명적인 제품 이름과 설명(이상적으로 50~100단어)을 사용하여 키워드와 의미 체계 일치 모두 작업할 강력한 카탈로그 텍스트가 있습니다.
- 기본 **[!UICONTROL Enable semantic search]** 설정으로 시작한 다음 결과가 너무 광범위하거나 너무 좁은 경우에만 **[!UICONTROL Semantic boost]** 또는 **[!UICONTROL Similarity threshold]**&#x200B;을(를) 조정합니다.
- 의미 체계 검색에 특수 용어가 포함되지 않을 수 있는 브랜드별 또는 고도의 기술적 [동의어](../merchandising/synonyms/overview.md)를 유지하십시오.

## 문제 해결

| 문제 | 할 일 |
| --- | --- |
| 저장 직후 상점 변경 사항 없음 | 인덱싱이 완료될 때까지 기다립니다. 큰 카탈로그는 시간이 더 걸릴 수 있습니다. |
| 결과가 너무 광범위하게 느껴짐 | **[!UICONTROL Advanced search]** 탭에서 **[!UICONTROL Similarity threshold]** 또는 **[!UICONTROL Semantic boost]**&#x200B;을(를) 높입니다. |
| 결과가 너무 좁게 느껴짐 | **[!UICONTROL Similarity threshold]**&#x200B;을(를) 낮추거나 **[!UICONTROL Semantic boost]**&#x200B;을(를) 올립니다. |
| 의미 체계 검색을 사용할 수 없음 | **[!UICONTROL Language]**&#x200B;이(가) **영어**(으)로 설정되어 있는지 확인하십시오. |

## 제한 사항 {#semantic-search-limitations}

- **카탈로그 언어:** 의미 체계 검색은 **영어** 언어 카탈로그에서만 사용할 수 있습니다.

## 이 항목에 대한 추가 도움말

- [고급 검색](../settings.md#advanced-search)
- [동의어](../merchandising/synonyms/overview.md)
- [검색 성능](../manage-results/search-performance.md)
