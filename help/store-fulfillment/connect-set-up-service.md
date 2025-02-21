---
title: 스토어 이행 솔루션 연결
description: Adobe Commerce과 스토어 이행 솔루션 간의 연결을 설정합니다. Adobe Commerce 통합을 만들고 권한을 부여한 다음 Adobe Commerce 서비스 구성에 스토어 이행 계정 자격 증명을 추가합니다.
role: Admin, Developer
level: Intermediate
feature: Shipping/Delivery, Install, Configuration, User Account, Tools and External Services
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---

# 스토어 이행 솔루션 연결

필요한 인증 자격 증명 및 연결 데이터를 Adobe Commerce 관리자에 추가하여 스토어 이행 서비스를 Adobe Commerce과 연결합니다.

- **[구성 [!DNL Commerce integration settings]](#create-an-adobe-commerce-integration)**-스토어 이행 서비스에 대한 Adobe Commerce 통합을 만들고 액세스 토큰을 생성하여 스토어 이행 서버에서 들어오는 요청을 인증합니다.

- **[스토어 이행 서비스에 대한 계정 자격 증명을 구성합니다](#configure-store-fulfillment-account-credentials)**-자격 증명을 추가하여 Adobe Commerce을 스토어 이행 계정에 연결합니다.

>[!NOTE]
>
>테스트를 시작하기 전에 연결 구성을 완료하고 연결을 성공적으로 확인하십시오.

## Adobe Commerce 통합 만들기

Adobe Commerce을 스토어 이행 서비스와 통합하려면 Commerce 통합을 만들고 스토어 이행 서버의 요청을 인증하는 데 사용할 수 있는 액세스 토큰을 생성합니다. 또한 Adobe Commerce [!UICONTROL Consumer Settings] 옵션을 업데이트하여 Adobe Commerce에서 [!DNL Store Fulfillment] 서비스로의 요청에 대해 `The consumer isn't authorized to access %resources.` 응답 오류를 방지해야 합니다.

1. 관리자에서 스토어 이행 통합을 생성합니다.

   - 확장 이름 지정
   - 이메일 주소 입력
   - 관리자 계정 암호 입력

1. 다음과 통합하기 위한 API 리소스 액세스 권한을 구성합니다.

   - 판매 > BOPIS 주문 업데이트
   - 시스템 > 스토어 이행 앱 권한

1. 통합을 저장하고 활성화하여 인증용 액세스 토큰을 생성합니다.

1. 액세스 토큰을 복사하여 안전한 암호화된 위치에 저장합니다.

1. 계정 관리자와 협력하여 스토어 이행 측에서 구성을 완료하고 통합을 승인합니다.

1. [!UICONTROL Allow OAuth Access Tokens to be used as standalone Bearer tokens]에 Adobe Commerce [!UICONTROL Consumer Settings] 옵션을 사용하도록 설정합니다.

   - 책임자에서 **[!UICONTROL Stores]** > [!UICONTROL Configuration] > **[!UICONTROL Services]** > **[!UICONTROL OAuth]** > **[!UICONTROL Consumer Settings]**(으)로 이동합니다.

   - [!UICONTROL Allow OAuth Access Tokens to be used as standalone Bearer tokens] 옵션을 **[!UICONTROL Yes]**(으)로 설정합니다.

>[!IMPORTANT]
>
> 통합 토큰은 환경에 따라 다릅니다. 다른 환경의 소스 데이터가 있는 환경에 대한 데이터베이스를 복원하는 경우(예: 스테이징 환경에서 프로덕션 데이터 복원) 복원 작업 중에 통합 토큰 세부 정보를 덮어쓰지 않도록 `oauth_token` 테이블을 데이터베이스 내보내기에서 제외합니다.


## 저장소 이행 계정 자격 증명 구성

접수 양식을 완료한 후 월마트 스토어 이행 계정이 생성됩니다. 사용 가능한 경우 다음 자격 증명을 받게 됩니다.

- [!DNL Merchant ID]
- [!DNL Consumer ID]
- [!DNL Consumer Secret]
- [!DNL API Server URL]
- [!DNL Token Auth Server URL]&#x200B;(일반적으로 위의 구성과 동일)

저장소 이행 기능을 구성하고 사용하려면 이러한 자격 증명이 필요합니다.

>[!NOTE]
>
>계정 만들기 프로세스를 완료하는 데 시간이 걸릴 수 있습니다. 자격 증명을 기다리는 동안 [스토어 이행 솔루션에 대한 다른 설정을 검토하고 구성](service-config-settings-overview.md)합니다.

### 자격 증명을 추가하여 저장소 이행

1. 프로덕션 및 샌드박스 환경에 대해 [계정 자격 증명](enable-general.md)을 구성하십시오.

1. 관리자의 **[!UICONTROL Stores > Configuration > Services > Store Fulfillment by Walmart Commerce Technologies]**(으)로 이동

1. **[!UICONTROL Production environment]**&#x200B;에 대해 제공된 계정 자격 증명을 입력하십시오. 모든 필드는 필수입니다.

1. **[!UICONTROL Save Config]**&#x200B;을(를) 선택합니다.

1. **[!UICONTROL Validate Credentials]**&#x200B;을(를) 선택하여 연결을 테스트합니다.

>[!NOTE]
>
>자격 증명이 유효하지 않은 경우 각 환경에 대해 올바른 값을 입력했는지 확인하고 다시 확인합니다. 연결에 여전히 문제가 있는 경우 계정 담당자에게 문의하십시오.
