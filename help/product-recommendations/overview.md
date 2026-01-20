---
title: ' [!DNL Product Recommendations] 소개'
description: '[!DNL Product Recommendations]은(는) 전환율을 높이고 매출을 증대하며 쇼핑객 참여를 촉진하는 데 사용할 수 있는 강력한 마케팅 도구입니다.'
recommendations: noCatalog
badgePaas: label="PaaS만" type="Informative" url="https://experienceleague.adobe.com/ko/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce 온 클라우드 프로젝트(Adobe 관리 PaaS 인프라) 및 온프레미스 프로젝트에만 적용됩니다."
exl-id: 72850cfd-555c-4e0e-ac3e-097e6dac2030
source-git-commit: 458f34c45406db871ec61ff408aa624f163b6ee0
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 0%

---

# [!DNL Product Recommendations] 소개

제품 추천은 전환율을 높이고 매출을 증대하며 쇼핑객 참여를 유도하는 데 사용할 수 있는 강력한 마케팅 도구입니다. Adobe Commerce 제품 권장 사항은 인공 지능과 머신 러닝 알고리즘을 사용하여 집계된 방문자 데이터를 심층 분석하는 [Adobe AI](https://business.adobe.com/kr/ai.html)에서 제공됩니다. 이 데이터를 Adobe Commerce 카탈로그와 결합하면 매력적이고 관련성이 높으며 개인화된 경험을 제공합니다.

제품 권장 사항은 &quot;이 제품을 본 고객이 본 경우도 본 경우&quot;와 같이 레이블이 있는 단위로 상점 전면에 표시됩니다. Adobe Commerce 관리에서 바로 스토어 보기 간에 권장 사항을 만들고, 관리하고, 배포할 수 있습니다.

PWA Studio을 사용하여 상점 전면이 구현된 경우 [PWA 설명서](https://developer.adobe.com/commerce/pwa-studio/integrations/product-recommendations/)를 참조하세요. React 또는 Vue JS와 같은 사용자 지정 프론트엔드 기술을 사용하는 경우 Headless Storefront에 [통합](headless.md) [!DNL Product Recommendations]하는 방법을 알아보세요.

>[!NOTE]
>
>Headless 또는 사용자 지정 구현을 개발하는 방법에는 여러 가지가 있습니다. 이 안내서에서는 PWA Studio을 사용하여 이 작업을 수행하는 한 가지 방법에 대해 설명합니다. 모든 시나리오나 상황을 다루지는 않습니다.

## 개인 정보 보호

[!DNL Product Recommendations]을(를) 위한 데이터 수집에는 PII(개인 식별 정보)가 포함되지 않습니다. 또한 쿠키 ID 및 IP 주소와 같은 모든 사용자 식별자는 엄격히 익명으로 처리됩니다. 자세한 내용은 [Adobe 개인정보 처리방침](https://www.adobe.com/privacy/policy.html)을 참조하세요.

데이터 동기화에 대한 자세한 내용은 [!DNL Product Recommendations]명의 사용자가 [데이터 관리 대시보드](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard.html?lang=ko)를 참조할 수 있습니다.

## 제품 권장 사항 대 제품 관계

온라인 쇼핑의 변화무쌍한 복잡성을 고려할 때, 상점에 가장 적합한 것은 종종 여러 주요 기술의 조합입니다. [!DNL Product Recommendations]과(와) [제품 관계](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/product-relationships/product-relationships.html?lang=ko)를 모두 사용하면 제품을 홍보할 때 보다 유연하게 대처할 수 있습니다. Adobe AI에서 제공하는 [!DNL Product Recommendations]을(를) 활용하여 규모에 맞게 권장 사항을 지능적으로 자동화할 수 있습니다. 그런 다음 수동으로 개입하여 대상 쇼핑객 세그먼트에 특정 권장 사항이 적용되는지 확인하거나 특정 비즈니스 목표를 충족해야 하는 경우 [관련 제품 규칙](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/product-relationships/product-related-rules.html?lang=ko)을 활용할 수 있습니다.

제품 권장 사항을 사용하면 다음 작업을 수행할 수 있습니다.

- 쇼핑객 기반, 항목 기반, 인기도 기반, 트렌드 및 유사성 기반의 9가지 지능형 추천 유형 중에서 선택합니다
- 행동 데이터를 사용하여 쇼핑객의 상점 여정 전체에서 권장 사항을 개인화합니다
- 각 권장 사항과 관련된 주요 지표를 측정하여 권장 사항의 영향을 이해하는 데 도움이 됩니다

## [!DNL Product Recommendations] 데모

[!DNL Product Recommendations]에 대해 알아보려면 이 비디오 보기:

>[!VIDEO](https://video.tv.adobe.com/v/3449965?captions=kor&quality=12)

## 카탈로그 데이터 보존 정책

테스트 환경에서 카탈로그 데이터에 대한 쿼리를 90일 연속 제출하지 않으면 카탈로그 데이터가 최대 절전 모드로 설정되고 쿼리에 대해 데이터가 반환되지 않습니다. 프로덕션 환경의 카탈로그 데이터는 이 정책의 영향을 받지 않습니다.

테스트 환경에서 카탈로그 데이터를 다시 활성화하려면 [지원 요청을 제출](https://experienceleague.adobe.com/ko/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#experience-league-start-page)하고 제목은 &quot;[!DNL Product Recommendations] 다시 활성화&quot;로 지정하고 환경 ID를 포함하십시오. 테스트 환경의 카탈로그 데이터는 2시간 이내에 복원되어야 합니다.
