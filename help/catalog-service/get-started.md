---
title: ' [!DNL Catalog Service] 시작'
description: ' [!DNL Catalog Service] 에 액세스하고 프론트엔드 애플리케이션 및 서드파티 서비스와 통합하는 방법을 알아봅니다.'
role: Admin, Developer
exl-id: ee178e67-519d-4283-8de8-2634ae1f347a
TQID: https://experienceleague.adobe.com/KBdWesEoKJu-qWsY-Ny1Om-msUkyUPfUTQWftEqSg1g
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: c32adafa-ed01-4b31-997e-2413013911b0id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7
subfeature_v2: id: ae62cf09-5996-4921-bda8-fbe67b62e470
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: e1e0219c-f879-479f-8427-888ed2a6e9c2id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 10a91a91337778648e99078bcbf0c9ef25a49f86
workflow-type: tm+mt
source-wordcount: 437
ht-degree: 0%

---

# [!DNL Catalog Service] 시작

[!DNL Catalog Service]이(가) 활성화되면 서비스에 액세스하여 이를 사용하여 Adobe Commerce 인스턴스에서 제품 및 범주 정보와 같은 카탈로그 데이터를 검색할 수 있습니다. 이 서비스는 GraphQL 관리자 또는 GraphQL 쿼리를 지원하는 모든 프론트엔드 애플리케이션에서 액세스할 수 있는 Commerce API로 사용할 수 있습니다.

{{aco-merchandising-services}}

## 서비스 액세스

[!DNL Catalog Service]은(는) GraphQL 관리자 또는 GraphQL 쿼리를 지원하는 모든 프론트엔드 애플리케이션에서 액세스할 수 있는 Commerce API로 사용할 수 있습니다. 이 서비스는 SaaS 및 PaaS 환경 모두에서 사용할 수 있습니다.

[!BADGE PaaS만]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce 온 클라우드 프로젝트(Adobe 관리 PaaS 인프라) 및 온프레미스 프로젝트에만 적용됩니다."}

| 환경 | 엔드포인트 |
| ------------ | ----------: |
| **테스트** | `https://catalog-service-sandbox.adobe.io/graphql` |
| **프로덕션** | `https://catalog-service.adobe.io/graphql` |

[!BADGE SaaS만]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."}

| 환경 | 엔드포인트 |
| ----------- | --------:|
| 테스트 | `https://na1-sandbox.api.commerce.adobe.com/{{tenant-id}}/graphql` |
| 프로덕션(아직 사용할 수 없음) | `https://na1.api.commerce.adobe.com/{{tenant-id}}/graphql` |

**SaaS 끝점에 대한 URL 구조**

```text
https://<region>-<environment>.api.commerce.adobe.com/<tenantId>/graphql
```

- `<region>`은(는) 인스턴스가 배포된 클라우드 영역입니다.
- `<environment>`은(는) `sandbox`과(와) 같은 환경 유형입니다. 환경이 프로덕션인 경우 이 값은 생략됩니다.
- `<tenantId>`은(는) Adobe Experience Cloud 내에서 조직의 특정 인스턴스에 대한 고유 식별자입니다.

카탈로그 서비스 GraphQL API 사용에 대한 자세한 내용은 *Adobe Commerce 개발자* 설명서에서 [Adobe Commerce용 카탈로그 서비스 안내서](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/)를 참조하십시오.

## 헤드리스 상점 또는 서드파티 서비스와 통합

Headless Storefront와 통합하려면 Storefront 구성을 업데이트하여 Storefront와 [!DNL Catalog Service] 간의 통신을 통해 제품 및 카테고리 데이터를 검색해야 합니다.

Edge Delivery Services에서 Adobe Commerce Storefront를 사용하는 경우 카탈로그 서비스 엔드포인트를 storefront 구성에 추가하십시오. 자세한 내용은 [Edge Delivery Services 설명서](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/#storefront-configuration)를 참조하세요.

다른 통합의 경우 서비스와 백엔드 데이터 소스 간의 통합을 구성하는 방법에 대한 자세한 내용은 프로젝트 설정 설명서 를 참조하십시오.

### 방화벽 구성

방화벽을 통해 [!DNL Catalog Service]을(를) 허용하려면 `commerce.adobe.io`을(를) 허용 목록에 추가하십시오.

## 카탈로그 서비스 및 API 메쉬

개발자는 [Adobe Developer App Builder용 API Mesh](https://developer.adobe.com/graphql-mesh-gateway/gateway/overview/)를 통해 Adobe IO를 사용하여 개인 또는 서드파티 API 및 기타 인터페이스를 Adobe 제품과 통합할 수 있습니다.

설치 및 구성에 대한 자세한 내용은 [[!DNL Catalog Service] 및 API Mesh](mesh.md) 항목을 참조하십시오.

## 데이터 내보내기 모니터링 및 문제 해결

{{$include /help/_includes/data-export/verify-commerce-service-data-sync.md}}

필요한 경우 피드를 수동으로 다시 동기화하려면 [Commerce CLI](../data-export/data-export-cli-commands.md)를 사용하십시오. 다시 동기화 옵션 및 추가 문제 해결 단계는 _SaaS 데이터 내보내기 안내서_&#x200B;의 [동기화 관리](../data-export/data-sync-manage.md)를 참조하십시오.

{{install-data-sync-feed-status}}
