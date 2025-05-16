---
title: 사용자 관리
description: ' [!DNL Adobe Commerce as a Cloud Service]에서 사용자를 관리하는 방법을 알아봅니다.'
exl-id: 9bc80fe6-6dfd-4bb3-8dc5-d5efd8a8d90c
badgeSaas: label="SaaS만" type="Positive" url="https://experienceleague.adobe.com/ko/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."
source-git-commit: 34057c1e55ff117ea7aab4407f31548ce826691b
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 0%

---

# 사용자 관리

{{accs-early-access}}

사용자가 [!DNL Adobe Commerce as a Cloud Service]에서 관리자에 액세스하려면 해당 사용자를 조직의 사용자로 추가하고 [Adobe Admin Console](https://adminconsole.adobe.com){target="_blank"}의 Cloud Service 제품에 액세스할 수 있는지 확인해야 합니다.

이 프로세스에는 [!DNL Adobe Commerce as a Cloud Service]에 액세스할 수 있는 IMS 조직이 필요합니다. 조직의 시스템 관리자 또는 제품 관리자만 이러한 프로세스를 수행할 수 있습니다.

>[!TIP]
>
>여러 사용자를 동시에 추가하려면 [일괄 CSV 업로드](https://helpx.adobe.com/kr/enterprise/using/bulk-upload-users.html){target="_blank"}를 수행할 수 있습니다.
> 
> [사용자 그룹](https://helpx.adobe.com/kr/enterprise/using/user-groups.html){target="_blank"}을 만들어 역할에 여러 사용자를 추가할 수도 있습니다. 그런 다음 [!UICONTROL **Adobe Commerce as a Cloud Service - 백엔드**] 제품을 사용자 그룹에 추가할 수 있습니다.

## 역할 이해

[!DNL Adobe Commerce as a Cloud Service]에 사용할 수 있는 역할은 다음과 같습니다. 이러한 역할을 보거나 편집하려면 Commerce 관리에서 **시스템** > **권한** > **사용자 역할**(으)로 이동합니다.

* **사용자** - 사용자는 Commerce 관리자에 대한 관리자 액세스 권한이 있지만 Admin Console에서 제품 수준 액세스를 관리할 수 없습니다. [!DNL Commerce Cloud Manager]에서 [인스턴스 만들기](./getting-started.md#create-an-instance)에 크레딧을 사용할 수도 있습니다.

* [**개발자**](https://helpx.adobe.com/kr/enterprise/using/manage-developers.html#Adddevelopers){target="_blank"} 개발자는 사용자 권한이 있으며 Commerce 인스턴스에 개발자 사용자로 추가됩니다. 즉, [관리 UI SDK](https://developer.adobe.com/commerce/extensibility/admin-ui-sdk/){target="_blank"}, [이벤트 구성](https://developer.adobe.com/commerce/extensibility/events/){target="_blank"} 및 [웹후크 만들기](https://developer.adobe.com/commerce/extensibility/webhooks/){target="_blank"}를 사용할 수 있습니다.

* 관리자 - 세 가지 유형의 관리자가 있습니다.
   * [시스템 관리자](https://helpx.adobe.com/kr/enterprise/using/admin-roles.html){target="_blank"} - 시스템 관리자는 Admin Console을 통해 조직의 모든 제품 및 제품 프로필에 액세스할 수 있습니다.
   * [제품 관리자](#add-a-product-admin) - 제품 관리자는 [!DNL Adobe Admin Console]에서 [제품에 대한 사용자, 역할 및 권한을 관리](#add-users-and-admins)하고 [Commerce 관리자의 사용자를 관리](https://experienceleague.adobe.com/ko/docs/commerce-admin/systems/user-accounts/permissions-users-all#create-a-user){target="_blank"}할 수 있습니다.
   * [제품 프로필 관리자](#add-users-developers-and-product-profile-admins) - 제품 프로필 관리자는 Adobe Commerce 관리자에 액세스할 수 없지만 [!DNL Adobe Admin Console]에서 제품에 대한 사용자를 관리할 수 있습니다.

Adobe Commerce 내의 각 역할에 부여된 권한에 대한 자세한 내용은 [사용자 권한](#user-permissions)을 참조하세요.

## 제품 관리자 추가

1. https://adminconsole.adobe.com으로 이동한 다음 Adobe ID으로 로그인합니다.

1. 조직을 선택합니다.

1. [!UICONTROL **제품**] 탭의 [!UICONTROL **제품 및 서비스**]&#x200B;에서 [!UICONTROL **Adobe Commerce as a Cloud Service - 백엔드**] 제품을 선택합니다.

   ![제품 선택](./assets/backend.png){width="600" zoomable="yes"}

1. [!UICONTROL **관리자**] 탭을 선택합니다.

1. [!UICONTROL **관리자 추가**]&#x200B;를 클릭합니다.

1. 관리자로 추가할 사용자의 사용자 이름 또는 전자 메일 주소를 입력하고 [!UICONTROL **저장**]&#x200B;을 클릭합니다.

## 사용자, 개발자 및 제품 프로필 관리자 추가

다음 지침은 [!DNL Commerce Cloud Manager] 및 Commerce 관리자에 사용자 및 개발자를 추가하는 방법에 대한 정보를 제공합니다. [!DNL Commerce Cloud Manager] 인터페이스를 사용하면 Commerce 인스턴스를 만들고 관리할 수 있습니다.

>[!NOTE]
>
>제품 관리자와 시스템 관리자만 Adobe Commerce as a Cloud Service 제품에 사용자와 개발자를 추가할 수 있습니다.

1. https://adminconsole.adobe.com으로 이동한 다음 Adobe ID으로 로그인합니다.

1. 조직을 선택합니다.

1. [!UICONTROL **제품**] 탭의 [!UICONTROL **제품 및 서비스**]&#x200B;에서 [!UICONTROL **Adobe Commerce as a Cloud Service - 백엔드**] 제품을 선택합니다.

   ![제품 선택](./assets/backend.png){width="600" zoomable="yes"}

1. [!UICONTROL **기본 - Cloud Manager**] 제품 프로필을 클릭합니다.

1. [!UICONTROL **사용자**], [!UICONTROL **개발자**] 또는 [!UICONTROL **관리자**] 탭을 선택하고 [!UICONTROL **사용자 추가**] 또는 [!UICONTROL **개발자 추가**] 또는 [!UICONTROL **관리자 추가**]&#x200B;를 클릭합니다.

   >[!NOTE]
   >
   >이 화면에서 추가된 관리자는 [제품 프로필 관리자](#understanding-roles)이며 Commerce 관리자에 대한 액세스 권한이 없습니다.

   ![탭 선택](./assets/tab-select.png){width=600 zoomable="yes"}

1. 관리자로 추가할 사용자의 사용자 이름 또는 전자 메일 주소를 입력하고 [!UICONTROL **저장**]&#x200B;을 클릭합니다.

## 역할 리소스

다음 목록은 기본 역할이 Adobe Commerce 관리자 내에서 액세스할 수 있는 권한을 갖는 리소스를 설명합니다. 각 역할에 대한 기본 권한을 편집하려면 Commerce 관리자의 **시스템** > **권한** > **사용자 역할**(으)로 이동합니다.

**사용자**

* 카탈로그
   * 인벤토리
      * 제품
         * 제품 가격 읽기

**개발자**

* 카탈로그
   * 인벤토리
      * 제품
         * 제품 가격 읽기
* 시스템
   * 데이터 전송
      * 가져오기 기록
* Adobe IO 이벤트 구성
   * 구성 확인
   * 이벤트 공급자 만들기
   * 구성 업데이트
   * 이벤트 동기화
   * 이벤트 공급자 목록 가져오기
* 이벤트 프레임워크
   * 이벤트 목록
   * 이벤트 연결 테스트
   * 이벤트 구독
   * 이벤트 구독 취소
   * 이벤트 상태
   * 이벤트 구독을 가져오기 위한 API
   * 이벤트 구독 관리 UI 보기
   * 이벤트 구독 관리 UI 만들기
   * 새 이벤트 관리자 UI 요청
* 웹훅
   * Webhooks 디지털 서명
      * Webhooks 디지털 서명 설정
      * Webhooks 디지털 서명 생성 키
   * Webhooks 관리
      * Webhooks 그리드
      * 웹후크 편집
      * 웹후크 테스트
      * Webhook에 대한 API 구독
      * Webhook에서 API 구독 취소
      * Webhooks 목록
      * 새 Webhook 요청
      * 웹후크 로그
      * Webhooks 목록 가져오기

**관리자**

관리자는 모든 권한에 액세스할 수 있습니다.
