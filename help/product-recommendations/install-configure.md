---
title: 설치 및 구성
description: ' [!DNL Product Recommendations]을(를) 설치, 업데이트 및 제거하는 방법을 알아봅니다.'
role: Admin, Developer
exl-id: 2e7f6454-d4cb-44bc-982f-354a179e8e59
source-git-commit: 3821893c3df01e2e36ab0142616e52c1c92b4d51
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# 설치 및 구성

상점 및 관리자에 [!DNL Product Recommendations]을(를) 배포하려면 모듈을 설치하고 [Commerce 서비스 커넥터](../landing/saas.md)를 구성해야 합니다. 업데이트가 릴리스되면 설치를 최신 버전으로 쉽게 업데이트할 수 있습니다.

- [설치](#install)
- [구성](#configure)
- [업데이트](#update)
- [제거](#uninstall)

## [!DNL Product Recommendations] 설치 {#install}

[!DNL Product Recommendations] 모듈은 독립 실행형 메타패키지이므로 Adobe Commerce보다 업데이트가 더 자주 릴리스됩니다. 최신 버그 수정 및 기능을 확인하려면 [릴리스 정보](release-notes.md)를 참조하세요.

>[!IMPORTANT]
>
>제품 추천을 사용할 올바른 [자격](../landing/saas.md#credentials)이 있는지 확인하십시오.

작성기를 사용하여 `magento/product-recommendations` 모듈 설치:

```bash
composer require magento/product-recommendations
```

### 페이지 빌더 지원 추가 {#pbsupport}

Page Builder용 [!DNL Product Recommendations]은(는) 선택적 모듈이며 별도로 설치됩니다. 페이지 빌더와 함께 [!DNL Product Recommendations]을(를) 사용하려면 다음 명령을 실행하여 모듈을 설치하십시오.

```bash
composer require magento/module-page-builder-product-recommendations
```

페이지 빌더에서 [!DNL Product Recommendations]을(를) 활성화하면 페이지, 블록 및 동적 블록과 같이 페이지 빌더에서 만든 모든 콘텐츠에 기존의 활성 [추천 단위](https://experienceleague.adobe.com/en/docs/commerce-admin/page-builder/add-content/recommendations)를 추가할 수 있습니다.

자세한 지침은 [페이지 빌더 콘텐츠로 사용 [!DNL Product Recommendations] 을 참조하세요](page-builder.md).

### 시각적 유사성 추천 유형 추가 {#vissimsupport}

_시각적 유사성_ 권장 사항 유형을 사용하면 보고 있는 제품과 [시각적으로 유사한](type.md#visualsim) 제품을 표시하는 제품 세부 정보 페이지에 권장 사항 단위를 배포할 수 있습니다. 이 권장 사항 유형은 제품의 이미지와 시각적 측면이 쇼핑 경험의 중요한 부분인 경우 가장 유용합니다. 다음 명령을 실행하여 _시각적 유사성_ 권장 사항 유형을 설치하십시오.

```bash
composer require magento/module-visual-product-recommendations
```

## [!DNL Product Recommendations] 구성 {#configure}

1. `magento/product-recommendations` 모듈을 설치한 후 API 키를 지정하고 SaaS 데이터 공간을 선택하여 [Commerce 서비스 커넥터](../landing/saas.md)를 구성하십시오.

   이 연결을 구성하면 Commerce 인스턴스, 카탈로그 서비스 및 기타 지원 서비스 간에 데이터를 동기화하고 통신할 수 있습니다. 데이터 동기화는 [SaaS 데이터 내보내기 확장](../data-export/overview.md)에서 처리됩니다.

1. 카탈로그 내보내기가 올바르게 실행되도록 하려면 [cron](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs) 작업과 [인덱서](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/manage-indexers)가 실행 중이며 `Product Feed` 인덱서가 `Update by Schedule`(으)로 설정되어 있는지 확인하십시오.

Commerce 응용 프로그램을 Commerce 서비스에 연결하고 [SaaS 데이터 공간](../landing/saas.md#saas-configuration)을 지정하면 카탈로그 동기화가 시작됩니다. 그런 다음 동작 데이터가 상점 앞으로 전송되고 있는지 [확인](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/verify/)할 수 있습니다.

## 데이터 동기화 모니터링 및 문제 해결

Commerce 관리에서 [데이터 관리 대시보드](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard)를 사용하여 동기화 프로세스를 모니터링할 수 있습니다. [Commerce CLI](../data-export/data-export-cli-commands.md#troubleshooting) 및 로그를 사용하여 프로세스를 관리하고 문제를 해결하십시오.

그런 다음 동작 데이터가 상점 앞으로 전송되고 있는지 [확인](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/verify/)할 수 있습니다.

## [!DNL Product Recommendations] 설치 업데이트 {#update}

모든 Adobe Commerce과 마찬가지로 [!DNL Product Recommendations]도 설치 및 업데이트를 위해 작성기를 사용합니다. `magento/product-recommendations` 모듈을 업데이트하려면 다음을 실행하십시오.

```bash
composer update magento/product-recommendations --with-dependencies
```

5.0에서 6.0으로 등 주요 버전으로 업데이트하려면 프로젝트의 루트 `composer.json` 파일을 편집해야 합니다. 최신 버전에 대한 정보는 [릴리스 정보](release-notes.md)를 참조하세요. 예를 들어 기본 `composer.json` 파일을 열고 `magento/product-recommendations` 모듈을 검색해 보겠습니다.

```json
"require": {
    ...
    "magento/product-recommendations": "^5.0",
    ...
}
```

주요 버전을 `5.0`에서 `6.0`(으)로 변경해 보겠습니다.

```json
"require": {
    ...
    "magento/product-recommendations": "^6.0",
    ...
}
```

`composer.json` 파일을 저장하고 다음을 실행합니다.

```bash
composer update magento/product-recommendations --with-dependencies
```

또는 `magento/module-visual-product-recommendations` 및 `magento/module-page-builder-product-recommendations` 모듈을 설치한 경우:

```bash
composer update --with-dependencies magento/product-recommendations magento/module-visual-product-recommendations magento/module-page-builder-product-recommendations
```

>[!NOTE]
>
> 제품 권장 사항 버전 3.x.x에서는 단일 API 키만 있으면 됩니다. 버전 4.x.x 이상에서는 샌드박스와 프로덕션 환경 모두에 공개 및 비공개 API 키를 제공해야 합니다. 두 쌍의 API 키를 모두 제공하지 않으면 관리자에서 제품 권장 사항 기능에 액세스할 수 없습니다. 그러나 데이터 수집은 상점 전면에서 계속되고 기존 권장 사항은 계속해서 쇼핑객에게 표시됩니다.

## 방화벽

방화벽을 통해 제품 권장 사항을 허용하려면 `commerce.adobe.io`을(를) 허용 목록에 추가하십시오.

## [!DNL Product Recommendations] 제거 {#uninstall}

필요한 경우 제품 권장 사항 모듈을 [제거](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/uninstall-modules)할 수 있습니다.
