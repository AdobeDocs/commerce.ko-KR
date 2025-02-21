---
title: 색인화
description: ' [!DNL Live Search] 제품 특성 속성을 인덱싱하는 방법을 알아봅니다.'
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 0%

---

# 색인화

[!DNL Live Search] 인덱싱 프로세스는 제품 특성을 카탈로그로 읽고 신속하게 제품을 검색, 필터링 및 제공할 수 있도록 인덱스를 만듭니다.

제품 속성 속성(메타데이터)은 다음을 결정합니다.

* 카탈로그에서 속성을 사용하는 방법
* 스토어에서의 모양 및 동작
* 데이터 전송 작업에 포함된 데이터

특성 메타데이터의 범위는 `website/store/store view`입니다.

[!DNL Live Search] API를 사용하면 클라이언트가 Adobe Commerce 관리자에서 [storefront 속성](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/product-attributes) `Use in Search`이(가) `Yes`(으)로 설정된 모든 제품 특성별로 정렬할 수 있습니다. 사용하도록 설정하면 특성에 `Search Weight`을(를) 설정할 수 있습니다.

[!DNL Live Search]은(는) 삭제된 제품 또는 `Not Visible Individually`(으)로 설정된 제품을 색인화하지 않습니다.

>[!NOTE]
>
> [!DNL Live Search]을(를) 보유한 Commerce 고객은 [SaaS 가격 인덱서](../price-index/price-indexing.md)를 통해 웹 사이트에서 더 빠른 가격 변경 업데이트 및 동기화 시간을 이용할 수 있습니다.

## 색인 지정 파이프라인

클라이언트가 검색(필터링 가능, 정렬 가능) 인덱스 메타데이터를 검색하기 위해 상점 첫 화면에서 검색 서비스를 호출합니다. *계층화된 탐색에서 사용* 속성이 `Filterable (with results)`(으)로 설정되어 있고 *제품 목록에서 정렬에 사용*&#x200B;이 `Yes`(으)로 설정된 검색 가능한 제품 특성만 검색 서비스에서 호출할 수 있습니다.

동적 쿼리를 만들려면 검색 서비스는 검색 가능한 특성과 해당 [가중치](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search-results)를 알아야 합니다. [!DNL Live Search]은(는) Adobe Commerce 검색 가중치를 적용합니다(1-10, 10이 가장 높은 우선 순위). 동기화되어 카탈로그 서비스와 공유되는 데이터 목록은 다음 위치에 정의된 스키마에서 찾을 수 있습니다.

`vendor/magento/module-catalog-data-exporter/etc/et_schema.xml`

![[!DNL Live Search] 인덱싱 클라이언트 검색 다이어그램](assets/indexing-pipeline.svg)

1. 판매자에게 [!DNL Live Search] 권한을 확인하십시오.
1. 속성 메타데이터에 대한 변경 사항을 포함하여 스토어 보기를 가져옵니다.
1. 색인 지정 속성을 저장합니다.
1. 검색 색인을 다시 색인화합니다.

### 전체 색인

온보딩 중에 [!DNL Live Search]이(가) 구성되어 동기화되면 초기 색인을 만드는 데 최대 60분이 걸릴 수 있습니다. 큰 카탈로그는 색인화하는 데 시간이 더 걸릴 수 있습니다. `cron`이(가) 피드를 제출하고 실행을 완료한 후 프로세스가 시작됩니다.

다음 이벤트는 전체 동기화 및 색인 빌드를 트리거합니다.

* [카탈로그 데이터 동기화](install.md#synchronize-catalog-data) 온보딩
* 속성 메타데이터 변경 사항

예를 들어 `color` 특성의 `Use in Search` 속성을 `No`에서 `Yes`(으)로 변경하면 특성 메타데이터가 `searchable=true`(으)로 변경되고 전체 동기화 및 색인 재지정을 트리거합니다. 다음 특성 메타데이터는 변경 시 전체 동기화를 트리거하고 다시 인덱싱합니다.

* `filterableInSearch`
* `searchable`
* `sortable`
* `visibleInSearch`

### 스트리밍 제품 업데이트

[온보딩](install.md#synchronize-catalog-data) 중에 초기 색인이 빌드되면 다음 증분 제품 업데이트가 계속 동기화되고 다시 색인화됩니다.

* 새 제품이 카탈로그에 추가됨
* 제품 속성 값 변경

예를 들어 `color` 특성에 새 견본 값을 추가하는 것은 스트리밍 제품 업데이트로 처리됩니다.

스트리밍 업데이트 워크플로우:

1. 업데이트된 제품은 Adobe Commerce 인스턴스에서 카탈로그 서비스로 동기화됩니다.
1. 색인 지정 서비스는 카탈로그 서비스에서 제품 업데이트를 계속 검색합니다. 업데이트된 제품은 카탈로그 서비스에 도착하면 색인화됩니다.
1. [!DNL Live Search]에서 제품 업데이트를 사용할 수 있는 데 최대 15분이 걸릴 수 있습니다.

#### 제품 가시성에 영향을 주는 업데이트

[!DNL Live Search] 관리 구성 설정, Adobe Commerce 관리 구성 설정 또는 카탈로그 데이터 업데이트를 업데이트할 때 이러한 변경 내용이 상점 앞에 표시되기 전에 지연이 발생할 수 있습니다.

다음 표는 다양한 변경 사항과 상점 첫 화면에 표시되기 전의 대략적인 대기 시간을 설명합니다.

| 업데이트 | 상점 앞에 표시될 때까지 지연 |
|---|---|
| [!DNL Live Search] 관리자가 패싯, 가격 설정, 검색 또는 카테고리 머천다이징 규칙에 대한 변경 내용을 적용했습니다. | 15-20분. |
| 언어 설정 또는 동의어 등 다시 인덱싱이 필요한 [!DNL Live Search] 관리 변경 사항입니다. | 색인 재지정이 완료된 후 최대 15분. |
| 전체 색인 재지정이 필요한 Adobe Commerce 관리 변경 사항(검색, 정렬 또는 필터링 가능한 속성 메타데이터)에 대해 설명합니다 | 색인 재지정이 완료된 후 최대 15분. |
| 제품 재고, 가격, 이름 등 색인 재지정이 필요하지 않은 카탈로그 데이터의 증분 변경. | Elastic Search 색인이 최신 데이터로 업데이트된 후 최대 15분. |

## 클라이언트 검색

[!DNL Live Search] API를 사용하면 클라이언트가 [storefront 속성](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/product-attributes), *제품 목록에서 정렬에 사용*&#x200B;을(를) `Yes`(으)로 설정하여 정렬 가능한 제품 특성별로 정렬할 수 있습니다. 테마에 따라 이 설정으로 인해 카탈로그 페이지의 [정렬 기준](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/navigation/navigation) 페이지 매김 컨트롤에 특성이 옵션으로 포함됩니다. 검색 및 필터링 가능한 [상점 속성](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/product-attributes)을(를) 사용하여 [!DNL Live Search]에서 최대 200개의 제품 특성을 색인화할 수 있습니다.

인덱스 메타데이터는 인덱싱 파이프라인에 저장되고 검색 서비스에서 액세스할 수 있습니다.

![[!DNL Live Search] 인덱스 메타데이터 API 다이어그램](assets/index-metadata-api.svg)

### 정렬 가능한 속성 워크플로

1. 클라이언트가 검색 서비스를 호출합니다.
1. 검색 서비스는 검색 관리자 서비스를 호출합니다.
1. 검색 서비스는 인덱싱 파이프라인을 호출합니다.

## 모든 제품에 대해 색인화됨

이 목록에 있는 필드의 순서는 내보낸 제품 데이터의 일반적인 열 순서를 반영합니다.

* `environment_id`
* `website_code`
* `store_code`
* `store_view_code`
* `product_id`
* `sku`
* `name`
* `type`
* `displayable`
* `deleted`
* `url`
* `currency`
* `meta_description`
* `meta_keyword`
* `meta_title`
* `description`
* `short_description`
* `weight`
* `image`
* `small_image`
* `thumbnail_image`
* `prices`
* `in_stock`
* `low_stock`

다음 필드는 구성 가능한 모든 제품에 대해 색인화됩니다.

* `childrenSkus`
