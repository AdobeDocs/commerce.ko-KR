---
title: '[!DNL Payment Services] 구성'
description: 설치 후 저장소 구성 시 [관리]에서  [!DNL Payment Services] 을(를) 구성할 수 있습니다.
role: Admin, User
level: Intermediate
exl-id: e1a3269d-bdf9-4b0f-972f-e8a0ef469503
feature: Payments, Checkout, Configuration
source-git-commit: efeca11f450906ec6fd4151e9de36f4ad7a999ab
workflow-type: tm+mt
source-wordcount: '2712'
ht-degree: 0%

---

# [!DNL Payment Services] 구성

관리자의 유용한 구성 옵션을 사용하여 필요에 맞게 [!DNL Payment Services]을(를) 사용자 지정할 수 있습니다.

관리자의 [!DNL Payment Services] 및 [!DNL Adobe Commerce]에 대해 [!DNL Magento Open Source]을(를) 구성할 때 해당 구성은 _[!UICONTROL Method]_&#x200B;의_[!UICONTROL General Configuration]_ 필드에 설정된 환경에만 적용됩니다. 구성 필드에서 변경한 내용은 _[!UICONTROL Method]_&#x200B;선택 항목을 전환하는 것과 관련이 없습니다. 메서드를 전환하는 경우 선택 항목이 재설정되지 않습니다.

## 일반 구성

스토어와 [!DNL Payment Services]에 대해 _[!UICONTROL Merchant Location]_&#x200B;을(를) 사용하도록 설정하고&#x200B;_[!UICONTROL General Configuration]_ 섹션에서 샌드박스 테스트 또는 실시간 결제를 사용하도록 설정할 수 있습니다.

1. _관리자_ 사이드바에서 **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**(으)로 이동합니다.
1. 왼쪽 패널에서 **[!UICONTROL Sales]**&#x200B;을(를) 확장하고 **[!UICONTROL Payment Methods]**&#x200B;을(를) 선택합니다.
1. _[!UICONTROL Merchant Country]_&#x200B;에서&#x200B;_[!UICONTROL Merchant Location]_ 필드를 설정합니다. _[!UICONTROL Merchant Country]_&#x200B;을(를) 지정하지 않으면 일반 구성의&#x200B;_[!UICONTROL Default Country]_&#x200B;이(가) 사용됩니다.
1. _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_&#x200B;섹션을 확장하여&#x200B;_[!UICONTROL [!DNL Payment Services]]_ 섹션에 액세스합니다.
1. _[!UICONTROL [!DNL Payment Services]]_&#x200B;섹션에서&#x200B;_[!UICONTROL General Configuration]_ 섹션을 확장합니다.
1. **사용**&#x200B;의 경우 스토어에 대해 `Yes`을(를) 사용하려면 [!DNL Payment Services]&#x200B;(으)로 설정하십시오.
1. **메서드**&#x200B;의 경우 스토어에 대해 `Sandbox`을(를) 테스트하는 경우 [!DNL Payment Services]&#x200B;(으)로 설정하고, 실시간 결제를 활성화할 준비가 된 경우 `Production`(으)로 설정하십시오.
1. **[!UICONTROL Payment Services Sandbox ID]** Commerce 서비스 커넥터&#x200B;**[!UICONTROL Payment Services Production ID]**&#x200B;를 설정하고 [&#x200B; 대시보드를 처음 방문하면 &#x200B;](https://experienceleague.adobe.com/ko/docs/commerce-merchant-services/user-guides/integration-services/saas){target=_blank} 및 [!DNL Payment Services] 값이 자동으로 채워집니다. 이렇게 하여 샌드박스 및/또는 프로덕션 환경에 대한 온보딩을 완료합니다. 이 값은 SaaS ID를 [!DNL Payment Services]에 연결합니다.

   >[!WARNING]
   >
   > Commerce 서비스 커넥터에서 데이터 공간 ID를 변경해야 하는 경우 [!DNL Payment Services] ID를 재설정해야 합니다. 샌드박스 ID를 재설정하려면 **결제 서비스 ID 재설정**&#x200B;을 클릭하세요. [!DNL Payment Services] 샌드박스 ID를 재설정하는 경우 다시 온보딩해야 합니다.

1. **[!UICONTROL PayPal Merchant ID]** 대시보드를 처음 방문하면 PayPal에서 **[!UICONTROL PayPal Merchant Status]** 및 [!DNL Payment Services] 값을 자동으로 제공합니다.
1. **소프트 설명자**(스토어/브랜드/카탈로그를 구분할 고객 거래 은행 거래 명세서에 표시되는 사용자 지정 값)의 경우 텍스트 필드에 사용자 지정 텍스트(최대 22자)를 추가하여 `Soft descriptor` 또는 기존 값을 바꿉니다.
1. 변경 내용을 저장하려면 **[!UICONTROL Save Config]**&#x200B;을(를) 클릭합니다.
1. **[!UICONTROL System]** > **[!UICONTROL Cache Management]**(으)로 이동한 다음 **[!UICONTROL Flush Cache]**&#x200B;을(를) 클릭하여 모든 잘못된 캐시를 새로 고칩니다.

### 구성 옵션

| 필드 | 범위 | 설명 |
|---|---|---|
| [!UICONTROL Enable] | 웹 사이트 | 웹 사이트에 대해 [!DNL Payment Services]을(를) 활성화하거나 비활성화합니다. 옵션: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Method] | 스토어 뷰 | 스토어에 대한 메서드 또는 환경을 설정합니다. 옵션: [!UICONTROL Sandbox] / [!UICONTROL Production] |
| [!UICONTROL Payment Services Sandbox ID] | 스토어 뷰 | 샌드박스 온보딩 중 자동으로 생성되는 샌드박스 판매자 ID입니다. |
| [!UICONTROL Payment Services Production ID] | 스토어 뷰 | 프로덕션(라이브) 온보딩 중에 자동으로 생성되는 프로덕션 판매자 ID입니다. |
| [!UICONTROL PayPal Merchant ID] | 스토어 뷰 | PayPal 계정을 만들 때 생성된 고유한 PayPal 판매자 계정 ID입니다. |
| [!UICONTROL PayPal Merchant Status] | 스토어 뷰 | PayPal 판매자 ID의 상태입니다. |
| [!UICONTROL Soft Descriptor] | 웹 사이트 또는 스토어 보기 | 웹 사이트 및 스토어 보기에 부드러운 설명자를 추가하여 브랜드, 스토어 또는 제품 라인을 설명하는 고객 거래에 정보를 추가합니다. |

## [!UICONTROL Credit Card Fields]

[!UICONTROL Credit Card Fields] 결제 옵션에서는 신용 카드 또는 직불 카드 결제 방법을 간단하고 안전하게 체크아웃할 수 있습니다.

자세한 내용은 [결제 옵션](payments-options.md#paypal-smart-buttons)을 참조하세요.

1. _관리자_ 사이드바에서 **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**(으)로 이동합니다.
1. 왼쪽 패널에서 **[!UICONTROL Sales]**&#x200B;을(를) 확장하고 **[!UICONTROL Payment Methods]**&#x200B;을(를) 선택합니다.
1. _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_&#x200B;섹션을 확장합니다.
1. _[!UICONTROL Payment Services]_&#x200B;섹션에서&#x200B;_[!UICONTROL Credit Card Fields]_ 섹션을 확장합니다.
1. **[!UICONTROL Title]**&#x200B;의 경우 필요한 경우 체크아웃 중에 표시된 대로 결제 방법 이름을 변경하려면 텍스트를 입력하십시오.
1. [결제 작업을 설정](production.md#set-payment-services-as-payment-method)하려면 **[!UICONTROL Authorize]** 또는 **승인 및 캡처**&#x200B;를 선택하십시오.
1. 체크아웃 페이지에서 결제 방법의 우선 순위를 지정하려면 `Numeric Only` 필드에 **[!UICONTROL Sort order]** 값을 입력하십시오.
1. **[!UICONTROL Show on checkout page]**&#x200B;의 경우 `Yes`을(를) 선택하여 체크아웃 페이지에서 신용 카드 필드를 사용하도록 설정합니다.
1. **[!UICONTROL Vault Enabled]**&#x200B;의 경우 `Yes`을(를) 선택하여 체크아웃에 신용 카드 보관을 사용하도록 설정하십시오.
1. **[!UICONTROL Vault Enabled in Admin]**&#x200B;에 대해 가맹점이 저장된 신용 카드를 사용하는 고객에 대한 주문을 만들 수 있도록 하려면 `Yes`을(를) 선택하십시오.
1. **[!UICONTROL 3D Secure authentication]**(기본적으로 `Off`)을(를) 사용하려면 `Always` 또는 `When required`을(를) 선택하십시오.
1. **[!UICONTROL Debug Mode]**&#x200B;의 경우 디버그 모드를 활성화하려면 `Yes`을(를) 선택하고 비활성화하려면 `No`을(를) 선택하십시오.
1. 변경 내용을 저장하려면 **[!UICONTROL Save Config]**&#x200B;을(를) 클릭합니다.
1. **[!UICONTROL System]** > **[!UICONTROL Cache Management]**(으)로 이동한 다음 **[!UICONTROL Flush Cache]**&#x200B;을(를) 클릭하여 모든 잘못된 캐시를 새로 고칩니다.

### 구성 옵션

| 필드 | 범위 | 설명 |
|---|---|---|
| [!UICONTROL Title] | 스토어 뷰 | 체크아웃 중에 결제 방법 보기에서 이 결제 방법의 제목으로 표시할 텍스트를 추가합니다. 옵션: [!UICONTROL text field] |
| [!UICONTROL Payment Action] | 웹 사이트 | 지정한 결제 방법에 대한 [결제 작업](https://experienceleague.adobe.com/docs/commerce-admin/config/sales/payment-methods/payment-methods.html?lang=ko). 옵션: [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Sort order] | 스토어 뷰 | 체크아웃 페이지에서 지정된 결제 방법에 대한 정렬 순서. `Numeric Only` 값 |
| [!UICONTROL Show on checkout page] | 웹 사이트 | 체크아웃 페이지에서 신용 카드 필드를 활성화 또는 비활성화합니다. 옵션: [!UICONTROL Yes] / [!UICONTROL No] |
| [!UICONTROL Vault enabled] | 스토어 뷰 | [신용 카드 보관](vaulting.md)을 활성화하거나 비활성화합니다. 옵션: [!UICONTROL Yes] / [!UICONTROL No] |
| [!UICONTROL Vault enabled in Admin] | 스토어 뷰 | [판매자가 보관된 결제 방법을 사용하여 &#x200B;](vaulting.md)에서 고객에 대한 주문을 완료할 수 있는 기능을 활성화하거나 비활성화합니다. 옵션: [!UICONTROL Yes] / [!UICONTROL No] |
| [!UICONTROL 3D Secure authentication] | 웹 사이트 | [3DS 보안 인증을 사용하거나 사용하지 않도록 설정](security.md#3ds). 옵션: [!UICONTROL Always] / [!UICONTROL When Required] / [!UICONTROL Off] |
| [!UICONTROL Debug Mode] | 웹 사이트 | 디버그 모드를 활성화하거나 비활성화합니다. 옵션: `[!UICONTROL Yes]` / `[!UICONTROL No]` |

## [!UICONTROL Fastlane]

[[!DNL Fastlane by PayPal]](https://www.paypal.com/us/cshelp/article/what-is-fastlane-by-paypal-help1096)은(는) 온라인에서 빠르고 간편하게 결제할 수 있는 방법입니다. **게스트 체크아웃**&#x200B;을 수행하는 동안 향후에 더욱 빠른 구매를 위해 카드와 배송 세부 정보를 안전하게 저장할 수 있습니다.

자세한 내용은 [결제 옵션](payments-options.md#fastlane-button)을 참조하세요.

1. _관리자_ 사이드바에서 **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**(으)로 이동합니다.
1. 왼쪽 패널에서 **[!UICONTROL Sales]**&#x200B;을(를) 확장하고 **[!UICONTROL Payment Methods]**&#x200B;을(를) 선택합니다.
1. _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_&#x200B;섹션을 확장합니다.
1. _[!UICONTROL Payment Services]_&#x200B;섹션에서&#x200B;_[!UICONTROL Fastlane]_ 섹션을 확장합니다.
1. 활성화하려면 `Yes`에 대해 **[!UICONTROL Enable Fastlane]**&#x200B;을(를) 선택합니다(`No`이(가) 비활성화함).

   >[!NOTE]
   >
   > [!UICONTROL Fastlane]이(가) 활성화된 경우 [!UICONTROL Credit Card Fields] 결제 옵션이 비활성화됩니다.

1. **[!UICONTROL Title]**&#x200B;의 경우 필요한 경우 체크아웃 중에 표시된 대로 결제 방법 이름을 변경하려면 텍스트를 입력하십시오. 기본 제목은 `Credit Card (via Fastlane)`입니다.
1. [결제 작업을 설정](production.md#set-payment-services-as-payment-method)하려면 **[!UICONTROL Authorize]** 또는 **승인 및 캡처**&#x200B;를 선택하십시오.
1. **[!UICONTROL 3D Secure Authentication for Fastlane]**(기본적으로 `Off`)을(를) 사용하려면 EU 규정을 준수하도록 `When required`을(를) 선택하거나, 사기 행위 보호 계층을 추가하도록 `Always`을(를) 선택하십시오.

   >[!NOTE]
   >
   > 카드 발급자에 3D 보안 인증이 필요한 경우 [!UICONTROL Payment Services] 구성에 관계없이 이 단계를 건너뛸 수 없습니다.

1. 체크아웃 페이지에서 결제 방법의 우선 순위를 지정하려면 `Numeric Only` 필드에 **[!UICONTROL Sort order]** 값을 입력하십시오.
1. [!UICONTROL Fastlane] 필드를 **[!UICONTROL Enable messaging]**(으)로 설정하여 Adobe Commerce에서 체크아웃 중에 `Yes` 브랜딩을 사용할지 여부를 지정합니다.
1. 변경 내용을 저장하려면 **[!UICONTROL Save Config]**&#x200B;을(를) 클릭합니다.
1. **[!UICONTROL System]** > **[!UICONTROL Cache Management]**(으)로 이동한 다음 **[!UICONTROL Flush Cache]**&#x200B;을(를) 클릭하여 모든 잘못된 캐시를 새로 고칩니다.

| 필드 | 범위 | 설명 |
|---|---|---|
| [!UICONTROL Enable Fastlane] | 스토어 뷰 | 체크아웃 페이지에서 [!DNL Fastlane]을(를) 활성화하거나 비활성화합니다. 옵션: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Title] | 스토어 뷰 | 체크아웃 중에 결제 방법 보기에서 이 결제 방법의 제목으로 표시할 텍스트를 추가합니다. 기본값은 `Credit Card (via Fastlane)`입니다. 옵션: [!UICONTROL text field] |
| [!UICONTROL Payment Action] | 웹 사이트 | 지정한 결제 방법에 대한 [결제 작업](https://experienceleague.adobe.com/docs/commerce-admin/config/sales/payment-methods/payment-methods.html?lang=ko). 옵션: [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL 3D Secure authentication] | 스토어 뷰 | Fastlane에 대한 [3D 보안 인증](security.md#3ds)을 활성화하거나 비활성화합니다. 옵션: [!UICONTROL Always] / [!UICONTROL When Required] / [!UICONTROL Off] |
| [!UICONTROL Sort order] | 스토어 뷰 | 체크아웃 페이지에서 지정된 결제 방법에 대한 정렬 순서. `Numeric Only` 값 |
| [!UICONTROL Enable messaging] | 스토어 뷰 | Adobe Commerce에서 체크아웃하는 동안 [!UICONTROL Fastlane] 브랜딩을 사용할지 여부를 지정하십시오. 옵션: `[!UICONTROL Yes]` / `[!UICONTROL No]` |

### 선택 사항입니다. 고급 스타일 설정

이러한 옵션 설정은 [!UICONTROL Fastlane]이(가) 웹 사이트에 표시되는 방식을 사용자 지정할 수 있습니다.

>[!TIP]
>
>액세스 가능성 지침을 충족하지 않는 스타일은 기본 설정으로 되돌아갑니다.

1. _[!UICONTROL Payment Services]_&#x200B;섹션에서&#x200B;_[!UICONTROL Fastlane]_ 섹션으로 이동합니다.
1. _[!UICONTROL Advanced Style Settings (optional)]_&#x200B;섹션을 확장합니다.
1. 필요에 따라 설정을 수정합니다.
1. 변경 내용을 저장하려면 **[!UICONTROL Save Config]**&#x200B;을(를) 클릭합니다.

사용자 지정에 대한 자세한 내용은 [PayPal 개발자 문서](https://developer.paypal.com/limited-release/accelerated-checkout-bt/)를 참조하십시오.

#### 루트 설정

이러한 옵션 설정은 전체 [!UICONTROL Fastlane] 체크 아웃 구성 요소를 수정합니다.

| 필드 | 범위 | 설명 |
|---|---|---|
| [!UICONTROL Background Color] | 스토어 뷰 | 구성 요소의 배경색을 정의합니다. `RGB`개 값만 |
| [!UICONTROL Border Color] | 스토어 뷰 | 구성 요소의 테두리 색상을 정의합니다. `RGB`개 값만 |
| [!UICONTROL Font Family] | 스토어 뷰 | 구성 요소의 글꼴을 설정합니다. 테마에서 사용할 수 있는 글꼴만 표시됩니다 |
| [!UICONTROL Font Size Base] | 스토어 뷰 | 글꼴 크기를 정의합니다. `px`개(픽셀) 값만 |
| [!UICONTROL Padding] | 스토어 뷰 | 구성 요소의 패딩을 설정합니다. `px`개(픽셀) 값만 |
| [!UICONTROL Primary Color] | 스토어 뷰 | 구성 요소의 기본 색상을 정의합니다. `RGB`개 값만 |
| [!UICONTROL Text Color] | 스토어 뷰 | 구성 요소 텍스트의 주 색상을 정의합니다. `RGB`개 값만 |

#### 입력 설정

이러한 선택적 설정은 [!UICONTROL Fastlane] 구성 요소의 고객 입력 필드에 적용됩니다.

| 필드 | 범위 | 설명 |
|---|---|---|
| [!UICONTROL Background Color] | 스토어 뷰 | 구성 요소의 배경색을 정의합니다. `RGB`개 값만 |
| [!UICONTROL Border Color] | 스토어 뷰 | 구성 요소의 테두리 색상을 정의합니다. `RGB`개 값만 |
| [!UICONTROL Border Radius] | 스토어 뷰 | 테두리 반경을 정의합니다. `px`개(픽셀) 값만 |
| [!UICONTROL Border Width] | 스토어 뷰 | 테두리 폭을 정의합니다. `px`개(픽셀) 값만 |
| [!UICONTROL Focus Border Color] | 스토어 뷰 | 구성 요소의 포커스 테두리 색상을 정의합니다. `RGB`개 값만 |
| [!UICONTROL Text Color Base] | 스토어 뷰 | 구성 요소 텍스트의 주 색상을 정의합니다. `RGB`개 값만 |

## [!UICONTROL Apple Pay]

[!DNL Apple Pay]을(를) 사용하면 판매자는 Safari에서 안전하고 빠르고 매끄러운 체크아웃 환경을 제공하여 판매자 계정당 최대 99개의 도메인을 지원할 수 있습니다. [!DNL Apple Pay] 버튼을 사용하면 고객의 iOS 또는 macOS 장치에서 결제, 연락처 및 배송 정보가 자동으로 채워져 전환율을 높이는 데 도움이 되는 빠른 한 번 클릭 구매를 수행할 수 있습니다.

자세한 내용은 [결제 옵션](payments-options.md#apple-pay-button)을 참조하세요.

1. _관리자_ 사이드바에서 **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**(으)로 이동합니다.
1. 왼쪽 패널에서 **[!UICONTROL Sales]**&#x200B;을(를) 확장하고 **[!UICONTROL Payment Methods]**&#x200B;을(를) 선택합니다.
1. _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_&#x200B;섹션을 확장합니다.
1. _[!UICONTROL Payment Services]_&#x200B;섹션에서&#x200B;_[!UICONTROL Apple Pay]_ 섹션을 확장합니다.
1. **[!UICONTROL Title]**&#x200B;의 경우 필요한 경우 체크아웃 중에 표시된 대로 결제 방법 이름을 변경하려면 텍스트를 입력하십시오.
1. [결제 작업을 설정](production.md#set-payment-services-as-payment-method)하려면 **[!UICONTROL Authorize]** 또는 **[!UICONTROL Authorize and Capture]**&#x200B;을(를) 선택하십시오.
1. 필요에 따라 다음 옵션에서 [!DNL Apple Pay]을(를) 선택하여 Adobe Commerce에서 `Yes` 옵션이 활성화된 위치를 지정하십시오.
   * **[!UICONTROL Show Apple Pay on checkout page]**
   * **[!UICONTROL Show Apple Pay on product detail page]**
   * **[!UICONTROL Show Apple Pay in mini cart preview]**
   * **[!UICONTROL Show Apple Pay on cart page]**
1. 디버그 모드를 사용하려면 `Yes`에 대해 **[!UICONTROL Debug Mode]**&#x200B;을(를) 선택합니다(`No`이(가) 비활성화함).
1. 변경 내용을 저장하려면 **[!UICONTROL Save Config]** 을(를) 클릭합니다.
1. **[!UICONTROL System]** > **[!UICONTROL Cache Management]**(으)로 이동한 다음 **[!UICONTROL Flush Cache]**&#x200B;을(를) 클릭하여 모든 잘못된 캐시를 새로 고칩니다.

### 구성 옵션

| 필드 | 범위 | 설명 |
|---|---|---|
| [!UICONTROL Title] | 스토어 뷰 | 체크아웃 중에 결제 방법 보기에서 이 결제 방법의 제목으로 표시할 텍스트를 추가합니다. 옵션: [!UICONTROL text field] |
| [!UICONTROL Payment Action] | 웹 사이트 | 지정한 결제 방법에 대한 [결제 작업](https://experienceleague.adobe.com/docs/commerce-admin/config/sales/payment-methods/payment-methods.html?lang=ko). 옵션: [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Show on checkout page] | 웹 사이트 | 체크아웃 페이지에서 [!DNL Apple Pay]을(를) 활성화하거나 비활성화합니다. 옵션: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Sort order] | 스토어 뷰 | 체크아웃 페이지에서 지정된 결제 방법에 대한 정렬 순서. `Numeric Only` 값 |
| [!UICONTROL Show buttons on product detail page] | 스토어 뷰 | 제품 세부 정보 페이지에서 [!DNL Apple Pay]을(를) 활성화하거나 비활성화합니다. 옵션: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons in mini-cart preview] | 스토어 뷰 | 미니 장바구니 미리 보기에서 [!DNL Apple Pay]을(를) 활성화하거나 비활성화합니다. 옵션: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons on cart page] | 스토어 뷰 | 장바구니 페이지에서 [!DNL Apple Pay]을(를) 활성화하거나 비활성화합니다. 옵션: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Debug Mode] | 웹 사이트 | 디버그 모드를 활성화하거나 비활성화합니다. 옵션: `[!UICONTROL Yes]` / `[!UICONTROL No]` |

## [!UICONTROL Google Pay]

[!UICONTROL Google Pay] 결제 옵션을 통해 가맹점은 구매 고객에게 Google Pay를 제공할 수 있으며, 구매자는 장치에서 Google Wallet을 사용하여 구매할 수 있습니다.

자세한 내용은 [결제 옵션](payments-options.md#google-pay-button)을 참조하세요.

1. _관리자_ 사이드바에서 **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**(으)로 이동합니다.
1. 왼쪽 패널에서 **[!UICONTROL Sales]**&#x200B;을(를) 확장하고 **[!UICONTROL Payment Methods]**&#x200B;을(를) 선택합니다.
1. _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_&#x200B;섹션을 확장합니다.
1. _[!UICONTROL Payment Services]_&#x200B;섹션에서&#x200B;_[!UICONTROL Google Pay]_ 섹션을 확장합니다.
1. (선택 사항) **[!UICONTROL Title]** 필드에 새 이름을 입력하여 체크아웃 중에 표시되는 결제 방법의 이름을 변경합니다.
1. [&#x200B; 또는 &#x200B;](production.md#set-payment-services-as-payment-method)을(를) 선택하여 **[!UICONTROL Authorize]**&#x200B;결제 작업을 설정&#x200B;**[!UICONTROL Authorize and Capture]**&#x200B;합니다.
1. 필요에 따라 다음 옵션에서 [!DNL Google Pay]을(를) 선택하여 Adobe Commerce에서 `Yes` 옵션이 활성화된 위치를 지정하십시오.
   * **[!UICONTROL Show Google Pay on checkout page]**
   * **[!UICONTROL Show Google Pay on product detail page]**
   * **[!UICONTROL Show Google Pay in mini cart preview]**
   * **[!UICONTROL Show Google Pay on cart page]**
1. **[!UICONTROL 3D Secure authentication]**(기본적으로 `Off`)을(를) 사용하려면 `Always` 또는 `When required`을(를) 선택하십시오.
1. 디버그 모드를 사용하려면 `Yes`에 대해 **[!UICONTROL Debug Mode]**&#x200B;을(를) 선택합니다(`No`이(가) 비활성화함).
1. 필요에 따라 _[!UICONTROL Google Pay]_,**[!UICONTROL Button Color]**&#x200B;및&#x200B;**[!UICONTROL Button Type]**&#x200B;을(를) 선택하여&#x200B;**[!UICONTROL Button Style]**&#x200B;단추의 모양을 구성합니다.
1. 높이를 설정하려면 **[!UICONTROL Button Style]**&#x200B;에 정의된 높이의 기본값을 사용합니다.
1. 변경 내용을 저장하려면 **[!UICONTROL Save Config]** 을(를) 클릭합니다.
1. **[!UICONTROL System]** > **[!UICONTROL Cache Management]**(으)로 이동한 다음 **[!UICONTROL Flush Cache]**&#x200B;을(를) 클릭하여 모든 잘못된 캐시를 새로 고칩니다.

### 구성 옵션

| 필드 | 범위 | 설명 |
|---|---|---|
| [!UICONTROL Title] | 스토어 뷰 | 체크아웃 중에 결제 방법 보기에 이 결제 옵션에 대해 표시되는 텍스트 레이블을 지정합니다. 옵션: `[!UICONTROL text field]` |
| [!UICONTROL Payment Action] | 웹 사이트 | 지정한 결제 방법에 대한 [결제 작업](https://experienceleague.adobe.com/docs/commerce-admin/config/sales/payment-methods/payment-methods.html?lang=ko). 옵션: `[!UICONTROL Authorize]` / `[!UICONTROL Authorize and Capture]` |
| [!UICONTROL Show on checkout page] | 웹 사이트 | 체크아웃 페이지에서 [!DNL Google Pay]을(를) 활성화하거나 비활성화합니다. 옵션: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Sort order] | 스토어 뷰 | 체크아웃 페이지에서 지정된 결제 방법에 대한 정렬 순서. `Numeric Only` 값 |
| [!UICONTROL Show buttons on product detail page] | 스토어 뷰 | 제품 세부 정보 페이지에서 [!DNL Google Pay]을(를) 활성화하거나 비활성화합니다. 옵션: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons in mini-cart preview] | 스토어 뷰 | 미니 장바구니 미리 보기에서 [!DNL Google Pay]을(를) 활성화하거나 비활성화합니다. 옵션: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons on cart page] | 스토어 뷰 | 장바구니 페이지에서 [!DNL Google Pay]을(를) 사용하거나 사용하지 않도록 설정합니다. 옵션: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL 3D Secure authentication] | 스토어 뷰 | [3D 보안 인증을 사용하거나 사용하지 않도록 설정합니다](security.md#3ds). 옵션: [!UICONTROL Always] / [!UICONTROL When Required] / [!UICONTROL Off] |
| [!UICONTROL Debug Mode] | 웹 사이트 | 디버그 모드를 활성화하거나 비활성화합니다. 옵션: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Button Color] | 스토어 뷰 | [!DNL Google Pay] 단추의 색상을 정의합니다. 옵션: `[!UICONTROL Default]` / `[!UICONTROL Black]` / `[!UICONTROL White]` |
| [!UICONTROL Button Type] | 스토어 뷰 | [!DNL Google Pay] 단추의 형식을 정의합니다. 옵션: `[!UICONTROL buy]` / `[!UICONTROL checkout]` / `[!UICONTROL order]` / `[!UICONTROL pay]` / `[!UICONTROL plain]` |

자세한 내용은 [Google Pay API 요청 개체 옵션](https://developers.google.com/pay/api/web/reference/request-objects) 설명서를 참조하십시오.

## [!DNL PayPal Payment Buttons]

[!DNL PayPal payment buttons] 결제 옵션은 고객에게 간단하고 빠르고 안전한 체크아웃 프로세스를 제공합니다.

자세한 내용은 [결제 옵션](payments-options.md#paypal-smart-buttons)을 참조하세요.

[!DNL PayPal payment buttons] 구성

관리자 내에서 PayPal 결제 버튼 결제 옵션을 활성화하고 구성할 수 있습니다.

1. _관리자_ 사이드바에서 **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**(으)로 이동합니다.
1. 왼쪽 패널에서 **[!UICONTROL Sales]**&#x200B;을(를) 확장하고 **[!UICONTROL Payment Methods]**&#x200B;을(를) 선택합니다.
1. _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_&#x200B;섹션을 확장합니다.
1. _[!UICONTROL Payment Services]_&#x200B;섹션에서&#x200B;_[!UICONTROL PayPal payment buttons]_ 섹션을 확장합니다.
1. 결제 방법 이름을 변경하려면 _[!UICONTROL Title]_&#x200B;필드를 편집합니다.
1. [결제 작업을 설정](production.md#set-payment-services-as-payment-method)하려면 **[!UICONTROL Authorize]** 또는 **[!UICONTROL Authorize and Capture]**&#x200B;을(를) 선택하십시오.
1. 체크아웃 페이지에서 결제 방법의 우선 순위를 지정하려면 `Numeric Only` 필드에 **[!UICONTROL Sort order]** 값을 입력하십시오.
1. [나중에 결제 메시지](payments-options.md#pay-later-button)를 활성화/비활성화하려면 `Yes`에 대해 `No`/**[!UICONTROL Display Pay Later Message]**&#x200B;을(를) 선택하십시오.

   * [나중에 결제 메시지](payments-options.md#pay-later-button)를 사용하도록 설정하면 **[!UICONTROL Configure Messaging]**&#x200B;의 스타일을 설정할 수 있도록 **[!UICONTROL PayPal Pay Later messaging]** 모달 단추가 표시됩니다.

1. 필요에 따라 다음 옵션에서 `Yes`을(를) 선택하여 Adobe Commerce에서 PayPal 결제 단추를 사용할 수 있는 위치를 지정하십시오.
   * **[!UICONTROL Show buttons on checkout page]**
   * **[!UICONTROL Show buttons on product detail page]**
   * **[!UICONTROL Show buttons in mini cart preview]**
   * **[!UICONTROL Show buttons on cart page]**
1. Venmo를 결제 옵션으로 사용하려면 `Yes`에 대해 **[!UICONTROL Venmo Enabled]**&#x200B;을(를) 선택하십시오.
1. 신용 카드와 직불 카드를 결제 옵션으로 사용하려면(PayPal 스마트 단추) `Yes`에 대해 **[!UICONTROL Credit and Debit Card Enabled]**&#x200B;을(를) 선택하십시오.
1. [PayPal 나중에 결제](payments-options.md#pay-later-button) 결제 옵션을 활성화/비활성화하려면 `Yes`에 대해 `No`/**[!UICONTROL PayPal Pay Later Enabled]**&#x200B;을(를) 선택하십시오.
1. 디버그 모드를 사용하려면 `Yes`에 대해 **[!UICONTROL Debug Mode]**&#x200B;을(를) 선택합니다(`No`이(가) 비활성화함).
1. 변경 내용을 저장하려면 **[!UICONTROL Save Config]** 을(를) 클릭합니다.
1. **[!UICONTROL System]** > **[!UICONTROL Cache Management]**(으)로 이동한 다음 **[!UICONTROL Flush Cache]**&#x200B;을(를) 클릭하여 모든 잘못된 캐시를 새로 고칩니다.

### 구성 옵션

| 필드 | 범위 | 설명 |
|---|---|---|
| [!UICONTROL Title] | 스토어 뷰 | 체크아웃 중에 결제 방법 보기에서 이 결제 방법의 제목으로 표시할 텍스트를 추가합니다. 옵션: 텍스트 필드 |
| [!UICONTROL Payment Action] | 웹 사이트 | 지정한 결제 방법에 대한 [결제 작업](https://experienceleague.adobe.com/ko/docs/commerce-admin/config/sales/payment-methods/payment-methods#payment-actions){target="_blank"}. 옵션: [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Display Pay Later Message] | 웹 사이트 | 장바구니, 제품 페이지, 미니 장바구니에서, 그리고 체크아웃 흐름 중에 PayPal 나중에 결제 메시지를 활성화하거나 비활성화합니다. 옵션: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Configure Messaging] | 스토어 뷰 | PayPal Pay Later 메시징 스타일을 수정합니다. 옵션: `[!UICONTROL Product page]` / `[!UICONTROL Cart]` |
| [!UICONTROL Show buttons on checkout page] | 스토어 뷰 | 체크아웃 페이지에서 [!DNL PayPal payment buttons]을(를) 활성화하거나 비활성화합니다. 옵션: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons on product detail page] | 스토어 뷰 | 제품 세부 정보 페이지에서 [!DNL PayPal payment buttons]을(를) 활성화하거나 비활성화합니다. 옵션: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons in mini-cart preview] | 스토어 뷰 | 미니 장바구니 미리 보기에서 [!DNL PayPal payment buttons]을(를) 활성화하거나 비활성화합니다. 옵션: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons on cart page] | 스토어 뷰 | 장바구니 페이지에서 [!DNL PayPal payment buttons]을(를) 활성화하거나 비활성화합니다. 옵션: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Venmo Enabled] | 스토어 뷰 | 결제 버튼이 표시되는 Venmo 결제 옵션을 활성화하거나 비활성화합니다. 옵션: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Credit and Debit Card Enabled] | 스토어 뷰 | 결제 버튼이 표시되는 신용 카드 및 직불 카드 옵션을 활성화하거나 비활성화합니다. 옵션: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL PayPal Pay Later Enabled] | 스토어 뷰 | 결제 버튼이 표시되는 PayPal Pay Later 결제 옵션 모양을 활성화하거나 비활성화합니다. 옵션: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Debug Mode] | 웹 사이트 | 디버그 모드를 활성화하거나 비활성화합니다. 옵션: `[!UICONTROL Yes]` / `[!UICONTROL No]` |

## 단추 스타일

결제 버튼의 _[!UICONTROL Button style]_&#x200B;옵션을 구성할 수도 있습니다.

1. _관리자_ 사이드바에서 **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**(으)로 이동합니다.
1. 왼쪽 패널에서 **[!UICONTROL Sales]**&#x200B;을(를) 확장하고 **[!UICONTROL Payment Methods]**&#x200B;을(를) 선택합니다.
1. _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_&#x200B;섹션을 확장합니다.
1. _[!UICONTROL [!DNL Payment Services]]_&#x200B;섹션에서&#x200B;_[!UICONTROL PayPal Smart Button Styling]_ 섹션을 확장합니다.
1. 레이아웃을 설정하려면 `Vertical`에 대해 `Horizontal` 또는 **[!UICONTROL Layout]**&#x200B;을(를) 선택하십시오
1. 색상을 설정하려면 **[!UICONTROL Color]**&#x200B;에서 사용 가능한 색상 중에서 선택하십시오.
1. 모양을 설정하려면 `Rectangular`에 대해 `Pill` 또는 **[!UICONTROL Shape]**&#x200B;을(를) 선택하십시오.
1. 기본 높이를 사용하려면 `Yes`에 대해 `No` 또는 **[!UICONTROL Use Default Height]**&#x200B;을(를) 선택하십시오.
1. 사용자 지정 높이를 설정하려면 **[!UICONTROL Height]**&#x200B;에 대해 원하는 픽셀 높이를 추가하십시오.
1. 태그 라인을 설정하려면 `Yes`에 대해 `No` 또는 **[!UICONTROL Tagline]**&#x200B;을(를) 선택하십시오.
1. 변경 내용을 저장하려면 **[!UICONTROL Save Config]** 을(를) 클릭합니다.
1. **[!UICONTROL System]** > **[!UICONTROL Cache Management]**(으)로 이동한 다음 **[!UICONTROL Flush Cache]**&#x200B;을(를) 클릭하여 모든 잘못된 캐시를 새로 고칩니다.

### 구성 옵션

| 필드 | 범위 | 설명 |
|--- |--- |--- |
| [!UICONTROL Layout] | 스토어 뷰 | Paypal 결제 버튼에 대한 레이아웃 스타일을 정의합니다. 옵션: `[!UICONTROL Vertical]` / `[!UICONTROL Horizontal]` |
| [!UICONTROL Color] | 스토어 뷰 | Paypal 결제 버튼의 색상을 정의합니다. 옵션: [!UICONTROL Blue] / `[!UICONTROL Gold]` / `[!UICONTROL Silver]` / `[!UICONTROL White]` / `[!UICONTROL Black]` |
| [!UICONTROL Shape] | 스토어 뷰 | Paypal 결제 버튼의 모양을 정의합니다. 옵션: `[!UICONTROL Rectangular]` / `[!UICONTROL Pill]` |
| [!UICONTROL Use Default Height] | 스토어 뷰 | PayPal 결제 단추에서 기본 높이를 사용하는지 여부를 정의합니다. 옵션: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Height] | 스토어 뷰 | PayPal 결제 버튼의 높이를 정의합니다. 기본값: 없음 |
| [!UICONTROL Label] | 스토어 뷰 | PayPal 결제 단추에 표시되는 레이블을 정의합니다. 옵션: `[!UICONTROL PayPal]` / `[!UICONTROL Checkout]` / `[!UICONTROL Buynow]` / `[!UICONTROL Pay]` / `[!UICONTROL Installment]` |
| [!UICONTROL Tagline] | 스토어 뷰 | 태그 지정을 활성화합니다. 옵션: `[!UICONTROL Yes]` / `[!UICONTROL No]` |

## 캐시 초기화

Apple Pay, Venmo 또는 PayPal PayLater 단추를 전환하는 등 _설정_&#x200B;에서 구성을 변경하는 경우 저장소에 최신 구성이 표시되도록 캐시를 수동으로 플러시하십시오.

1. _관리자_ 사이드바에서 **[!UICONTROL System]** > **[!UICONTROL Cache Management]**(으)로 이동합니다.
1. 잘못된 모든 캐시를 새로 고치려면 **[!UICONTROL Flush Cache]**&#x200B;을(를) 클릭합니다.

캐시 관리 테이블의 캐시 유형이 `INVALIDATED` 상태인 경우 저장소에 해당 항목에 대한 최신 구성이 표시되지 않을 수 있습니다. 최신 구성을 표시하도록 저장소를 업데이트하려면 캐시를 플러시하십시오.

저장소에 올바른 구성이 표시되는지 확인하려면 주기적으로 [캐시를 플러시](https://experienceleague.adobe.com/ko/docs/commerce-admin/systems/tools/cache-management)합니다.

## 역할 구성

관리자 사용자가 Commerce 관리에서 주문을 만들고 관리할 수 있도록 하려면 사용자 역할에 [!DNL Payment Services]별 리소스를 사용하도록 설정하십시오.

역할을 관리하는 방법은 [사용자 역할](https://experienceleague.adobe.com/docs/commerce-admin/systems/user-accounts/permissions-user-roles.html?lang=ko)을 참조하세요.

역할에 리소스를 할당할 때 다음을 선택해야 합니다.

* **결제 방법:[!DNL Payment Services]**—이 리소스는 관리자에서 주문을 만들 때 결제 방법으로 [!DNL Payment Services]개의 신용 카드를 사용할 수 있도록 합니다. **Actions** 상위 리소스를 선택하면 이 리소스도 선택됩니다.

* **[!DNL Payment Services]**—이 리소스에는 **대시보드** 및 **SaaS 서비스 프록시** 리소스가 포함되어 있으며, 이 리소스도 선택해야 합니다. [!DNL Payment Services]이(가) _판매_ 메뉴에 나타나는지 확인합니다.

  ![결제 서비스 리소스](assets/roles-payments.png){width="400" zoomable="yes"}


## 카드 보관

고객이 향후 구매를 위해 사용할 신용 카드 정보를 내 계정에 저장(저장)할 수 있는 기능을 활성화할 수 있습니다.

또한 관리자의 카드 보관을 사용하여 기존 고객에 대한 후속 주문을 완료할 수 있습니다.

[신용 카드 필드 설정](#credit-card-fields)에서 카드 보관을 활성화하거나 비활성화합니다.

자세한 내용은 [신용 카드 보관](vaulting.md)을 참조하세요.

## 3DS

3DS는 고객 및 상인의 매장 내 사기 행위를 방지하고 유럽 연합(EU) 표준을 준수할 수 있도록 해줍니다.

[신용 카드 필드 설정](#credit-card-fields)에서 3DS를 활성화하거나 비활성화합니다.

자세한 내용은 [보안의 3DS](security.md#3ds)를 참조하십시오.

## 여러 PayPal 계정 사용

[!UICONTROL Payment Services]에서 웹 사이트 수준의 **one** 판매자 계정 내에서 여러 PayPal 계정을 사용할 수 있습니다. 예를 들어, 여러 국가([다양한 통화](https://experienceleague.adobe.com/ko/docs/commerce-admin/stores-sales/site-store/currency/currency) 사용)에서 스토어를 운영하거나 비즈니스의 일부에 Adobe Commerce을 사용하려고 하지만 _모두_&#x200B;는 사용하지 않으려는 경우, 판매자 계정을 설정하여 여러 PayPal 계정을 사용할 수 있습니다.

웹 사이트, 스토어 및 스토어 보기의 계층 구조에 대한 자세한 내용은 [사이트, 스토어 및 보기 범위](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html?lang=ko)를 참조하십시오.

CLI를 통해 여러 PayPal 계정에 대한 범위를 구성하는 방법에 대한 자세한 내용은 [명령줄 구성](configure-cli.md#configure-scope-via-cli)을 참조하십시오.

영업 사원은 판매자 계정에 대한 새 [scope](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html?lang=ko#scope-settings)을(를) 만들고 PayPal로 추가 사이트를 온보딩하여 표시되는 PayPal 단추가 사이트에 표시되도록 할 수 있습니다. 영업 담당자에게 문의
웹 사이트에서 여러 PayPal 계정을 사용하는 데 도움이 되는 담당자.
