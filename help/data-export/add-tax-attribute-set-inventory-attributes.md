---
title: 세금 분류, 속성 세트 및 재고 속성 추가
description: 제품 피드 데이터를 확장하여 세금 분류, 속성 세트 및 고급 재고 설정에 대한 속성을 포함하는 방법에 대해 알아봅니다
role: Admin, Developer
badgePaas: label="PaaS만" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/
source-git-commit: 6abfeca68ab67fb11493f78440e09408479e1535
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 0%

---

# 세금 분류, 속성 세트 및 재고 속성 추가

Adobe Commerce 추가 제품 속성 모듈은 제품 데이터 피드를 확장합니다. 여기에는 Adobe Commerce 제품 구성의 추가 제품 속성이 포함됩니다.

* [세금 분류](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/taxes/tax-class)
* [특성 집합](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/create/attribute-sets)
* [인벤토리](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/configuration/product-options#advanced-product-options)

모듈이 설치되면 자동으로 작동합니다. 제품 동기화 중에 추가 속성을 캡처하고 내보냅니다. 추가 구성은 필요하지 않습니다.

## 주요 이점

* **자동 개선**: 세금 클래스, 특성 집합 및 재고 특성을 사용하여 제품 피드를 강화합니다.
* **원활한 통합**: 외부 시스템 및 서비스에 필요한 컨텍스트를 제공합니다.
* **Zero 구성**: 설치 후 즉시 작동합니다.
* **실시간 업데이트**: 제품 변경 사항과 자동으로 동기화됩니다.

## 기능 및 내보낸 특성

모듈은 기존 제품 데이터 피드에 다음 세 가지 속성을 추가합니다.

* `ac_tax_class`
* `ac_attribute_set`
* `ac_inventory`

### &#x200B;1. 세금 등급 정보(`ac_tax_class`)

**목적**: 각 제품에 대한 세금 분류 정보를 제공합니다.

**데이터 형식**: 세금 클래스 이름을 포함하는 문자열 값

**출력 예**:

```json
{
  "attributes": [
    {
      "code": "ac_tax_class",
      "values": ["Taxable Goods"]
    }
  ]
}
```

**사용 사례**:

세금 분류 데이터를 Commerce 카탈로그 서비스로 내보내면 이 데이터를 지원하는 애플리케이션에서 사용할 수 있습니다.

* 세금 준수 보고
* 외부 세금 계산 서비스와 통합
* 회계 시스템에 대한 제품 분류

### &#x200B;2. 특성 집합 정보(`ac_attribute_set`)

**목적**: 각 제품에 할당된 특성 집합을 식별합니다

**데이터 형식**: 특성 집합 이름을 포함하는 문자열 값입니다.

**출력 예**:

```json
{
  "attributes": [
    {
      "code": "ac_attribute_set",
      "values": [
        "Default"
      ]
    }
  ]
}
```

**사용 사례**:

속성 세트 데이터를 Commerce 카탈로그 서비스로 내보내면 외부 시스템에서 고급 제품 관리 기능이 활성화됩니다. 이러한 기능에는 다음이 포함됩니다.

* 제품 템플릿 식별
* 카탈로그 관리 및 구성
* 속성 세트 컨텍스트를 필요로 하는 서드파티 시스템 통합

### &#x200B;3. 고급 인벤토리 데이터(`ac_inventory`)

**목적**: 각 제품에 대한 재고 관리 설정을 제공합니다.

**데이터 형식**: 인벤토리 구성을 포함하는 JSON 인코딩 문자열

**포함된 필드**:

* `manageStock`(부울): 재고 관리가 활성화되어 있는지 여부
* `cartMinQty`(부동): 장바구니에 허용된 최소 수량입니다.
* `cartMaxQty`(부동): 장바구니에 허용되는 최대 수량
* `backorders`(문자열): 미납 주문 정책입니다. 값은 다음 중 하나입니다.
   * `"no"`: 미납 주문 허용 안 함
   * `"allow"`: 0 미만의 수량 허용
   * `"allow_notify"`: 0 미만의 수량을 허용하고 고객에게 알립니다.
* `enableQtyIncrements`(부울): 수량 증분이 사용되는지 여부
* `qtyIncrements`(부동 소수점): 필수 수량 증분 값

**출력 예**:

```json
{
  "attributes": [
    {
      "code": "ac_inventory",
      "values": [
        "{\"manageStock\":true,\"cartMinQty\":2,\"cartMaxQty\":42,\"backorders\":\"no\",\"enableQtyIncrements\":false,\"qtyIncrements\":2}"
      ]
    }
  ]
}
```

**사용 사례**:

인벤토리 데이터를 Commerce 카탈로그 서비스로 내보내면 외부 시스템에서 고급 인벤토리 관리 기능이 활성화됩니다. 이러한 기능에는 다음이 포함됩니다.

* Inventory management 시스템 통합
* 장바구니 유효성 검사 규칙
* 주문 이행 프로세스 최적화
* 고객 경험 사용자 정의

## 데이터 내보내기 피드 개선 사항

추가 제품 속성 모듈은 기존 제품 피드를 향상시킵니다. 새 속성 데이터를 자동으로 통합합니다.

* **제품 피드**(`products`): 세 가지 추가 특성을 사용하여 개선되었습니다

   * 각 제품 레코드에 `ac_tax_class`, `ac_attribute_set` 및 `ac_inventory` 특성을 추가합니다.
   * 원본 제품 데이터를 그대로 유지
   * 기존 피드 소비자와의 이전 버전과의 호환성 유지

* **제품 특성 피드**(`productAttributes`): 새 특성에 대한 특성 메타데이터로 개선됨

   * `productAttributes` 피드의 세 가지 새 특성에 대한 메타데이터를 자동으로 등록합니다.
   * 속성 구성 세부 사항(데이터 유형, 가시성 설정 등)을 제공합니다.
   * 외부 시스템이 새 특성 스키마를 이해할 수 있도록 지원

## 확장 설치

**요구 사항**

* PHP 8.1, 8.2, 8.3 또는 8.4
* Adobe Commerce 2.4.4+
* [Adobe Commerce 데이터 내보내기 확장](manage-extension.md#update-a-module-to-a-specific-version), 버전 103.4.11 이상
* [repo.magento.com에 액세스](https://repo.magento.com)

  키를 생성하고 필요한 권한을 얻으려면 [인증 키 가져오기](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/authentication-keys)를 참조하십시오. 클라우드 설치의 경우 [Commerce on Cloud Infrastructure Guide](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/authentication-keys)를 참조하십시오.
* Adobe Commerce 애플리케이션 서버의 명령줄에 액세스합니다.

### 설치 단계

작성기를 사용하여 `adobe-commerce/module-extra-product-attributes` 모듈 추가:

```shell
composer require adobe-commerce/module-extra-product-attributes
```

자세한 설치 단계는 다음 안내서를 참조하십시오.

* [클라우드 인프라에서 Adobe Commerce에 확장 설치](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/configure-store/extensions)
* [확장 Adobe Commerce 온-프레미스 설치](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/extension)

## 제품 데이터 동기화

재배포 후 Adobe Commerce 인스턴스는 제품 동기화 중에 추가 데이터를 자동으로 내보냅니다. `resync` CLI 명령을 사용하여 즉시 동기화할 수도 있습니다.

```shell
# Resync the products feed (includes the new attributes)
bin/magento saas:resync --feed=products
```

```shell
# Resync the product attributes feed (includes new attribute metadata)
bin/magento saas:resync --feed=productAttributes
```

## 문제 해결

**제품에 추가 특성이 없습니다.**

* 모듈이 제대로 설치되고 활성화되어 있는지 확인합니다.
* 재동기화 명령을 실행하여 제품 데이터를 새로 고칩니다.
* 제품에 유효한 세금 분류 및 속성 세트 지정이 있는지 확인합니다.

**인벤토리 데이터가 올바르지 않은 것으로 나타남:**

* 관리자에서 인벤토리 설정이 올바르게 구성되었는지 확인합니다.
* 웹 사이트별 인벤토리 무시 확인
* [Inventory management 모듈](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/guide-overview)이 올바르게 작동하는지 확인

자세한 내용은 [Inventory management 판매자 설명서](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/guide-overview)에서 *Adobe Commerce 안내서*&#x200B;를 참조하십시오.

**성능 문제:**

* 설치 후 내보내기 프로세스 성능 모니터링
* 트래픽이 적은 기간 동안 재동기화 일정 잡기 고려

### 로깅 및 디버깅

모듈은 표준 Commerce 로깅 시스템에 내보내기 오류 및 경고를 기록합니다. 제품 동기화 중에 문제가 발생하면 데이터 내보내기 로그를 확인하십시오.

자세한 내용은 [로그 검토 및 문제 해결](troubleshooting-logging.md)을 참조하세요.

