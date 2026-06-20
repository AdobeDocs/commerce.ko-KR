---
title: ' [!DNL Adobe Commerce Optimizer Connector] 문제 해결'
description: ' [!DNL Adobe Commerce] PaaS 통합에 대한  [!DNL Adobe Commerce Optimizer Connector] 자격 증명, 카탈로그 동기화 및 범위 내보내기 문제를 해결하는 방법에 대해 알아봅니다.'
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="PaaS만" type="Informative" url="https://experienceleague.adobe.com/ko/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce 온 클라우드 프로젝트(Adobe 관리 PaaS 인프라) 및 온프레미스 프로젝트에만 적용됩니다."
autotag-review: '2026-06-09T19:00:00.000Z'
TQID: 'https://experienceleague.adobe.com/ei86QuJ3nQ2d-6NRoAeJslgDxjGlZRejD-Nx-6SAVdc'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
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
source-wordcount: 331
ht-degree: 0%

---

# [!DNL Adobe Commerce Optimizer Connector] 문제 해결

이 안내서를 사용하여 초기 설정, 카탈로그 피드 동기화 및 범위 내보내기 구성 중에 [!DNL Adobe Commerce Optimizer Connector]과(와) 관련된 일반적인 문제를 진단하고 해결하십시오. 아래 섹션에서는 자격 증명 및 테넌트 유효성 검사, 데이터 동기화 실패 및 관련 [!DNL SaaS Data Export] 진단을 다룹니다.

## 자격 증명 또는 테넌트 유효성 검사 실패

자격 증명 유효성 검사 중에 `aco:config:init`이(가) 실패하면:

- `bin/magento aco:config:show` [!DNL Adobe Commerce] CLI 명령을 실행하여 저장된 값을 확인합니다.
- 테넌트 ID가 자격 증명을 얻는 데 사용되는 IMS 조직에 속하는지 확인합니다.
- OAuth 클라이언트에 [!DNL Adobe Commerce Optimizer] 수집 서비스에 필요한 범위가 있는지 확인합니다([IMS 자격 증명 가져오기](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/authentication/#obtain-ims-credentials) 참조).

## 데이터가 동기화되지 않음

**항목 수준 오류 세부 정보 확인:**

Commerce 관리자에서 **[!UICONTROL Data Feed Sync Status]**&#x200B;을(를) 여는 단계는 [데이터 동기화가 작동하는지 확인](./data-sync-manage.md#verify-that-the-data-sync-is-working)을(를) 참조하십시오. 항목별 오류 세부 정보를 보려면 실패한 피드를 선택하십시오.

오류 처리에 대한 주요 사항:

- **400개의 오류**&#x200B;이(가) 다시 시도되지 않습니다. 페이로드에서 형식이 잘못되었거나 누락된 필수 필드를 검사합니다. 필요한 형식은 [커넥터 피드에 대한 필드 매핑](reference/field-mapping.md)을 참조하십시오.
- `*_resend_failed_items` cron 작업에서 **5xx 오류**&#x200B;이(가) 자동으로 다시 시도됩니다(5분마다 실행).

**범위 구성 확인:**

문제가 특정 카탈로그 소스(스토어 보기 코드) 또는 가격 책에만 영향을 주는 경우 해당 웹 사이트 또는 스토어 보기에 동기화가 비활성화되어 있는지 확인하십시오. [Commerce 범위 내보내기 구성 사용자 지정](./get-started.md#customize-the-commerce-scopes-export-configuration)을 참조하십시오.

**해결 시:**

커넥터 피드는 **[!UICONTROL Data Feed Sync Status]**&#x200B;에서 성공 상태를 보여 주며 예상 제품, 가격 및 특성은 [!DNL Commerce Optimizer]의 **[!UICONTROL Data Sync]** 페이지에 나타납니다.

## 잘못된 구성 및 결과 해석

제품 누락, 잘못된 가격 또는 범위 수준 데이터 공백 등 동기화 결과를 잘못 구성하거나 잘못 해석하여 발생한 특정 동작의 카탈로그는 [문제 해결 시나리오](troubleshooting/troubleshooting-scenarios.md)를 참조하십시오.

## [!DNL SaaS Data Export] 진단

로그 위치 및 피드 다시 동기화 명령을 포함한 하위 수준의 [!DNL SaaS Data Export] 진단에 대해서는 [[!DNL SaaS Data Export] 문제 해결 안내서](https://experienceleague.adobe.com/ko/docs/commerce/saas-data-export/troubleshooting/logging){target="_blank"}를 참조하십시오.
