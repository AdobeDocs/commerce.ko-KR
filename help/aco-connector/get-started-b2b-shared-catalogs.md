---
title: B2B Commerce용 커넥터 설정
description: B2B 커넥터를 설치하고, Commerce 범위를 선택하고, 공유 카탈로그 데이터를 동기화하고, 카탈로그 보기를 확인하고, 프로젝션 상태를 모니터링하는 방법을 알아봅니다.
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
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
    internal-label: Admin tools and workspace
subfeature_v2:
  - id: e126554b-28f9-4290-b58c-10b888b88174
    internal-label: IMS integration
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
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
last-update: 2026-10-01
source-git-commit: 9ed3a09bc4e26e2ef787909700f51e25de0a18fa
workflow-type: tm+mt
source-wordcount: '843'
ht-degree: 0%
---

# B2B Commerce용 커넥터 설정

[!DNL Adobe Commerce]개의 B2B 공유 카탈로그를 사용하는 판매자는 [!DNL Adobe Commerce Optimizer Connector for B2B]을(를) 사용하여 사용자 지정 공유 카탈로그 데이터와 구성을 [!DNL Adobe Commerce Optimizer]에 동기화할 수 있습니다.

{{aco-integration-environment-alignment}}

## 통합 사용 요구 사항 {#requirements-to-use-the-integration}

* [Commerce B2B 버전 1.5.3+](https://experienceleague.adobe.com/ko/docs/commerce-admin/b2b/install)이(가) 설치되고 활성화된 Adobe Commerce 2.4.8+.

* 프로비저닝된 샌드박스 인스턴스가 있는 [!DNL Commerce Optimizer] 라이선스.

* 작성기를 사용하여 커넥터 메타 패키지를 다운로드하려면 [인증 키](https://experienceleague.adobe.com/ko/docs/commerce-operations/installation-guide/prerequisites/authentication-keys)를 사용하십시오.

* [[!DNL Commerce Optimizer] 샌드박스 인스턴스](../optimizer/get-started.md)에 대한 관리자 액세스 권한.

통합을 구성하는 [!DNL Adobe Commerce] 사용자에게는 다음이 있어야 합니다.

* Commerce 관리자에 대한 관리자 액세스 권한.

* [명령줄 액세스 [!DNL Adobe Commerce] 응용 프로그램 서버](https://experienceleague.adobe.com/ko/docs/commerce-on-cloud/user-guide/project/user-access).

* [!DNL Commerce Optimizer] 프로젝트가 프로비저닝된 [IMS 조직](https://experienceleague.adobe.com/ko/docs/core-services/interface/administration/organizations?)에 대한 개발자 액세스 권한.

### 애플리케이션 요구 사항

* Commerce cron 및 indexer가 정상적으로 작동합니다.
* 내보내기를 위해 식별된 필수 웹 사이트 및 스토어 조회수.
* Adobe Commerce에서 구성되었거나 구성할 준비가 된 공유 카탈로그, 회사 할당, 분류 및 B2B 가격입니다.

>[!BEGINSHADEBOX]

## 충돌하는 확장 제거 {#remove-conflicting-extensions}

{{$include /help/_includes/aco-connector/remove-conflicting-extensions.md}}

>[!ENDSHADEBOX]

## 구성 단계 {#configuration-steps}

[!DNL Adobe Commerce Optimizer Connector for B2B]을(를) 사용하도록 설정하고 [!DNL Adobe Commerce]에서 [!DNL Commerce Optimizer] 인스턴스로 사용자 지정 공유 카탈로그 구성을 동기화하려면 다음 단계를 수행하십시오.

1. **[작성기를 사용하여  [!DNL Adobe Commerce Optimizer Connector for B2B] 패키지](#install-the-adobe-commerce-optimizer-connector-for-B2B-package)**&#x200B;를 설치하여 [!DNL Adobe Commerce] 인스턴스를 [!DNL Commerce Optimizer]에 연결합니다.

1. 관리자의 **[Commerce 범위 내보내기 구성을 사용자 지정](#data-export-and-scope-mapping)**&#x200B;합니다.

1. **[통합을 사용하도록 설정 [!DNL Commerce Optimizer] 통합](#enable-the-adobe-commerce-optimizer-integration)**.

1. **[데이터 동기화가 작동하는지 확인](#verify-that-the-data-sync-is-working)**.

## [!DNL Adobe Commerce Optimizer Connector for B2B] 패키지 설치 {#install-the-adobe-commerce-optimizer-connector-for-B2B-package}

[!DNL Adobe Commerce Optimizer Connector for B2B]은(는) [!DNL Commerce Optimizer]에 대한 활성 라이선스가 있는 모든 Commerce 판매자가 사용할 수 있는 Composer 메타 패키지로 제공됩니다.

### 설치 단계

1. 작성기를 사용하여 `adobe-commerce/commerce-data-export-aco-adapter-b2b` 모듈 추가:

   ```shell
   composer require adobe-commerce/commerce-data-export-aco-adapter-b2b
   ```

1. [!DNL Adobe Commerce] 스테이징 환경에 변경 내용을 배포합니다.

   배포가 완료되면 Commerce 관리 메뉴에서 [!DNL Commerce Optimizer] 옵션을 사용할 수 있습니다. **[!UICONTROL Commerce Optimizer]**&#x200B;을(를) 선택하여 Commerce 관리자에서 직접 [!DNL Commerce Optimizer] 인스턴스를 엽니다.

{{install-extension-links}}

### 데이터 내보내기 및 범위 매핑

동기화할 웹 사이트 및 스토어 보기를 선택한 다음 초기 피드를 확인합니다. B2B의 경우 커넥터가 공유 카탈로그 데이터를 [!DNL Commerce Optimizer]에 투영할 때 활성화된 범위를 사용합니다.

* 지역화된 제품 콘텐츠가 포함된 카탈로그 원본→ **스토어 보기**
* **웹 사이트 및 고객 그룹** → 및 고객 그룹 가격 책자
* **공유된 카탈로그**→ 보호된 개인 카탈로그 보기 및 강제 적용된 정책

공유 카탈로그는 제품 분류를 정의하고 활성화된 각 스토어 뷰는 현지화된 카탈로그 소스를 제공합니다. 웹 사이트와 고객 그룹이 해당 가격 장부를 결정합니다. 커넥터는 활성화된 각 스토어 보기에 대해 각 사용자 정의 공유 카탈로그를 프로젝트하므로 B2B 프로젝션에 대해 별도의 범위 설정이 필요하지 않습니다.

사용자 지정 공유 카탈로그는 활성화된 각 저장소 보기에 대해 하나씩 여러 개의 보호된 개인 카탈로그 보기를 생성할 수 있습니다. 기본 공개 공유 카탈로그는 B2B 개인 카탈로그 보기로 투영되지 않습니다. 자세한 개체 매핑 및 런타임 권한 부여 흐름은 [B2B 공유 카탈로그 프로젝션](b2b-shared-catalog-projection.md)을 참조하십시오.

>[!IMPORTANT]
>
>내보내기 설정을 변경하면 전체 색인 재지정이 트리거되며, 이는 카탈로그 크기에 따라 상당한 시간이 걸릴 수 있습니다. 통합을 활성화하고 초기 데이터 동기화를 시작하기 전에 Commerce 범위를 구성합니다.

### 범위 내보내기 설정을 변경하려면

1. Commerce 관리에서 **[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL All Stores]**(으)로 이동합니다.

1. 구성할 웹 사이트 또는 스토어 보기를 선택합니다.

1. **[!DNL Commerce Optimizer]내보내기 설정**&#x200B;에서 확인란을 사용하여 필요에 따라 데이터 동기화를 활성화하거나 비활성화합니다.

   ![데이터 동기화 구성 업데이트](./assets/aco-connector-b2b-storeview-list.png){width="500" zoomable="yes"}

1. 변경 사항을 저장합니다.

### 비헤이비어 활성화 및 비활성화

| 액션 | 결과 |
| -------- | -------- |
| 스토어 보기 비활성화 | **동기화를 사용하지 않도록 설정하면 B2B 상점 앞에서 카탈로그 데이터가 제거됩니다.** 카탈로그 원본이 [!DNL Adobe Commerce Optimizer]에 남아 있지만 동기화된 모든 데이터는 다음 cron 실행 시 제거됩니다. |
| 스토어 조회수 비활성화 후 재활성화 | 동일한 카탈로그 소스가 전체 데이터 재동기화로 다시 채워집니다. |

### B2B 공유 카탈로그 변경 모니터링

커넥터는 공유 카탈로그 및 회사 할당에 대한 변경 사항을 감시합니다. Commerce 관리에서 공유 카탈로그를 제거하면 커넥터가 구성 가능한 유예 기간 후에 개인 카탈로그 보기에 대한 액세스를 제거합니다.

>[!NOTE]
>
>삭제 유예 기간은 기본적으로 7일로 설정됩니다. 카탈로그 보기 동기화 설정 구성을 업데이트하여 변경할 수 있습니다. [카탈로그 보기 동기화 상태 구성](catalog-view-sync-status.md#configure-aco-catalog-view-sync-settings)을 참조하세요.

## [!DNL Commerce Optimizer] 통합 사용 {#enable-the-adobe-commerce-optimizer-integration}

`aco:config:init` CLI 명령을 실행하여 통합을 활성화하고 데이터 동기화를 시작합니다. 이 명령은 다음 단계를 완료합니다.

1. 명령줄 인수로 제공된 자격 증명을 사용하여 IMS 액세스 토큰을 얻습니다.
1. 테넌트의 유효성을 검사하고 수집 URL 및 [!DNL Commerce Optimizer] Studio URL을 추출하기 위해 `https://ccm.api.commerce.adobe.com/api/v1/tenants/{tenantId}/owner/{orgId}`에서 Commerce Cloud 관리자(CCM) 서비스를 호출합니다.
1. `core_config_data`에 모든 구성(클라이언트 암호로 암호화됨)을 저장합니다.
1. 모든 [!DNL Commerce Optimizer] 피드 인덱서를 무효화하여 초기 전체 동기화를 예약합니다.

{{aco-data-sync-processing-note}}

## 필수 연결 세부 정보 가져오기

{{$include /help/_includes/aco-connector/connection-details.md}}

### [!DNL Commerce Optimizer] 인스턴스 세부 정보 가져오기

{{$include /help/_includes/aco-connector/configure-connection.md}}

## 데이터 동기화가 작동하는지 확인 {#verify-that-the-data-sync-is-working}

{{$include /help/_includes/aco-connector/verify-optimizer-data-sync.md}}

## 다음 단계

1. **B2B 카탈로그 뷰 투영 모니터링**

초기 피드 동기화 후 [카탈로그 보기 동기화 상태](catalog-view-sync-status.md)를 사용하여 예상 비공개 카탈로그 보기, 정책, 가격 장부 참조 및 제한된 액세스 키 구성을 확인합니다. 투영 모델 및 런타임 인증 흐름에 대해서는 [B2B 공유 카탈로그 투영](b2b-shared-catalog-projection.md)을 참조하십시오.

1. **[!DNL Edge Delivery Services]**&#x200B;에서 Commerce 상점 설정

   [!DNL Commerce Optimizer] 인스턴스에 상점 전선을 연결하고 개인화된 상거래 경험을 게재하려면 [상점 전선의 설정 설명서](https://experienceleague.adobe.com/en/tools/commerce-storefront/setup/){target="_blank"}를 따르십시오.
