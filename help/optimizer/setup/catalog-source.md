---
title: 카탈로그 소스
description: 카탈로그 소스가 무엇인지, 검색, 필터링 및 정렬 동작을 위한 신뢰할 수 있는 제품, 속성 및 카테고리 범위를 정의하는 방법에 대해 알아봅니다.
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="SaaS만" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 [!DNL Adobe Commerce Optimizer] 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."
autotag-review: '2026-06-09T19:36:23.516Z'
TQID: 'https://experienceleague.adobe.com/MiLbuYx6Pf95n3jvrgvou05Ery9XHXskx8p6KrN6CYg'
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: c18ed297-2187-4aec-affb-9d9654eca6fc
subfeature_v2: id: ae62cf09-5996-4921-bda8-fbe67b62e470
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b23e006f-0a29-4f1d-8fd0-77aa56f3d12bid: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: ecff841c8e88c3897358eaf91e54c732d1edcfe4
workflow-type: tm+mt
source-wordcount: 450
ht-degree: 0%

---

# 카탈로그 소스

카탈로그 소스는 제품, 특성 및 범주의 신뢰할 수 있는 범위를 나타냅니다. 카탈로그 소스는 일반적으로 언어, 대상자 또는 시스템 출처 경계에 매핑되고 검색, 필터링 및 정렬 동작을 결정합니다.

## 카탈로그 소스 및 관련 개념

카탈로그 원본과 다른 [!DNL Adobe Commerce Optimizer] 개념의 관계를 이해하면 데이터를 올바르게 모델링하는 데 도움이 됩니다.

* **카탈로그 원본** - 제품 정보를 제공하는 기본 데이터 컨텍스트입니다. 카탈로그 원본은 일반적으로 로케일(예: `en-US`, `fr-CA`) 또는 PIM 또는 ERP와 같은 외부 시스템입니다. 제품, 속성 메타데이터 및 범주는 모두 카탈로그 소스별로 범위가 지정됩니다. 카탈로그 원본을 *원본 카탈로그 데이터를 가져오는 위치* 및 제품 검색(검색 결과, 필터링 및 정렬 동작)에 영향을 주는 *방법*(으)로 간주합니다.

* **[카탈로그 보기](catalog-view.md)** - 특정 비즈니스 요구에 대해 구성된 카탈로그 보기. 카탈로그 보기를 만들 때 사용할 카탈로그 원본(또는 로케일)을 선택한 다음 [정책](policies.md)을 추가하여 표시되는 제품을 필터링하고 [가격 장부](pricebooks.md)를 연결하여 가격을 제어합니다. 단일 카탈로그 원본이 많은 카탈로그 보기 기능을 제공할 수 있습니다(예: 다른 브랜드 또는 지역에 대해 별도의 카탈로그 보기가 있는 하나의 `en-US` 원본). 카탈로그 보기를 *방법*(으)로 간주하면 해당 데이터를 상점, 채널 또는 대상에 노출할 수 있습니다.

* **[카탈로그 계층](catalog-layer.md)** - 원본 데이터를 변경하지 않고 제품 특성(이름, 설명, 이미지, 메타데이터)을 수정하기 위해 기본 카탈로그 데이터 위에 적용된 계층입니다. 차이가 제품 검색에 영향을 주지 않고 상점 디스플레이에만 영향을 미쳐야 하는 경우 카탈로그 계층을 사용합니다.

## 규칙 및 제한 사항

* 카탈로그 소스는 데이터 수집 API를 통해 제품을 수집하여 만들어집니다. 자세한 내용은 [개발자 문서 - 데이터 수집](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/)을 참조하십시오.
* 제품 고유성은 SKU + 카탈로그 소스로 결정됩니다.
* 쇼핑객은 카탈로그 소스에 직접 액세스하지 않습니다. 카탈로그 데이터가 [카탈로그 보기](catalog-view.md)를 통해 상점 앞에 노출되었습니다.

## 모델링 지침

카탈로그 소스를 구성하는 방법을 결정할 때 다음 지침을 따르십시오.

* 다른 카탈로그 언어별로 별도의 카탈로그 소스를 만듭니다.
* 제품 및 속성 차이가 검색, 필터링 또는 정렬 동작에 영향을 줘야 하는 경우(예: 동일한 속성에 대해 다른 검색, 필터링 또는 패싯 구성) 별도의 카탈로그 소스를 사용하십시오.
* 제품 및 특성 차이가 제품 검색이 아니라 상점 표시에만 영향을 미치는 경우 [카탈로그 계층](catalog-layer.md)을 사용하십시오.

>[!MORELIKETHIS]
>
> * [카탈로그 보기](catalog-view.md) - 카탈로그 원본 위에 필터링된 가격 보기를 구성합니다.
> * [카탈로그 계층](catalog-layer.md) - 원본 데이터를 변경하지 않고 제품 프레젠테이션을 수정합니다.
> * [정책](policies.md) - 카탈로그 보기에 대한 특성 기반 필터 만들기
> * [가격 장부](pricebooks.md) - 다양한 고객 세그먼트에 대한 가격 구조를 관리합니다.
