---
title: B2B 공유 카탈로그에 대한 카탈로그 보기 동기화 모니터링
last-update: 2026-09-03
description: '[카탈로그 뷰 동기화 상태] 페이지에서는 Adobe Commerce Optimizer에 동기화된 카탈로그 뷰, 정책, 가격 장부 참조 및 주요 구성 데이터를 모니터링하고 조정할 수 있습니다.'
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="PaaS만" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce 온 클라우드 프로젝트(Adobe 관리 PaaS 인프라) 및 온프레미스 프로젝트에만 적용됩니다."
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
    internal-label: Admin tools and workspace
subfeature_v2:
  - id: a40ebd6b-b542-4432-a730-1803ef74518d
    internal-label: Data Transfer
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
    internal-label: Data management
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
source-git-commit: 1fd5e3d84d5249ce96014cae46e045528d2790d0
workflow-type: tm+mt
source-wordcount: '1046'
ht-degree: 0%
---

# B2B 공유 카탈로그에 대한 카탈로그 보기 동기화 모니터링

Commerce 관리자의 [!UICONTROL Catalog View Sync Status] 대시보드를 사용하여 [!DNL Adobe Commerce]에서 [!DNL Adobe Commerce Optimizer]&#x200B;(으)로의 B2B 카탈로그 보기 동기화를 추적합니다.

[!UICONTROL Catalog View Sync Status]은(는) 각 B2B 공유 카탈로그에 대한 카탈로그 보기, 정책, 가격 장부 참조 및 제한된 액세스 키 구성이 [!DNL Adobe Commerce Optimizer]에 있으며 [!DNL Adobe Commerce] 구성과 일치하는지 확인합니다. 대신 제품, 가격 및 범주 피드 동기화를 추적하려면 [데이터 동기화 관리](data-sync-status.md#verify-that-the-data-sync-is-working)를 참조하십시오.

## 동기화 상태 페이지에 액세스 {#access-the-sync-status-page}

Commerce 관리자에서 **[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Catalog View Sync Status]**(으)로 이동합니다.

![Adobe Commerce Optimizer에서 카탈로그 보기, 정책, 가격표 및 액세스 키 구성의 동기화 상태를 모니터링하는 카탈로그 보기 동기화 상태 보기 페이지](assets/catalog-view-sync-status.png){width="600" zoomable="yes"}

페이지에는 [!UICONTROL Catalog Views], [!UICONTROL Orphaned in ACO] 및 [!UICONTROL Deleted]의 세 가지 탭이 있습니다.

## 공유 카탈로그의 동기화 상태 해석 {#interpret-sync-status}

[!UICONTROL Catalog View] 탭에서 각 행은 공유 카탈로그 및 저장소 보기 조합에서 예상한 하나의 사용자 지정 공유 카탈로그 보기를 나타냅니다. 예상 값은 [!DNL Commerce Optimizer Connector]이(가) 공유 카탈로그의 [!DNL Adobe Commerce Optimizer]&#x200B;(으)로 내보내는 카탈로그 보기, 정책, 가격 장부 참조 및 제한된 액세스 키 구성 데이터입니다. 상태 정보를 사용하여 회사의 상점 경험에 전달된 데이터가 완전하고 올바른지 확인하십시오. 다음 표에는 가장 일반적인 상태 값과 공유 카탈로그의 의미가 요약되어 있습니다.

| 상태 | 공유 카탈로그에 대한 의미 |
| --- | --- |
| **성능 저하** | [!DNL Adobe Commerce Optimizer]에서 정책 또는 연결된 가격 장부와 같은 항목이 직접 변경되었습니다. 귀하가 문제를 해결할 때까지 회사는 잘못된 분류나 가격을 볼 수 있습니다. Commerce Optimizer에서 액세스 키, 보기 이름 또는 소스를 변경하면 이러한 문제가 발생할 수도 있습니다. |
| **실패** | 카탈로그 보기가 [!DNL Adobe Commerce Optimizer]에 없거나, 첫 번째 프로젝션이 수행되기 전에 유예 기간이 지난 경우. ([ACO 카탈로그 보기 동기화 설정 구성](#configure-aco-catalog-view-sync-settings)을 참조하십시오.) 카탈로그 동기화 상태가 `Failed`인 경우 회사에서 이 공유 카탈로그의 상점 환경 액세스할 수 없습니다. |
| **중단** | [!DNL Adobe Commerce]에서 공유 카탈로그를 삭제했습니다. 삭제 유예 기간이 만료될 때까지 카탈로그 보기에 계속 액세스할 수 있습니다. 기본 유예 기간은 7일입니다. [카탈로그 보기 동기화 설정](#configure-aco-catalog-view-sync-settings)을 업데이트하여 기본값을 수정할 수 있습니다. |
| **고립됨** | 카탈로그 보기 또는 키가 커넥터가 아닌 [!DNL Adobe Commerce Optimizer] Studio에서 직접 만들어졌습니다. [고립되거나 삭제된 항목 검토](#review-orphaned-and-deleted-entries)를 참조하세요. |

[!UICONTROL Healthy], [!UICONTROL Pending] 및 [!UICONTROL Deleted]은(는) 동작이 필요하지 않은 정보 상태입니다. 전체 목록은 *Commerce 관리 가이드*&#x200B;의 [동기화 상태 값](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/catalog-view-sync/catalog-view-sync-status#sync-status-values){target="_blank"}을 참조하십시오.

### ACO 카탈로그 보기 동기화 설정 구성 {#configure-aco-catalog-view-sync-settings}

[!DNL Adobe Commerce] 관리자([!DNL Adobe Commerce Optimizer] Studio 아님)에서 **[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL Services]** > **[!UICONTROL ACO Catalog View Sync]**(으)로 이동하여 커넥터가 삭제 및 생성 시간을 초과하고 복구되는지 여부를 자동으로 제어합니다.

![삭제, 만들기 및 드리프트 조정자 섹션을 보여 주는 ACO 카탈로그 동기화 구성 보기 페이지](assets/aco-catalog-view-sync-configuration.png){width="600" zoomable="yes"}

- **[!UICONTROL Deletion Grace Period (days)]** - 삭제된 공유 카탈로그의 카탈로그 보기, 정책 및 메타데이터가 제거되기 전에 [!DNL Adobe Commerce Optimizer]에 유지되는 일 수입니다. 기본값은 7일입니다. 유예 기간 없이 프로젝션을 즉시 제거하려면 `0`(으)로 설정하십시오.

- **[!UICONTROL Creation Grace Period (days)]**—새로 등록된 카탈로그 보기가 [!UICONTROL Pending]&#x200B;(으)로 보고되는 동안 [!DNL Adobe Commerce Optimizer]에 대한 첫 프로젝션을 기다릴 수 있는 일 수입니다. 유예 기간이 프로젝션 없이 경과하면 상태는 [!UICONTROL Failed]이(가) 됩니다. 기본값은 1입니다.

- **[!UICONTROL Enabled]**(드리프트 조정자) - [!DNL Adobe Commerce Optimizer]을(를) [!DNL Adobe Commerce] 투영 상태와 비교하고 복구 또는 보고서 발산을 보고하는 예약된 드리프트 조정자를 실행합니다.

- **[!UICONTROL Automatically Repair Drift]** - **[!UICONTROL Yes]**(으)로 설정하면 예약된 실행이 복구 가능한 드리프트를 위해 [!DNL Adobe Commerce Optimizer]을(를) [!DNL Adobe Commerce]&#x200B;(으)로 다시 수렴합니다. **[!UICONTROL No]**(으)로 설정된 경우 예약된 실행은 드리프트만 감지하고 기록합니다. 분리된 항목은 항상 보고되며 자동으로 제거되지 않습니다. 이 설정은 예약된 조정자에만 영향을 줍니다. 이 페이지의 **[!UICONTROL Reconcile & Repair]** 작업은 항상 복구됩니다. [모니터링 또는 복구 선택](#choose-monitoring-or-repair)을 참조하세요.

각 설정에 대한 자세한 내용은 *[!DNL Commerce Admin]안내서*&#x200B;의 [ACO 카탈로그 동기화 보기 구성](https://experienceleague.adobe.com/en/docs/commerce-admin/configuration-reference/services/aco-catalog-view-sync.md)을 참조하십시오.

## 모니터링 또는 복구 선택 {#choose-monitoring-or-repair}

[!DNL Adobe Commerce]은(는) B2B 공유 카탈로그에 대한 카탈로그 보기, 정책, 가격 장부 및 주요 구성에 대한 신뢰할 수 있는 원본입니다. 귀하 또는 다른 관리자가 [!DNL Adobe Commerce Optimizer] Studio에서 직접 정책, 가격 장부 또는 주요 구성 설정을 변경한 경우 조정에서 구성 차이점을 드리프트로 보고합니다.

- **[!UICONTROL Reconcile]**&#x200B;을(를) 선택하여 아무 것도 변경하지 않고 드리프트를 확인합니다. 그러면 작업을 수행하기 전에 차이점을 검토할 수 있습니다.
- **[!UICONTROL Reconcile & Repair]**&#x200B;을(를) 선택하여 복구 가능한 드리프트에 대한 예상 구성을 복원합니다.

변경 사항 및 이유를 검토하려면 카탈로그 보기의 세부 사항 페이지를 열고 드리프트 내역을 확인합니다.

## 분리된 항목 및 삭제된 항목 검토 {#review-orphaned-and-deleted-entries}

**[!UICONTROL Orphaned in ACO]** 및 **[!UICONTROL Deleted]** 탭은 조정할 [!DNL Adobe Commerce] 공유 카탈로그가 없으므로 커넥터가 자동으로 복구할 수 없는 두 가지 경우를 다룹니다.

- **[!UICONTROL Orphaned in ACO]** - 커넥터가 동기화 상태 및 드리프트 조정 중에 분리된 엔터티를 보고합니다. 수리가 활성화된 상태에서 조정이 실행되더라도 이를 채택하거나 자동으로 삭제하지 않습니다.

  엔터티가 [!DNL Adobe Commerce Optimizer]에 있지만 커넥터가 해당 엔터티를 추적하지 않거나 추적된 카탈로그 보기와 연결하는 경우 엔터티가 분리됩니다. 이 문제는 엔티티가 수동으로 생성되거나 다른 통합에 의해 생성되거나 커넥터 작업이 중단된 후 방치될 때 발생할 수 있습니다.

  - **카탈로그 보기** - 커넥터가 보기를 추적하지 않습니다. 카탈로그 보기 링크를 선택하여 [!DNL Adobe Commerce Optimizer] Studio에서 카탈로그 보기 세부 정보 페이지를 엽니다. 카탈로그 보기가 더 이상 필요하지 않으면 제거합니다.

  - **제한된 액세스 키**—키를 참조하는 실시간 카탈로그 보기가 없습니다. 카탈로그 보기 링크를 선택하여 [!DNL Adobe Commerce Optimizer] Studio에서 카탈로그 보기 세부 정보 페이지를 엽니다. 구성된 액세스 키를 검토하고 더 이상 필요하지 않은 경우 제거합니다.

  - **정책**—커넥터가 정책을 추적하지 않으며 이를 참조하는 실시간 카탈로그 보기가 없습니다. 정책 링크를 선택하여 [!DNL Adobe Commerce Optimizer] Studio에서 엽니다.  검토한 후 더 이상 필요하지 않으면 제거합니다.

- **[!UICONTROL Deleted]** - [!DNL Adobe Commerce]에서 공유 카탈로그를 삭제했으며 해당 카탈로그 뷰 프로젝션이 이후에 제거되었습니다. 이러한 행은 제거된 항목에 대한 기록으로 90일 동안 유지됩니다.

>[!MORELIKETHIS]
>
> - [카탈로그 보기 동기화 상태 모니터링](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/catalog-view-sync-status.md){target="_blank"} — *Commerce 관리 안내서* —>의 카탈로그 보기 동기화 상태 페이지에 대한 전체 설명서 참조
> - [데이터 동기화 관리](data-sync-status.md) - 제품, 가격 및 범주 피드 동기화 확인
> - [비공개 카탈로그 보기](/help/optimizer/setup/private-catalog-view.md) - 커넥터 관리 비공개 카탈로그 보기에 대해 알아봅니다.
> - [제한된 액세스 키](/help/optimizer/setup/restricted-access-keys.md) — 커넥터 관리 키가 작동하는 방식을 알아봅니다.
> - [B2B 공유 카탈로그 변경 모니터링](get-started-b2b-shared-catalogs.md#monitor-b2b-shared-catalog-changes) — 커넥터가 B2B 공유 카탈로그에 대해 자동화하는 내용을 알아봅니다.
