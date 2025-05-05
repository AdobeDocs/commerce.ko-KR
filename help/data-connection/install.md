---
title: ' [!DNL Data Connection] 설치'
description: Adobe Commerce에서  [!DNL Data Connection] 확장을 설치, 업데이트 및 제거하는 방법을 알아봅니다.
role: Admin, Developer
feature: Install
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---

# [!DNL Data Connection] 설치

확장을 설치하기 전에 [필수 구성 요소를 검토하십시오](overview.md#prereqs).

## 확장 설치

[!DNL Data Connection] 확장은 [Adobe 마켓플레이스](https://commercemarketplace.adobe.com/magento-experience-platform-connector.html)에서 사용할 수 있습니다. 서버의 명령줄에서 이 확장을 설치하면 Adobe Commerce 설치에 [서비스](../landing/saas.md)(으)로 연결됩니다. 프로세스가 완료되면 **[!DNL Data Connection]** 및 **Commerce 서비스 커넥터**&#x200B;가 Commerce _관리_&#x200B;의 **서비스** 아래의 **시스템** 메뉴에 나타납니다.

![[!DNL Data Connection] 확장 관리자 보기](assets/epc-adminui.png)

>[!IMPORTANT]
>
>확장 이름이 Experience Platform 커넥터에서 [!DNL Data Connection]&#x200B;(으)로 변경되었지만 이전 버전과의 호환성을 지원하기 위해 패키지 이름은 `experience-platform-connector` 상태로 유지됩니다.

1. `experience-platform-connector` 패키지를 다운로드하려면 명령줄에서 다음을 실행하십시오.

   ```bash
   composer require magento/experience-platform-connector
   ```

   이 메타패키지에는 다음 모듈 및 확장이 포함되어 있습니다.

   - `magento/orders-connector`
   - `magento/data-services`
   - `magento/customers-connector`
   - `magento/module-experience-connector`
   - `magento/module-experience-connector-admin`
   - `magento/module-experience-connector-admin-graph-ql`
   - `magento/module-experience-connector-aep-integration`

1. (선택 사항) [검색 이벤트](events.md#search-events)를 구성하는 [!DNL Live Search] 데이터를 포함하려면 [[!DNL Live Search]](../live-search/install.md) 확장을 설치하십시오.

1. (선택 사항) [구매요청 이벤트](events.md#b2b-events)를 구성하는 B2B 데이터를 포함하려면 [B2B 확장](#install-the-b2b-extension)을 설치하십시오.

1. (선택 사항) 의료 서비스 판매자인 경우 [데이터 서비스 HIPAA](#install-the-data-services-hipaa-extension) 확장을 설치하여 [!DNL Commerce] 백 오피스 데이터가 HIPAA를 사용할 수 있도록 합니다.

### Adobe I/O Events 설치 및 customer-connector 모듈 구성

`experience-platform-connector` 확장을 설치한 후 Adobe Commerce용 Adobe I/O Events을 설치하고 `customers-connector` 모듈을 구성해야 합니다.

다음 단계는 Adobe Commerce on cloud infrastructure 및 온프레미스 설치 모두에 적용됩니다.

1. Commerce 2.4.4 또는 2.4.5를 실행하는 경우 다음 명령을 사용하여 이벤트 모듈을 로드합니다.

   ```bash
   composer require magento/commerce-eventing=^1.0 --no-update
   ```

   Commerce 2.4.6 이상 버전은 이러한 모듈을 자동으로 로드합니다.

1. 프로젝트 종속성을 업데이트합니다.

   ```bash
   composer update
   ```

1. 새 모듈 활성화:

   ```bash
   bin/magento module:enable Magento_AdobeCommerceEventsClient Magento_AdobeCommerceEventsGenerator Magento_AdobeIoEventsClient Magento_AdobeCommerceOutOfProcessExtensibility
   ```

배포 유형(Adobe Commerce on Cloud 인프라 또는 온프레미스)을 기반으로 설치를 완료합니다.

#### 클라우드 인프라

클라우드 인프라의 Adobe Commerce에서 `.magento.env.yaml`에서 `ENABLE_EVENTING` 전역 변수를 사용하도록 설정합니다. [자세히 알아보기](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-global.html?lang=ko#enable_eventing).

```bash
stage:
   global:
      ENABLE_EVENTING: true
```

업데이트된 파일을 커밋하고 클라우드 환경으로 푸시합니다. 배포가 완료되면 다음 명령을 사용하여 이벤트 전송을 활성화합니다.

```bash
bin/magento config:set adobe_io_events/eventing/enabled 1
```

#### 온-프레미스

온-프레미스 환경에서 코드 생성 및 Adobe Commerce 이벤트를 수동으로 활성화해야 합니다.

```bash
bin/magento events:generate:module
bin/magento module:enable Magento_AdobeCommerceEvents
bin/magento setup:upgrade
bin/magento setup:di:compile
bin/magento config:set adobe_io_events/eventing/enabled 1
```

### B2B 확장 설치

B2B 판매자의 경우 [구매요청 목록](events.md#b2b-events) 이벤트 데이터를 포함하도록 다음 확장을 설치하십시오.

명령줄에서 다음을 실행하여 `magento/experience-platform-connector-b2b` 확장을 다운로드합니다.

```bash
composer require magento/experience-platform-connector-b2b
```

### 데이터 서비스 HIPAA 확장 설치

의료 서비스 판매자의 경우 다음 확장을 설치하여 백오피스 이벤트 데이터가 HIPAA에 대비되도록 합니다.

명령줄에서 다음을 실행하여 `magento/module-data-services-hipaa` 확장을 다운로드합니다.

```bash
composer require magento/module-data-services-hipaa
```

## [!DNL Data Connection] 확장 업데이트 {#update}

[!DNL Data Connection] 확장을 업데이트하려면 명령줄에서 다음을 실행하십시오.

```bash
composer update magento/experience-platform-connector --with-dependencies
```

또는 B2B 판매자의 경우:

```bash
composer update magento/experience-platform-connector-b2b --with-dependencies
```

2.0.0에서 3.0.0으로 등 주요 버전으로 업데이트하려면 다음과 같이 프로젝트의 루트 [!DNL Composer] `.json` 파일을 편집하십시오.

1. 루트 `composer.json` 파일을 열고 `magento/experience-platform-connector`을(를) 검색합니다.

1. `require` 섹션에서 버전 번호를 다음과 같이 업데이트합니다.

   ```json
   "require": {
      ...
      "magento/experience-platform-connector": "^3.0",
      ...
    }
   ```

1. **저장** `composer.json`. 그런 다음 명령줄에서 다음을 실행합니다.

   ```bash
   composer update magento/experience-platform-connector –-with-dependencies
   ```

   또는 B2B 판매자의 경우:

   ```bash
   composer update magento/experience-platform-connector-b2b --with-dependencies
   ```

## [!DNL Data Connection] 확장 제거 {#uninstall}

[!DNL Data Connection] 확장을 제거하려면 [제거 모듈](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/tutorials/uninstall-modules.html?lang=ko)을 참조하세요.
