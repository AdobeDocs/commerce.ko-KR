---
title: 구현 워크플로
description: 상점 첫 화면에서  [!DNL Product Recommendations] 을(를) 성공적으로 구현하는 단계에 대해 알아봅니다.
exl-id: 4a784d04-8be6-473f-afb3-264af06c850a
source-git-commit: 458f34c45406db871ec61ff408aa624f163b6ee0
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---

# 구현 워크플로

[!DNL Product Recommendations]은(는) 동작 데이터와 카탈로그 데이터를 모두 사용합니다.

- 행동 - 제품 보기, 장바구니에 추가한 항목 및 구매와 같이, 사이트에 대한 쇼핑객 참여의 데이터. Adobe Commerce 및 Adobe AI는 개인 식별 정보를 수집하지 않습니다.

- 카탈로그 - 이름, 가격 및 가용성과 같은 제품 메타데이터.

`magento/product-recommendations module`을(를) 설치하면 Adobe AI가 동작 및 카탈로그 데이터를 집계하고 각 권장 사항 유형에 대해 [!DNL Product Recommendations]을(를) 만듭니다. 그런 다음 [!DNL Product Recommendations] 서비스는 이러한 권장 사항을 상점 앞에 배포합니다. 상점에서 제품 권장 사항을 구현하는 데 도움이 되도록 하려면 다음 워크플로를 사용하십시오.

>[!NOTE]
>
> PWA Studio을 사용하여 상점 전면이 구현된 경우 [PWA 설명서](https://developer.adobe.com/commerce/pwa-studio/integrations/product-recommendations/)를 참조하세요. React 또는 Vue JS와 같은 사용자 지정 프론트엔드 기술을 사용하는 경우 Headless Storefront에 [통합](headless.md) [!DNL Product Recommendations]하는 방법을 알아보세요.

## 워크플로

1. **프로덕션에 데이터 수집 배포**

   [!DNL Product Recommendations]을(를) 배포하려면 두 개의 기본 [데이터 원본](type.md)(카탈로그 및 동작)이 필요합니다. 프로덕션은 쇼핑객의 작업을 캡처하고 분석하는 유일한 환경이므로 가능한 한 빨리 프로덕션에 데이터 수집을 시작합니다. [Adobe AI가 고품질 추천을 제공하는 머신 러닝 모델을 교육하는 방법에 대해 알아봅니다](events.md). 추가된 혜택으로, 프로덕션에서 동작 데이터를 수집하기 시작할 때 비프로덕션 환경에서 작업하는 동안 이 프로덕션 데이터를 기반으로 [권장 사항을 가져오기](staging-environment.md#fetch-recommendations-from-production-environment-recommended)할 수 있습니다. 그런 다음 프로덕션에서 수집된 실제 구매자 데이터를 기반으로 계산되는 다양한 권장 사항을 테스트하고 실험할 수 있습니다.

   프로덕션에 데이터 수집을 배포하려면 [API 키](install-configure.md)를 제공하여 [!DNL Product Recommendations] 모듈을 [설치 및 구성](https://experienceleague.adobe.com/docs/commerce/user-guides/integration-services/saas.html)해야 합니다.

   >[!TIP]
   >
   > 데이터 수집을 배포해도 상점 모습이나 쇼핑객 경험은 변경되지 않습니다. 권장 사항 단위를 만들고 배포하기만 하면 상점 내 고객 환경이 변경됩니다. 프로덕션에 배포하기 전에 비프로덕션 환경에서 테스트해야 합니다. 또한 템플릿을 사용자 정의할 때까지 추천 단위를 만들지 마십시오. 다음 단계를 참조하십시오.

1. **내 스타일에 맞게 템플릿 사용자 지정**

   상점은 브랜드를 나타내므로 사이트 테마에 맞게 제품 추천 템플릿을 수정하십시오.

   >[!TIP]
   >
   > 템플릿을 사용자 정의하여 스타일시트를 지정하고 페이지에서 권장 사항 단위가 나타나는 위치를 덮어쓰는 등의 작업을 수행할 수 있습니다.

   이 단계를 완료하는 방법은 개발자 설명서에서 [사용자 지정](https://experienceleague.adobe.com/docs/commerce/product-recommendations/developer/customize.html)을 참조하십시오.

1. **비프로덕션 환경에서 권장 사항 테스트**

   프로덕션에 배포하기 전에 비프로덕션 환경에서 새 기술을 테스트하는 것이 항상 모범 사례입니다. 비프로덕션 환경에서 권장 사항을 테스트하면 다양한 권장 사항 단위 유형, 위치 및 페이지로 재생할 수 있습니다. 비프로덕션 환경에서 테스트하는 동안 프로덕션에 이미 수집된 행동 데이터를 기반으로 권장 사항을 가져올 수 있으므로 권장 사항 결과는 실제 고객의 쇼핑 행동을 기반으로 합니다.

   >[!TIP]
   >
   > 비프로덕션 환경 카탈로그가 프로덕션에 있는 카탈로그와 동일한지 확인합니다. 유사한 카탈로그를 사용하면 추천 단위에서 반품된 제품이 생산 중인 제품을 가깝게 모방할 수 있습니다.

   이 단계를 완료하는 방법을 알아보려면 프로덕션 환경에서 [동작 데이터 가져오기](staging-environment.md)를 참조하십시오.

1. **프로덕션 스토어에 권장 사항 만들기 및 배포**

   이제 프로덕션에 동작 데이터 수집을 배포하고, 제품 권장 사항 템플릿을 수정하고, 실제 구매자 동작을 사용하여 권장 사항을 테스트했으므로 모든 코드를 프로덕션으로 승격하고 [실시간 제품 권장 사항을 만들기](create.md)할 준비가 되었습니다.
