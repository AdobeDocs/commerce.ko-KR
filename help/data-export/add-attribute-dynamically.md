---
title: 제품 속성을 동적으로 추가
description: 데이터 동기화 프로세스 중에 사용자 지정 제품 속성을 데이터 내보내기 피드에 동적으로 추가하는 방법을 알아봅니다.
role: Admin, Developer
exl-id: d5ed7497-4be1-440a-a567-81b64fdc54fc
source-git-commit: bf45670a0bc5fb02dd229a9e3d7af7f2676c5a1f
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 0%

---

# 데이터 동기화 중에 제품 속성을 동적으로 추가

데이터 동기화 프로세스 중에 속성을 추가하는 플러그인을 만들어 Adobe Commerce에 등록하지 않고 제품 속성을 확장할 수 있습니다.

>[!NOTE]
>
>제품 특성을 확장하는 가장 좋은 방법은 [Adobe Commerce에 추가](extensibility-and-customizations.md#add-product-attributes-to-adobe-commerce)하는 것입니다. 여기서 Commerce 관리에서 해당 특성을 구성하고 관리할 수 있습니다. Commerce 상점 서비스에만 필요하고 Adobe Commerce에 등록하지 않으려는 경우에만 동적으로 추가하십시오. 카탈로그 서비스 GraphQL 스키마를 확장하기 위해 [카탈로그 서비스와 API Mesh](../catalog-service/mesh.md)를 사용하여 사용자 지정 특성을 관리하는 옵션도 있습니다.

## 제품 속성 추가

`Magento\CatalogDataExporter\Model\Provider\Product\Attributes` 클래스에 `customer_attribute`을(를) 추가하는 플러그인을 만듭니다.

1. 플러그인을 정의하려면 [종속성 삽입 구성 파일](https://developer.adobe.com/commerce/php/development/build/dependency-injection-file/)&#x200B;(`di.xml`)을(를) 업데이트하십시오.

   ```xml
   <type name="Magento\CatalogDataExporter\Model\Provider\Product\Attributes">
     <plugin name="product_customer_attributes" type="Vendor\CatalogDataExporter\Model\Plugin\AddAttribute"/>
   </type>
   ```

1. 플러그인을 만듭니다.

   ```php
    <?php
    declare(strict_types=1);
   
    namespace Vendor\CatalogDataExporter\Model\Plugin;
   
    use Magento\CatalogDataExporter\Model\Provider\Product\Attributes;
   
    class AddAttribute {
   
         /**
          * @param Attributes $subject
          * @param array $result
          * @param $arguments
          * @return array
          * @throws \Zend_Db_Statement_Exception
          */
          public function afterGet(Attributes $subject, array $result, $arguments): array
          {
              $additionalAttributes = [];
              $attributeCode = 'customer_attribute';
              foreach ($result as $product) {
                  if (!isset($product['productId']) || !isset($product['storeViewCode'])) {
                      continue;
                  }
                  // HINT: if needed, do filtration by "storeViewCode" and or "productId"
   
                  $productId = $product['productId'];
                  $storeViewCode = $product['storeViewCode'];
   
                  $newKey = \implode('-', [$product['storeViewCode'], $product['productId'], $attributeCode]);
                  if (isset($additionalAttributes[$newKey])) {
                      continue;
                  }
                  $additionalAttributes[$newKey] = [
                      'productId' => $productId,
                      'storeViewCode' => $storeViewCode,
                      'attributes' => [
                          'attributeCode' => $attributeCode,
                          // provide single or multiple values for the attribute
                          'value' => [
                              rand(1, 42)
                          ]
                      ]
                  ];
   
              }
   
              return array_merge($result, $additionalAttributes);
          }
    }
   ```

   플러그인을 추가하면 변경 사항이 다음에 예약된 동기화 동안 연결된 상점 서비스에 동기화됩니다. 업데이트를 즉시 보내려면 다음 CLI 명령을 사용하여 동기화 프로세스를 수동으로 시작하십시오.

   ```
   bin/magento saas:resync --feed=products
   ```

## 사용자 지정 제품 특성 메타데이터 선언

사용자 지정 제품 특성을 동적으로 만들고, 이 특성을 Storefront 서비스의 표시, 검색 또는 필터링에 사용하려면 제품 특성 메타데이터를 추가하여 Storefront 동작을 구성하십시오.

1. [종속성 삽입 구성 파일](https://developer.adobe.com/commerce/php/development/build/dependency-injection-file/)&#x200B;(`di.xml`)을(를) 업데이트하여 제품 특성 메타데이터에 대한 플러그인을 정의합니다.

   ```xml
   <type name="\Magento\CatalogDataExporter\Model\Provider\ProductMetadata">
     <plugin name="product_customer_attributes_metadata" type="Vendor\CatalogDataExporter\Model\Plugin\AddAttributeMetadata"/>
   </type>
   ```

1. 다음 공급자 `\Magento\CatalogDataExporter\Model\Provider\ProductMetadata`에 대한 플러그인을 만드십시오.

   필수 필드가 필요하면 `vendor/magento/module-catalog-data-exporter/etc/et_schema.xml`의 `ProductAttributeMetadata`을(를) 확인하십시오.

   ```php
    <?php
    declare(strict_types=1);
   
    namespace Vendor\CatalogDataExporter\Model\Plugin;
   
    use Magento\CatalogDataExporter\Model\Provider\ProductMetadata;
   
    class AddAttributeMetadata {
   
         /**
          * @param ProductMetadata $subject
          * @param array $result
          * @param $arguments
          * @return array
          * @throws \Zend_Db_Statement_Exception
          */
         public function afterGet(ProductMetadata $subject, array $result, $arguments): array
         {
              $result[] = [
                'id' => '123',
                // provide storeCode, websiteCode and storeViewCode applicable for your AC instance
                'storeCode' => 'default',
                'websiteCode' => 'base',
                'storeViewCode' => 'default',
                // specify the customer attribute code - should be the same as used in the products attributes plugin
                'attributeCode' => 'customer_attribute',
                // only product attributes are supported
                'attributeType' => 'catalog_product',
                // specify the data type
                'dataType' => 'int',
                'multi' => false,
                'label' => 'Customer Attribute',
                'frontendInput' => 'select',
                'required' => false,
                'unique' => false,
                'global' => true,
                'visible' => true,
                'searchable' => true,
                'filterable' => true,
                // This value must be set to true to export it to the storefront services
                'visibleInCompareList' => true,
                'visibleInListing' => true,
                'sortable' => true,
                'visibleInSearch' => true,
                'filterableInSearch' => true,
                'searchWeight' => 1.0,
                'usedForRules' => true,
                'boolean' => false,
                'systemAttribute' => false,
                'numeric' => false,
                // specify the list of attribute options
                'attributeOptions' => [
                    'option1',
                    'option2',
                    'option3'
                ]
             ];
   
              return $result;
         }
      }
   ```

   플러그인을 추가하면 변경 사항이 다음에 예약된 동기화 동안 연결된 상점 서비스에 동기화됩니다. 업데이트를 즉시 보내려면 다음 CLI 명령을 사용하여 동기화 프로세스를 수동으로 시작하십시오.

   ```
   bin/magento saas:resync --feed=productattributes
   ```
