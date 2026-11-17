---
source-git-commit: 4032a0871d0a9b129ad870c93f62a2a7596ea8b7
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 0%
---
<!--
SOURCE OF TRUTH: Edit this file in the commerce.en repo:
https://github.com/Adobe-Enterprise-Docs/commerce.en/blob/main/help/_includes/ccdm-shared/setup/catalog-sources.md

This content is shared by the Adobe Commerce Optimizer Guide (commerce.en) and the
Merchandising Services with CCDM Guide (commerce-admin.en). Changes made in commerce.en
are synced automatically to commerce-admin.en, so do not edit the copy in that repo.
This includes related images in help/assets/ccdm-shared/.
-->

# 카탈로그 소스

카탈로그 소스는 제품, 특성 및 범주의 신뢰할 수 있는 범위를 나타냅니다. 일반적으로 언어, 대상 또는 시스템 출처 경계에 매핑되고 검색, 필터링 및 정렬 동작을 결정합니다.

## 카탈로그 소스 및 관련 개념

카탈로그 소스가 다른 머천다이징 서비스 개념과 관련되는 방법을 이해하면 데이터를 올바르게 모델링하는 데 도움이 됩니다.

* **카탈로그 원본** - 제품 정보를 제공하는 기본 데이터 컨텍스트입니다. 카탈로그 소스는 일반적으로 로케일(예: `en-US`, `fr-CA`) 또는 PIM 또는 ERP와 같은 외부 시스템에서 제공하는 데이터 컨텍스트를 나타냅니다. 제품, 속성 메타데이터 및 범주는 모두 카탈로그 소스별로 범위가 지정됩니다. 카탈로그 소스는 원시 카탈로그 데이터의 출처와 제품 검색에 미치는 영향(검색 결과, 필터링 및 정렬 동작)을 정의합니다.

* **[카탈로그 보기](/help/optimizer/setup/catalog-view.md)** - 특정 비즈니스 요구에 대해 구성된 카탈로그 보기. 카탈로그 보기에서 카탈로그 원본(또는 로케일)을 선택하고, [정책](/help/optimizer/setup/policies.md)을 적용하여 제품 가시성을 필터링하고, [가격 장부](/help/optimizer/setup/pricebooks.md)를 보기에 연결합니다. 단일 카탈로그 원본이 많은 카탈로그 보기 기능을 제공할 수 있습니다(예: 다른 브랜드 또는 지역에 대해 별도의 카탈로그 보기가 있는 하나의 `en-US` 원본). 카탈로그 보기를 *방법*(으)로 간주하면 해당 데이터를 상점, 채널 또는 대상에 노출할 수 있습니다.

* **[카탈로그 계층](catalog-layer.md)** - 원본 데이터를 변경하지 않고 제품 특성(이름, 설명, 이미지, 메타데이터)을 수정하기 위해 기본 카탈로그 데이터 위에 적용된 계층입니다. 차이가 제품 검색에 영향을 주지 않고 상점 디스플레이에만 영향을 미쳐야 하는 경우 카탈로그 계층을 사용합니다.

## 카탈로그 소스 채우기 방법

카탈로그 소스는 카탈로그 데이터 수집을 통해 채워집니다. 해당 데이터를 제공하는 방법은 구현에 따라 다릅니다.

- **CCDM이 포함된 Adobe Commerce as a Cloud Service**—기본 동기화는 Commerce Foundation에서 카탈로그 데이터를 제공합니다. Commerce Foundation에서 기본 제품 및 스토어 뷰 구성을 관리하고 [데이터 동기화](data-sync.md) 작업 영역에서 동기화를 모니터링합니다. 별도의 데이터 수집 API 통합이 필요하지 않습니다.
- **타사 백엔드가 있는 Adobe Commerce Optimizer** - 통합에서 [데이터 수집 API](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/)를 통해 제품 및 카탈로그 소스 정보를 제공합니다.


## 규칙 및 제한 사항

* 카탈로그 소스는 새 로케일 또는 소스 시스템에 대한 카탈로그 데이터가 머천다이징 서비스 데이터 레이어에 처음 수신될 때 만들어집니다.
* 제품 고유성은 SKU + 카탈로그 소스로 결정됩니다.
* 쇼핑객은 카탈로그 소스에 직접 액세스하지 않습니다. 카탈로그 데이터가 [카탈로그 보기](catalog-view.md)를 통해 상점 앞에 노출되었습니다.

## 모델링 지침

카탈로그 구조를 계획할 때 다음 지침을 사용하십시오. CCDM이 있는 Adobe Commerce as a Cloud Service의 경우 별도의 수집 통합을 통해 카탈로그 소스를 만들지 않고 Commerce Foundation에서 기본 구성을 관리합니다.

* 각 카탈로그 언어에 대해 별도의 카탈로그 소스를 사용하십시오.
* 제품 및 속성 차이가 검색, 필터링 또는 정렬 동작(예: 다른 검색 가능성 또는 필터링 가능성 설정)에 영향을 미쳐야 하는 경우 별도의 카탈로그 소스를 사용하십시오.
* 검색, 필터링 또는 정렬 동작을 변경하지 않고 제품 및 특성 차이가 제품 표시에 영향을 주어야 하는 경우 [카탈로그 계층](catalog-layer.md)을 사용하십시오.

>[!MORELIKETHIS]
>
> * [카탈로그 보기](catalog-view.md) - 카탈로그 원본 위에 필터링된 가격 보기를 구성합니다.
> * [카탈로그 계층](catalog-layer.md) - 원본 데이터를 변경하지 않고 제품 프레젠테이션을 수정합니다.
> * [정책](policies.md) - 카탈로그 보기에 대한 특성 기반 필터 만들기
> * [가격 장부](/help/optimizer/setup/pricebooks.md) - 다양한 고객 세그먼트에 대한 가격 구조를 관리합니다.
> * [제한된 액세스 키](restricted-access-keys.md) - 서명된 토큰 인증을 사용하여 카탈로그 보기 보호
