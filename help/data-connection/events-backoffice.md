---
title: 백오피스 이벤트
description: 각 백오피스 이벤트가 캡처하는 데이터를 알아봅니다.
role: Admin, Developer
feature: Personalization, Integration, Eventing
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '3606'
ht-degree: 0%

---

# 백 오피스 이벤트 [!DNL Data Connection]개

다음은 [!DNL Data Connection] 확장을 설치할 때 사용할 수 있는 Commerce 백 오피스 이벤트 목록입니다. 이러한 이벤트가 수집하는 데이터는 Adobe Experience Platform으로 전송됩니다. 또한 [사용자 지정 이벤트](custom-events.md)를 만들어 기본 제공되지 않은 추가 데이터를 수집할 수 있습니다.

다음 이벤트에서 수집하는 데이터 외에 Adobe Experience Platform Web SDK에서 제공하는 [기타 데이터](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/automatic-information.html?lang=ko)도 가져옵니다.

백 오피스 이벤트에는 서버측 데이터가 포함되어 있습니다. 이 데이터에는 주문이 주문, 취소, 환불, 배송 또는 완료된 여부와 같은 [주문 상태](#order-status) 정보가 포함되어 있습니다. 서버측 데이터에는 계정이 생성, 업데이트 또는 삭제된 경우와 같은 [고객 프로필 이벤트](#customer-profile-events) 정보도 포함됩니다.

>[!NOTE]
>
>모든 백오피스 이벤트에는 가능한 경우 구매자의 이메일 주소 및 ECID를 포함하는 [`identityMap`](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/identitymap.html?lang=ko) 필드가 포함됩니다.

## 주문 상태

주문 상태 데이터는 구매자 주문의 360 보기를 보여줍니다. 이 보기는 마케팅 캠페인을 개발할 때 판매자가 전체 주문 상태를 더 잘 타겟팅하거나 분석하는 데 도움이 됩니다. 예를 들어 연중 다양한 시기에 탁월한 성능을 발휘하는 특정 제품 범주의 트렌드를 확인할 수 있습니다. 예를 들어, 추운 달에 더 잘 팔리는 겨울 옷이나 몇 년 동안 쇼핑객들이 관심을 갖는 특정 제품 색깔. 또한 주문 상태 데이터를 사용하면 이전 주문을 기반으로 전환하는 쇼핑객의 성향을 파악하여 라이프타임 고객 가치를 계산하는 데 도움이 될 수 있습니다.

### 주문

| 설명 | XDM 이벤트 이름 |
|---|---|
| 쇼핑객이 주문을 할 때 트리거됩니다. | `commerce.backofficeOrderPlaced` |

#### orderPlaced에서 수집된 데이터

다음 표에서는 이 이벤트에 대해 수집된 데이터에 대해 설명합니다.

| 필드 | 설명 |
|---|---|
| `commerce.order` | 주문에 대한 정보가 포함되어 있습니다. |
| `commerce.order.purchaseID` | 판매자가 해당 구매 또는 계약에 할당한 고유 식별자. ID가 고유하다고 보장할 수는 없습니다. |
| `commerce.order.payments` | 해당 주문에 대한 결제 목록. |
| `commerce.order.payments.paymentTransactionID` | 해당 결제 거래에 대한 고유 식별자. |
| `commerce.order.payments.paymentAmount` | 결제 값. |
| `commerce.order.payments.paymentType` | 해당 주문에 대한 결제 방법. 계산, 사용자 지정 값이 허용됩니다. |
| `commerce.order.payments.currencyCode` | 사용된 [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) 통화 코드(예: `USD` 또는 `EUR`). |
| `commerce.order.taxAmount` | 최종 지급의 일부로 구매자가 지불한 세액. |
| `commerce.order.discountAmount` | 전체 주문에 적용되는 할인 금액을 나타냅니다. |
| `commerce.order.createdDate` | 상거래 시스템에서 새 주문이 생성된 시간 및 날짜. 예: `2022-10-15T20:20:39+00:00`. |
| `commerce.order.currencyCode` | 주문 합계에 사용되는 ISO 4217 통화 코드. |
| `commerce.shipping` | 하나 이상의 제품에 대한 배송 세부 정보. |
| `commerce.shipping.shippingMethod` | 일반배송, 퀵배송, 매장픽업 등 고객이 선택한 배송 방법 |
| `commerce.shipping.shippingAmount` | 고객이 배송비로 지불해야 했던 금액. |
| `commerce.shipping.currencyCode` | 총 배송에 사용되는 ISO 4217 통화 코드. |
| `commerce.commerceScope` | 이벤트가 발생한 위치(스토어 보기, 스토어, 웹 사이트 등)를 나타냅니다. |
| `commerce.commerceScope.environmentID` | 환경 ID. 하이픈으로 구분된 32자리 영숫자 ID. |
| `commerce.commerceScope.storeCode` | 고유한 스토어 코드. 웹사이트당 많은 매장이 있을 수 있습니다. |
| `commerce.commerceScope.storeViewCode` | 고유한 스토어 보기 코드입니다. 매장당 여러 개의 매장을 볼 수 있습니다. |
| `commerce.commerceScope.websiteCode` | 고유 웹 사이트 코드. 하나의 환경에 여러 개의 웹 사이트가 있을 수 있습니다. |
| `commerce.billing.address` | 청구 우편 주소. |
| `commerce.billing.address.street1` | 기본 도로 정보, 아파트 번호, 도로 번호 및 도로명 |
| `commerce.billing.address.street2` | 상세 정보 필드를 위한 추가 필드입니다. |
| `commerce.billing.address.city` | 도시 이름. |
| `commerce.billing.address.state` | 상태 이름. 자유 형식의 필드입니다. |
| `commerce.billing.address.postalCode` | 위치의 우편 번호입니다. 우편 번호는 모든 국가에서 사용할 수 없습니다. 일부 국가에서는 우편 번호의 일부만 포함됩니다. |
| `commerce.billing.address.country` | 정부가 관리하는 지역의 이름입니다. `xdm:countryCode`이(가) 아닌 모든 언어의 국가 이름을 사용할 수 있는 자유 형식의 필드입니다. |
| `personalEmail` | 개인 이메일 주소. |
| `personalEmail.address` | 기술 주소(예: RFC2822 및 후속 표준에 일반적으로 정의된 `name@domain.com`). |
| `productListItems` | 순서대로 제품 배열. |
| `productListItems.id` | 해당 제품 항목에 대한 라인 항목 식별자. |
| `productListItems.SKU` | 재고 관리 장치. 제품에 대한 고유 식별자. |
| `productListItems.name` | 제품의 표시 이름 또는 사람이 인식할 수 있는 이름. |
| `productListItems.priceTotal` | 제품 라인 항목에 대한 총 가격. |
| `productListItems.quantity` | 장바구니에 있는 제품 단위의 수입니다. |
| `productListItems.discountAmount` | 적용되는 할인 금액을 나타냅니다. |
| `productListItems.currencyCode` | 사용된 [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) 통화 코드(예: `USD` 또는 `EUR`). |
| `productListItems.selectedOptions` | 구성 가능한 제품에 사용되는 필드. |
| `productListItems.selectedOptions.attribute` | 구성 가능한 제품의 특성을 식별합니다(예: `size` 또는 `color`). |
| `productListItems.selectedOptions.value` | `small` 또는 `black`과(와) 같은 특성의 값을 식별합니다. |
| `productListItems.categories` | 제품 범주에 대한 정보를 포함합니다. |
| `productListItems.categories.id` | 카테고리에 대한 고유 식별자. |
| `productListItems.categories.name` | 범주의 이름입니다. |
| `productListItems.categories.path` | 카테고리에 대한 경로입니다. |
| `productListItems.productImageUrl` | 제품의 기본 이미지 URL. |

### 인보이스 발행 주문

| 설명 | XDM 이벤트 이름 |
|---|---|
| 상인이 지급을 요청하기 위해 송장을 제출할 때 트리거됩니다. | `commerce.backofficeOrderInvoiced` |

#### orderInvoiced에서 수집된 데이터

다음 표에서는 이 이벤트에 대해 수집된 데이터에 대해 설명합니다.

| 필드 | 설명 |
|---|---|
| `commerce.order` | 주문에 대한 정보가 포함되어 있습니다. |
| `commerce.order.purchaseID` | 판매자가 해당 구매 또는 계약에 할당한 고유 식별자. ID가 고유하다고 보장할 수는 없습니다. |
| `commerce.order.priceTotal` | 할인 및 세금이 모두 적용된 후 이 주문의 총 가격. |
| `commerce.order.currencyCode` | 주문 합계에 사용되는 ISO 4217 통화 코드. |
| `commerce.order.purchaseOrderNumber` | 구매자가 해당 구매 또는 계약에 할당한 고유 식별자. |
| `commerce.order.payments` | 해당 주문에 대한 결제 목록. |
| `commerce.order.payments.currencyCode` | 사용된 [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) 통화 코드(예: `USD` 또는 `EUR`). |
| `commerce.order.payments.paymentType` | 해당 주문에 대한 결제 방법. 계산, 사용자 지정 값이 허용됩니다. |
| `commerce.order.payments.paymentAmount` | 결제 값. |
| `commerce.shipping` | 하나 이상의 제품에 대한 배송 세부 정보. |
| `commerce.shipping.shippingMethod` | 일반배송, 퀵배송, 매장픽업 등 고객이 선택한 배송 방법 |
| `commerce.shipping.shippingAmount` | 고객이 배송비로 지불해야 했던 금액. |
| `commerce.commerceScope` | 이벤트가 발생한 위치(스토어 보기, 스토어, 웹 사이트 등)를 나타냅니다. |
| `commerce.commerceScope.environmentID` | 환경 ID. 하이픈으로 구분된 32자리 영숫자 ID. |
| `commerce.commerceScope.storeCode` | 고유한 스토어 코드. 웹사이트당 많은 매장이 있을 수 있습니다. |
| `commerce.commerceScope.storeViewCode` | 고유한 스토어 보기 코드입니다. 매장당 여러 개의 매장을 볼 수 있습니다. |
| `commerce.commerceScope.websiteCode` | 고유 웹 사이트 코드. 하나의 환경에 여러 개의 웹 사이트가 있을 수 있습니다. |
| `personalEmail` | 개인 이메일 주소. |
| `personalEmail.address` | 기술 주소(예: RFC2822 및 후속 표준에 일반적으로 정의된 `name@domain.com`). |
| `productListItems` | 순서대로 제품 배열. |
| `productListItems.id` | 해당 제품 항목에 대한 라인 항목 식별자. |
| `productListItems.SKU` | 재고 관리 장치. 제품에 대한 고유 식별자. |
| `productListItems.name` | 제품의 표시 이름 또는 사람이 인식할 수 있는 이름. |
| `productListItems.priceTotal` | 제품 라인 항목에 대한 총 가격. |
| `productListItems.quantity` | 장바구니에 있는 제품 단위의 수입니다. |
| `productListItems.discountAmount` | 적용되는 할인 금액을 나타냅니다. |
| `productListItems.categories` | 제품 범주에 대한 정보를 포함합니다. |
| `productListItems.categories.id` | 카테고리에 대한 고유 식별자. |
| `productListItems.categories.name` | 범주의 이름입니다. |
| `productListItems.categories.path` | 카테고리에 대한 경로입니다. |

### orderItemsShipped

| 설명 | XDM 이벤트 이름 |
|---|---|
| 주문이 배송될 때 트리거됩니다. | `commerce.backofficeOrderItemsShipped` |

#### orderItemsShipped에서 수집한 데이터

다음 표에서는 이 이벤트에 대해 수집된 데이터에 대해 설명합니다.

| 필드 | 설명 |
|---|---|
| `commerce.order` | 주문에 대한 정보가 포함되어 있습니다. |
| `commerce.order.purchaseID` | 판매자가 해당 구매 또는 계약에 할당한 고유 식별자. ID가 고유하다고 보장할 수는 없습니다. |
| `commerce.order.payments` | 해당 주문에 대한 결제 목록. |
| `commerce.order.payments.paymentTransactionID` | 해당 결제 거래에 대한 고유 식별자. |
| `commerce.order.payments.paymentAmount` | 결제 값. |
| `commerce.order.payments.paymentType` | 해당 주문에 대한 결제 방법. 계산, 사용자 지정 값이 허용됩니다. |
| `commerce.order.payments.currencyCode` | 사용된 [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) 통화 코드(예: `USD` 또는 `EUR`). |
| `commerce.order.priceTotal` | 할인 및 세금이 모두 적용된 후 이 주문의 총 가격. |
| `commerce.order.purchaseOrderNumber` | 구매자가 해당 구매 또는 계약에 할당한 고유 식별자. |
| `commerce.order.currencyCode` | 사용된 [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) 통화 코드(예: `USD` 또는 `EUR`). |
| `commerce.order.lastUpdatedDate` | 상거래 시스템에서 특정 주문 레코드가 마지막으로 업데이트되는 시간. |
| `commerce.shipping` | 하나 이상의 제품에 대한 배송 세부 정보. |
| `commerce.shipping.shippingMethod` | 일반배송, 퀵배송, 매장픽업 등 고객이 선택한 배송 방법 |
| `commerce.shipping.shippingAmount` | 고객이 배송비로 지불해야 했던 금액. |
| `commerce.shipping.address` | 실제 배송 주소. |
| `commerce.shipping.address.street1` | 기본 도로 정보, 아파트 번호, 도로 번호 및 도로명. |
| `commerce.shipping.address.street2` | 2차선 도로 정보(선택 사항). |
| `commerce.shipping.address.city` | 도시 이름. |
| `commerce.shipping.address.state` | 주 이름입니다. 자유 형식의 필드입니다. |
| `commerce.shipping.address.postalCode` | 위치의 우편 번호입니다. 우편 번호는 모든 국가에서 사용할 수 없습니다. 일부 국가에서는 우편 번호의 일부만 포함됩니다. |
| `commerce.shipping.address.country` | 정부가 관리하는 지역의 이름입니다. `xdm:countryCode`이(가) 아닌 모든 언어의 국가 이름을 사용할 수 있는 자유 형식의 필드입니다. |
| `commerce.shipping.currencyCode` | 사용된 [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) 통화 코드(예: `USD` 또는 `EUR`). |
| `commerce.shipping.trackingNumber` | 주문 품목 선적에 대해 운송 회사가 제공하는 추적 번호. |
| `commerce.shipping.trackingURL` | 주문 항목의 배송 상태를 추적할 URL입니다. |
| `commerce.shipping.shipDate` | 주문에서 하나 이상의 품목이 배송된 날짜. |
| `commerce.commerceScope` | 이벤트가 발생한 위치(스토어 보기, 스토어, 웹 사이트 등)를 나타냅니다. |
| `commerce.commerceScope.environmentID` | 환경 ID. 하이픈으로 구분된 32자리 영숫자 ID. |
| `commerce.commerceScope.storeCode` | 고유한 스토어 코드. 웹사이트당 많은 매장이 있을 수 있습니다. |
| `commerce.commerceScope.storeViewCode` | 고유한 스토어 보기 코드입니다. 매장당 여러 개의 매장을 볼 수 있습니다. |
| `commerce.commerceScope.websiteCode` | 고유 웹 사이트 코드. 하나의 환경에 여러 개의 웹 사이트가 있을 수 있습니다. |
| `commerce.billing.address` | 청구 우편 주소. |
| `commerce.billing.address.street1` | 기본 도로 정보, 아파트 번호, 도로 번호 및 도로명 |
| `commerce.billing.address.street2` | 상세 정보 필드를 위한 추가 필드입니다. |
| `commerce.billing.address.city` | 도시 이름. |
| `commerce.billing.address.state` | 상태 이름. 자유 형식의 필드입니다. |
| `commerce.billing.address.postalCode` | 위치의 우편 번호입니다. 우편 번호는 모든 국가에서 사용할 수 없습니다. 일부 국가에서는 우편 번호의 일부만 포함됩니다. |
| `commerce.billing.address.country` | 정부가 관리하는 지역의 이름입니다. `xdm:countryCode`이(가) 아닌 모든 언어의 국가 이름을 사용할 수 있는 자유 형식의 필드입니다. |
| `personalEmail` | 개인 이메일 주소. |
| `personalEmail.address` | 기술 주소(예: RFC2822 및 후속 표준에 일반적으로 정의된 `name@domain.com`). |
| `productListItems` | 순서대로 제품 배열. |
| `productListItems.SKU` | 재고 관리 장치. 제품에 대한 고유 식별자. |
| `productListItems.name` | 제품의 표시 이름 또는 사람이 인식할 수 있는 이름. |
| `productListItems.priceTotal` | 제품 라인 항목에 대한 총 가격. |
| `productListItems.quantity` | 장바구니에 있는 제품 단위의 수입니다. |
| `productListItems.discountAmount` | 적용되는 할인 금액을 나타냅니다. |
| `productListItems.currencyCode` | 사용된 [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) 통화 코드(예: `USD` 또는 `EUR`). |
| `productListItems.selectedOptions` | 구성 가능한 제품에 사용되는 필드. |
| `productListItems.selectedOptions.attribute` | 구성 가능한 제품의 특성을 식별합니다(예: `size` 또는 `color`). |
| `productListItems.selectedOptions.value` | `small` 또는 `black`과(와) 같은 특성의 값을 식별합니다. |
| `productListItems.categories` | 제품 범주에 대한 정보를 포함합니다. |
| `productListItems.categories.id` | 카테고리에 대한 고유 식별자. |
| `productListItems.categories.name` | 범주의 이름입니다. |
| `productListItems.categories.path` | 카테고리에 대한 경로입니다. |

### orderCanceled

| 설명 | XDM 이벤트 이름 |
|---|---|
| 쇼핑객이 주문을 취소할 때 트리거됩니다. | `commerce.backofficeOrderCancelled` |

#### orderCanceled에서 수집된 데이터

다음 표에서는 이 이벤트에 대해 수집된 데이터에 대해 설명합니다.

| 필드 | 설명 |
|---|---|
| `commerce.order` | 주문에 대한 정보가 포함되어 있습니다. |
| `commerce.order.purchaseID` | 판매자가 해당 구매 또는 계약에 할당한 고유 식별자. ID가 고유하다고 보장할 수는 없습니다. |
| `commerce.order.purchaseOrderNumber` | 구매자가 해당 구매 또는 계약에 할당한 고유 식별자. |
| `commerce.order.cancelDate` | 쇼핑객이 주문을 취소하는 날짜 및 시간입니다. |
| `commerce.order.lastUpdatedDate` | 상거래 시스템에서 특정 주문 레코드가 마지막으로 업데이트되는 시간. |
| `commerce.commerceScope` | 이벤트가 발생한 위치(스토어 보기, 스토어, 웹 사이트 등)를 나타냅니다. |
| `commerce.commerceScope.environmentID` | 환경 ID. 하이픈으로 구분된 32자리 영숫자 ID. |
| `commerce.commerceScope.storeCode` | 고유한 스토어 코드. 웹사이트당 많은 매장이 있을 수 있습니다. |
| `commerce.commerceScope.storeViewCode` | 고유한 스토어 보기 코드입니다. 매장당 여러 개의 매장을 볼 수 있습니다. |
| `commerce.commerceScope.websiteCode` | 고유 웹 사이트 코드. 하나의 환경에 여러 개의 웹 사이트가 있을 수 있습니다. |
| `personalEmail` | 개인 이메일 주소. |
| `personalEmail.address` | 기술 주소(예: RFC2822 및 후속 표준에 일반적으로 정의된 `name@domain.com`). |

### orderLineItemReturned

| 설명 | XDM 이벤트 이름 |
|---|---|
| 구매자가 반품된 항목을 환불받을 때 트리거됩니다. | `commerce.backofficeCreditMemoIssued` |

#### orderLineItemRefferenced에서 수집한 데이터

다음 표에서는 이 이벤트에 대해 수집된 데이터에 대해 설명합니다.

| 필드 | 설명 |
|---|---|
| `commerce.order` | 주문에 대한 정보가 포함되어 있습니다. |
| `commerce.order.purchaseID` | 판매자가 해당 구매 또는 계약에 할당한 고유 식별자. ID가 고유하다고 보장할 수는 없습니다. |
| `commerce.order.lastUpdatedDate` | 상거래 시스템에서 특정 주문 레코드가 마지막으로 업데이트되는 시간. |
| `commerce.order.purchaseOrderNumber` | 구매자가 해당 구매 또는 계약에 할당한 고유 식별자. |
| `commerce.refunds` | 해당 주문에 대한 환불 목록. |
| `commerce.refunds.transactionID` | 해당 환불에 대한 고유 식별자. |
| `commerce.refunds.refundAmount` | 환불 금액. |
| `commerce.refunds.refundPaymentType` | 해당 주문에 대한 결제 방법. 계산, 사용자 지정 값이 허용됩니다. |
| `commerce.refunds.currencyCode` | 사용된 [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) 통화 코드(예: `USD` 또는 `EUR`). |
| `personalEmail` | 개인 이메일 주소. |
| `personalEmail.address` | 기술 주소(예: RFC2822 및 후속 표준에 일반적으로 정의된 `name@domain.com`). |
| `productListItems` | 순서대로 제품 배열. |
| `productListItems.SKU` | 재고 관리 장치. 제품에 대한 고유 식별자. |
| `productListItems.name` | 제품의 표시 이름 또는 사람이 인식할 수 있는 이름. |
| `productListItems.priceTotal` | 제품 라인 항목에 대한 총 가격. |
| `productListItems.quantity` | 장바구니에 있는 제품 단위의 수입니다. |
| `productListItems.discountAmount` | 적용되는 할인 금액을 나타냅니다. |
| `productListItems.currencyCode` | 사용된 [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) 통화 코드(예: `USD` 또는 `EUR`). |
| `productListItems.selectedOptions` | 구성 가능한 제품에 사용되는 필드. |
| `productListItems.selectedOptions.attribute` | 구성 가능한 제품의 특성을 식별합니다(예: `size` 또는 `color`). |
| `productListItems.selectedOptions.value` | `small` 또는 `black`과(와) 같은 특성의 값을 식별합니다. |
| `productListItems.categories` | 제품 범주에 대한 정보를 포함합니다. |
| `productListItems.categories.id` | 카테고리에 대한 고유 식별자. |
| `productListItems.categories.name` | 범주의 이름입니다. |
| `productListItems.categories.path` | 카테고리에 대한 경로입니다. |

### orderItemsReturnInitiated

| 설명 | XDM 이벤트 이름 |
|---|---|
| 구매자가 항목 반환을 요청할 때 트리거됩니다. | `commerce.backofficeOrderItemsReturnInitiated` |

#### orderItemsReturnInitiated에서 수집된 데이터

다음 표에서는 이 이벤트에 대해 수집된 데이터에 대해 설명합니다.

| 필드 | 설명 |
|---|---|
| `commerce.order` | 주문에 대한 정보가 포함되어 있습니다. |
| `commerce.order.purchaseID` | 판매자가 해당 구매 또는 계약에 할당한 고유 식별자. ID가 고유하다고 보장할 수는 없습니다. |
| `commerce.order.returns` | 이 주문에 대한 RMA(반품 상품 승인) 정보. |
| `commerce.order.returns.returnID` | 해당 RMA(Return Merchandises Authorization)의 고유 식별자. |
| `commerce.order.returns.returnStatus` | 보류 중, 마감됨 등과 같은 RMA(Return Merchandise Authorization)의 상태. |
| `commerce.commerceScope` | 이벤트가 발생한 위치(스토어 보기, 스토어, 웹 사이트 등)를 나타냅니다. |
| `commerce.commerceScope.environmentID` | 환경 ID. 하이픈으로 구분된 32자리 영숫자 ID. |
| `commerce.commerceScope.storeCode` | 고유한 스토어 코드. 웹사이트당 많은 매장이 있을 수 있습니다. |
| `commerce.commerceScope.storeViewCode` | 고유한 스토어 보기 코드입니다. 매장당 여러 개의 매장을 볼 수 있습니다. |
| `commerce.commerceScope.websiteCode` | 고유 웹 사이트 코드. 하나의 환경에 여러 개의 웹 사이트가 있을 수 있습니다. |
| `personalEmail` | 개인 이메일 주소. |
| `personalEmail.address` | 기술 주소(예: RFC2822 및 후속 표준에 일반적으로 정의된 `name@domain.com`). |
| `productListItems` | 순서대로 제품 배열. |
| `productListItems.SKU` | 재고 관리 장치. 제품에 대한 고유 식별자. |
| `productListItems.name` | 제품의 표시 이름 또는 사람이 인식할 수 있는 이름. |
| `productListItems.quantity` | 장바구니에 있는 제품 단위의 수입니다. |
| `productListItems.selectedOptions` | 구성 가능한 제품에 사용되는 필드. |
| `productListItems.selectedOptions.attribute` | 구성 가능한 제품의 특성을 식별합니다(예: `size` 또는 `color`). |
| `productListItems.selectedOptions.value` | `small` 또는 `black`과(와) 같은 특성의 값을 식별합니다. |
| `productListItems.categories` | 제품 범주에 대한 정보를 포함합니다. |
| `productListItems.categories.id` | 카테고리에 대한 고유 식별자. |
| `productListItems.categories.name` | 범주의 이름입니다. |
| `productListItems.categories.path` | 카테고리에 대한 경로입니다. |
| `productListItems.returnItem` | 이 품목에 대한 RMA(반품 상품 승인) 정보. |
| `productListItems.returnItem.returnStatus` | 보류 중, 승인됨 등 반환된 항목의 상태입니다. |
| `productListItems.returnItem.returnReason` | 이 항목에 대한 반환이 요청되는 이유입니다. |
| `productListItems.returnItem.returnItemCondition` | 반환이 요청되는 항목의 상태입니다. |
| `productListItems.returnItem.returnResolution` | 환불, 교환 등과 같이 반환되는 항목의 요청된 해결 방법. |
| `productListItems.returnItem.returnQuantityRequested` | 구매자가 반품을 요청한 이 항목의 번호입니다. |
| `productListItems.returnItem.returnQuantityAuthorized` | 반환할 수 있는 이 항목의 번호입니다. |
| `productListItems.returnItem.eturnQuantityReceived` | 받은 반환된 항목 수입니다. |
| `productListItems.returnItem.returnQuantityApproved` | 반품이 완전히 완료되고 승인된 이 항목의 수입니다. |

### orderItemReturnCompleted

| 설명 | XDM 이벤트 이름 |
|---|---|
| 구매자가 반환을 요청한 항목이 완료되면 트리거됩니다. | `commerce.backofficeOrderItemsReturnCompleted` |

#### orderItemReturnCompleted에서 수집된 데이터

다음 표에서는 이 이벤트에 대해 수집된 데이터에 대해 설명합니다.

| 필드 | 설명 |
|---|---|
| `commerce.order` | 주문에 대한 정보가 포함되어 있습니다. |
| `commerce.order.purchaseID` | 판매자가 해당 구매 또는 계약에 할당한 고유 식별자. ID가 고유하다고 보장할 수는 없습니다. |
| `commerce.order.returns` | 이 주문에 대한 RMA(반품 상품 승인) 정보. |
| `commerce.order.returns.returnID` | 해당 RMA(Return Merchandises Authorization)의 고유 식별자. |
| `commerce.order.returns.returnStatus` | 보류 중, 마감됨 등과 같은 RMA(Return Merchandise Authorization)의 상태. |
| `commerce.commerceScope` | 이벤트가 발생한 위치(스토어 보기, 스토어, 웹 사이트 등)를 나타냅니다. |
| `commerce.commerceScope.environmentID` | 환경 ID. 하이픈으로 구분된 32자리 영숫자 ID. |
| `commerce.commerceScope.storeCode` | 고유한 스토어 코드. 웹사이트당 많은 매장이 있을 수 있습니다. |
| `commerce.commerceScope.storeViewCode` | 고유한 스토어 보기 코드입니다. 매장당 여러 개의 매장을 볼 수 있습니다. |
| `commerce.commerceScope.websiteCode` | 고유 웹 사이트 코드. 하나의 환경에 여러 개의 웹 사이트가 있을 수 있습니다. |
| `personalEmail` | 개인 이메일 주소. |
| `personalEmail.address` | 기술 주소(예: RFC2822 및 후속 표준에 일반적으로 정의된 `name@domain.com`). |
| `productListItems` | 순서대로 제품 배열. |
| `productListItems.SKU` | 재고 관리 장치. 제품에 대한 고유 식별자. |
| `productListItems.name` | 제품의 표시 이름 또는 사람이 인식할 수 있는 이름. |
| `productListItems.selectedOptions` | 구성 가능한 제품에 사용되는 필드. |
| `productListItems.selectedOptions.attribute` | 구성 가능한 제품의 특성을 식별합니다(예: `size` 또는 `color`). |
| `productListItems.selectedOptions.value` | `small` 또는 `black`과(와) 같은 특성의 값을 식별합니다. |
| `productListItems.categories` | 제품 범주에 대한 정보를 포함합니다. |
| `productListItems.categories.id` | 카테고리에 대한 고유 식별자. |
| `productListItems.categories.name` | 범주의 이름입니다. |
| `productListItems.categories.path` | 카테고리에 대한 경로입니다. |
| `productListItems.returnItem` | 이 품목에 대한 RMA(반품 상품 승인) 정보. |
| `productListItems.returnItem.returnStatus` | 보류 중, 승인됨 등 반환된 항목의 상태입니다. |
| `productListItems.returnItem.returnReason` | 이 항목에 대한 반환이 요청되는 이유입니다. |
| `productListItems.returnItem.returnItemCondition` | 반환이 요청되는 항목의 상태입니다. |
| `productListItems.returnItem.returnResolution` | 환불, 교환 등과 같이 반환되는 항목의 요청된 해결 방법. |
| `productListItems.returnItem.returnQuantityRequested` | 구매자가 반품을 요청한 이 항목의 번호입니다. |
| `productListItems.returnItem.returnQuantityAuthorized` | 반환할 수 있는 이 항목의 번호입니다. |
| `productListItems.returnItem.eturnQuantityReceived` | 받은 반환된 항목 수입니다. |
| `productListItems.returnItem.returnQuantityApproved` | 반품이 완전히 완료되고 승인된 이 항목의 수입니다. |

### orderShipmentCompleted

| 설명 | XDM 이벤트 이름 |
|---|---|
| 선적이 완료되면 트리거됩니다. | `commerce.backofficeOrderShipmentCompleted` |

#### orderShipmentCompleted에서 수집한 데이터

다음 표에서는 이 이벤트에 대해 수집된 데이터에 대해 설명합니다.

| 필드 | 설명 |
|---|---|
| `commerce.order` | 주문에 대한 정보가 포함되어 있습니다. |
| `commerce.order.purchaseID` | 판매자가 해당 구매 또는 계약에 할당한 고유 식별자. ID가 고유하다고 보장할 수는 없습니다. |
| `commerce.order.payments` | 해당 주문에 대한 결제 목록. |
| `commerce.order.payments.paymentTransactionID` | 해당 결제 거래에 대한 고유 식별자. |
| `commerce.order.payments.paymentAmount` | 결제 값. |
| `commerce.order.payments.paymentType` | 해당 주문에 대한 결제 방법. 계산, 사용자 지정 값이 허용됩니다. |
| `commerce.order.payments.currencyCode` | 사용된 [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) 통화 코드(예: `USD` 또는 `EUR`). |
| `commerce.order.taxAmount` | 최종 지급의 일부로 구매자가 지불한 세액. |
| `commerce.order.createdDate` | 상거래 시스템에서 새 주문이 생성된 시간 및 날짜. 예: `2022-10-15T20:20:39+00:00`. |
| `commerce.shipping` | 하나 이상의 제품에 대한 배송 세부 정보. |
| `commerce.shipping.shippingMethod` | 일반배송, 퀵배송, 매장픽업 등 고객이 선택한 배송 방법 |
| `commerce.shipping.shippingAmount` | 고객이 배송비로 지불해야 했던 금액. |
| `commerce.shipping.shipDate` | 주문에서 하나 이상의 품목이 배송된 날짜. |
| `commerce.shipping.address` | 실제 배송 주소. |
| `commerce.shipping.address.street1` | 기본 도로 정보, 아파트 번호, 도로 번호 및 도로명. |
| `commerce.shipping.address.street2` | 2차선 도로 정보(선택 사항). |
| `commerce.shipping.address.city` | 도시 이름. |
| `commerce.shipping.address.state` | 주 이름입니다. 자유 형식의 필드입니다. |
| `commerce.shipping.address.postalCode` | 위치의 우편 번호입니다. 우편 번호는 모든 국가에서 사용할 수 없습니다. 일부 국가에서는 우편 번호의 일부만 포함됩니다. |
| `commerce.shipping.address.country` | 정부가 관리하는 지역의 이름입니다. `xdm:countryCode`이(가) 아닌 모든 언어의 국가 이름을 사용할 수 있는 자유 형식의 필드입니다. |
| `commerce.billing.address` | 청구 우편 주소. |
| `commerce.billing.address.street1` | 기본 도로 정보, 아파트 번호, 도로 번호 및 도로명 |
| `commerce.billing.address.street2` | 상세 정보 필드를 위한 추가 필드입니다. |
| `commerce.billing.address.city` | 도시 이름. |
| `commerce.billing.address.state` | 상태 이름. 자유 형식의 필드입니다. |
| `commerce.billing.address.postalCode` | 위치의 우편 번호입니다. 우편 번호는 모든 국가에서 사용할 수 없습니다. 일부 국가에서는 우편 번호의 일부만 포함됩니다. |
| `commerce.billing.address.country` | 정부가 관리하는 지역의 이름입니다. `xdm:countryCode`이(가) 아닌 모든 언어의 국가 이름을 사용할 수 있는 자유 형식의 필드입니다. |
| `personalEmail` | 개인 이메일 주소. |
| `personalEmail.address` | 기술 주소(예: RFC2822 및 후속 표준에 일반적으로 정의된 `name@domain.com`). |
| `productListItems` | 순서대로 제품 배열. |
| `productListItems.SKU` | 재고 관리 장치. 제품에 대한 고유 식별자. |
| `productListItems.name` | 제품의 표시 이름 또는 사람이 인식할 수 있는 이름. |
| `productListItems.priceTotal` | 제품 라인 항목에 대한 총 가격. |
| `productListItems.quantity` | 장바구니에 있는 제품 단위의 수입니다. |
| `productListItems.discountAmount` | 적용되는 할인 금액을 나타냅니다. |
| `productListItems.currencyCode` | 사용된 [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) 통화 코드(예: `USD` 또는 `EUR`). |
| `productListItems.selectedOptions` | 구성 가능한 제품에 사용되는 필드. |
| `productListItems.selectedOptions.attribute` | 구성 가능한 제품의 특성을 식별합니다(예: `size` 또는 `color`). |
| `productListItems.selectedOptions.value` | `small` 또는 `black`과(와) 같은 특성의 값을 식별합니다. |
| `productListItems.categories` | 제품 범주에 대한 정보를 포함합니다. |
| `productListItems.categories.id` | 카테고리에 대한 고유 식별자. |
| `productListItems.categories.name` | 범주의 이름입니다. |
| `productListItems.categories.path` | 카테고리에 대한 경로입니다. |

## 고객 프로필 이벤트

서버측에서 캡처된 프로필 이벤트에는 `accountCreated`, `accountUpdated`, `accountDeleted` 등의 계정 정보가 포함됩니다. 이 데이터는 등록 할인 오퍼, 계정 변경 확인 전송 등과 같이, 세그먼트를 더 잘 정의하거나 마케팅 캠페인을 실행하는 데 필요한 주요 고객 세부 정보를 채우는 데 사용됩니다. [storefront](events.md#customer-profile-events)에서 캡처된 유사한 프로필 이벤트가 있습니다.

>[!NOTE]
>
>각 고객 프로필 이벤트에는 프로필의 기본 식별자로 시스템에서 생성한 Commerce 고객 ID와 보조 식별자로 사용되는 이메일 ID가 포함된 [`identityMap`](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/identitymap.html?lang=ko) 필드도 포함됩니다.

### accountCreated

| 설명 | XDM 이벤트 이름 |
|---|---|
| 쇼핑객이 계정을 만들려고 할 때 트리거됩니다. | `userAccount.backofficeCreateProfile` |

#### accountCreated에서 수집된 데이터

다음 표에서는 이 이벤트에 대해 수집된 데이터에 대해 설명합니다.

| 필드 | 설명 |
|---|---|
| `person` | 고객에 대한 정보를 포함합니다. |
| `person.name` | 고객 이름에 대한 정보를 포함합니다. |
| `person.name.firstName` | 고객의 이름을 포함합니다. |
| `person.name.lastName` | 고객의 성을 포함합니다. |
| `personalEmail` | 개인 이메일 주소. |
| `personalEmail.address` | 기술 주소(예: RFC2822 및 후속 표준에 일반적으로 정의된 `name@domain.com`). |
| `commerce.commerceScope` | 이벤트가 발생한 위치(스토어 보기, 스토어, 웹 사이트 등)를 나타냅니다. |
| `commerce.commerceScope.environmentID` | 환경 ID. 하이픈으로 구분된 32자리 영숫자 ID. |
| `commerce.commerceScope.storeCode` | 고유한 스토어 코드. 웹사이트당 많은 매장이 있을 수 있습니다. |
| `commerce.commerceScope.storeViewCode` | 고유한 스토어 보기 코드입니다. 매장당 여러 개의 매장을 볼 수 있습니다. |
| `commerce.commerceScope.websiteCode` | 고유 웹 사이트 코드. 하나의 환경에 여러 개의 웹 사이트가 있을 수 있습니다. |

### 계정 업데이트됨

| 설명 | XDM 이벤트 이름 |
|---|---|
| 쇼핑객이 계정을 편집하려고 할 때 트리거됩니다. | `userAccount.backofficeUpdateProfile` |

#### accountUpdated에서 수집된 데이터

다음 표에서는 이 이벤트에 대해 수집된 데이터에 대해 설명합니다.

| 필드 | 설명 |
|---|---|
| `person` | 고객에 대한 정보를 포함합니다. |
| `person.name` | 고객 이름에 대한 정보를 포함합니다. |
| `person.name.firstName` | 고객의 이름을 포함합니다. |
| `person.name.lastName` | 고객의 성을 포함합니다. |
| `personalEmail` | 개인 이메일 주소. |
| `personalEmail.address` | 기술 주소(예: RFC2822 및 후속 표준에 일반적으로 정의된 `name@domain.com`). |
| `commerce.commerceScope` | 이벤트가 발생한 위치(스토어 보기, 스토어, 웹 사이트 등)를 나타냅니다. |
| `commerce.commerceScope.environmentID` | 환경 ID. 하이픈으로 구분된 32자리 영숫자 ID. |
| `commerce.commerceScope.storeCode` | 고유한 스토어 코드. 웹사이트당 많은 매장이 있을 수 있습니다. |
| `commerce.commerceScope.storeViewCode` | 고유한 스토어 보기 코드입니다. 매장당 여러 개의 매장을 볼 수 있습니다. |
| `commerce.commerceScope.websiteCode` | 고유 웹 사이트 코드. 하나의 환경에 여러 개의 웹 사이트가 있을 수 있습니다. |

### accountDeleted

| 설명 | XDM 이벤트 이름 |
|---|---|
| 쇼핑객이 계정을 삭제하려고 할 때 트리거됩니다. | `userAccount.backofficeDeleteProfile` |

#### accountDeleted에서 수집된 데이터

다음 표에서는 이 이벤트에 대해 수집된 데이터에 대해 설명합니다.

| 필드 | 설명 |
|---|---|
| `person` | 고객에 대한 정보를 포함합니다. |
| `person.name` | 고객 이름에 대한 정보를 포함합니다. |
| `person.name.firstName` | 고객의 이름을 포함합니다. |
| `person.name.lastName` | 고객의 성을 포함합니다. |
| `personalEmail` | 개인 이메일 주소. |
| `personalEmail.address` | 기술 주소(예: RFC2822 및 후속 표준에 일반적으로 정의된 `name@domain.com`). |
| `commerce.commerceScope` | 이벤트가 발생한 위치(스토어 보기, 스토어, 웹 사이트 등)를 나타냅니다. |
| `commerce.commerceScope.environmentID` | 환경 ID. 하이픈으로 구분된 32자리 영숫자 ID. |
| `commerce.commerceScope.storeCode` | 고유한 스토어 코드. 웹사이트당 많은 매장이 있을 수 있습니다. |
| `commerce.commerceScope.storeViewCode` | 고유한 스토어 보기 코드입니다. 매장당 여러 개의 매장을 볼 수 있습니다. |
| `commerce.commerceScope.websiteCode` | 고유 웹 사이트 코드. 하나의 환경에 여러 개의 웹 사이트가 있을 수 있습니다. |
