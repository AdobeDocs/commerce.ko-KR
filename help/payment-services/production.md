---
title: 프로덕션에  [!DNL Payment Services] 사용
description: 프로덕션에 대해  [!DNL Payment Services] 을(를) 활성화하여 온보딩 프로세스를 완료합니다.
exl-id: 3b1269e8-127b-47f8-9738-9722a5737c63
feature: Payments, Checkout, Configuration, Install, Paas, Saas
source-git-commit: 0f2e9c3a7d990a46bafc5f3b8a083436d42643b5
workflow-type: tm+mt
source-wordcount: '1045'
ht-degree: 0%

---

# 프로덕션에 [!DNL Payment Services] 사용

다음 단계를 수행한 후 이 항목의 단계에 따라 서비스를 프로덕션에 넣고 [온보딩 프로세스](onboard.md)를 완료할 수 있습니다.

* 결제 서비스 확장 [!BADGE PaaS만]{type=Informative tooltip="Adobe Commerce on Cloud 프로젝트에만 적용됩니다(Adobe 관리 PaaS 인프라)."} [설치](install.md)
* 인스턴스 [!BADGE Paa만]{type=Informative tooltip="Adobe Commerce on Cloud 프로젝트에만 적용됩니다(Adobe 관리 PaaS 인프라)."} [구성 및 연결](connect.md)
* 샌드박스 [설정](sandbox.md) 및 [테스트](test-validate.md)

## [!DNL Payment Services]을(를) 결제 방법으로 설정

[Commerce 서비스를 구성](connect.md#configure-commerce-services)하고 [샌드박스 테스트](sandbox.md#enable-sandbox-testing) 또는 [라이브 결제](#enable-live-payments)를 사용하도록 설정한 후에는 [!DNL Payment Services]을(를) 결제 방법으로 설정해야 합니다.

1. _관리자_ 사이드바에서 **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**(으)로 이동합니다.
1. **[!UICONTROL Enable Payment Services]**&#x200B;을(를) 클릭합니다.

   하나 이상의 웹 사이트에 대한 결제 방법으로 [!DNL Payment Services]을(를) 아직 구성하지 않은 경우 이 옵션이 표시됩니다.

   관련 옵션이 확장된 (**[!UICONTROL Sales]** > **[!UICONTROL Payment Services]** > _[!UICONTROL Settings]_) 홈 보기의 설정 영역으로 이동되었습니다. 이 영역에서 [!DNL Payment Services] 옵션을 [결제 방법](https://experienceleague.adobe.com/ko/docs/commerce-admin/config/sales/payment-methods/payment-methods){target="_blank"}(으)로 활성화할 수 있습니다.

1. _[!UICONTROL General Configuration]_&#x200B;에서&#x200B;**[!UICONTROL Enable]**&#x200B;을(를) `Yes`(으)로 설정합니다.
1. _[!UICONTROL Credit Card Fields]_&#x200B;과(와)_[!UICONTROL PayPal payment buttons]_ 모두에 대해 **[!UICONTROL Payment Action]**&#x200B;을(를) 다음 중 하나로 설정합니다.

   | 설정 | 설명 |
   |---|---|
   | `Authorize` | 구매를 승인하고 자금을 보류합니다. 상인에게 &#39;포착&#39;되기 전까지는 그 금액이 인출되지 않는다. |
   | `Authorize and Capture` | 구매를 승인하고 판매자가 자금을 &quot;캡처&quot;합니다. |

   >[!IMPORTANT]
   >
   >[!DNL Payment Services]은(는) 부분 캡처를 지원합니다. 판매자는 주문의 일부를 부분적으로 수집(송장)할 수 있습니다. 예를 들어 각 항목을 개별적으로 캡처하거나 지금 항목 하나와 나중에 항목 하나를 캡처할 수 있습니다.

1. **[!UICONTROL Save]**&#x200B;을(를) 클릭합니다.
1. [!DNL Payment Services] 홈으로 돌아가려면 **[!UICONTROL Go to Payment Services]**&#x200B;을(를) 클릭하십시오.
1. [캐시를 지웁니다](https://experienceleague.adobe.com/docs/commerce-admin/systems/tools/cache-management.html?lang=ko).

   모든 구성 변경 후 지우기를 수행해야 합니다.

신용 카드 필드 및 PayPal 결제 단추 구성에 대한 자세한 내용은 [결제 서비스 구성](settings.md)을 참조하십시오.

## 완전한 판매자 온보딩

스토어가 결제 서비스와 연동되도록 하는 다음 단계는 라이브 온보딩을 완료하는 것입니다.

결제 서비스는 운영하는 국가와 선호하는 결제 환경에 따라 [**고급**(전체 지원) 및 **표준**(빠른 체크아웃) 결제 옵션](../payment-services/payments-options.md#standard-vs-advanced-payments-experience)과(와) 온보딩 흐름을 제공합니다.

1. _관리자_ 사이드바에서 **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**(으)로 이동합니다.
1. **[!UICONTROL Live onboarding]**&#x200B;을(를) 클릭합니다.

   [!DNL Payment Services]에 대한 실시간 온보딩을 아직 완료하지 않은 경우 이 옵션이 표시됩니다.

1. _국가 선택_ 모달에서 운영 중인 국가를 선택합니다.

   결제 서비스는 현재 [5개국](../payment-services/introduction.md#availability)의 모든 결제 옵션을 완벽하게 지원합니다. 결제 서비스는 국가 목록에 표시된 다른 모든 국가에 대해 빠른 체크아웃 기능(결제 옵션의 하위 집합)을 제공합니다.

   목록에서 선택한 국가에 따라 결제 옵션이 결정되며, 온보딩 플로우([고급](#advanced-onboarding)(전체 지원) 또는 [표준](#standard-onboarding)(빠른 체크아웃))를 사용할 수 있습니다.

>[!TIP]
>
> 온보딩 옵션(Standard 또는 Advanced)을 선택하고 진행한 후에는 온보딩을 다시 완료하여 초기 선택에서 업그레이드 또는 다운그레이드해야 합니다.

### 고급 온보딩

이 온보딩 플로우는 [완전히 지원되는 국가](../payment-services/introduction.md#availability)의 판매자에 대해 사용할 수 있습니다.

국가를 선택한 후:

1. 표시되는 모달에서 **고급**&#x200B;을 선택합니다.

   **표준** 옵션의 경우 [표준 온보딩 흐름](#standard-onboarding)을 진행하십시오.

1. **계속**&#x200B;을 클릭합니다.
1. PayPal 계정 자격 증명(샌드박스 계정 자격 증명이 아님)을 사용하여 완전히 지원되는 고급 온보딩을 위해 PayPal 흐름을 계속 사용하거나 _또는_&#x200B;새 PayPal 계정에 등록하세요.

>[!IMPORTANT]
>
>**고급 온보딩**&#x200B;을(를) 사용하려면 가맹점이 [결제 권한을 요청](#request-payments-entitlement-from-adobe)해야 합니다.

### 표준 온보딩

이 표준 온보딩 플로우는 [빠른 체크아웃 지원](../payment-services/introduction.md#availability)이 제공되는 국가의 상인에 대해 사용할 수 있습니다.

국가를 선택한 후:

1. 표시되는 _결제 서비스 계약_ 양식에서 **결제 서비스 계약** 링크를 클릭하여 Adobe Commerce 결제 서비스 계약을 봅니다.
1. _결제 서비스 계약_ 양식에서 **동의함**&#x200B;을 클릭합니다.
1. PayPal 계정 자격 증명(샌드박스 계정 자격 증명이 아님)을 사용하거나 새 PayPal 계정에 등록하여 빠른 체크아웃 온보딩을 위한 PayPal 흐름을 계속 진행합니다.

>[!IMPORTANT]
>
>[Apple 결제 및 신용 카드 필드](../payment-services/payments-options.md)은(는) **표준 온보딩**&#x200B;에 사용할 수 없습니다.

## 이메일 주소 확인

1. 관리 사이드바에서 **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**(으)로 이동합니다.

   _[!UICONTROL Live onboarding]_&#x200B;단추가 더 이상 표시되지 않으며 &quot;[!UICONTROL Live payments pending]&quot; 텍스트 상자가 표시됩니다.

   이 텍스트 상자에는 온보딩을 완료하기 위해 PayPal을 사용하여 이메일 주소를 확인하라는 메시지가 표시될 수도 있습니다.

1. 이메일 주소를 확인하라는 메시지가 표시되면 PayPal에서 보낸 확인 메시지에 대해 이메일을 확인하고 을 클릭하여 이메일 주소를 확인합니다.
1. 관리 사이드바에서 **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**(으)로 이동합니다.
1. 브라우저 창을 새로 고칩니다.

   PayPal 판매자 온보딩이 승인되면 결제 시스템이 샌드박스 모드이고 라이브 결제를 처리하지 않는다는 알림이 표시됩니다.

   >[!IMPORTANT]
   >
   >[!DNL Adobe Commerce] 및 [!DNL Magento Open Source]에 대한 [!DNL Payment Services]&#x200B;(PayPal 계정 설정에서) 결제 처리에 대한 동의를 취소하는 경우 [!DNL Payment Services]이(가) 스토어의 주문을 처리할 수 없습니다. 결제 서비스 홈에서 해지된 동의에 대한 경고가 나타납니다.

## Adobe에서 결제 권한 요청

스토어를 라이브로 사용하려면 Adobe에 결제 권한을 요청하세요([고급 온보딩만](#advanced-onboarding)).

1. _관리자_ 사이드바에서 **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**(으)로 이동합니다.
1. [!DNL Payment Services] 홈에서 **[!UICONTROL Get Live Payments]**&#x200B;을(를) 클릭합니다.

   ![권한 요청](assets/request-entitlements.png){width="500" zoomable="yes"}

1. 양식을 작성합니다.
1. 영업팀 직원이 연락을 드릴 것입니다.

또는 [business.adobe.com](https://business.adobe.com/resources/payment-services.html)에서 Adobe에 결제 권한을 요청할 수 있습니다.

>[!IMPORTANT]
>
>결제 권한이 승인될 때까지 **실시간 온보딩**&#x200B;에 액세스할 수 없습니다.

## 가격 책정 계층 구성

[!DNL Payment Services] _판매자 ID_ 받기:

1. _관리자_ 사이드바에서 **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**(으)로 이동합니다.
1. 홈 보기에서 **[!UICONTROL Settings]**&#x200B;을(를) 클릭합니다. 자세한 내용은 [홈](payments-home.md)을 참조하세요.
1. 필요한 _판매자 ID_&#x200B;를 선택하고 영업 담당자에게 제출하면 영업 담당자가 올바른 가격 책정 계층을 구성합니다.

결제 거래에 대한 자세한 내용은 [수준 2 및 수준 3 처리](levels-card-payment-transactions.md)를 참조하십시오.

## 라이브 결제 활성화

_프로덕션 판매자 ID_&#x200B;이(가) 자동으로 생성되고 [구성](configure-admin.md)에서 채워집니다. 이 ID를 변경하거나 변경하지 마십시오.

라이브 결제 활성화:

1. _관리자_ 사이드바에서 **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**(으)로 이동합니다.
1. 홈에서 페이지의 오른쪽 상단에 있는 **[!UICONTROL Settings]**&#x200B;을(를) 클릭합니다. 자세한 내용은 [홈](payments-home.md)을 참조하세요.
1. _[!UICONTROL General Configuration]_&#x200B;섹션에서&#x200B;**[!UICONTROL Payment mode]**&#x200B;을(를) `Production`(으)로 설정합니다.
1. **[!UICONTROL Save]**&#x200B;을(를) 클릭합니다.
1. [캐시를 지웁니다](https://experienceleague.adobe.com/ko/docs/commerce-admin/systems/tools/cache-management){target="_blank"}.

   >[!IMPORTANT]
   >
   >캐시를 지우지 않으면 고객이 체크아웃 중에 PayPal 결제 옵션을 볼 수 없습니다.

[!DNL Payment Services] 홈으로 돌아오면 이제 실시간 결제를 처리하고 있으므로 더 이상 샌드박스 결제 모드 메시지가 나타나지 않습니다.

기존 구성 옵션에 대해서는 [관리에서 구성](configure-admin.md)을 참조하십시오.

>[!IMPORTANT]
>
>PayPal 계정 설정에서 결제 처리를 위해 [!DNL Payment Services]에 대한 동의를 취소하면 [!DNL Payment Services]이(가) 스토어의 주문을 처리할 수 없습니다. 결제 처리를 다시 활성화하려면 온보딩을 다시 완료해야 합니다. 결제 서비스 홈에서 해지된 동의에 대한 경고가 나타납니다.

## 프로덕션에서 테스트

이 기능을 쇼핑객에게 노출하기 전에 실제 신용 카드 및 은행으로 생산 시 결제를 테스트하는 것이 좋습니다.

자세한 내용은 [테스트 및 유효성 검사](test-validate.md)를 참조하십시오.
