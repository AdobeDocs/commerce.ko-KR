---
title: ' [!DNL SaaS Data Export]에 대한 시나리오 문제 해결'
description: 구성 오류, 인덱서 설정 오류 또는 동기화 결과 오독으로 인해 예기치 않은 [!DNL SaaS Data Export] 동기화 동작을 진단하고 해결하는 방법에 대해 알아봅니다.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="PaaS만" type="Informative" url="https://experienceleague.adobe.com/ko/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce 온 클라우드 프로젝트(Adobe 관리 PaaS 인프라) 및 온프레미스 프로젝트에만 적용됩니다."
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
subfeature_v2:
  - id: a40ebd6b-b542-4432-a730-1803ef74518d
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 991
ht-degree: 0%

---


# [!DNL SaaS Data Export]에 대한 시나리오 문제 해결

이 페이지에서는 [!DNL SaaS Data Export] 작업을 수행할 때 일반적으로 잘못된 구성 또는 동기화 결과 해석으로 인해 발생할 수 있는 동작을 설명합니다. 아래 설명을 사용하여 근본 원인을 식별하고 적절한 해결 방법을 적용하십시오.

## Commerce 서비스에서 구성 가능 또는 번들 제품 누락 {#configurable-bundle-missing}

**문제:** 구성 가능한 또는 번들 제품의 상태가 [!DNL Adobe Commerce]이지만 상점 앞에서 반환되지 않거나 Commerce SaaS 서비스에서 *사용 안 함* 상태로 표시됩니다.**

**원인:** 복합 제품의 유효 상태는 상위 제품 상태뿐만 아니라 하위 제품의 상태에 따라 다릅니다. Commerce SaaS 서비스는 다음과 같은 계산된 상태를 반영합니다.

- **구성 가능한 제품** - 하나 이상의 제품 변형을 사용하도록 설정해야 합니다.
- **제품 번들** - 각 필수 번들 옵션에 대해 하나 이상의 제품을 활성화해야 합니다.

이러한 조건이 충족되지 않으면 상위 제품이 자신의 상태가 *사용 가능*(으)로 설정되어 있어도 사용하지 않는 것으로 처리됩니다.

**솔루션:**

- 구성 가능한 제품의 경우, 하나 이상의 관련 단순 제품 변형이 활성화되어 있고 올바른 웹 사이트 및 스토어 보기에 할당되어 있는지 확인하십시오.
- 번들 제품의 경우 각 필수 번들 옵션에 하나 이상의 활성화된 하위 제품이 있는지 확인합니다. 모든 장애가 있는 소아가 있는 필수 옵션을 사용하면 전체 번들이 장애인으로 취급됩니다.
- 적절한 하위 제품을 활성화한 후 다시 동기화를 트리거하거나 예약된 다음 동기화를 기다린 다음 Commerce SaaS 서비스에서 업데이트된 상태를 확인합니다.

## 카탈로그 가격 규칙 활성화 후 가격이 업데이트되지 않음 {#prices-not-updated}

**문제:** 업데이트 예약 기능을 사용하여 카탈로그 가격 규칙을 활성화한 후 가격이 업데이트되지 않습니다. 예약된 업데이트가 적용된 후 `commerce-data-export.log`에 `prices` 피드에 대한 `synced: 0`이(가) 표시됩니다.

**원인:** 카탈로그 가격 규칙에 예약된 업데이트를 사용할 때 크론 그룹 간에 경합 조건이 발생할 수 있습니다. `catalog_data_exporter_product_prices` 인덱서는 해당 종속인 `catalogrule_product` 인덱스의 다시 작성을 완료하기 전에 실행될 수 있습니다. 그 결과 가격 익스포터가 오래된 데이터를 읽고 변경 사항을 내보냅니다.

**솔루션:**

이 문제에 대한 즉각적인 수정 사항은 해결 방법입니다. 경쟁 조건을 제거하기 위해 순차적으로 실행되도록 두 cron 그룹을 모두 구성합니다.

1. **[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL Advanced]** > **[!UICONTROL System]** > **[!UICONTROL Cron (Scheduled Tasks)]**(으)로 이동합니다.
1. 두 항목에 대해 **[!UICONTROL Use Separate Process]**&#x200B;을(를) **[!UICONTROL No]**(으)로 설정:
   - 그룹에 대한 크론 구성 옵션: **[!UICONTROL index]**
   - 그룹에 대한 크론 구성 옵션: **[!UICONTROL staging]**
1. 저장한 후 구성 캐시를 플러시합니다.

>[!NOTE]
>
>두 그룹이 모두 처리 중 및 순차적으로 실행되는 경우 느린 전체 색인 재지정은 완료될 때까지 스테이징 실행을 차단합니다. 대규모 카탈로그의 경우 이로 인해 스테이징 업데이트가 지연될 수 있습니다.

## [!DNL Adobe Commerce]과(와) 연결된 서비스 간의 카탈로그 데이터 불일치 {#catalog-data-discrepancy}

**문제:** 연결된 Commerce 서비스에 표시된 제품 데이터(예: [!DNL Live Search] 또는 [!DNL Product Recommendations])가 [!DNL Adobe Commerce]의 카탈로그 데이터와 일치하지 않습니다. 예를 들어, 제품 이름, 가격 또는 설명이 상점 앞에 오래되거나 올바르지 않은 것으로 나타납니다.

**원인:** 재동기화가 트리거된 후 데이터를 업데이트하고 UI 구성 요소에 반영되기까지 최대 한 시간이 걸릴 수 있습니다. 불일치가 해당 창 이상으로 지속되면 마지막 동기화에서 항목을 선택하지 않았거나 피드 데이터가 이미 최신 상태로 표시되었기 때문에 동기화에서 변경 사항을 감지하지 못했을 수 있습니다.

**솔루션:**

1. Commerce 상점에서 검색 결과를 엽니다. 그런 다음 해당 제품을 선택하여 세부 보기를 엽니다.
1. JSON 출력을 복사하고 [!DNL Commerce] 카탈로그에 있는 것과 일치하는지 확인합니다.
1. 콘텐츠가 일치하지 않으면 공백 또는 마침표 추가와 같이, 카탈로그의 제품에 대한 부분 편집을 수행하여 변경 사항을 감지하도록 합니다.
1. 재동기화를 기다리거나 CLI 또는 관리자의 [[!UICONTROL Data Feed Sync Status]](https://experienceleague.adobe.com/ko/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status) 페이지에서 수동 재동기화를 트리거하십시오.

[!DNL Product Recommendations]의 카탈로그 데이터 문제 해결에 대한 자세한 내용은 Commerce 기술 자료에서 [제품 권장 사항 모듈 문제 해결](https://experienceleague.adobe.com/ko/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/troubleshoot-product-recommendations-module-in-magento-commerce)을 참조하세요.

## 데이터 동기화가 일정에 따라 실행되고 있지 않음 {#sync-not-on-schedule}

**문제:** 데이터 동기화가 일정에 따라 실행되지 않거나 [!DNL Adobe Commerce]의 제품 변경 사항에도 불구하고 동기화되는 항목이 없습니다.

**원인:** 크론 작업이 실행되지 않거나 인덱서가 **[!UICONTROL Update by Schedule]** 모드에서 구성되지 않은 것이 가장 일반적인 원인입니다.

**솔루션:**

- [cron 작업이 실행 중인지 확인](https://experienceleague.adobe.com/ko/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-readiness-check-issues).
- 카탈로그 특성, Product, Product Overrides 및 Product Variant 피드의 인덱서가 **[!UICONTROL Update by Schedule]**(으)로 설정되어 있는지 확인하십시오. Commerce 관리자 또는 CLI를 사용하여 [[!UICONTROL Index Management]](https://experienceleague.adobe.com/ko/docs/commerce-admin/systems/tools/index-management)에서 확인하십시오. `bin/magento indexer:show-mode | grep -i feed`.

## 카탈로그 동기화가 실패 상태입니다. {#catalog-sync-failed}

**문제:** 카탈로그 동기화가 **[!UICONTROL Data Feed Sync Status]** 페이지에서 **실패** 상태를 표시합니다.

**원인:** 데이터 수집 또는 제출 단계에서 복구할 수 없는 오류가 발생했습니다. 일반적인 원인에는 API 인증 문제, 네트워크 오류 또는 데이터 유효성 검사 오류가 포함됩니다.

**솔루션:**

1. 오류에 대한 자세한 내용은 데이터 내보내기 오류 로그를 검토하십시오. 로그 형식 및 확장 로깅 옵션에 대해서는 [로그 검토 및 문제 해결](logging.md)을 참조하십시오.
   - 데이터를 수집하는 동안 오류가 발생한 경우 `var/log/commerce-data-export-errors.log`.
   - 데이터를 제출하는 동안 오류가 발생한 경우 `var/log/saas-export-errors.log`.
1. 오류가 구성 또는 타사 확장과 관련이 없는 경우 관련 로그 항목을 사용하여 [지원 티켓을 제출](https://experienceleague.adobe.com/ko/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket)하십시오.

## 로그에 &quot;작업 건너뜀 - 프로세스 잠김&quot; 메시지가 표시됨 {#process-locked}

**문제:** `commerce-data-export.log` 파일에 다음과 유사한 항목이 있습니다.

```json
{"feed":"products","operation":"partial sync","status":"operation skipped - process locked by \"full sync(1234)\"", ...}
```

**원인:** 이는 오류가 아닌 예상된 동작입니다. 이 메시지는 전체 색인 재지정 또는 `saas:resync`이(가) 이미 진행 중인 상태에서 크론 트리거된 부분 동기화를 실행하려고 할 때 나타납니다. [!DNL SaaS Data Export] 확장은 피드 잠금 메커니즘을 사용하여 충돌하는 동시 동기화 작업을 방지합니다.

**솔루션:**

별도의 작업이 필요하지 않습니다. 실행 중인 프로세스가 완료되고 잠금이 해제되면 다음 cron 실행에서 보류 중인 모든 변경 사항을 선택하고 동기화합니다. 잠금 메커니즘의 작동 방식에 대한 자세한 내용은 [SaaS 데이터 내보내기를 위한 피드 잠금 메커니즘](../feed-lock-mechanism.md)을 참조하십시오.

>[!MORELIKETHIS]
>
> - [로그 검토 및 문제 해결](logging.md)
> - [로그 코드 참조](log-codes-reference.md)
> - [SaaS 데이터 내보내기를 위한 피드 잠금 메커니즘](../feed-lock-mechanism.md)
