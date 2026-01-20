---
title: Headless
description: Headless 상점 앞에서  [!DNL Product Recommendations] 을(를) 통합하는 방법을 알아봅니다.
exl-id: c40dac31-f87e-402a-ba50-e8aa4c1d66aa
source-git-commit: 458f34c45406db871ec61ff408aa624f163b6ee0
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---

# Headless

[!DNL Product Recommendations]PWA Studio[&#x200B; 또는 React 또는 Vue JS와 같은 사용자 지정 프론트엔드 기술을 사용하여 Headless Storefront에서 &#x200B;](https://developer.adobe.com/commerce/pwa-studio/)을(를) 통합할 수 있습니다.

사용자 정의 및 Headless 통합자는 제안된 구현으로 이 Luma 및 PWA 지침을 참조해야 합니다. 제품 권장 사항을 Headless 솔루션에 구현하는 방법은 여러 가지가 있으며 이 설명서는 모든 시나리오를 다루지 않습니다. 통합자는 해당 구현에 대한 이벤트, 설계 및 테스트를 다룹니다.

[!DNL Product Recommendations]을(를) 사용하려면 [동작 및 카탈로그 데이터](https://experienceleague.adobe.com/docs/commerce/product-recommendations/developer/development-overview.html)가 필요합니다. 카탈로그 데이터 동기화 프로세스는 Headless 구현에서 변경되지 않지만 동작 데이터 수집에는 변경이 필요합니다.

>[!NOTE]
>
>Headless 인스턴스는 제품 추천 대시보드를 구동하는 이벤트를 구현해야 합니다.

Headless 상점 앞에서 [!DNL Product Recommendations]을(를) 통합하려면 다음을 수행해야 합니다.

1. 행동 데이터를 Adobe AI로 전송하여 제품 추천 결과를 분석하고 계산합니다. 제품 추천 [지표 보고](workspace.md)을 사용하도록 설정하는 추가 데이터를 보낼 수도 있습니다.

1. 제품 추천 결과를 가져오고 페이지에서 해당 결과를 렌더링합니다.

다음 워크플로에 설명된 대로 사용 가능한 SDK를 사용하여 이러한 작업을 모두 수행할 수 있습니다.

1. [&#x200B; 모듈을 &#x200B;](install-configure.md)설치[!DNL Product Recommendations]합니다.

1. [Adobe Commerce Storefront Event SDK](https://developer.adobe.com/commerce/services/shared-services/storefront-events/sdk/)을(를) 설치하고 사용하여 [동작 이벤트](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#product-recommendations)을(를) 실행합니다.

   [!DNL Product Recommendations]개의 결과를 반환하는 데 필요한 최소 이벤트:

   | 이벤트 | 범주 |
   |--- | ---|
   | `view` | 제품 |
   | `add-to-cart` | 제품 |
   | `place-order` | 체크아웃 |

   [지표 보고](workspace.md)를 사용하려면 다음 추가 이벤트가 필요합니다.

   | 이벤트 | 범주 |
   |--- | ---|
   | `impression-render` | recommendation-unit |
   | `view` | recommendation-unit |
   | `rec-click` | recommendation-unit |
   | `rec-add-to-cart-click` | 권장 사항 단위(&quot;장바구니에 추가&quot; 단추가 권장 사항 템플릿에 있는 경우) |

1. 이벤트가 실행되면 [Adobe Commerce 상점 이벤트 수집기](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/)를 사용하여 이벤트를 처리하고 Adobe AI로 보내십시오.

1. 동작 데이터가 수집되면 관리자에서 [만들기](create.md) [!DNL Product Recommendations]할 수 있습니다.

1. [권장 사항 SDK](https://developer.adobe.com/commerce/services/product-recommendations/)을(를) 사용하여 상점에서 권장 사항 단위를 가져옵니다. SDK은 페이지에서 추천 단위를 렌더링하는 데 필요한 제품 데이터를 반환합니다.

1. [`recommendations` GraphQL 쿼리](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/)를 사용하여 특정 SKU 등에 대한 제품 추천 블록에 대한 정보를 반환하는 방법을 알아봅니다.
