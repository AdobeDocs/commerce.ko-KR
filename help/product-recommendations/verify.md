---
title: 이벤트 컬렉션 확인
description: 동작 데이터가 Adobe Commerce으로 전송되고 있는지 확인하는 방법을 알아봅니다.
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 0%

---

# 이벤트 컬렉션 확인

`magento/product-recommendations` 모듈을 [설치 및 구성](install-configure.md)한 후 동작 데이터가 Adobe Commerce으로 전송되고 있는지 확인할 수 있습니다. Chrome에서 사용할 수 있는 개발자 도구를 사용하거나 Snowploy Chrome 확장을 설치할 수 있습니다. 추가 도움이 필요한 경우 지원 기술 자료에서 [문제 해결 [!DNL Product Recommendations] 모듈](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/troubleshoot-product-recommendations-module-in-magento-commerce.html)을 참조하세요.

## Chrome에서 개발자 도구를 사용하여 확인

이벤트 수집기 JS 파일이 모든 사이트 페이지에 로드되도록 하려면 다음을 수행하십시오.

1. Chrome에서 **Google Chrome 사용자 지정 및 제어**&#x200B;를 선택한 다음 **추가 도구** > **개발자 도구**&#x200B;를 선택합니다.
1. **네트워크** 탭을 선택한 다음 **JS** 유형을 선택하십시오.
1. `ds.` 필터링
1. 페이지를 다시 로드합니다.
1. **이름** 열에 `ds.js` 또는 `ds.min.js`이(가) 표시됩니다.

![이벤트 수집기 JS](assets/filter-ds.png)
_이벤트 수집기 JS_

이벤트가 사이트의 페이지(홈, 제품, 체크아웃 등)에서 실행되도록 하려면 다음을 수행합니다.

1. 브라우저에서 광고 차단기를 비활성화하고 사이트에서 쿠키를 허용하는지 확인하십시오.
1. Chrome에서 **Google Chrome 사용자 지정 및 제어**(브라우저의 오른쪽 상단에 있는 세 개의 세로 점)를 선택한 다음 **추가 도구** > **개발자 도구**&#x200B;를 선택합니다.
1. **네트워크** 탭을 선택하고 `tp2`을(를) 필터링하세요.
1. 페이지를 다시 로드합니다.
1. **이름** 열의 `tp2` 아래에 호출이 표시됩니다.

![이벤트 실행](assets/filter-tp2.png)
_이벤트가 실행되고 있는지 확인_

## Snowploy Chrome 확장 사용 확인

Chrome용 [Snowploy Analytics 디버거 확장 설치](https://chrome.google.com/webstore/detail/snowplow-analytics-debugg/jbnlcgeengmijcghameodeaenefieedm). 이 확장은 수집 및 Adobe Commerce으로 전송되는 이벤트를 표시합니다.

1. 브라우저에서 광고 차단기를 비활성화하고 사이트에서 쿠키를 허용하는지 확인하십시오.

1. Chrome에서 **Google Chrome 사용자 지정 및 제어**(브라우저의 오른쪽 상단에 있는 세 개의 세로 점)를 선택한 다음 **추가 도구** > **개발자 도구**&#x200B;를 선택합니다.

1. **Snowploy Analytics 디버거** 탭을 선택합니다.

1. **Event** 열에서 **구조화된 이벤트**&#x200B;를 선택합니다.

1. **컨텍스트 데이터 _n_**&#x200B;이(가) 표시될 때까지 아래로 스크롤합니다.**스키마**&#x200B;에서 Storefront 인스턴스를 찾습니다.

1. [SaaS 데이터 공간 ID](https://experienceleague.adobe.com/docs/commerce-admin/config/services/saas.html)이(가) 올바르게 설정되어 있는지 확인하십시오.

![Snowploy 필터](assets/snowplow-filter.png)
_Snowploy 필터_

>[!NOTE]
>
> 디버거의 `Data validity : NOT FOUND` 값은 내부 스키마를 나타냅니다. Snowploy Chrome 플러그인은 내부 스키마로 이벤트를 확인할 수 없습니다. 이는 실제 기능에는 영향을 주지 않습니다.

## 이벤트가 올바르게 실행되는지 확인

지표에 사용된 이벤트가 올바로 실행되는지 확인하려면 Snowflow Analytics 디버거에서 `impression-render`, `view` 및 `rec-click` 이벤트를 찾으십시오. [전체 이벤트 목록](https://experienceleague.adobe.com/docs/commerce/product-recommendations/developer/events.html)을 참조하세요.

>[!NOTE]
>
> [쿠키 제한 모드](https://experienceleague.adobe.com/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law.html)가 활성화된 경우, Adobe Commerce은 구매자가 동의할 때까지 행동 데이터를 수집하지 않습니다. 쿠키 제한 모드 가 비활성화되면 기본적으로 동작 데이터가 수집됩니다.
