---
title: ' [!DNL Adobe Commerce Optimizer] 시작'
description: ' [!DNL Adobe Commerce Optimizer]을(를) 시작하는 방법에 대해 알아봅니다.'
hide: true
recommendations: noCatalog
exl-id: de57d93d-e156-45c1-86aa-de29a8c34bd2
source-git-commit: ac79c8aa43ced017743fbef1f181b4eaf8e0a754
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 0%

---

# 시작

>[!NOTE]
>
>이 설명서는 초기 액세스 개발 상태의 제품에 대해 설명하고 일반 가용성을 위한 모든 기능을 반영하지는 않습니다.

이 안내서에서는 [!DNL Adobe Commerce Optimizer] 인스턴스를 만들고 작업하는 과정을 안내합니다.

<!--Click the tabs below to see high-level workflow overviews for the following user types:

- Administrators
- Merchants
- Developers

>[!BEGINTABS]

>[!TAB Administrator and merchant workflow]

This diagram provides a high-level overview of how administrators and merchants access and manage [!DNL Adobe Commerce Optimizer] instances. See the [Adobe Admin Console Guide](https://helpx.adobe.com/kr/enterprise/admin-guide.html) for more information about administrator workflows.

NEED DIAGRAM

>[!TAB Developer workflow]

This diagram provides a high-level overview of how developers create integrations for [!DNL Adobe Commerce Optimizer] using App Builder. See the [API documentation](https://developer.adobe.com/commerce/services/cloud/) for more information.

NEED DIAGRAM

>[!ENDTABS]
-->

## 프로비저닝

[!DNL Adobe Commerce Optimizer] 인스턴스가 준비되면 [!DNL Adobe Commerce Optimizer] 프로비저닝 팀이 다음 끝점을 제공합니다.

| 항목 | 샘플 URL | 목적 |
|---|---|---|
| [!DNL Adobe Commerce Optimizer] UI | `https://experience.adobe.com/#/@commerceprojectbeacon/commerce-optimizer-studio?tenant=<tenantId>` | <br>1에서 카탈로그를 관리하기 위해 Commerce Optimizer UI에 액세스하십시오. 머천다이징 규칙(제품 검색, 제품 권장 사항).<br>2. 카탈로그 관리(채널 및 정책 생성).<br>3. 데이터 인사이트(카탈로그 데이터 수집 상태 보기). |
| Storefront API | `https://na1-sandbox.api.commerce.adobe.com/<tenantId>/graphql` | Edge Delivery Services에서 제공하는 Commerce 상점 설정에 필요한 API에 액세스합니다. |
| 카탈로그 데이터 수집 API | `https://na1-sandbox.api.commerce.adobe.com/<tenantId>/v1/catalog/<entity>` | 카탈로그 데이터를 수집하는 데 필요한 API에 액세스합니다. |

>[!NOTE]
>
>Storefront 설정 및 카탈로그 수집에 필요한 API에 대한 자세한 내용은 [개발자 설명서](https://developer-stage.adobe.com/commerce/services/composable-catalog/)를 참조하세요.

조기 액세스 참가자는 IMS 토큰과 함께 [!DNL Adobe Commerce Optimizer]에 로그인하거나 API를 호출할 수 있는 보안 링크가 포함된 전자 메일을 받게 됩니다.

## 상점 배치

이제 [!DNL Adobe Commerce Optimizer] 인스턴스가 준비되었으므로 Edge Delivery Services에서 제공하는 Commerce Storefront를 [설정](./storefront.md)할 준비가 되었습니다.

## 조기 액세스 참가자에게 사용 가능한 카탈로그 데이터

조기 액세스 참가자인 [!DNL Adobe Commerce Optimizer] 인스턴스에는 [Carvelo 사용 사례](./use-case/admin-use-case.md)를 기반으로 하는 모의 카탈로그 데이터가 포함되어 있습니다. 미리 구성된 채널 및 정책과 함께 모의 데이터를 사용하면 [!DNL Adobe Commerce Optimizer] UI에 익숙해질 수 있습니다.

<!--Ingest catalog data

By default, [!DNL Adobe Commerce Optimizer] instances do not include any product data.

See the [Ingestion API](https://developer-stage.adobe.com/commerce/services/composable-catalog/data-ingestion/using-the-api/) documentation to learn how you can import your catalog data into [!DNL Adobe Commerce Optimizer].

The catalog data that you ingest is visible in the [data insights](./insights-overview.md) page. Additionally, you can use the [Catalog](./catalog-overview.md) page to define the channels and policies.-->
