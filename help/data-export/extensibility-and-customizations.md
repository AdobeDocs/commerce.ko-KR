---
title: SaaS 데이터 내보내기 피드 데이터 확장 및 사용자 지정
description: ' [!DNL SaaS Data Export] 피드 데이터를 확장하고 사용자 지정하는 방법을 알아봅니다.'
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
exl-id: 694bd281-12c5-415c-a251-b4251e2edea7
TQID: https://experienceleague.adobe.com/T71zNl7WOrqzEsz4H8A8arx--q6w1B0h33CF2Q0VI4A
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 815
ht-degree: 0%

---

# SaaS 데이터 내보내기 피드 데이터 확장 및 사용자 지정

[!DNL Commerce Data Export] 확장을 사용하면 [!DNL Commerce] 응용 프로그램에서 Live Search, Catalog Service 및 Product Recommendations와 같은 Commerce 서비스로 데이터를 내보낼 수 있습니다. 필요한 경우 피드 데이터를 확장 및 사용자 정의하여 추가 속성 데이터를 포함하거나 수집된 데이터를 수정할 수 있습니다.

특성 데이터를 추가한 후 storefront 서비스를 위한 GraphQL 스키마의 [특성 필드](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/#productviewattribute-type)에서 액세스할 수 있습니다.

>[!NOTE]
>
>피드 데이터를 추가하거나 수정하면 Commerce 백엔드의 성능 및 처리 논리에 영향을 줄 수 있습니다. 프로덕션으로 병합하기 전에 사용자 지정된 코드를 테스트합니다. 백엔드에 데이터를 추가하는 대신 API Mesh를 사용하여 카탈로그 서비스 GraphQL 스키마를 확장합니다. 구성에 대한 자세한 내용은 [카탈로그 서비스 및 API Mesh](../catalog-service/mesh.md)를 참조하세요.

## 제품 피드의 시스템 속성 데이터 확장

제품 피드에는 제품 처리에 필요하거나 소비자가 일반적으로 사용하는 기본 시스템 속성이 포함됩니다. 추가 시스템 속성을 피드에 추가하여 제품 피드에 포함할 수 있습니다.

이 작업을 완료하려면 `magento/catalog-data-exporter` 모듈을 업데이트하여 [종속성 삽입 구성 파일](https://developer.adobe.com/commerce/php/development/build/dependency-injection-file/)&#x200B;(`di.xml`)에 추가 시스템 특성을 추가하십시오.

제품 특성 쿼리(`Magento\CatalogDataExporter\Model\Query\ProductAttributeQuery`)에 특성을 추가합니다.

**예**

```xml
    <type name="Magento\CatalogDataExporter\Model\Query\ProductAttributeQuery">
        <arguments>
            <argument name="systemAttributes" xsi:type="array">
                <item name="news_from_date" xsi:type="string">news_from_date</item>
                ...
                <item name="some_system_attribute_code">some_system_attribute_code</item>
            </argument>
        </arguments>
    </type>
```

## Adobe Commerce에 제품 속성 추가

개발자는 다음 방법 중 하나를 사용하여 [제품 특성 필드](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/#output-fields)에서 액세스할 수 있는 제품 특성을 추가할 수 있습니다.

- Commerce 상점 서비스로 내보낸 `products` 피드 데이터에 포함할 특성을 Adobe Commerce에 추가합니다.
- 플러그인을 사용하여 피드 동기화 프로세스 중에 속성을 동적으로 추가합니다.

### Adobe Commerce에 속성 추가

Commerce 관리자에서 제품 특성을 추가하거나 프로그래밍 방식으로 사용자 지정 PHP 모듈을 사용하여 특성을 정의하고 Adobe Commerce을 업데이트할 수 있습니다. 속성과 필요한 모든 메타데이터를 한 번에 추가할 수 있으므로 Commerce 관리자의 속성을 추가하는 것이 가장 간단한 방법입니다. 새 속성 및 해당 메타데이터 속성은 다음에 예약된 동기화 중에 자동으로 SaaS 서비스로 내보내집니다.

#### 관리에서 제품 속성 만들기

1. Commerce 관리자의 제품 특성 구성 페이지에서 특성을 만듭니다([!UICONTROL Stores] > *[!UICONTROL Attributes]* > [!UICONTROL Product]).

1. 필요에 따라 속성 집합에 속성을 추가합니다.

*Adobe Commerce 관리 안내서*&#x200B;에서 [제품 특성 만들기](https://experienceleague.adobe.com/ko/docs/commerce-admin/catalog/product-attributes/create/attribute-product-create)를 참조하십시오.

#### 프로그래밍 방식으로 제품 특성 만들기

`DataPatchInterface`을(를) 구현하는 데이터 패치를 만들어 프로그래밍 방식으로 제품 특성을 추가하고 생성자 내에서 `EavSetup Factory` 클래스의 복사본을 인스턴스화하여 특성 옵션을 구성합니다.

특성 옵션을 정의할 때 `type`, `label` 및 `input`을(를) 제외한 모든 특성 매개 변수는 선택 사항입니다. 다음 추가 매개 변수와 기본 설정과 다른 매개 변수를 정의합니다.

- **`user_defined`=`1`**—데이터를 동기화하는 동안 특성을 상점 서비스로 내보냅니다.
- **`used_in_product_listing`=`1`**—제품 목록 데이터베이스 쿼리 내에서 특성에 액세스할 수 있도록 설정합니다.

데이터 패치 만들기에 대한 자세한 내용은 *PHP 개발자 안내서*&#x200B;에서 [데이터 및 스키마 패치 개발](https://developer.adobe.com/commerce/php/development/components/declarative-schema/patches/)을 참조하십시오.

### 제품 속성을 동적으로 추가

새 EAV 특성을 도입하지 않고 제품 특성을 동적으로 만드는 방법에 대한 자세한 내용은 [제품 특성을 동적으로 추가](add-attribute-dynamically.md)를 참조하십시오.

## 피드 스키마 개요(`et_schema.xml`) {#feed-schema-overview}

각 피드 데이터 구조는 간단한 XML DSL을 사용하여 `etc/et_schema.xml`에서 선언됩니다. 프레임워크는 이 파일을 읽어 수집할 필드와 호출할 PHP 공급자 클래스를 결정합니다.

```xml
<record name="Product">
  <field name="sku" type="ID" />
  <field name="name" type="String" />
  <field name="attributes" type="Attribute" repeated="true"
         provider="Magento\CatalogDataExporter\Model\Provider\Product\Attributes">
    <using field="productId" />
    <using field="storeViewCode" />
  </field>
</record>
```

주요 요소:

- `<record>` - 피드 엔터티 정의
- `<field>` - 데이터 필드를 선언합니다. `provider` 특성은 데이터를 가져오는 `DataProcessorInterface`을(를) 구현하는 PHP 클래스를 가리킵니다
- `repeated="true"` - 필드가 개체 배열입니다.
- `<using>` - 부모 레코드 컨텍스트에서 공급자로 전달된 입력 매개 변수

>[!IMPORTANT]
>
>`et_schema.xml`에 새 필드를 추가하면 [!DNL Adobe Commerce]에서 로컬로 수집하는 내용만 변경됩니다. 수신 SaaS 서비스도 업데이트하여 새 필드를 수락하고 처리해야 상점 앞에 영향을 미칠 수 있습니다.

## 제출 후 데이터 관찰 {#observe-data-after-submission}

[!DNL SaaS Data Export]은(는) SaaS 서비스에 일괄 처리 제출이 완료되면 `data_sent_outside` 이벤트를 발송합니다. 감사 로깅, 웹후크 트리거 또는 지표 수집에 이 이벤트를 사용합니다.

**이벤트:** `data_sent_outside`

**사용 가능한 데이터:**

| 키 | 설명 |
|---|---|
| `timestamp` | 제출 서류의 Unix 타임스탬프 |
| `type` | 피드 이름(예: `products`, `prices`) |
| `data` | 제출된 피드 페이로드 |

**예제 관찰자:**

```php
<?php
namespace My\Module\Observer;

use Magento\Framework\Event\Observer;
use Magento\Framework\Event\ObserverInterface;

class DataSentOutsideObserver implements ObserverInterface
{
    public function execute(Observer $observer): void
    {
        $feedName = $observer->getData('type');
        $timestamp = $observer->getData('timestamp');
        $data = $observer->getData('data');

        // Custom logic: audit logging, webhook, metrics
    }
}
```

`etc/events.xml`에서 관찰자 등록:

```xml
<event name="data_sent_outside">
    <observer name="my_module_data_sent_outside"
              instance="My\Module\Observer\DataSentOutsideObserver" />
</event>
```

이벤트 및 관찰자에 대한 일반적인 정보는 Adobe Commerce 개발자 설명서에서 [이벤트 및 관찰자](https://developer.adobe.com/commerce/php/development/components/events-and-observers){target="_blank"}를 참조하십시오.

## 제출 전 데이터 필터링

SaaS 서비스로 데이터를 보내기 전에 중요한 필드를 수정하거나 특정 엔터티를 건너뛰려면 `Magento\SaaSCommon\Model\DataFilter` 확장 지점을 사용하십시오. 이 기능은 특정 필드가 Commerce 인스턴스를 벗어나지 않아야 하는 GDPR 또는 PCI와 같은 규정 준수 요구 사항에 유용합니다.

인터페이스를 구현하고 `etc/di.xml`에서 DI 환경 설정을 통해 연결합니다.

```xml
<preference for="Magento\SaaSCommon\Model\DataFilter"
            type="My\Module\Model\MyDataFilter" />
```

>[!NOTE]
>
>데이터 수집 후에는 필터링이 적용됩니다. `PERSIST_EXPORTED_FEED=1`이(가) 설정되면 필터링이 발생하기 전에 피드 테이블에 필터링되지 않은 페이로드가 저장됩니다.

>[!MORELIKETHIS]
>
> - [제품 특성을 동적으로 추가](add-attribute-dynamically.md)
> - [세금 클래스, 특성 집합 및 인벤토리 메타데이터 추가](add-tax-attribute-set-inventory-attributes.md)
> - [동기화 작동 방식](sync-overview.md)
