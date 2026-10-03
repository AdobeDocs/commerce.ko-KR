---
title: B2B 공유 카탈로그에 대한 제한된 액세스 키 관리
description: Adobe Commerce Optimizer 커넥터가 B2B 공유 카탈로그 프로젝션의 보안을 위해 사용하는 제한된 액세스 키를 관리하는 방법에 대해 알아봅니다.
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="PaaS만" type="Informative" url="https://experienceleague.adobe.com/ko/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce 온 클라우드 프로젝트(Adobe 관리 PaaS 인프라) 및 온프레미스 프로젝트에만 적용됩니다."
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
source-git-commit: a3ade1a31d3c2905b601f71bda118de89c43cf59
workflow-type: tm+mt
source-wordcount: '1105'
ht-degree: 0%
---

# B2B 공유 카탈로그에 대한 제한된 액세스 키 관리

[!BADGE Private Beta]{type=Caution tooltip="현재 비공개 베타에 있는 Adobe Commerce Optimizer 커넥터 B2B 확장이 필요합니다."}

[!DNL Adobe Commerce Optimizer Connector B2B extension]과(와) 함께 [!DNL Adobe Commerce]개의 B2B 공유 카탈로그를 사용하는 경우 카탈로그 보기가 만들어질 때 확장이 자동으로 첫 번째 제한된 액세스 키를 생성하고 할당합니다. Commerce 관리자의 [!UICONTROL Restricted Access Keys] 페이지를 사용하여 해당 키를 보고 추가 키를 만들거나 할당하거나 삭제합니다.

![B2B 공유 카탈로그 보기에 대해 제한된 액세스 키](assets/restricted-access-keys.png){width="800" zoomable="yes"}

>[!NOTE]
>
>파트너 포털과 같은 B2B가 아닌 사용 사례에 대해 수동으로 만드는 키를 관리하려면 [제한된 액세스 키](/help/optimizer/setup/restricted-access-keys.md#create-a-restricted-access-key)를 참조하십시오.

## 페이지 액세스 {#access-the-page}

Commerce 관리자에서 **[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Restricted Access Keys]**(으)로 이동합니다.

공유 카탈로그 그리드 또는 회사 그리드에서 카탈로그 보기에 키를 할당할 수 있습니다. [B2B 공유 카탈로그 보기에 키 할당](#assign-keys-to-a-shared-catalog-view)을 참조하세요.

>[!NOTE]
>
>이 페이지의 필드를 참조하려면 *Commerce 관리 가이드*&#x200B;에서 [제한된 액세스 키 관리](https://experienceleague.adobe.com/ko/docs/commerce-admin/systems/data-transfer/data-sync/catalog-view-sync/restricted-access-keys){target="_blank"}하십시오.—>

## 자동 키 이상이 필요한 경우 {#when-you-need-more-than-the-automatic-key}

[!DNL Adobe Commerce Optimizer Connector B2B extension]에 의해 생성된 자동 키는 사용자의 작업 없이 대부분의 B2B 공유 카탈로그를 포함합니다. 다음과 같은 경우 직접 키를 관리합니다.

- **키 회전**—새 키를 만들어 기존 키와 함께 카탈로그 보기에 할당하고, 제대로 작동하는지 확인한 다음 이전 키를 삭제합니다. 자동 회전은 아직 사용할 수 없습니다.
- **키 연결에 실패했습니다**—[카탈로그 보기 동기화 상태](catalog-view-sync-status.md)에 키 관련 드리프트가 표시되면 카탈로그 보기 할당을 다시 저장하여 실패한 링크를 다시 시도하십시오. 키가 여전히 실패하면 [!UICONTROL Reconcile & Repair]을(를) 실행하여 키 또는 상태를 복구한 후 대체 항목을 만드십시오. 키가 만료되었거나 오류가 지속적으로 복구할 수 없는 경우에만 대체 키를 만듭니다.
- **공개 키 찾기**—제한된 액세스 키 페이지에서 **[!UICONTROL View Public Key]**&#x200B;을(를) 선택하여 키의 공개 키를 보고 복사합니다.

카탈로그 보기에는 최대 3개의 키가 한 번에 할당될 수 있습니다. 키 순환 중에 [!DNL Adobe Commerce Optimizer]은(는) 할당되고 만료되지 않은 키로 서명된 토큰을 수락합니다. &quot;활성&quot; 키를 설정하는 수동 단계는 없습니다.

## 키 만들기

[!UICONTROL Restricted Access Keys] 페이지에서 **[!UICONTROL Create Key]**&#x200B;을(를) 선택하여 키를 만듭니다.

Commerce은 새 키 쌍을 생성하고 개인 키를 보유합니다. 제한된 액세스 키 테이블은 고유 키 ID를 보여주는 새 키 항목으로 업데이트됩니다. 카탈로그 보기에 키를 할당할 때 이 [!UICONTROL Key ID]을(를) 사용합니다.

카탈로그 보기에 키를 할당할 때까지 공개 키가 [!DNL Adobe Commerce Optimizer]에 등록되지 않습니다. 등록 후 제한된 액세스 키 테이블 항목이 업데이트되어 카탈로그 할당 및 만료 날짜가 표시됩니다.

## B2B 공유 카탈로그에서 예상되는 카탈로그 보기에 키 할당 {#assign-keys-to-a-shared-catalog-view}

기본 [!UICONTROL Restricted Access Keys] 그리드가 아닌 회사 계정 또는 공유 카탈로그 페이지의 카탈로그 보기에서 키를 할당하거나 할당 해제합니다.

카탈로그 보기에는 키가 하나 이상 있어야 하며 최대 3개를 가질 수 있습니다.

- 네 번째 키를 할당하려고 하면 값을 저장하려고 할 때 오류 메시지가 표시됩니다. `A Catalog View can have at most 3 access keys.`
- 카탈로그 보기에 하나의 키만 있는 경우 해당 키를 삭제하거나 할당 해제할 수 없습니다.

카탈로그 보기 키 구성을 업데이트하려면 회사 계정 페이지 또는 공유 카탈로그 페이지에서 액세스할 수 있습니다.

>[!BEGINTABS]

>[!TAB 회사 계정의 키 관리]

1. Commerce 관리자에서 회사 페이지를 엽니다(**[!UICONTROL Customers]** > **[!UICONTROL Companies]**).

1. 회사의 [!UICONTROL Action] 열에서 [!UICONTROL Edit]을(를) 선택합니다.

1. 회사에 할당된 공유 카탈로그에서 예상되는 카탈로그 보기 목록을 보려면 _[!UICONTROL Catalog Views]_&#x200B;섹션을 확장합니다.

탭에는 할당된 키를 포함하여 공유 카탈로그에서 예상된 카탈로그 보기가 나열됩니다.

1. 업데이트할 카탈로그 보기의 [!UICONTROL Actions] 열에서 **[!UICONTROL Edit Restricted Access Keys]**&#x200B;을(를) 선택합니다.

   ![카탈로그 보기에 할당된 키를 표시하는 제한된 액세스 키 편집 드롭다운](assets/restricted-access-key-selector.png){width="500" zoomable="yes"}

1. 키를 할당하려면 **[!UICONTROL Access Keys]** 드롭다운 목록을 선택하십시오. 그런 다음 [!UICONTROL key ID]&#x200B;(예: `#42`)에서 할당 해제된 키를 선택합니다. 그런 다음 [!UICONTROL Done]을(를) 클릭하여 카탈로그 보기에 할당합니다.

   다른 카탈로그 보기에 이미 할당된 키의 레이블이 그에 따라 지정됩니다.

1. 액세스 토큰을 제거하려면 키 레이블에서 `x` 컨트롤을 선택하여 [!UICONTROL Access Tokens] 필드에서 제거하십시오.

1. 구성 업데이트를 저장하고 적용하려면 **[!UICONTROL Save]**&#x200B;을(를) 선택합니다.

>[!TAB 공유 카탈로그의 키 관리]

1. Commerce 관리자에서 공유 카탈로그 페이지를 엽니다(**[!UICONTROL Catalog]** > **[!UICONTROL Shared catalogs]**).

1. 공유에 대한 [!UICONTROL Action] 열의 [!UICONTROL Select] 메뉴에서 **[!UICONTROL General Settings]**&#x200B;을(를) 선택합니다.

1. 공유 카탈로그에서 예상되는 카탈로그 보기 목록을 보려면 [!UICONTROL Shared Catalog Information] 메뉴에서 **[!UICONTROL Catalog Views]**&#x200B;을(를) 선택하십시오.

[!UICONTROL Catalog Views] 페이지에는 카탈로그 보기 ID, 연결된 저장소 보기 및 각 카탈로그 보기에 대한 액세스 키가 나열됩니다.

1. 업데이트할 카탈로그 보기의 [!UICONTROL Actions] 열에서 **[!UICONTROL Edit Restricted Access Keys]**&#x200B;을(를) 선택합니다.

   ![카탈로그 보기에 할당된 키를 표시하는 제한된 액세스 키 편집 드롭다운](assets/restricted-access-key-selector.png){width="500" zoomable="yes"}

1. 키를 할당하려면 **[!UICONTROL Access Keys]** 드롭다운 목록을 선택하십시오. 그런 다음 기본 키 제목(예: `#42`)으로 할당되지 않은 키를 선택합니다. 그런 다음 [!UICONTROL Done]을(를) 클릭하여 카탈로그 보기에 할당합니다.

   다른 카탈로그 보기에 이미 할당된 키의 레이블이 그에 따라 지정됩니다.

1. 액세스 토큰을 제거하려면 키 레이블에서 `x` 컨트롤을 선택하여 [!UICONTROL Access Tokens] 필드에서 제거하십시오.

1. 구성 업데이트를 저장하고 적용하려면 **[!UICONTROL Save]**&#x200B;을(를) 선택합니다.

>[!ENDTABS]

## 키 만료 및 갱신 관리

제한된 액세스 키의 기본 키 수명을 구성할 수 있습니다. 이 값은 [!DNL Adobe Commerce Optimizer Connector B2B] 확장에서 초기 키를 생성하거나 새 키를 수동으로 만들 때 설정된 만료 날짜를 결정합니다.

[!UICONTROL Restricted Access Keys] 페이지의 [!UICONTROL Expires At] 열에 만료 날짜가 표시됩니다.

기간을 변경하려면 **[!UICONTROL Stores]** > [!UICONTROL Settings] > **[!UICONTROL Configuration]** > **[!UICONTROL Services]** > **[!UICONTROL ACO Restricted Access Keys]**(으)로 이동하십시오. [!UICONTROL Provisioning] 페이지에서 **[!UICONTROL Default Key Expiry (days)]** 필드를 업데이트합니다. 기본 시스템 키 수명은 초기에 연장된 기간(~100년)으로 설정됩니다. 보안 정책과 일치하는 값으로 업데이트해야 합니다.

### 키 갱신

키가 만료 후 10일 이내에 있으면 [!UICONTROL Restricted Access Keys] 페이지에 해당 항목 옆에 경고 아이콘이 표시됩니다. 키가 만료되기 전에 갱신하지 않으면 새 키를 할당할 때까지 카탈로그 보기에 액세스할 수 없습니다.

언제든지 새 키를 만들어 할당하고, 새 키가 작동하는지 확인한 후 이전 키를 제거할 수 있습니다.

## 알려진 제한 사항

자동 키 회전은 아직 사용할 수 없습니다.

>[!MORELIKETHIS]
>
> - [제한된 액세스 키 관리](https://experienceleague.adobe.com/ko/docs/commerce-admin/systems/data-transfer/data-sync/catalog-view-sync/restricted-access-keys){target="_blank"} — *Commerce 관리 가이드* —>에서 이 페이지에 대한 전체 필드 참조
> - [카탈로그 보기 동기화 모니터링](catalog-view-sync-status.md) - 이 키가 보호하는 카탈로그 보기 모니터링
> - [비공개 카탈로그 보기](/help/optimizer/setup/private-catalog-view.md) - 커넥터 관리 비공개 카탈로그 보기에 대해 알아봅니다.
> - [제한된 액세스 키](/help/optimizer/setup/restricted-access-keys.md) - B2B 이외의 사용 사례에서 수동 ACO Studio 기반 키 흐름이 작동하는 방식을 알아봅니다.
