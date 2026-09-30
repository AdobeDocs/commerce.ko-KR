---
title: 확장 업데이트 확인
description: Adobe Commerce에서 수동 CLI 확인을 포함하여 새 AEM Assets 통합 확장 버전을 확인하고 관리자에게 알리는 방법에 대해 알아봅니다.
feature: CMS, Media
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
    internal-label: Accounts
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
source-git-commit: 7950f5d171b35054be42ca60d19bafcf43c53cd6
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 4%
---
# 확장 업데이트 확인

AEM Assets 통합 확장 버전 1.4.6 이상을 사용하면 Adobe Commerce은 최신 버전의 확장을 사용할 수 있는지 자동으로 확인하고 관리자의 관리자에게 알립니다. 이 검사는 예약된 처리의 일부로 비동기적으로 실행되며 관리 페이지 렌더링을 차단하지 않습니다.

## 업데이트 확인 작동 방식

* 업데이트 검사는 설치된 `aem-assets-integration` 패키지 버전을 [repo.magento.com](https://repo.magento.com/admin/dashboard)에서 사용 가능한 호환 가능한 가장 높은 버전과 비교합니다.
* 결과가 캐시됩니다. 관리 페이지를 로드하면 라이브 네트워크 요청이 트리거되지 않고 가장 최근에 캐시된 결과가 읽힙니다.
* `repo.magento.com`을(를) 사용할 수 없거나 반환된 메타데이터가 잘못된 경우, Commerce은 마지막으로 성공한 캐시된 결과를 유지하고 관리자를 차단하지 않습니다.

>[!NOTE]
>
>업데이트 확인은 Adobe Commerce on Cloud 및 온프레미스 배포용입니다.

## 업데이트 알림 보기

관리자는 다음 위치 중 하나에서 사용 가능한 업데이트 알림을 볼 수 있습니다.

* **[!UICONTROL Stores]** > [!UICONTROL Settings] > **[!UICONTROL Configuration]** > **[!UICONTROL Adobe Services]** > **[!UICONTROL AEM Assets Integration]**
* 관리자 알림 드롭다운

각 알림은 다음을 표시합니다.

* 설치된 버전
* 사용 가능한 버전
* 릴리스 분류
* 릴리스 정보에 대한 링크

**[!UICONTROL Remind me later]**&#x200B;을(를) 선택하여 이 Commerce 인스턴스에 대한 알림을 다시 시작하거나 업데이트 알림을 완전히 옵트아웃합니다.

## 수동 업데이트 확인 실행

사용 가능한 업데이트를 즉시 확인하려면 Commerce 루트 디렉터리에서 다음 명령을 실행합니다.

```bash
bin/magento aem:assets:check-update
```

이 명령은 사용 가능한 업데이트만 확인하고 보고합니다. 작성기 파일을 수정하거나 업데이트를 배포하지 않습니다. 업데이트를 설치하려면 [Adobe Commerce 패키지 설치](configure-commerce.md)의 작성기 지침을 따르십시오.

## 확장 패키지에 대한 릴리스 메타데이터

업데이트 검사는 설치된 패키지의 `composer.json` 파일에 있는 `extra` 섹션에서 릴리스 메타데이터를 읽습니다.

```json
{
  "extra": {
    "release_notes_url": "https://experienceleague.adobe.com/...",
    "release_type": "feature",
    "compatible_commerce_versions": ">=2.4.7 <2.5.0"
  }
}
```

## 다음 단계

* [Adobe Commerce 패키지 설치](configure-commerce.md)
