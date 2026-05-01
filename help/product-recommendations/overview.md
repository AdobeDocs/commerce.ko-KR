---
title: 제품 추천이란 무엇입니까?
description: Adobe Commerce의 제품 권장 사항에 대해 알아봅니다. AI 기반 상점, 개인 정보, 관리 및 상점 경로, 주요 데이터 보존 등을 살펴볼 수 있습니다.
recommendations: noCatalog
exl-id: 72850cfd-555c-4e0e-ac3e-097e6dac2030
source-git-commit: 6bfc2c0ed53b44fb30a142dc87f87dca8a601a33
workflow-type: tm+mt
source-wordcount: '738'
ht-degree: 0%

---

# [!DNL Product Recommendations]이란?

[!DNL Product Recommendations]을(를) 통해 [Adobe AI](https://business.adobe.com/kr/ai.html)을(를) 사용하여 Adobe Commerce 상점 첫 화면에서 개인화된 제품 추천을 표시하고, 종합 쇼핑객 행동 및 카탈로그에 대한 머신 러닝을 확인할 수 있습니다. 이 개요에서는 서비스 제한(HIPAA 포함), 데이터 및 개인 정보, 추천 단위가 표시되는 위치, 상점 구현 경로, 추천이 제품 관계를 보완하는 방법, 카탈로그 데이터 보존에 대해 설명합니다.

>[!IMPORTANT]
>
>**[!DNL Product Recommendations]은(는) HIPAA 지원 서비스가 아닙니다.** HIPAA 지원 서비스를 사용하거나 PHI(보호 상태 정보)를 처리하는 Adobe Commerce 구현에서 [!DNL Product Recommendations]을(를) 활성화하거나 사용하지 마십시오. [!DNL Product Recommendations]은(는) 현재 비 HIPAA 준비로 분류된 Commerce SaaS 서비스의 일부입니다.
>
>HIPAA가 준비된 Adobe Commerce 기능 및 PHI와 함께 사용하지 말아야 하는 서비스에 대한 자세한 내용은 [Adobe Commerce의 HIPAA 준비](https://experienceleague.adobe.com/ko/docs/commerce-admin/start/compliance/hipaa-ready-service/overview) 및 [작업](https://experienceleague.adobe.com/ko/docs/commerce-admin/start/compliance/hipaa-ready-service/operations#adobe-commerce-services)을 참조하십시오.

## 데이터 처리 및 개인 정보 보호

[!DNL Product Recommendations]에 대한 데이터 수집에 PII(개인 식별 정보)가 포함되어 있지 않습니다. 쿠키 ID 및 IP 주소와 같은 모든 사용자 식별자는 엄격히 익명으로 처리됩니다. 자세한 내용은 [Adobe 개인정보 처리방침](https://www.adobe.com/privacy/policy.html)을 참조하세요.

데이터 동기화에 대한 자세한 내용은 [데이터 관리 대시보드](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard.html?lang=ko)를 참조하세요.

## 권장 사항 표시 위치

권장 사항은 &quot;이 제품을 본 고객이 본 항목&quot;과 같이 레이블이 있는 단위로 상점 전면에 표시됩니다. Adobe Commerce 관리에서 스토어 보기 간에 권장 사항을 만들고, 관리하고, 배포할 수 있습니다. Commerce 프로젝트에서 [Adobe Commerce Optimizer 커넥터](https://experienceleague.adobe.com/ko/docs/commerce/aco-optimizer-connector/overview)를 사용하는 경우 [Adobe Commerce Optimizer](../optimizer/overview.md)을 통해 권장 사항을 만들고 관리하고 배포합니다.

## Storefront 구현

상점과 일치하는 설명서를 선택합니다.

- **PWA Studio** — [PWA 설명서](https://developer.adobe.com/commerce/pwa-studio/integrations/product-recommendations/)
- **사용자 지정 프론트엔드(예: React 또는 Vue.js)** — Headless Storefront의 [통합 [!DNL Product Recommendations]](headless.md)
- **EDS(Commerce Edge Delivery Services)** — [EDS에 대한 Adobe Commerce 상점 첫 화면 설명서](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/?lang=ko)

>[!NOTE]
>
>Headless 및 사용자 지정 설정은 스택별로 다릅니다. 이 제품 영역은 PWA Studio 경로 및 일반적인 Headless 통합 패턴을 문서화합니다. 모든 타사 또는 사용자 지정 시나리오를 다루지 않습니다.

## 제품 권장 사항 대 제품 관계

온라인 쇼핑의 변화무쌍한 복잡성을 고려할 때, 상점에 가장 적합한 것은 종종 여러 주요 기술의 조합입니다. [!DNL Product Recommendations]과(와) [제품 관계](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/product-relationships/product-relationships.html?lang=ko)를 모두 사용하면 제품을 홍보할 때 보다 유연하게 대처할 수 있습니다. Adobe AI 기반의 [!DNL Product Recommendations]을(를) 활용하여 규모에 맞게 권장 사항을 지능적으로 자동화할 수 있습니다. 그런 다음 수동으로 개입하여 대상 쇼핑객 세그먼트에 특정 권장 사항이 적용되는지 확인하거나 특정 비즈니스 목표를 충족해야 하는 경우 [관련 제품 규칙](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/product-relationships/product-related-rules.html?lang=ko)을 활용할 수 있습니다.

제품 권장 사항을 사용하면 다음 작업을 수행할 수 있습니다.

- 쇼핑객 기반, 항목 기반, 인기도 기반, 트렌드 및 유사성 기반의 9가지 지능형 추천 유형 중에서 선택합니다
- 행동 데이터를 사용하여 쇼핑객의 상점 여정 전체에서 권장 사항을 개인화합니다
- 각 권장 사항과 관련된 주요 지표를 측정하여 권장 사항의 영향을 이해하는 데 도움이 됩니다

## 제품 추천 데모

[!DNL Product Recommendations]에 대해 알아보려면 이 비디오 보기:

>[!VIDEO](https://video.tv.adobe.com/v/3449965?captions=kor&quality=12)

## 카탈로그 데이터 보존 정책

[!DNL Product Recommendations] 서비스는 Adobe Commerce 환경과 계속 동기화되는 카탈로그 데이터에 따라 다릅니다. 해당 데이터의 쿼리를 중지하는 비활성 카탈로그 또는 환경은 최대 절전 모드로 들어갈 수 있으며, 이는 다시 활성화하기 전까지 서비스가 반환하는 내용에 영향을 줍니다.

연속 90일 동안 **테스트** 환경에서 카탈로그 데이터에 대한 쿼리를 제출하지 않으면 카탈로그 데이터가 최대 절전 모드로 설정되고 쿼리에 대해 데이터가 반환되지 않습니다. **프로덕션** 환경의 카탈로그 데이터는 90일 규칙의 영향을 받지 않습니다.

생성 45일 후 환경에 **빈 카탈로그**&#x200B;가 있는 경우 카탈로그 데이터가 최대 절전 모드로 설정되고 쿼리에 대해 데이터가 반환되지 않습니다. 이는 프로덕션 및 테스트 환경 모두에 적용됩니다.

### 카탈로그 데이터 다시 활성화

최대 절전 모드 이후에 카탈로그 데이터를 복원하려면 [지원 요청을 제출](https://experienceleague.adobe.com/ko/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#experience-league-start-page)하고 제목은 &quot;[!DNL Product Recommendations] 다시 활성화&quot;로 환경 ID를 포함하십시오. 카탈로그 데이터는 2시간 이내에 복원되어야 합니다.
