---
title: 설치
description: PHP용 Composer를 사용하여 Adobe Commerce 스토어프론트용  [!DNL Store Fulfillment solution] 을(를) 설치합니다.
role: Admin, Developer
level: Intermediate
feature: Shipping/Delivery, Install
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 0%

---


# 설치

예외 처리를 허용하도록 구성된 큐 관리자를 실행하고 캐싱을 사용하여 비프로덕션 환경에서 [!DNL Store Fulfillment for Adobe Commerce by Walmart Commerce Technologies] 확장의 초기 설치를 완료합니다. 개발 환경에 Adobe Commerce 인스턴스의 운영 및 유지 관리에 대한 우수 사례를 확인할 수 있는 개발 도구가 포함되어 있는지 확인합니다.

>[!TIP]
>
>_Adobe Commerce 업그레이드 안내서_&#x200B;의 [업그레이드 지침](https://experienceleague.adobe.com/docs/commerce-operations/upgrade-guide/modules/upgrade.html?lang=ko)에 따라 온 프레미스에서 Adobe Commerce의 스토어 이행 확장을 업그레이드하십시오. 클라우드 인프라의 Adobe Commerce에 대해서는 *Cloud Infrastructure의 Commerce 안내서*&#x200B;에서 [확장 업그레이드](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure-store/extensions.html?lang=ko#upgrade-an-extension)를 참조하십시오.

## 전제 조건

Adobe Commerce용 [!DNL Store Fulfillment] 확장을 설치하거나 업그레이드하기 전에 스토어 이행 솔루션에 대한 [요구 사항](solution-requirements.md)을 검토하고 필요한 정보를 수집하십시오.

Adobe Commerce용 스토어 이행 확장 기능의 프리릴리스 또는 베타 버전을 설치한 경우 현재 버전을 설치하기 전에 다음 명령을 사용하여 제거하십시오.

```bash
rm -rf composer.lock vendor/walmart &&
composer require walmart/magento-bopis-metapackage:1.0.0
```

## 설치 요구 사항

- **Walmart Commerce Technologies 소프트웨어 아카이브(.zip 파일)의 스토어 이행 액세스** - 온보딩 및 활성화 프로세스 동안 계정 관리자와 협력하여 스토어 이행 확장에 대한 설치 파일에 액세스하십시오.

- **Adobe Commerce 계정 정보** - [!DNL Store Fulfillment] 솔루션을 설치하려면 [[!DNL Commerce] 계정](https://experienceleague.adobe.com/ko/docs/commerce-admin/start/commerce-account/commerce-account-create){target="_blank"}이 필요합니다. [!DNL Adobe Commerce] 프로젝트에 대한 소유자 또는 관리자 액세스 권한을 가진 계정 ID 및 자격 증명이 필요합니다.

- 클라우드 인프라 프로젝트의 [!DNL Adobe Commerce]에 대해 소프트웨어 설치 관리자에게는 클라우드 프로젝트에 대한 관리자 액세스 권한이 있어야 합니다. [사용자 액세스 관리](https://experienceleague.adobe.com/ko/docs/commerce-cloud-service/user-guide/project/user-access)를 참조하십시오.

- **작성기 및[!DNL Commerce CLI]**&#x200B;을(를) 사용한 환경—이러한 도구를 사용하여 [!DNL Adobe Commerce] 플랫폼에서 확장을 설치하고 관리하는 방법에 대한 자세한 내용은 [일반 CLI 설치](https://experienceleague.adobe.com/ko/docs/commerce-operations/installation-guide/tutorials/extensions){target="_blank"}를 참조하십시오.

- **Adobe Commerce에 타사 확장 설치 경험** - 자세한 내용은 Adobe Commerce 설명서를 참조하십시오.

   - [클라우드 인프라 인스턴스에 Adobe Commerce용 확장을 설치](https://experienceleague.adobe.com/ko/docs/commerce-cloud-service/user-guide/configure-store/extensions#install-an-extension).

   - [Adobe Commerce 온-프레미스 인스턴스에 대한 확장을 설치](https://experienceleague.adobe.com/ko/docs/commerce-operations/installation-guide/tutorials/extensions).

### 1단계: 확장 번들 다운로드

계정 담당자가 제공하는 지침에 따라 Store Fulfillment Services 확장 설치를 위한 Composer 패키지가 포함된 아카이브 파일을 다운로드하십시오.

### 2단계: 응용 프로그램에 확장 아티팩트 추출

통합 번들이 포함된 아카이브 파일을 추출하여 Store Fulfillment Services 확장을 설치합니다.

1. 추출된 파일에 대한 대상 디렉토리를 만듭니다.

   - 명령줄에서 웹 서버 문서 루트 디렉토리로 이동합니다.

   - `artifacts` 디렉터리를 만듭니다.

1. 아카이브 파일을 새 디렉토리에 추출합니다.

1. 파일 목록을 검토하여 파일의 압축을 성공적으로 풀었는지 확인합니다.

   ```
   ../var/www/html/artifacts]$ ls -a
   .
   ..
   bopis-sdk.zip
   module-magento-bopis-alternate-pickup-contact-admin-ui.zip
   module-magento-bopis-alternate-pickup-contact-api.zip
   ```

### 3단계: Composer를 사용하여 앱 구성

Composer를 사용하여 설치를 위한 소스 디렉토리를 구성하고 Store Fulfillment Services 확장을 설치합니다.

1. Composer 설치를 위한 소스 저장소를 구성합니다.

   ```bash
   composer config repositories.artifacts artifact artifacts/
   ```

1. Store Fulfillment Services 확장을 `composer.json`에 추가하십시오.

   ```bash
   composer require walmart/magento-bopis-metapackage:1.0.0
   ```

>[!NOTE]
>
>Adobe Commerce 온-프레미스 인스턴스에서 향상된 성능을 위해 [자동 로드 구성을 업데이트](https://experienceleague.adobe.com/docs/commerce-operations/performance-best-practices/deployment-flow.html?lang=ko#update-the-autoloader)할 수 있습니다. `composer dump-autoload --optimize`

### 4단계: 데이터베이스 스키마 및 데이터 업그레이드

`bin/magento setup:upgrade`을(를) 사용하여 저장소 이행 솔루션을 지원하도록 데이터베이스 스키마와 데이터를 업데이트하여 설치를 완료합니다.

>[!NOTE]
>
>클라우드 인프라 프로젝트의 Adobe Commerce의 경우 확장을 등록할 필요가 없습니다. 대신 이전 단계의 코드 변경 사항을 커밋하고 환경 분기에 푸시합니다. 데이터베이스 스키마와 데이터를 업데이트하는 명령은 클라우드 빌드 및 배포 프로세스 중에 자동으로 실행됩니다.

### 5단계: 설치 완료

1. `setup:upgrade` Magento CLI 명령을 사용하여 Adobe Commerce에 확장을 등록합니다.

   ```bash
   bin/magento setup:upgrade
   ```

1. 메시지가 표시되면 [!DNL Commerce] 프로젝트를 다시 컴파일하십시오.

   ```bash
   bin/magento setup:di:compile
   ```

1. 캐시를 정리합니다.

   ```bash
   bin/magento cache:clean
   ```

1. 유지 관리 모드를 비활성화합니다.

   ```bash
   bin/magento maintenance:disable
   ```

### 6단계: 설치 확인

Adobe Commerce 서버에서 Store Fulfillment Services 확장의 모듈이 설치되고 활성화되어 있는지 확인합니다.

1. 서버에 로그인.

   클라우드 인프라의 Adobe Commerce에 설치하는 경우 [SSH를 사용하여 원격 환경에 로그인합니다](https://experienceleague.adobe.com/ko/docs/commerce-cloud-service/user-guide/develop/secure-connections#ssh).

1. Store Fulfillment Services 모듈이 활성화되어 있는지 확인합니다.

   ```bash
   bin/magento module:status  --enabled | grep Walmart
   ```

   출력에는 다음 모듈이 포함되어야 합니다.

   ```
   Walmart_BopisBase
   Walmart_BopisAlternatePickupContact
   Walmart_BopisAlternatePickupContactFrontend
   Walmart_BopisApiConnector
   Walmart_BopisAlternatePickupContactAdminUi
   Walmart_BopisCheckoutPickInStoreApi
   Walmart_BopisInventorySourceAdminUi
   Walmart_BopisCheckoutPickInStore
   Walmart_BopisInventoryCatalogApi
   Walmart_BopisPreferredLocationApi
   Walmart_BopisHomeDeliveryApi
   Walmart_BopisHomeDelivery
   Walmart_BopisPreferredLocation
   Walmart_BopisInventoryCatalog
   Walmart_BopisPreferredLocationFrontend
   Walmart_BopisCheckoutPickInStoreAdminUi
   Walmart_BopisInventorySourceApi
   Walmart_BopisInventorySourceFaasSync
   Walmart_BopisInventorySourceReservation
   Walmart_BopisLocationCheckInApi
   Walmart_BopisLogging
   Walmart_BopisStoreAssociateApi
   Walmart_BopisLocationCheckInFrontend
   Walmart_BopisStoreAssociate
   Walmart_BopisOperationQueue
   Walmart_BopisOperationQueueAdminUi
   Walmart_BopisOperationQueueApi
   Walmart_BopisOrderFaasSync
   Walmart_BopisOrderUpdateApi
   Walmart_BopisLocationCheckIn
   Walmart_BopisInventoryCatalogAdminUi
   Walmart_BopisPreferredLocationAdminUi
   Walmart_BopisDeliverySelection
   Walmart_BopisCheckoutPickInStoreFrontend
   Walmart_BopisLocationCheckInAdminUi
   Walmart_BopisStoreAssociateAdminUi
   Walmart_BopisOrderUpdate
   Walmart_BopisStoreAssociateTfa
   Walmart_BopisStoreAssociateTfaApi
   ```

### 추가 단계

필요한 경우 [setup:static-content:deploy](https://experienceleague.adobe.com/ko/docs/commerce-operations/tools/cli-reference/commerce-on-premises){target="_blank"} CLI 명령을 사용하여 정적 보기 파일을 프로덕션 환경에 배포합니다.

```bash
php bin/magento setup:static-content:deploy -f
```

빈 테마를 사용하는 경우 `-f` 옵션이 필요합니다.

>[!NOTE]
>
>자세한 내용은 Adobe Commerce 도움말 센터에서 [Adobe Commerce의 정적 콘텐츠 배포 모범 사례](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/development/static-content-deployment.html?lang=ko) 문서를 참조하십시오.


