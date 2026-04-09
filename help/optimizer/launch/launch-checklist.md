---
title: 시작 체크리스트
description: ' [!DNL Adobe Commerce Optimizer] 프로덕션에 대한 구성, 상점, SEO, CDN, 통합, 보안, 분석 및 테스트의 유효성을 검사하는 방법을 알아봅니다.'
solution: Commerce
feature: Integration, Storefront, Search, Catalog Management, Personalization
feature-set: Commerce
role: Admin, Developer
level: Intermediate
topic: Administration
recommendations: noCatalog
badgeSaas: label="SaaS만" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 [!DNL Adobe Commerce Optimizer] 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."
source-git-commit: 37b8b8a334ca11daacfd3da03b0441e77329e2e1
workflow-type: tm+mt
source-wordcount: '1940'
ht-degree: 0%

---


# 시작 체크리스트

이 체크리스트를 사용하여 프로덕션 [!DNL Adobe Commerce Optimizer] 프로젝트가 구성, 테스트되고 시작할 준비가 되었는지 확인하십시오. 팀과 함께 각 섹션을 진행하고 고유한 프로젝트 계획 또는 추적기에서 완료를 추적합니다. 아래 참조된 제품 기능 및 UI 영역에 대해서는 [[!DNL Adobe Commerce Optimizer] 설명서](../overview.md)를 참조하세요.

## 사용 사례 및 아키텍처 {#use-case}

[!DNL Adobe Commerce Optimizer] 및 EDS(Edge Delivery Services)를 기존 Cloud on Cloud 인스턴스와 결합하는 B2C 경험을 제공할 때 이 체크리스트를 사용합니다.

솔루션에는 일반적으로 다음 구성 요소가 포함됩니다.

- **Cloud**—Cloud의 Adobe Commerce은 카탈로그 데이터, 고객, 자산 및 구매 흐름(체크아웃, 주문 관리, 배송 등)을 관리합니다.
- **최적화 도구**—[!DNL Adobe Commerce Optimizer]에서 머천다이징 경험을 제공합니다.
- **Storefront**—Edge Delivery Services의 Adobe Commerce Storefront에서 UI를 제공합니다.
- **타사 서비스**—결제, 배송 및 세금 공급자.
- **App Builder**—확장성.
- **API Mesh**—요청 라우팅입니다.

## 클라우드에서 Adobe Commerce 확인 {#verify-cloud}

클라우드 환경의 Adobe Commerce을 프로덕션할 준비가 되었는지 확인합니다.

▢ 클라우드 인스턴스가 [프로비저닝됨](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/start/new-project)입니다.
▢ 테스트 및 더미 데이터가 인스턴스에서 제거됩니다.
▢ 프로덕션 데이터가 인스턴스에 로드되었습니다.
▢ [GraphQL 끝점](https://developer.adobe.com/commerce/webapi/graphql/)을 알고 있습니다.
▢ 인스턴스가 [실행 준비](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/launch/checklist) 요구 사항을 충족합니다.

## Commerce Optimizer 인스턴스 확인 {#verify-optimizer}

[!DNL Adobe Commerce Optimizer] 프로덕션 인스턴스가 올바르게 설정되어 있는지 확인하십시오.

▢ 프로덕션 인스턴스가 활성 상태입니다. 프로비전하는 방법은 [시작하기](../get-started.md)를 참조하세요.
▢ 인스턴스가 올바른 영역에 있습니다.
▢ 환경 유형이 프로덕션입니다.
▢ 조직 ID, 클라이언트 ID, 수집 URL 및 Commerce Optimizer URL을 알고 있습니다. [시작하기](../get-started.md)를 참조하세요.
▢ 구성된 제한 및 경계는 Adobe 고객 기술 관리자(CTA)가 확인한 값과 일치합니다.
▢ 테스트 아티팩트 및 더미 데이터가 인스턴스에서 제거되었습니다.

## Storefront 사이트 확인 {#verify-storefront-site}

Edge Delivery Services 상점 사이트가 존재하며 액세스가 제한되어 있는지 확인합니다.

▢ Storefront 사이트가 있습니다. [상점 만들기](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/)를 참조하세요.
▢ 사이트 이름을 알고 있습니다.
▢ 권한이 있는 사람만 [게시할 수 있는 권한](https://tools.aem.live/tools/user-admin/index.html)을 가집니다.
▢ 권한이 있는 사용자만 [작성자 권한](https://docs.da.live/administrators/guides/permissions)을 갖습니다.

## Cloud 및 Optimizer 통합 확인 {#cloud-optimizer-integration}

클라우드의 Adobe Commerce과 [!DNL Adobe Commerce Optimizer]이(가) 데이터를 올바르게 교환하는지 확인하십시오.

### Adobe Commerce에서

클라우드 프로젝트에서 이러한 검사를 완료하십시오.

▢ Commerce Optimizer 커넥터가 [설치 및 구성되었습니다](../../aco-connector/get-started.md).
▢ `aco:conf:show` CLI 명령이 프로덕션 Commerce Optimizer 인스턴스에 대한 연결을 확인합니다. 조직 ID, 클라이언트 ID, 수집 URL 및 Commerce Optimizer URL은 프로덕션과 일치합니다.
▢구성 내보내기[의 &#x200B;](../../aco-connector/get-started.md) 동기화 범위가 요구 사항과 일치합니다.
▢ [데이터 피드 동기화 상태](../../aco-connector/get-started.md)에서 클라우드 인스턴스에서 데이터 내보내기를 확인합니다.

### Commerce Optimizer에서

[!DNL Adobe Commerce Optimizer] UI에서 이러한 검사를 완료합니다.

▢ [데이터 동기화 대시보드](../setup/data-sync.md)에 수신된 데이터가 표시됩니다. 카탈로그 서비스, 제품 검색 및 권장 사항에 대한 제품, 가격 및 특성이 표시됩니다.
▢ [가격 장부](../setup/pricebooks.md)는 클라우드의 고객 그룹에서 자동으로 만들어집니다.
▢ [카탈로그 보기](../setup/catalog-view.md)가 있으며 해당 ID를 알고 있습니다.
▢ [정책](../setup/policies.md)이(가) 있으며 해당 ID를 알고 있습니다.
▢ [패싯](../merchandising/facets/overview.md)이(가) 구성되었습니다.
▢ [동의어](../merchandising/synonyms/overview.md)이(가) 구성되었습니다.
▢ [머천다이징 규칙](../merchandising/rules/overview.md)이(가) 구성되었습니다.
▢ [가격 팩팅 및 검색 언어](../settings.md)는 해당 기능을 사용할 때 요구 사항과 일치합니다.
▢ [제품 권장 사항](../merchandising/recommendations/create.md)이(가) 있으며 미리 보기에서 예상대로 동작합니다.
▢ [검색 성능 데이터](../manage-results/search-performance.md)가 *관리자*에 표시됩니다.
▢ [권장 사항 성능 데이터](../manage-results/recommendation-performance.md)가 *관리자*&#x200B;에 표시됩니다.

## Storefront 및 Cloud 통합 확인 {#storefront-cloud-integration}

상점 전면이 올바른 Adobe Commerce GraphQL 끝점에서 읽는지 확인합니다.

### Adobe Commerce에서

▢ Storefront 호환성 패키지가 [설치됨](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/storefront-compatibility/install/)입니다.

### 상점 앞에서

▢ 상점 `commerce-core-endpoint` 설정이 [Cloud GraphQL 끝점](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/)을 가리킵니다.
▢ API Mesh를 Cloud GraphQL의 프록시로 사용하는 경우 `commerce-core-endpoint`은(는) Cloud GraphQL 끝점 대신 API Mesh 끝점을 가리킵니다.

## Storefront 및 Optimizer 통합 확인 {#storefront-optimizer-integration}

Storefront 구성에서 Commerce Optimizer 설정을 확인합니다.

▢ 상점 첫 화면에서 올바른 [Commerce Optimizer 설정](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/)을 사용합니다.
▢ `adobe-commerce-optimizer`은(는) `true`입니다.
▢ `commerce-endpoint`은(는) 프로덕션 Commerce Optimizer GraphQL 끝점 또는 API Mesh 사용 시 API Mesh 끝점을 가리킵니다.
▢ `headers.cs.AC-view-ID`은(는) 프로덕션 Commerce Optimizer 인스턴스의 카탈로그 보기 ID를 보유합니다.

## 클라우드에서 타사 서비스 확인 {#third-party-services}

[!DNL Adobe Commerce Optimizer]이(가) 아닌 호스트 상거래 시스템에서 실행되는 통합을 확인합니다.

▢ **결제:** 결제 게이트웨이가 실시간 실행되고 테스트됩니다(Stripe, PayPal, Adyen 등).
▢ **배송:** 배송 API 연결이 작동합니다(UPS, FedEx 등).
▢ **배송:** 이행 플랫폼이 연결되어 테스트되었습니다(예: ShipStation).
▢ **세금:** 세금 계산 통합이 확인되었습니다(Avalara, TaxJar 등).
▢ **세금:** 회계 소프트웨어 동기화가 작동합니다(QuickBooks 등).
▢ **재고:** PIM, ERP 또는 재고 관리 통합을 테스트하고 동기화합니다.
▢ **아키텍처:** 호스트 상거래 시스템은 결제, 배송, 세금 및 인벤토리를 처리합니다([!DNL Adobe Commerce Optimizer]은(는) 아님).
▢ **아키텍처:** API Mesh 및 App Builder이 Host Commerce 시스템과 [!DNL Adobe Commerce Optimizer] 간에 동기화 상태를 유지합니다.
▢ **전자 메일:** 트랜잭션 전자 메일 게재가 작동합니다(주문 확인, 배송 등).
▢ **전자 메일:** 전자 메일 템플릿이 브랜드와 일치하며 올바른 링크를 사용합니다.

## App Builder 및 API Mesh 확인 {#app-builder-mesh}

프로덕션에 대한 확장성 구성을 확인합니다.

### App Builder

▢ 프로덕션 작업 영역에 필요한 모든 구성 및 서비스가 포함됩니다.
▢ 프로덕션 앱이 빌드 시나리오 간에 테스트를 통과합니다.
▢ 제품 제한 및 경계는 [Adobe Developer App Builder 제품 설명](https://helpx.adobe.com/legal/product-descriptions/adobe-developer-app-builder.html){target="_blank"} 및 [App Builder 시스템 설정 및 제한 사항](https://developer.adobe.com/app-builder/docs/guides/runtime_guides/system-settings){target="_blank"}을 기반으로 검토 및 확인되었습니다.
▢ 프로덕션 앱은 App Builder 프로덕션 끝점을 사용합니다.
▢ 사용자 지정 *관리자* 패널 확장이 프로덕션 작업 영역에 배포됩니다.

### API 메쉬

▢개의 구성 및 원본을 프로덕션할 준비가 되었습니다.

### 이벤트

▢ Adobe I/O Events이 구성되어 있으며 구독이 확인되었습니다.

## Storefront 경험 완료 {#finalize-storefront}

시작 전 폴란드 콘텐츠, SEO, 성능, 보안 및 CDN 동작.

### 컨텐츠 및 작성

작성 워크플로 및 Storefront 구성 요소를 확인합니다.

▢ [AEM/EDS Go-Live 확인 목록](https://www.aem.live/docs/go-live-checklist) 검토가 완료되었습니다.
▢ 작성 원본이 문서 기반 또는 유니버설 편집기이며 구성되어 있습니다.
▢ 콘텐츠가 게시 주기 미리보기→ 사용하여 게시됩니다.
▢ 도메인에서 `.aem.live` 콘텐츠 및 디자인 QA가 완료되었습니다.
▢ favicon이 사이트에서 올바르게 구성되고 제공됩니다.
▢ da.live 및 제품 비주얼은 [구성된](https://docs.da.live/administrators/guides/permissions) 전용 자격 증명을 사용합니다.
▢ 드롭인(장바구니, 체크아웃, PDP, PLP, 인증, 계정)이 [사용자 지정되고](../storefront.md) 테스트됩니다.
▢ 상점 브랜딩이 CSS 디자인 토큰, 타이포그래피 및 색상을 반영합니다.

### SEO 및 색인 지정

메타데이터, URL 및 크롤링 동작을 확인합니다.

▢ 문서 제목 메타데이터가 키 페이지(특히 PDP 및 PLP)에 대해 있습니다. [Adobe Commerce 상점](https://experienceleague.adobe.com/developer/commerce/storefront/setup/seo/metadata/){target="_blank"} 설명서에서 _SEO 메타데이터_을(를) 참조하십시오.
▢개의 PDP에 [메타데이터 및 구조화된 데이터](https://experienceleague.adobe.com/developer/commerce/storefront/setup/seo/metadata/){target="_blank"}(예: JSON-LD)가 포함되어 있습니다.
▢ 제품 URL 형식이 일관됩니다(예: `domain/product-name`).
▢ 가상 URL이 표준 URL로 리디렉션됩니다.
▢ 프로젝트에 필요한 경우 인덱싱을 허용하고 사이트 맵을 참조하며 인덱싱하지 않을 경로를 차단하는 `robots.txt`이(가) 포함되어 있습니다(예: `/drafts`).
▢ [리디렉션](https://www.aem.live/docs/redirects) 파일은 `.html`을(를) 제거한 후 마이그레이션에서 URL 변경 사항을 다룹니다.
▢ 사이트 맵이 있으며 필요에 따라 Google 검색 콘솔에 제출됩니다.
▢개의 정식 URL이 `2xx` 또는 `3xx`이(가) 아닌 `4xx` 상태를 반환합니다.
▢개의 다국어 사이트가 사이트 맵에 `hreflang`개의 태그를 포함합니다.
▢ Google 검색 콘솔 검사 보고서가 최신 상태입니다.

### 사전 렌더링

활성화된 서버측 렌더링을 확인합니다.

키 페이지에 대해 ▢ 미리 렌더링이 설정되어 있습니다. [AEM 상점](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/aem-prerender/){target="_blank"} 설명서에서 _Adobe Commerce용 사전 렌더링_을 참조하십시오.
▢ URL은 소문자를 사용하므로 사전 렌더링이 링크를 끊지 않습니다.
▢ HTML 소스에는 사전 렌더링 작업을 확인하는 메타데이터 및 본문 콘텐츠가 포함되어 있습니다.
해당되는 경우 ▢개의 로케일에 올바른 번역된 페이지가 표시됩니다.
▢ 필요에 따라 추가 HTML 마크업이 [구성됨](https://www.aem.live/docs/redirects)됩니다.

### 성능 및 모니터링

성능 기준선 및 분석 배선을 확인합니다.

▢ 스토어프론트는 [Adobe Commerce 스토어프론트](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/performance/){target="_blank"} 설명서에서 _성능 모범 사례_를 따릅니다.
▢(선택 사항) Google Analytics 및 Google Tag Manager가 구성되어 있습니다.
▢ [Storefront 이벤트](https://github.com/adobe/commerce-events/tree/main/examples/events/snowplow-debugger) 구현이 유효하고 Adobe Commerce [!DNL Live Search]관리자[!DNL Product Recommendations]의 *및* 대시보드에 데이터가 표시됩니다.
▢ `environment`Commerce 구성[의 &#x200B;](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/){target="_blank"} 분석 매개 변수는 개발 중 `"Testing"`이고 Go-Live 시 `"Production"`입니다. [분석 계측](https://experienceleague.adobe.com/developer/commerce/storefront/setup/analytics/instrumentation/){target="_blank"}을 참조하십시오.
▢ 등대 점수는 이 항목의 지침에 따라 대상(예: 키 페이지의 `100`)을 충족합니다.

### 보안 및 액세스

권한 및 비밀을 확인합니다.

DA 콘텐츠 및 EDS 사이트에 대해 적절한 권한이 ▢개 구성되었습니다. 작성에 대한 [DA.live 권한](https://da.live/docs/administration/permissions) 및 [인증 설정](https://www.aem.live/docs/authentication-setup-authoring)을 참조하세요.
▢ 제품 시각적 개체 통합이 프로비전되었습니다. [AEM Cloud Service 액세스 개요](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/accessing/overview#)를 참조하십시오.
전자 메일 템플릿의 암호 재설정 링크 ▢개가 Edge Delivery Services 설정과 일치합니다. 상점 FAQ를 참조하십시오. [Edge Delivery Services 또는 Helix로 마이그레이션한 후 이메일 템플릿 링크가 끊어진 경우 어떻게 해야 합니까?](https://experienceleague.adobe.com/developer/commerce/storefront/troubleshooting/faq/#what-should-i-do-if-my-email-template-links-are-broken-after-migrating-to-edge-delivery-services-or-helix){target="_blank"}.
통합 및 결제 공급자를 위한 ▢ 프로덕션 키가 있습니다.
▢ 도메인은 허용 목록에추가된이며 백엔드 웹후크가 작동합니다.

### CDN 및 캐싱

CDN, DNS 및 캐시 동작을 확인합니다.

▢ CDN 구성은 Sidekick 확장 및 스크립트(예: 사이트 맵 생성 및 이미지 가져오기)에 대해 프로덕션 GraphQL 끝점(`yourproject.com/graphql`)을 사용합니다.
▢ Adobe Commerce Fastly를 사용하는 경우 CDN 제거 토큰을 사용할 수 있고 [사이트 구성](https://tools.aem.live/tools/cdn-setup/index.html)에 `authToken` 및 `serviceId`이(가) 포함됩니다.
▢ [CDN 구성](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/content-delivery-network/){target="_blank"}이(가) 캐싱 및 무효화를 확인합니다.
▢ [다중 저장소 설정](https://experienceleague.adobe.com/developer/commerce/storefront/setup/seo/indexing/#multi-store-setups){target="_blank"}의 경우 카탈로그 서비스 및 [!DNL Live Search] 요청에 저장소 특정 캐시 버스터(예: 쿼리 매개 변수 또는 CDN 규칙)가 포함되어 있습니다.
▢ 푸시 무효화가 끝까지 작동합니다(변경 내용을 게시한 다음 프로덕션 도메인에서 확인).
전환 전에 ▢ DNS TTL이 충분히 낮습니다.
▢ DNS A 및 CNAME 레코드가 모든 도메인 및 호스트 이름에 대해 올바릅니다.
▢ 프로덕션 도메인에 대해 SSL/TLS 인증서가 프로비저닝되고 확인되었습니다.
▢ `www` 및 apex 리디렉션이 올바르게 동작합니다.

## 보안 및 규정 준수 {#security-compliance}

보안 태세 및 규정 준수 작업을 확인합니다.

▢ **SSL:** 신뢰할 수 있는 SSL/TLS 인증서가 설치되어 있습니다.
▢ **SSL:** HTTPS가 사이트 전체에 적용됩니다.
▢ **액세스:** 기본 *관리자* 암호가 변경되었으며 강력한 암호 정책이 적용됩니다. [!DNL Adobe Commerce Optimizer] [사용자 및 ID 관리](../user-management.md)를 참조하십시오.
▢ **액세스:** *관리자* URL이 기본값이 아닙니다.
▢ **액세스:** 모든 *관리자* 사용자에 대해 2단계 인증을 사용할 수 있습니다.
▢ **액세스:** 프로젝트와 연결된 비활성 또는 사용하지 않는 관리자 사용자가 없습니다.
▢ **방화벽:** 웹 응용 프로그램 방화벽(WAF)이 구성 및 확인되었습니다.
▢ **PCI:** 프로덕션에 대한 보안 침투 테스트(PCI 범위)가 완료되었습니다.
▢ **검색:** Adobe 보안 검색 도구가 등록되었으며 초기 검색이 완료되었습니다.
▢ **액세스:** CORS는 승인된 원본만 허용합니다.
▢ **준수:** [에 대한 &#x200B;](../shared-responsibility.md)공유 책임 모델[!DNL Adobe Commerce Optimizer]이(가) 최신 상태이며 Adobe과 고객 책임을 명확하게 정의합니다.
▢ **준수:** 개인정보 처리방침, 쿠키 동의 및 GDPR 또는 CCPA 요구 사항이 확인되었습니다.

## 분석 및 모니터링 {#analytics-monitoring}

측정 및 베이스라인을 확인합니다.

▢ **RUM:** RUM(Real User Monitoring)은 이전 및 이후 비교를 위해 계측됩니다.
▢ **Analytics:** Adobe Experience Platform 데이터 수집이 구성되었습니다(해당하는 경우).
▢ **Analytics:** MarTech 태그가 프로덕션 호스트 이름에서 실행되는지 확인했습니다.
▢ **Analytics:** 기준선 분석이 문서화되어 있습니다. 시작 후 변동(페이지 보기, 바운스 비율 등)이 예상됩니다.
▢ **이벤트:** 전환 추적이 처음부터 끝까지 작동합니다(확인 → 장바구니에 추가 → 체크아웃).

## 테스트 {#testing}

시작 전후의 품질을 확인합니다.

▢ **기능:** 핵심 흐름이 끝까지 작동함: 검색 → 필터→ 검색하여 장바구니→ 추가하고 계정 만들기→ 체크 아웃→ 추가합니다.
▢ **기능:** 결제 게이트웨이가 실제 및 테스트 트랜잭션을 수락합니다.
▢ **기능:** 주문 배치, 확인 전자 메일 및 주문 추적 작업.
▢ **기능:** 배송 옵션과 세금 계산이 정확합니다.
▢ **기능:** 쿠폰, 할인 및 충성도 프로그램은 예상대로 작동합니다.
▢ **UAT:** 사용자 수락 테스트가 스테이징 및 프로덕션에서 완료되었습니다.
▢ **성능:** 부하 및 스트레스 테스트가 완료되었으며 Adobe CTA 또는 CSE의 결과가 나왔습니다.
▢ **성능:** 데스크톱 및 모바일에서 페이지 로드 시간이 3초 미만입니다.
▢ **성능:** 등대 점수는 주요 페이지의 목표를 충족합니다(예: PageSpeed Insights를 통해).
▢ **성능:** 이미지, 스크립트 및 자산이 최적화되었습니다.
▢ **호환성:** Chrome, Firefox, Safari 및 Edge이 예상대로 동작합니다.
▢ **호환성:** 응답형 레이아웃은 모바일, 태블릿 및 데스크톱에서 작동합니다.
▢ **호환성:** 성능은 3G, 4G 및 Wi-Fi에서 사용할 수 있습니다.
▢ **접근성:** 접근성 감사가 완료되었습니다(WCAG, 화면 판독기, 키보드 탐색).
▢ **기능:** 실행 후 404 모니터링 플랜이 있습니다.
▢ **UAT:** 롤백 계획이 있으며 시작 문제가 발생하면 테스트를 통과합니다.

## 론치 날짜 및 론치 후 {#launch-post-launch}

소통, 지원 및 후속 작업을 확인합니다.

▢ **시작 조정:** Adobe에 확정된 시작 날짜가 있습니다. CTA에 전자 메일로 알림이 전송되었습니다.
▢ **지원:** P1 핫라인 번호가 기록되었습니다. 미국(+1) 800-497-0335, Commerce의 경우 6번을 누르십시오.
▢ **지원:** 팀이 P1 핫라인으로 전화하는 **이전** 지원 티켓을 열도록 교육되었습니다.
▢ **시작 후:** 프로덕션 도메인에서 Lighthouse 점수를 확인하십시오.
▢ 시작 후: **크롤링 검색 오류를 색인화하기 위해 Google 콘솔을 모니터링**
▢ **게시물 실행:** 모니터 404에서 트래픽이 많은 레거시 URL에 대해 보고하고 리디렉션을 추가합니다.
▢ **출시 이후:** 프로덕션에서 MarTech 및 Analytics 데이터를 확인합니다.
▢ **출시 이후:** CTA, CSE 또는 AM에 SLA 모니터링 활성화하도록 요청하십시오.
▢ 재해 복구 계획이 있으며 테스트를 통과했습니다.
▢ 보일러플레이트 및 확장 패키지를 추적하여 현재 버전으로 업그레이드하는 프로세스가 있습니다.
