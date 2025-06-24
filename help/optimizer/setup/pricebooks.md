---
title: 가격 장부
description: ' [!DNL Adobe Commerce Optimizer]에서 가격 장부를 관리하는 방법을 알아보세요.'
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="SaaS만" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."
source-git-commit: 553490762ef10e43ccce1654acec59aeb83bb5f9
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---

# 가격 장부

이 문서에서는 적절한 데이터 거버넌스 컨트롤을 사용하여 가격 장부를 정의하고 카탈로그 보기에 할당하는 방법을 설명합니다.

Price Book API를 사용하여 타사 시스템에서 [!DNL Adobe Commerce Optimizer]&#x200B;(으)로 가격 장부 정보를 수집하는 방법에 대한 자세한 내용은 [개발자 설명서](https://developer-stage.adobe.com/commerce/services/composable-catalog/data-ingestion/api-reference/#tag/Price-Books)를 참조하십시오.

Price Book을 사용하면 가격 책정 카탈로그 소스를 정의하여 다양한 고객 계층과 시장에서 제품 가격을 관리할 수 있습니다. 가격 장부는 계층 모델을 지원하므로 각 기본 가격 장부 아래에 최대 3단계의 중첩된 하위 가격 장부를 사용할 수 있습니다. 각 가격 장부는 상위 가격 장부를 참조할 수 있으며 가격 카탈로그 출처에 대한 트리 구조를 형성합니다.

기본 가격 장부는 자체 통화 및 모든 하위 가격 장부를 정의합니다. 하위 가격 장부는 이 통화를 상속하며 재정의할 수 없습니다.

## 주요 개념

| 용어 | 설명 |
|------|-------------|
| **가격표** | 가격 카탈로그 소스(예: 특정 지역 또는 고객 계층)를 정의하고 제품 가격을 관리하는 데 사용되는 논리적 그룹화입니다. |
| **가격표 대체** | 계층 구조에서 가장 가격이 높은 책입니다. 여기에는 상위 항목이 없으며 자신과 모든 하위 항목의 가격 장부를 정의하는 *only* 가격 장부입니다.<br/><br/>가격 장부를 만드는 동안 부모가 정의되지 않은 경우(API를 통해) 새 대체 가격 장부가 만들어집니다. |
| **상위 가격표** | 하위 항목에서 명시적으로 설정되지 않은 경우 하위 항목별 가격표가 가격을 상속할 수 있는 상위 수준의 가격표. |
| **계층 구조 깊이** | 최대 3개 수준(하위 또→ 손자→ 대체)<br/><br/>수집 시 강제 적용되지 않음. |
| **통화** | 대체 요금제에서만 정의됩니다. 모든 아이들에게 물려받은 책들, 가격 책들.<br/><br/>대체 가격 장부를 만드는 동안 통화가 지정되지 않은 경우(API를 통해) 통화 기본값은 USD입니다. |
| **제품 가격** | 특정 가격표 내의 제품(SKU)에 지정된 특정 가격. |
| **할인** | 할인은 제품 가격에 정의됩니다. 상속되지 않음. |
