---
title: SaaS 가격 인덱싱
description: SaaS 가격 색인을 사용하여 성능 향상
seo-title: Adobe SaaS Price Indexing
seo-description: Price indexing give performance improvements using SaaS infrastructure
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 0%

---

# SaaS 가격 인덱싱

SaaS 가격 산정 색인화는 색인 지정 및 가격 계산과 같은 리소스 집약적인 작업을 Commerce 애플리케이션에서 Adobe의 클라우드 인프라로 오프로드하여 사이트 성능을 최적화합니다. 이 접근 방식을 통해 판매자는 신속하게 리소스를 확장하여 가격 인덱싱 시간을 단축하고 상점 및 연결된 Commerce 서비스에 보다 빠르게 가격 업데이트를 제공할 수 있습니다.

다음 다이어그램은 Commerce이 Commerce 애플리케이션에 포함된 [가격 인덱싱](https://experienceleague.adobe.com/ko/docs/commerce-operations/configuration-guide/cli/manage-indexers) 프로세스를 사용할 때 SaaS 서비스로 이동하는 인덱싱 데이터 흐름을 보여 줍니다.

![기본 데이터 흐름](assets/old_way.png)

SaaS 가격 인덱싱이 활성화되면 데이터 흐름이 변경됩니다. 가격 인덱싱은 [Commerce SaaS 데이터 내보내기](../data-export/data-synchronization.md)를 사용하여 수행됩니다.

![SaaS 가격 인덱싱 데이터 흐름](assets/new_way.png)

모든 가맹점은 SaaS 가격 색인을 사용하면 혜택을 받을 수 있지만, 다음과 같은 특성을 가진 프로젝트가 있는 가맹점은 가장 큰 이익을 실현할 수 있습니다.

* **지속적인 가격 변경**-빈번한 프로모션, 시즌 할인 또는 재고 가격 인하와 같은 전략적 목표를 충족하기 위해 가격을 반복적으로 변경해야 하는 판매자.
* **여러 웹 사이트 및/또는 고객 그룹**-여러 웹 사이트(도메인/브랜드) 및/또는 고객 그룹에 공유된 제품 카탈로그를 보유한 판매자입니다.
* **웹 사이트 또는 고객 그룹의 고유 가격**-웹 사이트 또는 고객 그룹의 고유 가격이 들어 있는 광범위한 공유 제품 카탈로그를 사용하는 판매자입니다. 가격을 사전 협상한 B2B 가맹점이나 가격 전략이 다른 브랜드가 대표적이다.

## SaaS 가격 색인화 사용

Adobe Commerce Services를 설치하면 SaaS 가격 색인화가 자동으로 활성화됩니다. 모든 기본 제공 Adobe Commerce 제품 유형에 대한 가격 계산을 지원합니다.

### 요구 사항

* Adobe Commerce 2.4.4+

### 전제 조건

* 다음 Commerce 서비스 중 하나를 최신 버전의 Commerce 확장 프로그램과 함께 설치해야 합니다.

   * [카탈로그 서비스](../catalog-service/overview.md)
   * [라이브 검색](../live-search/overview.md)
   * [제품 추천](../product-recommendations/guide-overview.md)


>[!NOTE]
>
>필요한 경우 [카탈로그 어댑터](catalog-adapter.md)를 사용하여 Commerce 응용 프로그램의 기본 가격 인덱서를 사용하지 않도록 설정할 수 있습니다.

## SaaS 가격 인덱싱과 가격 동기화

Adobe Commerce에 대해 SaaS 가격 인덱싱을 활성화한 후 새 피드를 동기화하여 상점 및 Commerce 서비스의 가격을 업데이트합니다.

```bash
bin/magento saas:resync --feed=scopesCustomerGroup
bin/magento saas:resync --feed=scopesWebsite
bin/magento saas:resync --feed=prices
```

### 사용자 정의 제품 유형에 대한 가격

가격 계산은 기준 가격, 특별 가격, 그룹 가격, 카탈로그 규칙 가격 등과 같은 사용자 지정 제품 유형에 대해 지원됩니다.

특정 공식을 사용하여 최종 가격을 계산하는 사용자 정의 제품 유형이 있는 경우 제품 가격 피드의 동작을 확장할 수 있습니다.

1. `Magento\ProductPriceDataExporter\Model\Provider\ProductPrice` 클래스에 플러그인을 만듭니다.

   ```xml
   <config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:noNamespaceSchemaLocation="urn:magento:framework:ObjectManager/etc/config.xsd">
       <type name="Magento\ProductPriceDataExporter\Model\Provider\ProductPrice">
           <plugin name="custom_type_price_feed" type="YourModule\CustomProductType\Plugin\UpdatePriceFromFeed" />
       </type>
   </config>
   ```

1. 사용자 지정 수식으로 메서드를 만듭니다.

   ```php
   class UpdatePriceFromFeed
   {
       /**
       * @param ProductPrice $subject
       * @param array $result
       * @param array $values
       *
       * @return array
       */
       public function afterGet(ProductPrice $subject, array $result, array $values) : array
       {
           // Override the output $result with your data for the corresponding products (see original method for details) 
           return $result;
       }
   }
   ```

