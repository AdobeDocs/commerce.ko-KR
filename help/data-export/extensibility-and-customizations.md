---
title: SaaS 데이터 내보내기 피드 데이터 확장 및 사용자 지정
description: ' [!DNL SaaS Data Export] 피드 데이터를 확장하고 사용자 지정하는 방법을 알아봅니다.'
role: Admin, Developer
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 0%

---

# SaaS 데이터 내보내기 피드 데이터 확장 및 사용자 지정

[!DNL Commerce Data Export] 확장을 사용하면 [!DNL Commerce] 응용 프로그램에서 Live Search, Catalog Service 및 Product Recommendations와 같은 Commerce 서비스로 데이터를 내보낼 수 있습니다. 필요한 경우 피드 데이터를 확장 및 사용자 정의하여 추가 속성 데이터를 포함하거나 수집된 데이터를 수정할 수 있습니다.

특성 데이터를 추가한 후 storefront 서비스를 위한 GraphQL 스키마의 [특성 필드](https://developer.adobe.com/commerce/services/graphql/catalog-service/products/#productviewattribute-type)에서 액세스할 수 있습니다.

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

개발자는 다음 방법 중 하나를 사용하여 [제품 특성 필드](https://developer.adobe.com/commerce/services/graphql/catalog-service/products/#output-fields)에서 액세스할 수 있는 제품 특성을 추가할 수 있습니다.

- Commerce 상점 서비스로 내보낸 `products` 피드 데이터에 포함할 특성을 Adobe Commerce에 추가합니다.
- 플러그인을 사용하여 피드 동기화 프로세스 중에 속성을 동적으로 추가합니다.

### Adobe Commerce에 속성 추가

Commerce 관리자에서 제품 특성을 추가하거나 프로그래밍 방식으로 사용자 지정 PHP 모듈을 사용하여 특성을 정의하고 Adobe Commerce을 업데이트할 수 있습니다. 속성 및 필요한 모든 메타데이터를 추가할 수 있으므로 제품 속성을 추가하는 가장 간단한 방법입니다. 새 속성 및 해당 메타데이터 속성은 다음에 예약된 동기화 중에 자동으로 SaaS 서비스로 내보내집니다.

#### 관리에서 제품 속성 만들기

1. Commerce 관리자의 제품 특성 구성 페이지에서 특성을 만듭니다([!UICONTROL Stores] > *[!UICONTROL Attributes]* > [!UICONTROL Product]).

1. 필요에 따라 속성 집합에 속성을 추가합니다.

*Adobe Commerce 관리 안내서*&#x200B;에서 [제품 특성 만들기](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/create/attribute-product-create)를 참조하십시오.

#### 프로그래밍 방식으로 제품 특성 만들기

`DataPatchInterface`을(를) 구현하는 데이터 패치를 만들어 프로그래밍 방식으로 제품 특성을 추가하고 생성자 내에서 `EavSetup Factory` 클래스의 복사본을 인스턴스화하여 특성 옵션을 구성합니다.

특성 옵션을 정의할 때 `type`, `label` 및 `input`을(를) 제외한 모든 특성 매개 변수는 선택 사항입니다. 다음 추가 옵션 및 기본 설정과 다른 옵션을 정의합니다.

- `user_defined` = `1`을(를) 설정하여 데이터를 동기화하는 동안 속성을 Storefront 서비스로 내보내야 합니다.
- 제품 목록 데이터베이스 쿼리 내에서 특성에 액세스할 수 있도록 하려면 `used_in_product_listing` = `1`을(를) 설정합니다.

데이터 패치 만들기에 대한 자세한 내용은 *PHP 개발자 안내서*&#x200B;에서 [데이터 및 스키마 패치 개발](https://developer.adobe.com/commerce/php/development/components/declarative-schema/patches/)을 참조하십시오.

### 제품 속성을 동적으로 추가

새 Eav 특성을 도입하지 않고 제품 특성을 동적으로 만드는 방법에 대한 자세한 내용은 [특성을 동적으로 추가](add-attribute-dynamically.md)를 참조하십시오.
