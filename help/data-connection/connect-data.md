---
title: Commerce 데이터를 Adobe Experience Platform에 연결
description: Commerce 데이터를 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
feature: Personalization, Integration, Configuration
exl-id: 8ba33277-38a5-45af-86e0-906cfb3b998d
source-git-commit: 5f7565f5bb80fcc65cbbcdc31c5c3b12fed4e5ee
workflow-type: tm+mt
source-wordcount: '2917'
ht-degree: 0%

---

# Commerce 데이터를 Adobe Experience Platform에 연결

[!DNL Data Connection] 확장을 설치하면 Commerce **관리자**&#x200B;의 **서비스** 아래의 _시스템_ 메뉴에 두 개의 새 구성 페이지가 나타납니다.

- Commerce 서비스 커넥터
- [!DNL Data Connection]

Adobe Commerce 인스턴스를 Adobe Experience Platform에 연결하려면 Commerce 서비스 커넥터로 시작한 다음 [!DNL Data Connection] 확장으로 끝나도록 두 커넥터를 모두 구성해야 합니다.

## Commerce 서비스 커넥터 구성

이전에 Adobe Commerce 서비스를 설치한 경우에는 Commerce 서비스 커넥터를 이미 구성했을 수 있습니다. 그렇지 않으면 [Commerce 서비스 커넥터](../landing/saas.md) 페이지에서 다음 작업을 완료해야 합니다.

1. [프로덕션 및 샌드박스 API 키를 검색](../landing/saas.md#credentials)하려면 Commerce 계정에 로그인하십시오.
1. [SaaS 데이터 공간](../landing/saas.md#saas-configuration)을 선택하세요.
1. [조직 ID를 검색](../landing/saas.md#ims-organization-optional)하려면 Adobe 계정에 로그인하십시오.

Commerce 서비스 커넥터를 구성한 후 [!DNL Data Connection] 확장을 구성합니다.

## [!DNL Data Connection] 확장 구성

이 섹션에서는 [!DNL Data Connection] 확장을 구성하는 방법을 배웁니다.

### 서비스 계정 및 자격 증명 세부 정보 추가

[주문 내역 데이터](#send-historical-order-data) 또는 [고객 프로필 데이터](#send-customer-profile-data)를 수집하여 전송하려는 경우 서비스 계정 및 자격 증명 세부 정보를 추가해야 합니다. 또한 [Audience Activation](https://experienceleague.adobe.com/docs/commerce-admin/customers/audience-activation.html?lang=ko) 확장을 구성하는 경우 다음 단계를 완료해야 합니다.

상점 또는 백오피스 데이터만 수집하여 보내는 경우 [일반](#general) 섹션으로 건너뛸 수 있습니다.

#### 1단계: Adobe Developer Console에서 프로젝트 만들기

Experience Platform API를 호출할 수 있도록 Commerce을 인증하는 프로젝트를 Adobe Developer Console에서 만듭니다.

프로젝트를 만들려면 [Experience Platform API 인증 및 액세스](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=ko) 자습서에 설명된 단계를 따르십시오.

튜토리얼을 진행할 때 프로젝트에 다음과 같은 사항이 있는지 확인합니다.

- 다음 [제품 프로필](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=ko#select-product-profiles)에 액세스: **기본 프로덕션 모든 액세스** 및 **AEP 기본 모든 액세스**.
- 올바른 [역할 및 권한이 구성되었습니다](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=ko#assign-api-to-a-role).
- JSON 웹 토큰(JWT)을 서버 간 인증 방법으로 사용하려는 경우 개인 키도 업로드해야 합니다.

이 단계의 결과 다음 단계에서 사용하는 구성 파일이 만들어집니다.

#### 2단계: 구성 파일 다운로드

[작업 영역 구성 파일](https://developer.adobe.com/commerce/extensibility/events/project-setup/#download-the-workspace-configuration-file)을 다운로드합니다. `<workspace-name>.json` 파일에는 Commerce 관리자의 **서비스 계정/자격 증명 세부 정보** 페이지에 입력해야 하는 모든 값이 포함되어 있습니다.

![[!DNL Data Connection] 관리자 구성](./assets/epc-admin-config.png){width="700" zoomable="yes"}

1. Commerce 관리에서 **스토어** > 설정 > **구성** > **서비스** > **[!DNL Data Connection]**(으)로 이동합니다.

1. **Adobe Developer 인증 유형** 메뉴에서 구현한 서버 간 인증 방법을 선택합니다. Adobe에서는 OAuth를 사용하는 것이 좋습니다. JWT는 더 이상 사용되지 않습니다. [자세히 알아보기](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/)

1. (JWT만 해당) `private.key` 파일의 내용을 복사하여 **클라이언트 암호** 필드에 붙여넣습니다. 다음 명령을 사용하여 내용을 복사합니다.

   ```bash
   cat config/private.key | pbcopy
   ```

   [ 파일에 대한 자세한 내용은 ](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/)서비스 계정(JWT) 인증`private.key`을 참조하십시오.

1. `<workspace-name>.json` 파일의 내용을 **서비스 계정/자격 증명 세부 정보** 필드(예: `"client_id"`, `"client_secrets"`, `"technical_account_email"`, `"technical_account_id"` 등)에 복사합니다.

1. **구성 저장**&#x200B;을 클릭합니다.

1. 입력한 서비스 계정 및 자격 증명 정보가 올바른지 확인하려면 **[!UICONTROL Test connection]** 단추를 클릭하십시오.

### 일반

1. 관리에서 **시스템** > 서비스 > **[!DNL Data Connection]**(으)로 이동합니다.

   ![[!DNL Data Connection] 설정](./assets/epc-settings.png){width="700" zoomable="yes"}

1. **일반**&#x200B;의 **설정** 탭에서 [Commerce 서비스 커넥터](../landing/saas.md#organizationid)에 구성된 대로 Adobe Experience Platform 계정과 연결된 ID를 확인하십시오. 조직 ID는 글로벌입니다. Adobe Commerce 인스턴스당 하나의 조직 ID만 연결할 수 있습니다.

1. **범위** 드롭다운에서 컨텍스트를 **웹 사이트**(으)로 설정합니다.

1. (선택 사항) 이미 사이트에 [AEP Web SDK(alloy)](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=ko)을 배포한 경우 확인란을 활성화하고 AEP Web SDK의 이름을 추가합니다. 그렇지 않으면 이러한 필드를 비워 두고 [!DNL Data Connection] 확장에서 자동으로 배포합니다.

   >[!NOTE]
   >
   >고유한 AEP Web SDK을 지정하는 경우 [!DNL Data Connection] 확장은 이 페이지에 지정된 데이터 스트림 ID가 아닌 해당 SDK과 연결된 데이터 스트림 ID를 사용합니다(있는 경우).

### 데이터 수집

이 섹션에서는 수집하고 Experience Platform 에지로 전송할 데이터 유형을 지정합니다. 데이터에는 세 가지 유형이 있습니다.

- **동작**(클라이언트측 데이터)은 상점 첫 화면에서 캡처된 데이터입니다. 여기에는 `View Page`, `View Product`, `Add to Cart` 및 [구매요청 목록](events.md#b2b-events) 정보(B2B 판매자의 경우)와 같은 구매자 상호 작용이 포함됩니다.

- **백 오피스**(서버측 데이터)는 Commerce 서버에 캡처된 데이터입니다. 여기에는 주문이 주문, 취소, 환불, 배송 또는 완료 여부와 같은 주문 상태에 대한 정보가 포함됩니다. [이전 순서 데이터](#send-historical-order-data)도 포함됩니다.

- **프로필**&#x200B;은(는) 구매자의 프로필 정보와 관련된 데이터입니다. [자세히](#send-customer-profile-data)를 알아보세요.

Adobe Commerce 인스턴스가 데이터 수집을 시작할 수 있는지 확인하려면 [필수 구성 요소](overview.md#prerequisites)를 검토하십시오.

[상점](events.md#storefront-events), [사무실](events-backoffice.md) 및 [프로필](events-backoffice.md#customer-profile-events-server-side) 이벤트에 대한 자세한 내용은 이벤트 항목을 참조하세요.

>[!NOTE]
>
>**데이터 수집** 섹션의 모든 필드가 **웹 사이트** 범위 이상에 적용됩니다.

1. Storefront 동작 데이터를 전송하려면 **Storefront 이벤트**&#x200B;를 선택하십시오.

1. 주문이 주문, 취소, 환불 또는 배송된 경우와 같은 주문 상태 정보를 보내려면 **사무실 뒷면 이벤트**&#x200B;를 선택하십시오.

   >[!NOTE]
   >
   >**이전 사무실 이벤트**&#x200B;를 선택하면 모든 이전 사무실 데이터가 Experience Platform Edge로 전송됩니다. 쇼핑객이 데이터 수집을 옵트아웃하는 경우 Experience Platform에서 쇼핑객의 개인 정보 보호 기본 설정을 명시적으로 설정해야 합니다. 이는 컬렉터가 이미 구매자 환경 설정에 따라 동의를 처리하는 상점 이벤트와는 다릅니다. Experience Platform에서 쇼핑객 개인 정보 기본 설정을 설정하는 방법에 대해 [자세히](https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/consent/adobe/dataset.html?lang=ko)알아보세요.

1. (자체 AEP Web SDK을 사용하는 경우 이 단계를 건너뜁니다.) Adobe Experience Platform에서 데이터 스트림을 [만들기](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=ko#create)하거나 컬렉션에 사용할 기존 데이터 스트림을 선택하십시오. **데이터 스트림 ID** 필드에 해당 데이터 스트림 ID를 입력합니다.

1. Commerce 데이터를 포함할 **데이터 세트 ID**&#x200B;를 입력하십시오. 데이터 세트 ID 찾기:

   1. Experience Platform UI를 열고 왼쪽 탐색에서 **데이터 세트**&#x200B;를 선택하여 **데이터 세트** 대시보드를 엽니다. 대시보드에는 조직에서 사용 가능한 모든 데이터 세트가 나열됩니다. 이름, 데이터 세트가 준수하는 스키마, 가장 최근 수집 실행 상태 등 나열된 각 데이터 세트에 대한 세부 사항이 표시됩니다.
   1. 데이터 스트림과 연결된 데이터 세트를 엽니다.
   1. 오른쪽 창에서 데이터 세트에 대한 세부 정보를 봅니다. 데이터 세트 ID를 복사합니다.

1. [cron](https://experienceleague.adobe.com/docs/commerce-admin/systems/tools/cron.html?lang=ko) 작업에 따라 일정에 따라 백 오피스 이벤트 데이터를 업데이트하려면 `Sales Orders Feed` 인덱스를 `Update by Schedule`(으)로 변경해야 합니다.

   1. _관리자_ 사이드바에서 **[!UICONTROL System]** > _[!UICONTROL Tools]_>**[!UICONTROL Index Management]**(으)로 이동합니다.

   1. `Sales Orders Feed` 인덱서에 대한 확인란을 선택하십시오.

   1. **[!UICONTROL Actions]**&#x200B;을(를) `Update by Schedule`(으)로 설정합니다.

   1. 백 오피스 데이터를 처음 활성화하는 경우 다음 명령을 실행하여 다시 인덱싱하고 재동기화를 트리거합니다. [cron](https://experienceleague.adobe.com/docs/commerce-admin/systems/tools/cron.html?lang=ko) 작업이 올바르게 설정된 경우 이후의 재동기화가 자동으로 수행됩니다.

      ```bash
      bin/magento index:reindex sales_order_data_exporter_v2
      ```

      ```bash
      bin/magento saas:resync --feed orders
      ```

#### 필드 설명

| 필드 | 설명 |
|--- |--- |
| 범위 | 구성 설정을 적용할 특정 웹 사이트입니다. |
| 조직 ID (전역) | Adobe DX 제품을 구입한 조직의 ID입니다. 이 ID는 Adobe Commerce 인스턴스를 Adobe Experience Platform에 연결합니다. |
| AEP 웹 SDK이 이미 사이트에 배포되었습니까 | 자신의 AEP Web SDK을 사이트에 배포한 경우 이 확인란을 선택합니다 |
| AEP 웹 SDK 이름(전역) | 사이트에 Experience Platform Web SDK이 이미 배포되어 있는 경우 이 필드에 해당 SDK의 이름을 지정합니다. 이렇게 하면 Storefront 이벤트 수집기 및 Storefront 이벤트 SDK이 [!DNL Data Connection] 확장에 의해 배포된 버전이 아니라 Experience Platform Web SDK을 사용할 수 있습니다. 사이트에 Experience Platform Web SDK이 배포되지 않은 경우 이 필드를 비워 두면 [!DNL Data Connection] 확장에서 자동으로 배포됩니다. |
| Storefront 이벤트 | 조직 ID 및 데이터 스트림 ID가 유효한 경우 기본적으로 선택되어 있습니다. Storefront 이벤트는 사이트를 탐색할 때 쇼핑객으로부터 익명으로 처리된 행동 데이터를 수집합니다. |
| 백오피스 이벤트 | 선택하면 이벤트 페이로드에 주문이 주문, 취소, 환불 또는 배송된 경우와 같이 익명으로 처리된 주문 상태 정보가 포함됩니다. |
| 데이터 스트림 ID(웹 사이트) | Adobe Experience Platform에서 다른 Adobe DX 제품으로 데이터가 흐를 수 있는 ID입니다. 이 ID는 특정 Adobe Commerce 인스턴스 내의 특정 웹 사이트에 연결되어야 합니다. 고유한 Experience Platform Web SDK을 지정하는 경우 이 필드에 데이터 스트림 ID를 지정하지 마십시오. [!DNL Data Connection] 확장은 해당 SDK과 연결된 데이터 스트림 ID를 사용하며 이 필드에 지정된 데이터 스트림 ID는 무시합니다(있는 경우). |
| 데이터 세트 ID(웹 사이트) | Commerce 데이터가 포함된 데이터 세트의 ID. **Storefront 이벤트** 또는 **Back Office 이벤트** 확인란을 선택 취소하지 않은 경우 이 필드가 필요합니다. 또한 자체 Experience Platform Web SDK을 사용 중이므로 데이터 스트림 ID를 지정하지 않은 경우에도 데이터 스트림과 연결된 데이터 세트 ID를 추가해야 합니다. 그렇지 않으면 이 양식을 저장할 수 없습니다. |

온보딩 후 상점 데이터가 Experience Platform 에지로 흐르기 시작합니다. 백오피스 데이터가 가장자리에 표시되는 데 약 5분이 소요됩니다. cron 일정에 따라 에지에서 후속 업데이트가 표시됩니다.

### 고객 프로필 데이터 보내기

Experience Platform에 보낼 수 있는 프로필 데이터에는 프로필 레코드와 시계열 프로필 이벤트의 두 가지 유형이 있습니다.

프로필 레코드에는 쇼핑객이 Commerce 인스턴스에서 쇼핑객 이름과 같은 프로필을 만들 때 저장되는 데이터가 포함됩니다. 스키마와 데이터 세트가 [올바르게 구성](profile-data.md)되면 프로필 레코드가 Experience Platform으로 전송되고 Adobe의 프로필 관리 및 세분화 서비스 [Real-Time CDP](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=ko)로 전달됩니다.

시계열 프로필 이벤트에는 사이트에서 계정을 생성, 편집 또는 삭제하는 경우와 같이 쇼퍼의 프로필 정보에 대한 데이터가 포함됩니다. 프로필 이벤트 데이터가 Experience Platform으로 전송되면 다른 DX 제품에서 사용할 수 있는 데이터 세트에 상주합니다.

1. 서비스 계정 및 자격 증명 세부 정보를 [제공](#add-service-account-and-credential-details)했는지 확인하세요.

1. [프로필 레코드 데이터 수집](profile-data.md) 및 [시계열 프로필 이벤트 데이터 수집](update-xdm.md#time-series-profile-event-data)에 대해 지정된 스키마와 데이터 세트가 있는지 확인하십시오.

1. 프로필 데이터를 Experience Platform으로 보내려면 **고객 프로필** 확인란에 확인 표시를 합니다.

1. **프로필 데이터 세트 ID**&#x200B;를 입력하십시오.

   프로필 레코드 데이터는 행동 및 백 오피스 이벤트 데이터에 현재 사용하고 있는 것과 다른 데이터 세트를 사용해야 합니다.

1. 동작 및 백 오피스 데이터에 사용 중인 동일한 데이터 스트림 ID를 통해 프로필 이벤트를 스트리밍하지 않으려면 **동일한 데이터 스트림 ID를 통해 고객 프로필 스트리밍**&#x200B;에서 확인 표시를 제거하고 대신 사용할 데이터 스트림 ID를 입력하십시오.

Real-Time CDP에서 프로필 레코드를 사용할 수 있도록 하는 데 약 10분 정도 걸릴 수 있습니다. 프로필 이벤트가 즉시 스트리밍을 시작합니다.

>[!TIP]
>
>Experience Platform에 프로필 데이터가 표시되지 않으면 [Commerce 기술 자료](https://experienceleague.adobe.com/ko/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/data-connection-customer-profiles-not-exported)에서 문제 해결 제안을 확인하십시오.

#### 필드 설명

| 필드 | 설명 |
|--- |--- |
| 고객 프로필 | 고객 프로필 기록을 수집하고 전송하려면 이 확인란을 선택합니다. |
| 프로필 데이터 세트 ID | 프로필 레코드는 행동 및 백 오피스 이벤트에 사용되는 데이터 세트와 다른 데이터 세트를 사용해야 합니다. |
| 동일한 데이터 스트림 ID를 통해 고객 프로필 스트리밍 | 행동 및 백 오피스 이벤트에 현재 사용되는 것과 동일한 데이터 스트림을 사용할지 여부를 결정합니다. |
| 고객 프로필용 데이터스트림 | 고객 프로필 레코드별 데이터 스트림을 지정합니다. |

### 이전 주문 데이터 보내기

Adobe Commerce은 최대 5년간의 [내역 주문 데이터 및 상태](events-backoffice.md#back-office-events)를 수집합니다. [!DNL Data Connection] 확장을 사용하여 해당 내역 데이터를 Experience Platform으로 보내어 고객 프로필을 보강하고 이전 주문을 기반으로 고객 경험을 개인화할 수 있습니다. 데이터는 Experience Platform 내의 데이터 세트에 저장됩니다.

Commerce이 이미 이전 주문 데이터를 수집하는 동안 해당 데이터를 Experience Platform으로 보내려면 몇 가지 단계를 완료해야 합니다.

이 비디오를 통해 이전 주문에 대해 자세히 알아본 후 다음 단계를 완료하여 이전 주문 수집을 구현합니다.

>[!VIDEO](https://video.tv.adobe.com/v/3424672)

#### 주문 동기화 서비스 설정

주문 동기화 서비스는 [메시지 큐 프레임워크](https://developer.adobe.com/commerce/php/development/components/message-queues/) 및 RabbitMQ를 사용합니다. 이 단계를 완료하면 주문 상태 데이터를 SaaS에 동기화할 수 있습니다. Experience Platform으로 전송되기 전에 이 데이터가 필요합니다.

1. 서비스 계정 및 자격 증명 세부 정보를 [제공](#add-service-account-and-credential-details)했는지 확인하세요.

1. [RabbitMQ를 사용](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/service/rabbitmq.html?lang=ko)합니다.

   >[!NOTE]
   >
   >RabbitMQ는 Commerce 버전 2.4.7 이상에 대해 이미 설정되었지만 소비자를 활성화해야 합니다.

1. `.magento.env.yaml` 환경 변수를 사용하여 `CRON_CONSUMERS_RUNNER`에서 cron 작업별로 메시지 큐 소비자를 사용하도록 설정하십시오.

   ```yaml
      stage:
        deploy:
          CRON_CONSUMERS_RUNNER:
            cron_run: true
   ```

   >[!NOTE]
   >
   >사용 가능한 모든 구성 옵션에 대해 알아보려면 [변수 배포 설명서](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-deploy.html?lang=ko#cron_consumers_runner)를 참조하세요.

주문 동기화 서비스를 사용하면 **[!UICONTROL [!DNL Data Connection]]** 페이지에서 이전 주문 날짜 범위를 지정할 수 있습니다.

#### 주문 내역 날짜 범위 지정

Experience Platform으로 전송할 과거 주문의 날짜 범위를 지정합니다.

1. 관리에서 **시스템** > 서비스 > **[!DNL Data Connection]**(으)로 이동합니다.

1. **주문 내역** 탭을 선택합니다.

   ![[!DNL Data Connection] 주문 내역](./assets/epc-order-history.png){width="700" zoomable="yes"}

1. **주문 기록 동기화**&#x200B;에서 **설정에서 데이터 세트 ID 복사** 확인란이 이미 활성화되어 있습니다. 이렇게 하면 **설정** 탭에 지정된 동일한 데이터 세트를 사용할 수 있습니다.

1. **시작** 및 **종료** 필드에서 전송할 이전 주문 데이터의 날짜 범위를 지정합니다. 5년을 초과하는 날짜 범위는 선택할 수 없습니다.

1. 동기화를 시작하려면 **[!UICONTROL Start Sync]**&#x200B;을(를) 선택하십시오. 이전 주문 데이터는 스트리밍 데이터인 상점 및 백오피스 데이터가 아닌 일괄 처리된 데이터입니다. 일괄 처리된 데이터가 Experience Platform에 도착하는 데 약 45분이 소요됩니다.

##### 필드 설명

| 필드 | 설명 |
|--- |--- |
| 설정에서 데이터 세트 ID 복사 | **설정** 탭에 입력한 데이터 세트 ID를 복사합니다. |
| 데이터 세트 ID(웹 사이트) | Commerce 데이터가 포함된 데이터 세트의 ID. **Storefront 이벤트** 또는 **Back Office 이벤트** 확인란을 선택 취소하지 않은 경우 이 필드가 필요합니다. 또한 자체 Experience Platform Web SDK을 사용 중이므로 데이터 스트림 ID를 지정하지 않은 경우에도 데이터 스트림과 연결된 데이터 세트 ID를 추가해야 합니다. 그렇지 않으면 이 양식을 저장할 수 없습니다. |
| 출처: | 주문 내역 데이터 수집을 시작할 시작 날짜. |
| 종료 | 주문 내역 데이터 수집을 종료할 날짜. |
| 동기화 시작 | 주문 내역 데이터를 Experience Platform Edge와 동기화하는 프로세스를 시작합니다. **[!UICONTROL Dataset ID]** 필드가 비어 있거나 데이터 세트 ID가 잘못된 경우 이 단추가 비활성화됩니다. |

### 데이터 사용자 지정

**데이터 사용자 지정** 탭에서 [!DNL Commerce]에 구성되어 Experience Platform으로 전송된 사용자 지정 특성을 볼 수 있습니다.

![[!DNL Data Connection] 데이터 사용자 지정](./assets/epc-data-customization.png){width="700" zoomable="yes"}

>[!IMPORTANT]
>
>[데이터 수집](#data-collection) 탭에서 **지정한** 데이터 스트림 ID가 사용자 지정 특성을 수집하기 위해 스키마에 연결된 ID와 일치하는지 확인하십시오.

주문에 대한 사용자 지정 특성을 만들어 Experience Platform으로 보낼 때 Commerce의 특성 이름은 Experience Platform의 [!DNL Commerce] 스키마에 있는 특성 이름과 일치해야 합니다. 일치하지 않을 경우 차이점을 확인하기 어려울 수 있습니다. 이름이 일치하지 않으면 **사용자 지정 순서 특성** 표를 통해 문제를 해결할 수 있습니다.

**사용자 지정 순서 특성** 테이블은 [!DNL Commerce] 백 오피스와 Experience Platform의 [!DNL Commerce] 스키마 간의 사용자 지정 순서 특성의 구성 및 매핑을 볼 수 있습니다. 이 테이블을 사용하면 여러 소스의 주문 레벨 및 주문 품목 레벨 사용자 정의 속성을 볼 수 있으므로 누락되거나 잘못 정렬된 속성을 더 쉽게 식별할 수 있습니다. 또한 각 데이터 세트에는 고유한 사용자 지정 속성이 있을 수 있으므로 라이브 데이터 세트와 내역 데이터 세트를 구분하는 데 도움이 되는 데이터 세트 ID가 표시됩니다.

테이블에서 사용자 지정 속성 이름 옆에 녹색 확인 표시가 표시되지 않으면 소스의 속성 이름이 일치하지 않음을 나타냅니다. 한 소스에서 속성 이름을 수정하고 녹색 확인 표시가 나타나 이름이 일치함을 나타냅니다.

- Experience Platform의 스키마에서 특성 이름이 업데이트된 경우 Experience Platform 스키마 변경을 트리거하려면 **데이터 사용자 지정** 탭에 구성을 저장해야 합니다. 이 변경 사항은 **단추를 클릭할 때**&#x200B;사용자 지정 순서 특성&#x200B;**[!UICONTROL Refresh]** 표에 반영됩니다.
- 특성 이름이 [!DNL Commerce]에서 업데이트된 경우 **사용자 지정 순서 특성** 테이블에서 이름을 업데이트하려면 순서 이벤트를 생성해야 합니다. 변경사항은 약 60분 후에 반영될 예정입니다.

[사용자 지정 특성을 설정](custom-attributes.md)하는 방법에 대해 자세히 알아보세요.

#### 필드 설명

| 필드 | 설명 |
|--- |--- |
| 데이터 세트 | 사용자 지정 특성을 포함하는 데이터 세트를 표시합니다. 라이브 및 내역 데이터 세트에는 고유한 사용자 지정 속성이 있을 수 있습니다. |
| Adobe Commerce | [!DNL Commerce] 백 오피스에서 만든 사용자 지정 특성을 표시합니다. |
| Experience Platform | Experience Platform의 [!DNL Commerce] 스키마에 지정된 사용자 지정 특성을 표시합니다. |
| 새로 고침 | Experience Platform의 [!DNL Commerce] 스키마에서 사용자 지정 특성 이름을 검색합니다. |

## 이벤트 데이터 수집 확인

Commerce 스토어에서 데이터가 수집되고 있는지 확인하려면 [Adobe Experience Platform 디버거](https://experienceleague.adobe.com/docs/experience-platform/debugger/home.html?lang=ko)를 사용하여 Commerce 사이트를 검사하십시오. 데이터가 수집되고 있는지 확인한 후 만든 [데이터 집합](overview.md#prerequisites)에서 데이터를 반환하는 쿼리를 실행하여 상점 및 백 오피스 이벤트 데이터가 가장자리에 표시되는지 확인할 수 있습니다.

1. Experience Platform의 왼쪽 탐색에서 **쿼리**&#x200B;를 선택하고 [!UICONTROL Create Query]을(를) 클릭합니다.

   ![쿼리 편집기](assets/query-editor.png)

1. 쿼리 편집기가 열리면 데이터 세트에서 데이터를 선택하는 쿼리를 입력합니다.

   ![쿼리 만들기](assets/create-query.png)

   예를 들어 쿼리는 다음과 같을 수 있습니다.

   ```sql
   SELECT * from `your_dataset_name` ORDER by TIMESTAMP DESC
   ```

1. 쿼리가 실행되면 **콘솔** 탭 옆의 **결과** 탭에 결과가 표시됩니다. 이 보기는 쿼리의 테이블 형식 출력을 보여 줍니다.

   ![쿼리 편집기](assets/query-results.png)

이 예제에서는 [`commerce.productListAdds`](events.md#addtocart), [`commerce.productViews`](events.md#productpageview), [`web.webpagedetails.pageViews`](events.md#pageview) 등의 이벤트 데이터가 표시됩니다. 이 보기를 통해 Commerce 데이터가 에지에 도달했는지 확인할 수 있습니다.

결과가 예상과 다른 경우 데이터 세트를 열고 실패한 일괄 처리 가져오기를 찾습니다. [일괄 가져오기 문제 해결](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/troubleshooting.html?lang=ko)에 대해 자세히 알아보세요.

### 프로필 데이터가 Experience Platform에 표시되는지 확인

Experience Platform에 프로필 데이터가 표시되지 않으면 [Commerce 기술 자료](https://experienceleague.adobe.com/ko/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/data-connection-customer-profiles-not-exported)에서 문제 해결 제안을 확인하십시오.

## 다음 단계

Commerce 데이터가 Experience Platform Edge로 전송되면 Adobe Journey Optimizer과 같은 다른 Adobe Experience Cloud 제품에서 해당 데이터를 사용할 수 있습니다. 예를 들어 특정 이벤트를 수신하고 해당 이벤트 데이터를 기반으로 첫 번째 사용자에 대해 이메일을 트리거하거나 포기한 장바구니가 있는 경우 Journey Optimizer을 구성할 수 있습니다. Journey Optimizer에서 [고객 여정을 생성](using-ajo.md)하여 Commerce 플랫폼을 확장하는 방법을 알아봅니다.
