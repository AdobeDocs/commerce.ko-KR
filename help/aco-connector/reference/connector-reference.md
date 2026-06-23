---
title: '[!DNL Adobe Commerce Optimizer Connector]개 모듈 및 피드 끝점'
description: ' [!DNL Adobe Commerce]에 대한  [!DNL Adobe Commerce Optimizer Connector] 모듈, 카탈로그 피드 API 끝점, 일괄 처리 제한 및 core_config_data 구성 경로에 대해 알아봅니다.'
feature: Integration, Configuration
badgePaas: label="PaaS만" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce 온 클라우드 프로젝트(Adobe 관리 PaaS 인프라) 및 온프레미스 프로젝트에만 적용됩니다."
autotag-review: '2026-06-09T15:48:19.494Z'
TQID: 'https://experienceleague.adobe.com/UM6Y-xoQpUDzWpaMe1GRPp4XoAtHBLBsHw388kumN8g'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: 19de20caafd45e3a00896d0d4b29b7e96dfe94e1
workflow-type: tm+mt
source-wordcount: 301
ht-degree: 1%

---

# Adobe Commerce Optimizer 커넥터용 커넥터 모듈 및 피드 엔드포인트

이 참조는 [!DNL Adobe Commerce Optimizer Connector] 모듈 패키지, 지원되는 피드 API 끝점 및 `core_config_data`에 저장된 구성 키 경로를 나열합니다. 동기화 중에 이러한 구성 요소가 함께 작동하는 방법에 대해 알아보려면 [커넥터 동기화 파이프라인](../connector-sync-pipeline.md)을 참조하세요.

## 모듈

커넥터에는 카탈로그 데이터를 수집하고 피드 데이터를 [!DNL Commerce Optimizer] API에서 지원하는 형식에 매핑하며 제출 및 범위 제어를 관리하는 여러 Magento 모듈이 포함되어 있습니다. 다음 표에는 각 모듈과 그 역할이 요약되어 있습니다.

| 모듈 | 역할 |
| ------ | ---- |
| `DataExporterAdapter` | [!DNL Adobe Commerce] 피드를 [!DNL Adobe Commerce Optimizer] API에 필요한 형식으로 매핑합니다. 피드 풀 및 스키마 구성을 재정의합니다. |
| `SaasExportAdapter` | [!DNL Commerce Optimizer] 피드를 수집 API로 라우팅하고 지원되지 않는 피드를 제출하지 못하도록 차단합니다. |
| `CommerceAcoExporter` | [!DNL Commerce Optimizer] 자격 증명을 관리하고 CLI 설정 명령을 제공합니다. |
| `CommerceAdapter` | [!DNL Commerce Optimizer] API 호환성 계층(GraphQL, 번들 추가 장바구니, 구성 UI) |
| `PriceBookDataExporter` | 웹 사이트 및 고객 그룹에 의해 색인화된 가격 장부 피드 |
| `SaasPriceBook` | 가격표 제출을 위한 SaaS 인프라 |
| `CommerceOptimizerScopeMapper` | 웹 사이트 및 스토어 뷰 단위 동기화 지원 |

## 지원되는 피드

커넥터가 여러 피드 형식을 [!DNL Commerce Optimizer] [[!DNL Catalog Data Ingestion API]](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/){target="_blank"}에 제출합니다. 아래 표는 [!DNL Adobe Commerce]에 끝점, 배치 제한, 인덱서 이름 및 피드 테이블이 있는 각 피드를 나열합니다.

| 피드 | [!DNL Commerce Optimizer] API 끝점 | 배치 한도 | AC 색인 이름 | 피드 테이블 |
| ---- | ----------------------------------- | ----------- | ------------- | ---------- |
| `products` | `POST /v1/catalog/products` | 100 | `catalog_data_exporter_products` | `cde_products_feed` |
| `categories` | `POST /v1/catalog/categories` | 100 | `catalog_data_exporter_categories` | `cde_categories_feed` |
| `productAttributes` | `POST /v1/catalog/products/metadata` | 100 | `catalog_data_exporter_product_attributes` | `cde_product_attributes_feed` |
| `prices` | `POST /v1/catalog/products/prices` | 500 | `catalog_data_exporter_product_prices` | `cde_product_prices_feed` |
| `priceBooks` | `POST /v1/catalog/price-books` | 500 | `data_exporter_price_books` | `cde_price_books_feed` |

`products`, `productAttributes`, `categories` 및 `prices` 피드는 [!DNL SaaS Data Export] 인덱서에서 수집한 데이터를 다시 사용합니다. 커넥터는 웹 사이트 및 고객 그룹 구성에서 `priceBooks` 피드를 생성하며 [!DNL SaaS Data Export] 인덱서에 의존하지 않습니다.

각 피드에 대한 필드 수준 매핑 세부 정보는 [&#128279;](field-mapping.md)피드 [!DNL Commerce Optimizer Connector] 2&rbrace;에 대한 필드 매핑을 참조하십시오.
카탈로그 크기에 따라 동기화 시간을 예측하려면 [데이터 볼륨 및 동기화 시간 예측](estimate-data-volume-sync-time.md)을 참조하세요.

## 구성 경로

[!DNL Commerce Optimizer Connector] 자격 증명과 서비스 URL이 `aco_exporter/general/` 경로 접두사의 `core_config_data`에 저장됩니다. 현재 값을 검토하려면 `bin/magento aco:config:show`을(를) 실행하십시오. 이 명령은 클라이언트 암호를 표시하지 않습니다.

```text
aco_exporter/general/org_id
aco_exporter/general/tenant_id
aco_exporter/general/client_id
aco_exporter/general/client_secret       (encrypted)
aco_exporter/general/type
aco_exporter/general/ingestion_url
aco_exporter/general/optimizer_studio_url
```
