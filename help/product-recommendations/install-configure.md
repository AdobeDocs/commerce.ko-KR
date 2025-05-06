---
title: 설치 및 구성
description: ' [!DNL Product Recommendations]을(를) 설치, 업데이트 및 제거하는 방법을 알아봅니다.'
role: Admin, Developer
exl-id: 2e7f6454-d4cb-44bc-982f-354a179e8e59
badgePaas: label="PaaS만" type="Informative" url="https://experienceleague.adobe.com/ko/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce 온 클라우드 프로젝트(Adobe 관리 PaaS 인프라) 및 온프레미스 프로젝트에만 적용됩니다."
source-git-commit: be1c739f3821a5f1e846b3026088e3a3ff45a60f
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 0%

---

# 설치 및 구성

Deploying [!DNL Product Recommendations] to your storefront and Admin requires that you install the module and configure the [Commerce Services Connector](../landing/saas.md). As updates are released, you can easily update the installation with the latest version.

- [설치](#install)
- [구성](#configure)
- [업데이트](#update)
- [제거](#uninstall)

## [!DNL Product Recommendations] 설치 {#install}

Because the [!DNL Product Recommendations] module is a stand-alone metapackage, updates are released more frequently than Adobe Commerce. 최신 버그 수정 및 기능을 확인하려면 [릴리스 정보](release-notes.md)를 참조하세요.

>[!IMPORTANT]
>
>Make sure you have the correct [entitlements](../landing/saas.md#credentials) to use Product Recommendations.

Install the `magento/product-recommendations` module with Composer:

```bash
composer require magento/product-recommendations
```

### 페이지 빌더 지원 추가 {#pbsupport}

Page Builder용 [!DNL Product Recommendations]은(는) 선택적 모듈이며 별도로 설치됩니다. 페이지 빌더와 함께 [!DNL Product Recommendations]을(를) 사용하려면 다음 명령을 실행하여 모듈을 설치하십시오.

```bash
composer require magento/module-page-builder-product-recommendations
```

페이지 빌더에서 [!DNL Product Recommendations]을(를) 활성화하면 페이지, 블록 및 동적 블록과 같이 페이지 빌더에서 만든 모든 콘텐츠에 기존의 활성 [추천 단위](https://experienceleague.adobe.com/ko/docs/commerce-admin/page-builder/add-content/recommendations)를 추가할 수 있습니다.

자세한 지침은 [페이지 빌더 콘텐츠로 사용 [!DNL Product Recommendations] 을 참조하세요](page-builder.md).

### 시각적 유사성 추천 유형 추가 {#vissimsupport}

_시각적 유사성_ 권장 사항 유형을 사용하면 보고 있는 제품과 [시각적으로 유사한](type.md#visualsim) 제품을 표시하는 제품 세부 정보 페이지에 권장 사항 단위를 배포할 수 있습니다. 이 권장 사항 유형은 제품의 이미지와 시각적 측면이 쇼핑 경험의 중요한 부분인 경우 가장 유용합니다. 다음 명령을 실행하여 _시각적 유사성_ 권장 사항 유형을 설치하십시오.

```bash
composer require magento/module-visual-product-recommendations
```

## [!DNL Product Recommendations] 구성 {#configure}

1. `magento/product-recommendations` 모듈을 설치한 후 API 키를 지정하고 SaaS 데이터 공간을 선택하여 [Commerce 서비스 커넥터](../landing/saas.md)를 구성하십시오.

   이 연결을 구성하면 Commerce 인스턴스, 카탈로그 서비스 및 기타 지원 서비스 간에 데이터를 동기화하고 통신할 수 있습니다. 데이터 동기화는 [SaaS 데이터 내보내기 확장](../data-export/overview.md)에서 처리됩니다.

1. To ensure that catalog export can run correctly, confirm that the [cron](https://experienceleague.adobe.com/ko/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs) jobs and the [indexers](https://experienceleague.adobe.com/ko/docs/commerce-operations/configuration-guide/cli/manage-indexers) are running and the `Product Feed` indexer is set to `Update by Schedule`.

After you successfully link the Commerce application to Commerce Services and specify the [SaaS Data Space](../landing/saas.md#saas-configuration), the catalog sync begins. You can then [verify](verify.md) that behavioral data is being sent to your storefront.

## Monitor and troubleshoot data synchronization

From the Commerce Admin, you can monitor the synchronization process using the [Data Management Dashboard](https://experienceleague.adobe.com/ko/docs/commerce-admin/systems/data-transfer/data-dashboard). Use the [Commerce CLI](../data-export/data-export-cli-commands.md#troubleshooting) and logs to manage and troubleshoot the process.

You can then [verify](verify.md) that behavioral data is being sent to your storefront.

## Update your [!DNL Product Recommendations] installation {#update}

Like all of Adobe Commerce, [!DNL Product Recommendations] uses Composer for installation and updates. `magento/product-recommendations` 모듈을 업데이트하려면 다음을 실행하십시오.

```bash
composer update magento/product-recommendations --with-dependencies
```

To update to a major version, such as from 5.0 to 6.0, you must edit the root `composer.json` file for your project. (See the [release notes](release-notes.md) for information about the latest version.) For example, let&#39;s open the main `composer.json` file and search for the `magento/product-recommendations` module:

```json
"require": {
    ...
    "magento/product-recommendations": "^5.0",
    ...
}
```

Let&#39;s bump the major version from `5.0` to `6.0`:

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

## Uninstall [!DNL Product Recommendations] {#uninstall}

If necessary, you can [uninstall](https://experienceleague.adobe.com/ko/docs/commerce-operations/installation-guide/tutorials/uninstall-modules) the product-recommendations module.
