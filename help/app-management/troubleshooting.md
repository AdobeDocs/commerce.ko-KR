---
title: '[!DNL App Management] 문제 해결'
description: 앱 연결, 설치, 구성 및 업그레이드와 관련된 일반적인 문제를 해결합니다.
feature: App Builder, Extensibility, Integration
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 72863f3c-9d27-5dda-afe1-d9f934b1fba0
    internal-label: Extensibility
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: cc250cf1-34eb-4863-80d0-d170d45ea067
    internal-label: Developer tools
subfeature_v2:
  - id: a743e5dc-8f37-4b5d-a848-03c32ca30598
    internal-label: App Builder
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: a00b9e1654a572e1773b5b7e321683332882d86f
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 0%
---
# [!DNL App Management] 문제 해결

다음 솔루션을 사용하여 앱 연결, 설치, 구성 및 업그레이드와 관련된 일반적인 문제를 해결하십시오.

## 앱 공급자에게 문의하기 전

아래 문제에 대한 단계를 따르십시오. 앱 개발자 또는 공급자의 도움이 필요한 경우 다음 정보를 수집합니다.

* 앱 카드의 **[!UICONTROL Manage]** > **[!UICONTROL Details]**&#x200B;에서 사용 가능한 경우 앱 이름 및 설치된 버전.
* 영향을 받는 Commerce 인스턴스 및 Adobe 조직입니다.
* 설치 또는 업그레이드와 같이 실패한 작업과 실패한 단계입니다.
* 오류 메시지와 오류 스크린샷이 표시됩니다(가능한 경우).
* 시간대를 포함하여 대략적인 실패 시간입니다.
* 재시도 횟수 및 결과.

## 앱이 표시되지 않음

배포 후 목록에 앱이 표시되지 않으면 다음 단계를 확인하십시오.

1. 조직에서 앱을 배포하고 사용할 수 있는지 확인합니다.

1. Developer Console에서 올바른 Adobe 조직에 로그인했는지 확인합니다.

1. 앱이 연결할 준비가 되었는지 확인합니다(앱 개발자나 파트너가 확인할 수 있음).

앱이 여전히 나타나지 않으면 앱 개발자에게 문의하거나 [Commerce 확장성 [!DNL App Management]](https://developer.adobe.com/commerce/extensibility/app-management/){target="_blank"} 설명서에서 기술 정보를 확인하십시오.

## 범위 동기화 실패

앱을 연결할 때 범위 동기화가 실패하면 다음을 시도해 보십시오.

1. Commerce 인스턴스가 액세스 가능하고 온라인인지 확인합니다.

1. API 자격 증명이 유효하고 올바른 권한이 있는지 확인합니다.

1. 앱 구성에서 **[!UICONTROL Manage Scopes]**&#x200B;에서 수동으로 동기화해 보십시오.

## 구성이 저장되지 않음

구성 변경 사항이 저장되지 않으면 다음을 시도해 주십시오.

1. 모든 필수 필드가 채워져 있고 유효한지 확인하십시오.

1. 앱 구성을 수정할 수 있는 올바른 권한이 있는지 확인하십시오.

1. 페이지를 새로 고치고 다시 저장해 보십시오.

문제가 지속되면 브라우저 콘솔에서 오류를 확인하거나 앱 개발자에게 문의하십시오.

## 설치 실패

설치가 완료될 때까지 새로 고치지 않고 설치 페이지를 열어 두십시오. 닫거나 새로 고치면 설치가 제대로 완료되지 않을 수 있습니다.

설치 시 오류가 보고되는 경우:

1. 실패한 항목과 표시된 오류 메시지를 확인합니다.

1. 앱의 사전 설치 지침을 완료했는지 확인합니다.

1. 앱 개발자에게 실패한 단계를 검사하고 원인을 수정한 후 설치를 다시 시도하십시오.

설치하지 못하면 일부 변경 사항이 적용될 수 있습니다. 설치를 다시 시도하면 성공으로 기록된 사용자 정의 단계가 생략되고 실패 또는 중단된 단계가 다시 실행될 수 있습니다. 개발자에게 부분 실행으로 생성된 리소스를 확인하도록 요청합니다.

## 업그레이드 실패

업그레이드 실패 시 일부 작업이 적용될 수 있습니다. 연결 해제는 구성을 제거하고 파괴적인 정리 스크립트를 실행할 수 있으므로 앱을 연결 해제하고 일상적인 복구 단계로 다시 설치하지 마십시오.

1. 실패한 단계를 식별하고 표시된 오류 메시지를 기록합니다.

1. 앱 개발자에게 로그를 검사하고 Commerce 또는 외부 리소스에 대한 변경 사항을 이미 확인하고 원인을 수정하도록 요청합니다.

1. [!DNL App Management]에서 **[!UICONTROL Retry Upgrade]**&#x200B;을(를) 선택합니다. 이 작업은 수동 및 자동 업그레이드 모드 모두에서 사용할 수 있습니다.

다시 시도할 때마다 현재 상태에서 새 계획을 만듭니다. 성공으로 기록된 사용자 정의 설치 단계는 생략되며, 실패하거나 중단된 단계는 다시 실행할 수 있습니다. 자동 모드에서 앱을 다시 배포하면 다른 업그레이드 시도도 트리거됩니다.

반복 시도가 실패할 경우 앱 개발자에게 문제 해결을 위해 실행 또는 시도 ID와 실행 활성화 ID를 보유하도록 요청합니다. 상태 명령, 시도 기록 및 런타임 로그에 대해서는 개발자 설명서에서 [실패한 업그레이드 다시 시도](https://developer.adobe.com/commerce/extensibility/app-management/upgrade-app/#retry-a-failed-upgrade){target="_blank"}를 참조하십시오.

## 업그레이드 후 리소스 남음

앱 구성에서 사용자 지정 설치 단계를 제거해도 제거 스크립트가 실행되지 않거나 만들어진 리소스가 제거되지 않습니다. 업그레이드 계획은 제거된 단계에 대해 스크립트가 실행되지 않으며, 업그레이드 후 진행 화면 또는 앱 세부 정보에 해당 단계가 표시되지 않는다는 경고를 표시합니다.

앱 개발자에게 리소스가 여전히 필요한지 확인하고 필요한 경우 정리 마이그레이션을 제공하도록 요청하십시오. 관리자 워크플로에 대해서는 [앱 업그레이드](manage-app.md#upgrade-an-app)를 참조하십시오.

기술 문제 해결에 대한 자세한 내용은 [Commerce 확장성 [!DNL App Management]](https://developer.adobe.com/commerce/extensibility/app-management/){target="_blank"}을 참조하십시오.
