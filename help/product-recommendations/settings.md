---
title: 설정
description: ' [!DNL Product Recommendations] 데이터 소스를 변경하는 방법과 시각적 권장 사항을 활성화하는 방법을 알아봅니다.'
exl-id: fe37624d-c53e-40cd-b182-10f62cba74c0
source-git-commit: fe5f864262478d1f9e205f2cd275452594cf4675
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# 설정

권장 사항에 대해 [SaaS 데이터 공간을 구성](../landing/saas.md#saas-configuration)하면 SaaS 데이터 공간은 카탈로그 데이터와 상점 행동 데이터를 수집합니다. [Adobe Sensei](https://www.adobe.com/sensei.html)은(는) 해당 데이터를 분석하고 제품 추천을 제공하는 데 사용되는 제품 연결을 계산합니다.

테스트 또는 스테이징을 위한 비프로덕션 환경에는 일반적으로 실제 제품 추천을 제공하는 상점 행동 데이터의 수량이나 품질이 없습니다. 규모에 따른 실제 구매자 행동은 프로덕션 환경에서만 캡처할 수 있습니다. 이 문제를 해결하기 위해 Adobe Commerce에서는 프로덕션 환경의 제품 권장 사항을 다른 비프로덕션 SaaS 데이터 공간과 함께 사용할 수 있습니다. 비프로덕션 환경에서 실제 상점 데이터를 사용하면 쇼핑객이 보는 권장 사항을 미리 보고 다양한 권장 사항 유형 및 배치 위치를 실험할 수 있습니다. 다른 SaaS 데이터 공간의 권장 사항은 구매자가 미리 볼 수 있지만 클릭은 할 수 없습니다.

스테이징 순서는 스테이징 `environmentId`을(를) 사용하여 기록됩니다. 프로덕션 데이터에는 영향을 주지 않습니다. 프로덕션 데이터는 `alternateEnvironmentId`을(를) 사용하여 검색됩니다.

>[!NOTE]
>
>REST를 통해 제품 추천을 사용할 때 `alternateEnvironmentId` 매개 변수를 사용하여 다른 데이터 공간을 지정할 수 있습니다. [GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/)를 통해 제품 권장 사항을 사용할 때는 이 매개 변수를 사용할 수 없습니다.

## 권장 사항 소스 선택

제품 권장 사항 데이터의 소스를 변경하려면 사용할 동작 데이터가 있는 SaaS 데이터 공간을 선택합니다. 시작하기 전에 다음을 확인하십시오.

- Storefront 데이터 수집은 프로덕션 환경에 대해 [구성 및 활성화](install-configure.md)되어야 하며 동작 데이터가 Adobe Commerce으로 전송되고 있는지 [확인](verify.md)되어야 합니다.
- 비프로덕션 환경 카탈로그는 기본적으로 프로덕션 카탈로그와 동일해야 합니다. 유사한 카탈로그를 사용하면 반환된 제품 추천 단위가 프로덕션 단위의 추천 단위와 거의 비슷하게 모방됩니다.

1. 비프로덕션 Adobe Commerce 환경의 관리자에 로그인합니다.

1. _관리자_ 사이드바에서 **마케팅** > _프로모션_ > **제품 추천**(으)로 이동합니다.

1. **설정**&#x200B;을 클릭합니다.

   ![제품 추천 설정](assets/settings.png)
   _설정_

1. _권장 사항 소스_ 섹션에서 **다른 SaaS 데이터 공간에서 권장 사항 가져오기** 옵션을 사용하도록 설정합니다. _권장 사항 소스_ 섹션은 비프로덕션 환경에만 나타납니다.

   _사용 가능한 SaaS 데이터 공간_ 목록이 나타납니다.

   ![제품 추천 설정](assets/settings-select-saas.png)
   _설정_

1. 사용하려는 구매자 데이터가 있는 SaaS 데이터 공간을 선택합니다.

1. **변경 내용 저장**&#x200B;을 클릭합니다.

   이제 Adobe Commerce은 선택한 데이터 공간에서 권장 사항을 가져옵니다.

   >[!NOTE]
   >
   > 비프로덕션 상점 전면의 다른 SaaS 데이터 공간에서 가져온 권장 사항을 볼 수는 있지만 권장 사항을 클릭할 수는 없습니다.

### 새 SaaS 데이터 공간 구성

1. 권장 사항 소스 섹션에서 **구성 편집**&#x200B;을 클릭합니다.

1. 지침에 따라 새 [[!DNL Commerce] 서비스](/help/landing/saas.md)를 구성하십시오.

## 시각적 권장 사항 활성화

[시각적 제품 권장 사항](install-configure.md) 모듈이 설치된 경우 시각적 권장 사항이 [시각적 유사성](type.md#visualsim) 권장 사항 유형을 사용하도록 설정해야 합니다.

_시각적 권장 사항_ 섹션에서 **시각적 권장 사항 사용**&#x200B;을(를) 활성 위치로 설정합니다.
