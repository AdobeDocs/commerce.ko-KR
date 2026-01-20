---
title: 제품 추천 관리자 개발
description: 제품 추천 아키텍처 및 개발 기능에 대한 개요입니다.
exl-id: 5967259e-c531-4fc7-9abd-cc18433fab33
source-git-commit: 458f34c45406db871ec61ff408aa624f163b6ee0
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# 제품 추천 관리자 개발

제품 추천 은 전환율을 높이고 매출을 증대하며 쇼핑객 참여를 유도하는 데 사용할 수 있는 강력한 마케팅 도구입니다. 상품 추천은 &#39;이 상품을 본 고객도 본 고객&#39;, &#39;이 상품을 구매한 고객도 본 고객&#39;, &#39;추천 고객&#39; 등과 같은 단위 형태로 점포에 표시된다. Adobe Commerce 제품 권장 사항은 인공 지능과 머신 러닝 알고리즘을 사용하여 집계된 쇼핑객 데이터를 심층 분석하는 [Adobe AI](https://business.adobe.com/kr/ai.html)에서 제공됩니다. 이 데이터를 Commerce 카탈로그와 결합하면 쇼핑객에게 매력적이고 관련성이 높으며 개인화된 경험을 제공합니다.

>[!NOTE]
>
>PWA Studio을 사용하여 상점 전면이 구현된 경우 [PWA 설명서](https://developer.adobe.com/commerce/pwa-studio/integrations/product-recommendations/)를 참조하세요. React 또는 Vue JS와 같은 사용자 지정 프론트엔드 기술을 사용하는 경우 [headless](headless.md) 환경에서 제품 권장 사항을 통합하는 방법에 대해 알아보려면 사용 안내서를 참조하세요. Headless 인스턴스는 제품 추천 작업 영역을 향상시키기 위해 이벤트를 구현해야 합니다.

## 아키텍처 개요

높은 수준에서 Commerce 제품 권장 사항은 SaaS로 배포됩니다. Commerce 측에는 이벤트 수집기 및 권장 사항 레이아웃 템플릿이 포함된 상점 및 데이터 서비스, SaaS 내보내기 모듈 및 관리 UI가 포함된 백엔드가 포함됩니다. Adobe AI 인텔리전스 서비스는 SaaS 측면에서 활용됩니다.

![제품 추천 아키텍처 다이어그램](assets/arch-diag-sensei.svg)

권장 사항 모듈을 설치하고 구성하면 상점 첫 화면에서 동작 데이터 수집을 시작합니다. Adobe AI는 카탈로그 데이터와 함께 이 행동 데이터를 처리하고 recommendations 서비스에서 활용하는 제품 연결을 계산합니다. 이 시점에서 판매자는 관리 UI에서 직접 제품 추천 단위를 만들고, 관리하고, 상점 앞에 배포할 수 있습니다.

## 다음 단계

제품 권장 사항을 시작하려면 다음 항목을 참조하십시오.

- [제품 추천 구현 방법](implementation-workflow.md)

- [제품 권장 사항 설치 및 구성](install-configure.md)

- [제품 추천 만들기](create.md)
