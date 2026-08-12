---
title: 웹 사이트의 다른 PayPal 계정 연결
description: 관리자에서 웹 사이트 범위의 PayPal 온보딩을 완료하여 다른 PayPal 판매자 계정을 개별 웹 사이트에 연결합니다.
role: Admin, User
level: Intermediate
feature: Payments, Checkout, Configuration, Paas, Saas
TQID: 'https://experienceleague.adobe.com/U1zGAU6vYKjk2tc2KXnvyqnYdbA2HKTCNZSKhHdS0Vw'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
source-git-commit: d754c71e287d7d9ff297dd7d95efbaaae7ffc2fc
workflow-type: tm+mt
source-wordcount: 393
ht-degree: 0%

---

# 웹 사이트의 다른 PayPal 계정 연결

**여러 웹 사이트**&#x200B;가 있는 Commerce 인스턴스의 경우 **다른 PayPal 판매자 계정**&#x200B;이 필요할 수 있습니다. [!DNL Payment Services]은(는) **전역** 온보딩 후에 **웹 사이트 범위** PayPal 온보딩을 사용할 수 있습니다.

>[!NOTE]
>
> 이 기능은 새 계정 연결만 지원합니다.

## 웹 사이트 범위 온보딩을 위한 사전 요구 사항

웹 사이트 수준 온보딩은 스토어가 다음 요구 사항을 충족해야 사용할 수 있습니다.

- [Commerce 서비스 커넥터](https://experienceleague.adobe.com/ko/docs/commerce/user-guides/integration-services/saas) 설정이 완료되었습니다.
- PayPal 계정은 글로벌(기본 구성) 범위에서 연결됩니다.

다음 필드가 기본 범위에서 채워졌는지 확인하여 이를 확인할 수 있습니다.

- [!UICONTROL Payment Services Sandbox ID]
- [!UICONTROL Payment Services Production ID]
- [!UICONTROL PayPal Merchant ID]

이 필드가 비어 있으면 먼저 [전역 온보딩을 완료](configure-admin.md)해야 합니다. 필수 구성 요소를 완료할 때까지 **[!UICONTROL Connect different account]** 단추를 사용할 수 없습니다.

## 웹 사이트 수준 연결 시작

1. _관리자_ 사이드바에서 **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**>**[!UICONTROL Sales]**(으)로 이동한 다음&#x200B;**[!UICONTROL Payment Methods]**&#x200B;을(를) 선택합니다.
1. 왼쪽 상단 모서리의 범위 선택기에서 **[!UICONTROL Default Config]**&#x200B;에서 온보딩할 **[!UICONTROL Website]**(으)로 전환합니다.
1. **[!UICONTROL Connect different account]**&#x200B;을(를) 클릭합니다.

   단추가 비활성화되어 있으면 스토어가 위의 [필수 구성 요소](#prerequisites-global-scope)를 충족하지 않습니다.

## 온보딩 모달 완료

팝업 창이 열립니다.

1. 드롭다운에서 **[!UICONTROL Country]**&#x200B;을(를) 선택합니다.
1. 온보딩 유형을 선택하십시오. **[!UICONTROL Basic]** 또는 **[!UICONTROL Advanced]**.
1. **[!UICONTROL Next]**&#x200B;을(를) 클릭합니다.

>[!NOTE]
>
> 헝가리, 스페인 또는 오스트리아에서 온보딩하는 경우 **[!UICONTROL I Accept]** 단추를 클릭하기 전에 사용 약관 링크를 열어 확인해야 합니다. 사용 약관을 열 때까지 단추가 비활성화됩니다.

## PayPal에 로그인

PayPal 로그인으로 리디렉션되면 로그인한 다음 PayPal 내에서 온보딩 단계를 완료하십시오.

>[!IMPORTANT]
>
> **[!UICONTROL Confirm and Continue]**&#x200B;을(를) 클릭하면 전역 범위에 대한 세션이 종료되고 웹 사이트 수준 연결이 시작됩니다. 실수로 **[!UICONTROL Connect different account]**&#x200B;을(를) 클릭한 경우 **[!UICONTROL Cancel]**&#x200B;을(를) 선택하거나 확인 전에 **X** 아이콘을 클릭하여 취소할 수 있습니다.

## 완료 후 책임자에게 돌아가기

1. PayPal 단계를 완료한 후 PayPal 창을 닫습니다.
1. **[!UICONTROL Finish]**&#x200B;을(를) 클릭하거나 오른쪽 상단의 **X**&#x200B;을(를) 클릭하여 온보딩 팝업을 닫습니다.
1. Commerce 구성 페이지가 자동으로 새로 고쳐집니다.

## 결과 확인

페이지를 새로 고친 후 웹 사이트 범위 구성 페이지에서 다음 작업을 확인하십시오.

- 해당 웹 사이트에 대해 업데이트된 **[!UICONTROL PayPal Merchant ID]**.
- 온보딩 결과를 보여 주는 상태 레이블:

| 상태 | 의미 |
| --- | --- |
| `ACTIVE` | 온보딩이 완료되었습니다 |
| `PENDING` | 온보딩이 아직 처리 중입니다. |
| `ERROR` | 온보딩이 완료되지 않았습니다. |

`ERROR` 상태가 표시되면 문제를 설명하는 오류 메시지가 표시됩니다. **[!UICONTROL Connect different account]**&#x200B;을(를) 다시 클릭하여 온보딩 프로세스를 다시 시도할 수 있습니다.
