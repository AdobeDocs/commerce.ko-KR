---
title: '[!DNL App Management] 문제 해결'
description: 앱 연결 및 구성과 관련된 일반적인 문제를 해결합니다.
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
source-git-commit: 76e77db86adecdbd3be76040970c0d0899c34cdc
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%
---
# [!DNL App Management] 문제 해결

다음 솔루션을 사용하여 앱 연결 및 구성과 관련된 일반적인 문제를 해결하십시오.

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

기술 문제 해결에 대한 자세한 내용은 [Commerce 확장성 [!DNL App Management]](https://developer.adobe.com/commerce/extensibility/app-management/){target="_blank"}을 참조하십시오.
