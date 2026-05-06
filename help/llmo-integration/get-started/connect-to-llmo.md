---
title: ' [!DNL Adobe Commerce] to [!DNL Adobe LLM Optimizer] 연결'
description: 기회를 검토하거나 업데이트를 배포하기 전에 필요한 Commerce 서비스를 활성화하고, LLM Optimizer 연결을 구성하고, 카탈로그 액세스를 확인하고, 테넌트 준비 상태를 확인합니다.
role: Admin, User
recommendations: noCatalog
badgePaas: label="PaaS만" type="Informative" url="https://experienceleague.adobe.com/ko/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce 온 클라우드 프로젝트(Adobe 관리 PaaS 인프라) 및 온프레미스 프로젝트에만 적용됩니다."
source-git-commit: 47348a44ff7c5f890c10594f44cae6e771be046f
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 0%

---

# [!DNL Adobe Commerce]을(를) [!DNL Adobe LLM Optimizer]에 연결

>[!IMPORTANT]
>
>이 통합에 대한 액세스가 제한됩니다. 자세한 내용은 기술 계정 관리자에게 문의하십시오.

이 문서에서는 LLM Optimizer에서 사용할 수 있는 [!DNL Adobe Commerce] 카탈로그를 연결하는 방법에 대해 설명합니다.

>[!NOTE]
>
>이 문서에서는 통합의 Commerce 측면에 중점을 둡니다. LLM Optimizer에 대한 일반적인 정보는 [LLM Optimizer 제품 설명서](https://experienceleague.adobe.com/ko/docs/llm-optimizer/using/home)를 참조하세요.

## 필요한 Commerce 서비스 활성화 {#enable-commerce-services}

Commerce 관리자 또는 구현 파트너와 협력하여 다음 사항을 확인하십시오.

- LLM Optimizer이 읽어야 하는 카탈로그 데이터는 아키텍처(배포에 있는 모든 SaaS 데이터 내보내기 도구 또는 커넥터 포함)에 따라 **내보내거나 동기화됨**&#x200B;입니다.
- API 액세스, 자격 증명 및 환경 URL(샌드박스 및 프로덕션)이 LLM Optimizer에서 사용할 **테넌트**&#x200B;와(과) 일치합니다.

## LLM Optimizer에서 Commerce 연결 구성 {#configure-commerce-connection}

**Commerce 연결을 구성하려면:**

1. [!DNL Adobe LLM Optimizer] UI에서 **고객 구성**&#x200B;을 연 다음 **[!UICONTROL Commerce]** 탭을 선택합니다.

   고객 구성 탭의 ![Commerce 구성](../assets/llmo-commerce-config.png)

1. **[!UICONTROL Add Store View]**&#x200B;을(를) 클릭하여 새 행을 만들거나 기존 스토어 보기 항목을 확장하여 편집합니다.
1. **[!UICONTROL Store View URL]**&#x200B;을(를) 입력하십시오(필수).

   로케일이나 경로 접두사를 포함하여 해당 스토어 보기에 대한 상점 URL을 사용하십시오(예: `https://brand.example.com/` 또는 `https://brand.example.com/fr/`).

1. LLM Optimizer이 연결해야 하는 Adobe Commerce 환경의 식별자인 **[!UICONTROL Environment ID]**(필수)을(를) 입력하십시오.
1. **[!UICONTROL Website Code]**, **[!UICONTROL Store Code]** 및 **[!UICONTROL Store View Code]**&#x200B;을(를) 입력하십시오(필수).

   이러한 값은 연결하는 웹 사이트, 스토어 및 스토어 보기에 대한 Commerce 관리자의 코드와 일치해야 합니다.

1. 선택 사항: 해당 값이 URL과 다른 경우 Commerce 인스턴스의 호스트 이름(예: `www.example.com`)으로 **[!UICONTROL Host Name]**&#x200B;을(를) 입력하십시오.
1. API 액세스에 사용되는 Adobe Commerce 인스턴스의 기본 URL인 **[!UICONTROL Adobe Commerce Endpoint]**&#x200B;을(를) 입력하십시오.
1. Commerce API에 대한 요청을 인증하는 데 사용되는 **[!UICONTROL API Key]**&#x200B;을(를) 입력하거나 붙여 넣습니다.

   키를 다른 곳에 안전하게 복사해야 하는 경우 필드 옆에 있는 **[!UICONTROL Copy]**&#x200B;을(를) 클릭합니다.

1. 구성을 저장하려면 **[!UICONTROL Save]**&#x200B;을(를) 클릭합니다.

저장한 후 해당 저장소 보기에 대한 카탈로그 또는 감사 결과를 신뢰하기 전에 **초기 동기화** 또는 유효성 검사 작업이 완료될 때까지 기다리십시오.

저장소 보기 구성을 제거하려면 해당 항목을 열고 **[!UICONTROL Delete]**&#x200B;을(를) 클릭합니다.

### 필드 설명 {#commerce-connection-fields}

| 필드 | 설명 |
| --- | --- |
| 보기 URL 저장 | 스토어 보기 LLM Optimizer의 공개 URL은 카탈로그 및 감사 워크플로우의 범위에서 로 처리되어야 합니다. |
| 환경 ID | Commerce 환경 식별자(해당되는 경우 클라우드 또는 배포 설명서 또는 관리자). |
| 웹 사이트 코드 | 카탈로그를 소유한 웹 사이트의 Commerce **[!UICONTROL Website Code]**. |
| 코드 저장 | 해당 웹 사이트의 스토어에 대한 Commerce **[!UICONTROL Store Code]**. |
| 보기 코드 저장 | 스토어 보기에 대한 Commerce **[!UICONTROL Store View Code]**(예: `default`). |
| 호스트 이름 | 양식에서 다른 URL 외에 Commerce 상점 또는 인스턴스를 요청할 때 해당 인스턴스의 호스트 이름입니다. |
| Adobe Commerce 엔드포인트 | LLM Optimizer이 Commerce API에 도달하기 위해 사용하는 인스턴스 URL입니다. |
| API 키 | API 인증을 위한 비밀 키. 모든 프로덕션 자격 증명처럼 처리합니다. |

## 임차인 및 환경 준비 확인 {#confirm-tenant-readiness}

- 의도적으로 그렇게 하지 않는 한 연결된 **샌드박스** 프로젝트가 **프로덕션** Commerce 데이터와 혼합되지 않았는지 확인하십시오.
- 배포 작업을 승인하는 사람이 양쪽에서 올바른 권한을 가질 수 있도록 Experience Cloud 및 Commerce에서 **사용자 역할**&#x200B;을 맞춥니다.

## 다음 단계 {#next-steps}

[Adobe Commerce과 함께 LLM Optimizer을 사용](use-llmo-with-commerce.md)하여 기회를 검토하고, 카탈로그 업데이트를 배포하고, 재정의 동작을 이해합니다.
