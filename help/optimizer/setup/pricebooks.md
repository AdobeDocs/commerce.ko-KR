---
title: 가격 장부
description: ' [!DNL Adobe Commerce Optimizer]에서 가격 장부를 관리하는 방법을 알아보세요.'
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="SaaS만" type="Positive" url="https://experienceleague.adobe.com/ko/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."
exl-id: a1849830-3d0e-4df9-ab73-380659c3f9dc
source-git-commit: 513ed97442bfffe74d64f4eb0484cfa8f25b5ecc
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# 가격 장부

가격 장부를 사용하면 다양한 고객 계층 및 시장에서 카탈로그 소스의 제품 가격을 정의할 수 있습니다. 가격 장부는 계층 모델을 지원하므로 각 기본 가격 장부 아래에 최대 3단계의 중첩된 하위 가격 장부를 사용할 수 있습니다. 각 가격 장부는 상위 가격 장부를 참조할 수 있으며 가격 카탈로그 출처에 대한 트리 구조를 형성합니다.

기본 가격 장부는 자체 통화 및 모든 하위 가격 장부를 정의합니다. 하위 가격 장부는 이 통화를 상속하며 재정의할 수 없습니다.

Price Book API를 사용하여 [ 가격 장부를 만들고, 업데이트하고, 삭제하는 방법은 ](https://developer.adobe.com/commerce/services/reference/rest/)개발자 설명서[!DNL Adobe Commerce Optimizer]를 참조하세요.

## 주요 개념

| 용어 | 설명 |
|------|-------------|
| **가격표** | 카탈로그 소스의 가격(예: 특정 지역 또는 고객 계층)을 정의하고 제품 가격을 관리하는 데 사용되는 논리적 그룹입니다. |
| **가격표 대체** | 계층 구조에서 가장 가격이 높은 책입니다. 여기에는 상위 항목이 없으며 자신과 모든 하위 항목의 가격 장부를 정의하는 *only* 가격 장부입니다.<br/><br/>가격 장부를 만드는 동안 부모가 정의되지 않은 경우(API를 통해) 새 대체 가격 장부가 만들어집니다. |
| **상위 가격표** | 하위 가격에 명시적으로 설정되지 않은 경우 하위 가격 장부가 가격을 상속할 수 있는 상위 수준의 가격 장부입니다. |
| **계층 구조 깊이** | 최대 3개 수준(대체 -> 하위 -> 손자)<br/><br/>수집 시 적용되지 않습니다. |
| **통화** | 대체 가격 장부에만 정의됩니다. 모든 하위 가격표에 상속됨.<br/><br/>대체 가격 장부를 만드는 동안 통화가 지정되지 않은 경우(API를 통해) 통화 기본값은 USD입니다. |
| **제품 가격** | 특정 가격표 내의 제품(SKU)에 지정된 특정 가격. |
| **할인** | 할인은 제품 가격으로 정의됩니다. 상속되지 않음. |
