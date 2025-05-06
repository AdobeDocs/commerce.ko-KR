---
title: 온보딩 및 설치
description: ' [!DNL Catalog Service]을(를) 설치하는 방법 알아보기'
exl-id: 3f8492c3-f76d-49b7-a201-35deace36a1d
badgePaas: label="PaaS만" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce 온 클라우드 프로젝트(Adobe 관리 PaaS 인프라) 및 온프레미스 프로젝트에만 적용됩니다."
source-git-commit: be1c739f3821a5f1e846b3026088e3a3ff45a60f
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 0%

---

# 온보딩 및 설치

카탈로그 서비스를 설치하여 [카탈로그 서비스 GraphQL API](https://developer.adobe.com/commerce/services/graphql/catalog-service/)를 사용하여 Commerce 인스턴스에서 제품 데이터를 요청하고 받습니다. 카탈로그 서비스는 repo.magento.com 저장소에서 작성기 메타패키지로 제공됩니다.

>[!NOTE]
>
>Commerce 인스턴스가 라이브 검색 또는 제품 권장 사항을 사용하는 경우 해당 서비스를 온보딩하거나 업그레이드할 때 카탈로그 서비스가 자동으로 설치 또는 업데이트됩니다. 자세한 내용은 [실시간 검색](https://experienceleague.adobe.com/en/docs/commerce/live-search/install) 및 [제품 추천](https://experienceleague.adobe.com/en/docs/commerce/product-recommendations/getting-started/install-configure)에 대한 설치 지침을 참조하십시오.



## 시스템 요구 사항

**소프트웨어 요구 사항**

- Adobe Commerce 2.4.4+
- PHP 8.1, 8.2, 8.3, 8.4
- 작성기: 2.x

**지원되는 플랫폼**

- 클라우드 인프라의 Adobe Commerce: 2.4.4+
- Adobe Commerce 온프레미스: 2.4.4+

## 엔드포인트

[!DNL Catalog Service]에는 온보딩에 사용할 수 있는 두 개의 끝점이 있습니다.

- 샌드박스(`https://catalog-service-sandbox.adobe.io/graphql`) - 시작하기 전에 테스트 및 유효성 검사에 사용됨
- 프로덕션(`https://catalog-service.adobe.io/graphql`) - Commerce 판매자 및 웹 사이트의 라이브 트래픽에 사용됩니다.

모든 Commerce 테스트 인스턴스는 샌드박스 엔드포인트를 사용합니다.

샌드박스 엔드포인트에서 모든 로드 테스트를 수행합니다. 부하 테스트를 시작하기 전에 [지원 티켓](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket)을 제출하여 서비스 팀이 추가 서버 트래픽을 예측할 수 있도록 합니다.

## 설치 및 구성

Adobe Commerce용 [!DNL Catalog Service]을(를) 시작하려면 다음 단계가 필요합니다.

- 카탈로그 서비스 확장 설치(`magento/catalog-service`)
- 서비스 및 데이터 내보내기 구성
- 서비스 액세스

### 카탈로그 서비스 확장 설치

>[!BEGINSHADEBOX]

**필수 구성 요소**

- 확장을 설치하려면 [repo.magento.com](https://repo.magento.com)에 액세스하세요. 키를 생성하고 필요한 권한을 얻으려면 [인증 키 가져오기](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/authentication-keys)를 참조하십시오. 클라우드 설치의 경우 [클라우드 인프라의 Commerce 안내서](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/authentication-keys)를 참조하십시오.

- Adobe Commerce 애플리케이션 서버의 명령줄에 액세스합니다.

>[!ENDSHADEBOX]

Adobe Commerce 버전 2.4.4 이상을 실행 중인 Adobe Commerce 인스턴스에 최신 버전의 카탈로그 서비스 확장(`magento/catalog-service`)을 설치하십시오. 카탈로그 서비스는 [repo.magento.com](https://repo.magento.com) 리포지토리에서 작성기 메타패키지로 제공됩니다.

>[!BEGINTABS]

>[!TAB 클라우드 인프라]

이 메서드를 사용하여 Commerce Cloud 인스턴스의 [!DNL Catalog Service]을(를) 설치합니다.

1. 로컬 워크스테이션에서 Adobe Commerce on cloud infrastructure 프로젝트의 프로젝트 디렉터리로 변경합니다.

   >[!NOTE]
   >
   >Commerce 프로젝트 환경을 로컬로 관리하는 방법에 대한 자세한 내용은 _Adobe Commerce on Cloud Infrastructure 사용 안내서_&#x200B;의 [CLI로 분기 관리](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/cli-branches)를 참조하십시오.

1. Adobe Commerce Cloud CLI를 사용하여 업데이트할 환경 분기를 확인하십시오.

   ```shell
   magento-cloud environment:checkout <environment-id>
   ```

1. 카탈로그 서비스 모듈을 추가합니다.

   ```bash
   composer require magento/catalog-service --no-update
   ```

1. 패키지 종속성을 업데이트합니다.

   ```bash
   composer update "magento/catalog-service"
   ```

1. `composer.json` 및 `composer.lock` 파일에 대한 코드 변경 내용을 커밋하고 푸시합니다.

1. `composer.json` 및 `composer.lock` 파일에 대한 코드 변경 내용을 클라우드 환경에 추가, 커밋 및 푸시합니다.

   ```shell
   git add -A
   git commit -m "Add catalog service module"
   git push origin <branch-name>
   ```

   업데이트를 클라우드 환경으로 푸시하면 변경 사항을 적용하기 위해 [Commerce 클라우드 배포 프로세스](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/deploy/process)가 시작됩니다. [배포 로그](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/test/log-locations#deploy-log)에서 배포 상태를 확인하십시오.

>[!TAB 온-프레미스]

이 메서드를 사용하여 온-프레미스 인스턴스에 대한 [!DNL Catalog Service]을(를) 설치합니다.

1. 작성기를 사용하여 프로젝트에 카탈로그 서비스 모듈을 추가합니다.

   ```bash
   composer require magento/catalog-service --no-update
   ```

1. 종속성을 업데이트하고 확장을 설치합니다.

   ```bash
   composer update  "magento/catalog-service"
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

### 서비스 및 데이터 내보내기 구성

[!DNL Catalog Service]을(를) 설치한 후 다음 작업을 완료하여 카탈로그 서비스를 Adobe Commerce 인스턴스와 통합합니다. 이 통합을 통해 Commerce 인스턴스, 카탈로그 서비스 및 기타 지원 서비스 간에 데이터를 동기화하고 통신할 수 있습니다. 데이터 동기화는 [SaaS 데이터 내보내기 확장](../data-export/overview.md)에서 처리됩니다.

1. API 키를 지정하고 SaaS 데이터 공간을 선택하여 [Commerce 서비스 커넥터](https://experienceleague.adobe.com/en/docs/commerce/user-guides/integration-services/saas)를 설정합니다.

   Commerce 서비스 커넥터 설정은 카탈로그 서비스, 라이브 검색 및 제품 추천과 같은 Adobe Commerce 서비스를 사용하는 데 필요한 일회성 프로세스입니다. 다른 서비스에 대한 커넥터를 이미 구성한 경우 이 단계를 건너뜁니다.

1. [데이터 관리 대시보드](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard)에서 초기 데이터 동기화를 수행합니다.

   초기 동기화는 카탈로그 크기에 따라 몇 분에서 몇 시간 정도 소요될 수 있습니다. 데이터 관리 대시보드에서 동기화 상태를 모니터링할 수 있습니다. 초기 동기화 후 카탈로그는 지속적으로 제품 데이터를 내보내 서비스를 최신 상태로 유지합니다.

   >[!NOTE]
   >
   >Commerce CLI를 사용하여 명령줄에서 초기 동기화를 시작할 수도 있습니다. _SaaS 데이터 내보내기 안내서_&#x200B;에서 [초기 동기화](../data-export/data-export-cli-commands.md#initial-sync)를 참조하십시오.

카탈로그 내보내기가 올바르게 실행되는지 확인하려면 다음을 수행하십시오.

- [cron 작업이 실행 중인지 확인](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-readiness-check-issues).
- 인덱서가 [Admin](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management)에서 실행되거나 Commerce CLI 명령 `bin/magento indexer:info`을(를) 사용하여 실행되고 있는지 확인하십시오.
- `Catalog Attributes Feed, Product Feed, Product Overrides Feed` 및 `Product Variant Feed` 인덱서가 `Update by Schedule`(으)로 설정되어 있는지 확인하십시오.

### 데이터 동기화 모니터링 및 문제 해결

Commerce 관리에서 [데이터 관리 대시보드](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard)를 사용하여 동기화 프로세스를 모니터링할 수 있습니다. [Commerce CLI](../data-export/data-export-cli-commands.md#troubleshooting) 및 로그를 사용하여 프로세스를 관리하고 문제를 해결하십시오.

### 서비스 액세스

HTTPS를 통해 POST 명령을 사용하여 ` https://catalog-service.adobe.io/graphql` 끝점에서 [!DNL Catalog Service] GraphQL API에 액세스할 수 있습니다.

GraphQL 쿼리에서 관리자의 Adobe Commerce 서비스 커넥터 구성에 추가한 공개 API 키를 포함하여 여러 HTTP 헤더를 지정해야 합니다. 자세한 내용은 [Storefront Services GraphQL](https://developer.adobe.com/commerce/services/graphql/) 설명서를 참조하십시오.

### 방화벽 구성

방화벽을 통해 [!DNL Catalog Service]을(를) 허용하려면 `commerce.adobe.io`을(를) 허용 목록에 추가하십시오.

## 카탈로그 서비스 및 API 메쉬

개발자는 [Adobe Developer App Builder용 API Mesh](https://developer.adobe.com/graphql-mesh-gateway/gateway/overview/)를 통해 Adobe IO를 사용하여 개인 또는 서드파티 API 및 기타 인터페이스를 Adobe 제품과 통합할 수 있습니다.

설치 및 구성에 대한 자세한 내용은 [[!DNL Catalog Service] 및 API Mesh](mesh.md) 항목을 참조하십시오.

## 데이터 관리 대시보드

[!DNL Catalog Service] 데이터 동기화에 대한 자세한 내용은 [데이터 관리 대시보드](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard)를 참조하세요.
