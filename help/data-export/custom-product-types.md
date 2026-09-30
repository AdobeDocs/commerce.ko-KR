---
title: SaaS 카탈로그 데이터 내보내기에서 사용자 지정 제품 유형 지원
description: Commerce Storefront MCP 카탈로그 지원 모듈을 통해 SaaS 데이터 내보내기가 라이브 검색 및 카탈로그 서비스로 전송된 카탈로그 데이터에서 인식되지 않은 사용자 지정 서드파티 제품 유형을 간단한 제품으로 표시하는 방법에 대해 알아봅니다.
role: Admin, Developer
hide: true
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: d3cdead0-685a-4489-9250-4bb709942f66
    internal-label: Data collection
source-git-commit: fd87417a494987f33009d386019d870b306dcf73
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%
---
# SaaS 카탈로그 데이터 내보내기에서 사용자 지정 제품 유형 지원

>[!IMPORTANT]
>
>사용자 지정 제품 유형에 대한 지원은 현재 [!DNL Commerce Storefront MCP]의 일부로 **조기 액세스**&#x200B;에 있습니다. 이 모듈은 Adobe Commerce 버전 2.4.4 이상에서 지원됩니다. 가용성, 패키징 및 설치 요구 사항은 일반 공급 이전에 변경될 수 있습니다. 이 **조기 액세스**&#x200B;에 대한 초대를 요청하려면 [commerceeap@adobe.com](mailto:commerceeap@adobe.com)에 전자 메일을 보내세요. Adobe 팀이 다음 단계 및 자격 요구 사항에 응답합니다.

## 개요

[!DNL SaaS Data Export]은(는) 연결된 Adobe Commerce 서비스(예: [Live Search](../live-search/overview.md) 및 [Catalog Service](../catalog-service/overview.md))에 대한 카탈로그 데이터를 준비할 때 표준 Commerce 제품 유형(단순, 구성 가능, 번들 등)을 인식합니다. 타사 확장은 [!DNL SaaS Data Export]이(가) 기본적으로 인식하지 못하는 **사용자 지정 제품 유형**&#x200B;을(를) 도입할 수 있습니다.

Commerce Storefront MCP 카탈로그 지원 모듈을 통해 [!DNL SaaS Data Export]이(가) 이러한 인식할 수 없는 사용자 지정 제품 유형을 아웃바운드 카탈로그 페이로드에서 **단순 제품**(으)로 나타내므로 [!DNL Commerce Storefront MCP]을(를) 사용하는 쇼핑객이 카탈로그 지원 서비스를 통해 이를 검색할 수 있습니다.

## 비헤이비어 범위

- Commerce Storefront MCP 카탈로그 지원 모듈은 Adobe Commerce에 저장된 제품 유형을 변경하지 않습니다. 사용자 지정 제품 형식을 단순 제품으로 나타내는 것은 [!DNL Live Search] 및 [!DNL Catalog Service]&#x200B;(으)로 전송된 카탈로그 데이터에만 적용됩니다.
- 관리자 설정 또는 런타임 구성이 필요하지 않습니다. 표준 제품 유형은 정상적으로 계속 내보내집니다.
- 이 모듈은 표준 Commerce 제품 유형이 아니라 서드파티 확장에서 도입한 사용자 지정 제품 유형을 타깃팅합니다.

## 모듈 설치

Commerce Storefront MCP 카탈로그 지원 모듈을 활성화하려면 명령줄에서 다음을 실행하십시오.

```bash
composer require magento/module-storefront-mcp-enablement --no-update
composer update magento/module-storefront-mcp-enablement --with-dependencies
bin/magento setup:upgrade
```

## 카탈로그 데이터 다시 동기화

모듈을 설치해도 Adobe Commerce의 기본 제품 데이터는 변경되지 않으므로 기존 사용자 지정 제품 유형 항목은 자동으로 다시 내보내지지 않습니다. 모듈을 설치하기 전에 이미 동기화된 카탈로그 데이터에 새 간단한 제품 표현을 적용하려면 카탈로그 데이터를 수동으로 다시 동기화하십시오. [수동으로 데이터 다시 동기화](data-sync-manage.md#manually-resync-data)를 참조하십시오.
