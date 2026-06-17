---
title: '[!DNL Manage the Data Export extension]'
description: ' [!DNL Data Export] 확장을 업그레이드하고 필요하지 않은 데이터 내보내기 서비스를 제거하거나 사용하지 않도록 설정하는 방법을 알아봅니다.'
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
exl-id: 94702995-d272-47b9-9560-198eee3250a6
TQID: https://experienceleague.adobe.com/ghrA-YFR7hurQgEnjS8PdxR7Zcx-ayLTuyBfhbCC-KI
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: d3cdead0-685a-4489-9250-4bb709942f66
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 312
ht-degree: 0%

---

# SaaS 데이터 내보내기 확장 관리

SaaS 서비스용 [[!DNL data export] 확장](https://github.com/magento/commerce-data-export)은(는) Adobe Commerce과 연결된 Commerce 서비스 간의 데이터 수집 및 동기화를 가능하게 하는 모듈의 컬렉션입니다.

특정 모듈은 다음과 같은 Adobe Commerce 서비스 확장의 메타패키지에 포함되어 있습니다
[실시간 검색](/help/live-search/overview.md), [제품 추천](/help/product-recommendations/overview.md), [카탈로그 서비스](/help/catalog-service/overview.md) 및 [[!DNL Adobe Commerce Optimizer Connector]](/help/aco-connector/overview.md). 이러한 서비스를 사용하는 경우 데이터 내보내기 확장을 활성화하기 위해 별도의 설치가 필요하지 않습니다.

## Commerce 데이터 내보내기 기능 제거 또는 비활성화

설치된 상거래 데이터 내보내기 모듈 중 하나가 필요하지 않으면 `magento:module:disable` CLI 명령을 사용하여 사용하지 않도록 설정하십시오.

예를 들어 내부적으로 범주 권한 피드 데이터를 사용하는 [범주 API](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/)가 있습니다. 이 API를 사용하지 않는 경우 카테고리 권한 피드에 대한 데이터 내보내기를 비활성화할 수 있습니다.

```shell
bin/magento module:disable Magento_CategoryPermissionDataExporter Magento_SaaSCategoryPermissions
```

### 특정 버전으로 모듈 업데이트

작성기를 사용하여 설치된 상거래 데이터 내보내기 모듈을 업데이트할 수 있습니다. [릴리스 정보](release-notes.md)를 검토하여 필요한 수정 사항을 사용할 수 있는지 확인한 다음 해당 특정 버전 및 필요한 종속성으로 업그레이드하십시오.

>[!NOTE]
>
>최신 버전의 [Live Search](/help/live-search/overview.md), [카탈로그 서비스](/help/catalog-service/overview.md), [제품 권장 사항](/help/product-recommendations/overview.md) 또는 [[!DNL Adobe Commerce Optimizer Connector]](/help/aco-connector/overview.md)(으)로 업데이트하면 최신 버전의 데이터 내보내기 확장도 제공됩니다. 데이터 내보내기 메타패키지는 이러한 서비스에 대한 Composer 패키지의 종속입니다.

1. Commerce 애플리케이션 서버에 로그인합니다.

1. 명령줄에서 Composer를 사용하여 모듈을 업데이트합니다.

   ```bash
   composer require magento/module-data-exporter:103.0.4 --with-all-dependencies
   ```

Commerce 인스턴스가 클라우드 인프라에 배포된 경우 클라우드 프로젝트 디렉터리에서 확장을 업데이트합니다. _Adobe Commerce on Cloud Infrastructure Guide_&#x200B;에서 [확장 업그레이드](https://experienceleague.adobe.com/ko/docs/commerce-cloud-service/user-guide/configure-store/extensions#upgrade-an-extension)를 참조하십시오.

>[!MORELIKETHIS]
>
> - [릴리스 정보](release-notes.md)
> - [SaaS 데이터 내보내기 모듈](reference/data-export-modules.md)
> - [안내서 개요](overview.md)
