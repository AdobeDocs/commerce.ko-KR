---
title: 앱 관리
description: App Builder 애플리케이션을 Commerce 인스턴스와 연결, 구성 및 연결 해제합니다.
feature: App Builder, Extensibility, Integration
source-git-commit: 780cef7af3574cd846fd7ee82d7814f2ebe9d6cc
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 0%

---


# 앱 관리

App Manager는 App Builder 애플리케이션을 Commerce 인스턴스와 연결합니다. 구성 양식은 앱의 스키마를 기반으로 동적으로 렌더링되므로 사용자 지정 관리자 UI 개발이 필요하지 않습니다. App Manager는 Commerce이 자동으로 생성하는 양식을 통해 설정을 구성합니다.

![앱 관리](assets/app-management-view.png){width="500" zoomable="yes"}

## 관리자에서 애플리케이션 찾기

**[!UICONTROL Apps]** > **[!UICONTROL App Management]**&#x200B;에서 각 응용 프로그램이 카드로 표시됩니다. 목록에는 선택한 Adobe IMS 조직의 Adobe Commerce 인스턴스와 연결된 모든 앱이 포함될 수 있습니다. 카드 위의 컨트롤을 사용하여 결과 범위를 좁힐 수 있습니다.

| 제어 | 설명 |
| --- | --- |
| **앱별로 필터링...** | 애플리케이션 이름별로 검색합니다. |
| **상태** | 라이프사이클 상태별로 카드를 제한합니다. **모든 상태**&#x200B;는 모든 앱을 표시합니다. 다른 값에는 **연결**, **설치됨**, **부분적으로 설치됨** 및 **연결 해제**&#x200B;가 포함됩니다. 각 카드의 상태가 목록의 색상 표시기와 일치합니다. |
| **확장성 패턴** | 앱에서 사용하는 기능으로 카드를 제한합니다. **모든 확장성 패턴**&#x200B;은(는) 모든 앱을 표시합니다. 다른 값은 **비즈니스 구성**, **관리 UI SDK**, **웹후크**, **이벤트**&#x200B;와 같이 각 카드의 배지와 일치합니다. |

검색 텍스트와 두 드롭다운이 함께 적용됩니다(논리적 AND). 전체 목록을 다시 표시하려면 **상태** 및 **확장성 패턴**&#x200B;을(를) 다시 **모두...** 옵션으로 설정하고 검색 필드를 지웁니다.

## 앱 획득

**[!UICONTROL Acquire App]**&#x200B;에서 [Adobe Exchange](https://exchange.adobe.com/experiencecloud){target="_blank"}에 대한 새 브라우저 탭(또는 별도의 브라우저 보기)을 엽니다. 이 탭에서 Commerce 관련 마켓플레이스 목록을 검색하고 Adobe IMS 조직에 응용 프로그램을 추가할 수 있습니다. 앱을 획득, 승인 및 배포하면 [연결 및 설치](#associate-an-app)를 위해 [!DNL App Management]에 앱이 표시됩니다.

## 사전 요구 사항

앱을 연결하기 전에 다음을 확인하십시오.

| 요구 사항 | 설명 |
|-------------|-------------|
| **관리자 액세스** | [!DNL App Management] 권한이 있는 Commerce 관리자 |
| **배포된 앱** | 조직에 배포되고 연결할 준비가 된 App Builder 애플리케이션 |
| **조직 액세스** | 앱이 배포된 Adobe 조직에 대한 액세스 |

## 튜토리얼

이 비디오를 통해 앱을 Commerce 인스턴스와 연결하고 설정을 구성하는 방법에 대해 알아보십시오.

>[!VIDEO](https://video.tv.adobe.com/v/3478944)

## 앱 연결

연결 프로세스는 Commerce에서 웹 사이트, 스토어 및 스토어 보기를 가져오고 앱과 Commerce 인스턴스 간에 링크를 만듭니다.

App Builder 애플리케이션을 Commerce 인스턴스에 연결하려면 다음을 수행하십시오.

1. **[!UICONTROL Apps]** > **[!UICONTROL App Management]**(으)로 이동합니다.

1. **[!UICONTROL Associate App]**&#x200B;을(를) 클릭합니다.

   ![앱 연결](assets/associate-app.png){width="500" zoomable="yes"}

1. 목록에서 **[!UICONTROL Project]**&#x200B;을(를) 선택하십시오.

1. **[!UICONTROL Workspace]** 선택.

1. **[!UICONTROL Associate]**&#x200B;을(를) 클릭합니다.

   ![앱 세부 정보](assets/app-details.png){width="500" zoomable="yes"}

>[!WARNING]
>
>범위 동기화가 실패하면 연결이 계속 완료됩니다. 나중에 연결된 앱의 구성에 있는 **[!UICONTROL Manage Scopes]** 보기에서 범위를 수동으로 동기화할 수 있습니다.

## 설정 구성

[!DNL App Management] 보기에서 앱을 연결한 후 다음 양식을 통해 설정을 구성하십시오.

1. 연결된 앱에서 **[!UICONTROL Configure]**&#x200B;을(를) 클릭합니다.

1. 앱의 구성 가능한 설정이 양식에 표시됩니다.

1. 필요에 따라 값을 수정합니다.

1. **[!UICONTROL Save]**&#x200B;을(를) 클릭합니다.

### 범위별 구성

서로 다른 웹 사이트, 스토어 또는 스토어 보기에 고유한 설정이 필요한 경우 범위별 구성을 사용하십시오. 예를 들어 특정 지역 또는 스토어 보기에 대해서만 기능을 활성화하거나 브랜드별로 다른 설정을 사용합니다. 낮은 범위의 설정은 높은 범위의 설정을 덮어씁니다.

특정 범위 레벨에서 글로벌 값을 재정의하려면

1. **[!UICONTROL Change Scope]**&#x200B;을(를) 클릭합니다.

1. 목록에서 범위를 선택합니다.

1. 이 범위의 값을 수정합니다.

1. **[!UICONTROL Save]**&#x200B;을(를) 클릭합니다.

## 범위 관리

앱 세부 정보 화면에서 **[!UICONTROL Manage Scopes]**&#x200B;에 액세스하여 앱의 범위 계층 구조를 관리합니다.

![범위 관리](assets/manage-scopes.png){width="500" zoomable="yes"}

| 액션 | 설명 |
|--------|-------------|
| **[!UICONTROL Add root scope]** | 앱에만 적용되는 범위를 추가합니다. |
| **[!UICONTROL Sync Commerce scopes]** | 추가 또는 변경 후 Commerce에서 웹 사이트, 스토어 및 스토어 보기 목록을 새로 고칩니다. |
| **[!UICONTROL Import scopes]** | 파일에서 범위를 일괄적으로 가져옵니다. |

## 앱 연결 해제

더 이상 Commerce 인스턴스에 연결할 필요가 없을 때 앱 연결을 해제합니다. 예를 들어 통합을 중단하거나, 다른 작업 공간으로 전환하거나, 테스트 구성을 정리해야 할 수 있습니다.

>[!WARNING]
>
> 연결을 해제하면 이 인스턴스에 대한 모든 구성 값이 제거됩니다. 이 작업은 취소할 수 없습니다.

Commerce 인스턴스에서 앱을 제거하려면 다음 작업을 수행하십시오.

1. **[!UICONTROL Apps]** > **[!UICONTROL App Management]**(으)로 이동합니다.

1. 앱에서 **[!UICONTROL Unassociate]**&#x200B;을(를) 클릭합니다.

1. 작업을 확인합니다.

## 관련 설명서

* [문제 해결 [!DNL App Management]](troubleshooting.md) - 앱 연결 및 구성과 관련된 일반적인 문제를 해결합니다.
