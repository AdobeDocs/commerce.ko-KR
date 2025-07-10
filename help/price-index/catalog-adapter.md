---
title: 카탈로그 어댑터 확장
description: 카탈로그 어댑터를 사용하여 Commerce 서비스의 가격 렌더링
seo-title: Catalog Adapter Extension
seo-description: Using Catalog Adapter to render prices from Commerce Services
exl-id: e42101fa-9c30-482c-a649-44dc35376abb
source-git-commit: 74f6cb64724194651c4eeb538c0c69142b01ac5d
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 0%

---

# 카탈로그 어댑터

`[!DNL Catalog Adapter]` 확장은 Commerce 애플리케이션에 포함된 기본 제품 가격 인덱서를 비활성화하고 대신 [카탈로그 서비스](../catalog-service/overview.md)에서 제공하는 가격을 사용합니다.

어댑터는 [SaaS 데이터 내보내기](../data-export/overview.md) 및 Adobe Commerce 서비스와 함께 작동하도록 설계되었습니다. SaaS 데이터 내보내기는 가격 제출을 담당하며 [!DNL Catalog Adapter]은(는) Adobe Commerce 서비스에서 모든 가격을 검색합니다.

[!DNL Catalog Adapter]을(를) 사용하면 가격 인덱싱과 작업이 다음과 같은 방식으로 영향을 받습니다.

- Adobe Commerce 애플리케이션에 포함된 가격 인덱서가 비활성화되었습니다.
- SaaS 데이터 내보내기 및 [SaaS 가격 인덱서](price-indexing.md)를 사용하여 가격을 관리합니다.
- 고객이 제품, 카테고리 또는 제품 가격을 보여 주는 다른 페이지를 열면 Adobe Commerce 서비스에서 가격을 검색합니다.
- 가격은 [SaaS 데이터 내보내기](../data-export/overview.md)에서 데이터를 동기화하여 Adobe Commerce 서비스로 전송됩니다.
- 체크아웃은 가격을 동적으로 재계산합니다.

카탈로그 어댑터 확장을 제거하거나 비활성화하여 Commerce 애플리케이션에서 가격 색인화를 다시 활성화할 수 있습니다.

## 요구 사항

- Adobe Commerce 2.4.4+
- Adobe Commerce 환경에는 다음 Commerce 서비스 중 하나가 활성화 및 구성되어 있어야 합니다.

   - [라이브 검색](../live-search/install.md)
   - [제품 추천](../product-recommendations/install-configure.md)
   - [카탈로그 서비스](../catalog-service/installation.md)

## 설치

카탈로그 어댑터 확장은 다음 모듈을 설치하는 작성기 메타패키지입니다.

- **가격 색인화 사용 안 함**-이 모듈은 SaaS 가격 색인화를 통해 가격이 전달되도록 Commerce 애플리케이션의 가격 색인을 사용하지 않도록 설정합니다. SaaS 가격 색인화 확장 프로그램이 설치된 경우 Commerce 애플리케이션의 제품 가격 색인화기를 켤 수 없습니다.
- **가격 공급자**-이 모듈은 Adobe Commerce 서비스의 제품 가격을 제공합니다. 검색 쿼리를 구성하고 프론트엔드에 있는 제품의 가격을 가져옵니다.
- **카탈로그 서비스 검색 어댑터**-이 모듈은 제품 검색 요청에 대한 응답으로 Adobe Commerce 응용 프로그램에서 Adobe Commerce 서비스로 가격을 전송합니다.

## 설치 단계

>[!BEGINTABS]

>[!TAB 클라우드 인프라]

이 메서드를 사용하여 Commerce Cloud 인스턴스의 [!DNL Catalog Adapter]을(를) 설치합니다.

1. 로컬 워크스테이션에서 Adobe Commerce on cloud infrastructure 프로젝트의 프로젝트 디렉터리로 변경합니다.

   >[!NOTE]
   >
   >Commerce 프로젝트 환경을 로컬로 관리하는 방법에 대한 자세한 내용은 [Adobe Commerce on Cloud Infrastructure 사용 안내서](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/cli-branches)의 _CLI로 분기 관리_&#x200B;를 참조하십시오.

1. Adobe Commerce Cloud CLI를 사용하여 업데이트할 환경 분기를 확인하십시오.

   ```shell
   magento-cloud environment:checkout <environment-id>
   ```

1. 카탈로그 어댑터 모듈을 추가합니다.

   ```bash
   composer require magento/catalog-adapter --no-update
   ```

1. 패키지 종속성을 업데이트합니다.

   ```bash
   composer update "magento/catalog-adapter"
   ```

1. `composer.json` 및 `composer.lock` 파일에 대한 코드 변경 내용을 커밋하고 푸시합니다.

1. `composer.json` 및 `composer.lock` 파일에 대한 코드 변경 내용을 클라우드 환경에 추가, 커밋 및 푸시합니다.

   ```shell
   git add -A
   git commit -m "Add catalog adapter module"
   git push origin <branch-name>
   ```

   업데이트를 클라우드 환경으로 푸시하면 변경 사항을 적용하기 위해 [Commerce 클라우드 배포 프로세스](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/deploy/process)가 시작됩니다. [배포 로그](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/test/log-locations#deploy-log)에서 배포 상태를 확인하십시오.

>[!TAB 온-프레미스]

이 메서드를 사용하여 온-프레미스 인스턴스에 대한 [!DNL Catalog Adapter]을(를) 설치합니다.

1. 작성기를 사용하여 프로젝트에 카탈로그 어댑터 추가:

   ```bash
   composer require magento/catalog-adapter --no-update
   ```

1. 종속성을 업데이트하고 확장을 설치합니다.

   ```bash
   composer update  "magento/catalog-adapter"
   ```

1. Adobe Commerce 업그레이드:

   ```bash
   bin/magento setup:upgrade
   ```

1. 캐시를 지웁니다.

   ```bash
   bin/magento cache:clean
   ```

   >[!TIP]
   >
   >경우에 따라, 특히 프로덕션에 배포 시 시간이 걸릴 수 있으므로 컴파일된 코드를 지우지 않는 것이 좋습니다. 변경하기 전에 시스템을 백업해야 합니다.

>[!ENDTABS]


## Adobe Commerce 제품 가격 인덱서 다시 활성화

기본 Adobe Commerce 제품 가격 인덱서를 사용하는 서드파티 애플리케이션이 있는 경우 다음 명령을 사용하여 다시 활성화할 수 있습니다.

```bash
# re-enable Product Price indexer
bin/magento module:disable Magento_PriceIndexerDisabler
# re-index Product Price indexer
bin/magento index:reindex catalog_product_price
```

## Headless Storefront 시나리오에 대한 제품 가격 인덱서 비활성화

Headless Commerce 인스턴스가 있는 경우 Adobe Commerce 인스턴스의 로드를 줄이려면 Adobe Commerce 제품 가격 인덱서를 비활성화해야 할 수 있습니다. `magento/module-price-indexer-disabler` 모듈을 설치하여 이 작업을 완료할 수 있습니다.

```bash
composer require magento/module-price-indexer-disabler
```

## 사용 시나리오

다음은 일반적인 `[!DNL Catalog Adapter]` 시나리오입니다.

### Adobe Commerce 제품 가격 인덱서에 대한 종속성 없음

- 필요한 서비스(라이브 검색, 제품 추천, 카탈로그 서비스)가 설치된 Luma 또는 Adobe Commerce 핵심 GraphQL 판매자입니다
- Adobe Commerce 제품 가격 인덱서를 사용하는 서드파티 확장 프로그램과의 통합 없음

1. [!DNL Catalog Adapter] 설치

### Adobe Commerce 제품 가격 인덱서에 대한 종속성 포함

- 지원 서비스(라이브 검색, 제품 추천, 카탈로그 서비스)가 설치된 Luma 또는 Adobe Commerce 핵심 GraphQL 판매자입니다
- Adobe Commerce 제품 가격 인덱서에 의존하는 타사 확장을 사용합니다

1. [!DNL Catalog Adapter] 설치
1. 기본 Adobe Commerce 제품 가격 인덱서를 다시 사용하도록 설정합니다.

### 헤드리스 Commerce 인스턴스

- 필수 서비스(라이브 검색, 제품 추천, 카탈로그 서비스)가 설치된 Headless Commerce 인스턴스가 있는 판매자
- 기본 Adobe Commerce 제품 가격 인덱서에 의존하지 않음

1. `magento/module-price-indexer-disabler` 패키지에서 [!DNL Catalog Adapter] 모듈을 설치합니다.
