---
title: 스테이징 환경에서 테스트
description: 테스트 목적으로 스테이징 환경의 프로덕션 환경에서  [!DNL Product Recommendations] 을(를) 사용하는 방법을 알아봅니다.
feature: Services, Recommendations, Staging
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# 스테이징 환경에서 테스트

프로덕션 환경에 권장 사항을 배포하기 전에 비프로덕션 환경에서 서비스를 테스트하여 모든 것이 예상대로 작동하는지 확인하십시오.

[!DNL Product Recommendations]님이 상점 앞에서 수집한 [쇼핑객 행동 데이터](events.md)를 기반으로 제품을 반품했습니다. 그러나 비프로덕션 환경에서는 쇼핑객의 행동 데이터가 없을 수 있습니다. 동작 데이터 없이 테스트할 수 있는 유일한 권장 사항 형식은 `More like this`입니다. 이 권장 사항 유형은 직접적인 콘텐츠 유사성 일치를 사용하므로 입력 데이터가 필요하지 않습니다.

다음 권장 사항 유형에는 동작 데이터가 필요합니다.

- 가장 많이 본 항목
- 이 항목을 보고 다른 항목도 보았습니다.
- 구매, 구매

비프로덕션 환경에서 행동 데이터를 사용하여 권장 사항을 테스트하려면 어떻게 해야 합니까? 몇 가지 옵션이 있습니다.

## 프로덕션 환경에서 권장 사항 가져오기(권장)

Adobe Commerce을 사용하면 프로덕션 환경에서 권장 사항을 가져오고 SaaS 데이터 공간을 [전환](settings.md)하여 비프로덕션 환경에서 미리 볼 수 있습니다.

프로덕션 환경에서 권장 사항을 가져오려면 다음을 확인해야 합니다.

- 프로덕션 환경에서 Storefront 데이터 수집이 [구성 및 사용](install-configure.md)되었습니다.
- 비프로덕션 환경의 카탈로그는 주로 프로덕션 환경의 카탈로그와 동일합니다. 유사한 카탈로그를 사용하면 추천 단위에서 반품된 제품이 프로덕션 환경의 제품과 거의 비슷하게 모방됩니다.

## 비프로덕션 환경에서 동작 데이터 생성

1. 카탈로그 데이터가 프로덕션 카탈로그와 유사한 비프로덕션 환경에 `magento/product-recommendations` 모듈을 배포합니다.

1. 관리자의 [구성](../landing/saas.md#saas-configuration)에 비프로덕션 데이터 공간 ID 중 하나를 사용합니다.

1. 상점 전면을 클릭하여 데이터를 직접 생성하여 실제 구매자의 행동을 모방하거나 자동화 스크립트를 만듭니다. 테스트를 통해 비프로덕션 환경에서 동작 이벤트를 생성합니다. 이러한 이벤트는 권장 사항을 제공하는 제품 관심도를 생성하는 데 사용됩니다. 테스트를 위해 [!DNL Commerce]은(는) 다음 추천 유형과 상호 작용하도록 제안합니다.

   - 가장 많이 본 항목 - 최소한의 입력 데이터가 필요합니다. 사용자는 제품을 확인해야 합니다.
   - 검토함. 검토함 - 여러 제품을 보려면 여러 사용자가 필요합니다.
   - 구매, 구매 - 여러 사용자가 여러 제품을 구매해야 합니다.

### 주의 사항

- 비프로덕션 [SaaS 데이터 공간](../landing/saas.md#saas-configuration)의 동작 및 카탈로그 데이터는 결과 제품 권장 사항이 연결된 상점 전면에서 생성된 동작 데이터를 전적으로 기반으로 하는 격리된 환경을 식별합니다.

- 동작 데이터가 많지 않으므로 제품 연결을 계산하기 위한 입력 데이터는 희박합니다. 그러나 이 데이터는 여전히 Sensei으로 전송되어 머신 러닝 모델을 계산하고 이 환경 내에서 생성된 데이터를 기반으로 권장 사항을 제공합니다.
