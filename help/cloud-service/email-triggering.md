---
title: REST를 통한 이메일 트리거
description: ' [!DNL Adobe Commerce as a Cloud Service]에 대한 템플릿 ID, 수신자 이메일 및 템플릿 변수를 지정하여 REST API를 사용하여 요청 시 트랜잭션 이메일을 트리거하는 방법에 대해 알아봅니다.'
role: Admin
level: Experienced
badgeSaas: label="SaaS만" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."
source-git-commit: 9661e368f7a0dc85edcd3e52a67ae2a98355d8b5
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 0%

---

# REST API를 통한 이메일 트리거

이전에는 고객 등록 또는 주문 구매 중과 같이, 이벤트가 트리거될 때만 이메일을 보낼 수 있었습니다. [!DNL Adobe Commerce as a Cloud Service]에서 템플릿 ID, 수신자 이메일 및 템플릿 변수를 지정하여 요청 시 REST API를 통해 이메일을 보낼 수 있습니다.

>[!NOTE]
>
>현재는 새로 생성된 사용자 정의 템플릿만 보낼 수 있습니다. 사전 정의된 시스템 템플릿은 지원되지 않습니다.

`V1/custom-email/send` 끝점을 사용하면 통합 및 외부 서비스와 같은 **타사 시스템**&#x200B;에서 다음을 지정하여 요청 시 이메일을 보낼 수 있습니다.

- **템플릿 ID** - 전자 메일 템플릿 ID입니다.
- **수신자 이메일** - 이 요청의 대상 이메일 주소입니다.
- **변수** - (선택 사항) `customer_name` 또는 `order_id`과(와) 같이 템플릿에 삽입할 사용자 지정 정의 키-값 쌍입니다.

>[!NOTE]
>
>전자 메일은 현재 저장소 범위와 기본 **보낸 사람** 전자 메일 주소 또는 템플릿에 대해 정의된 전자 메일 주소를 사용하여 동기적으로 전송됩니다.

## REST 계약

다음 섹션에서는 REST API를 사용하여 트랜잭션 이메일을 온디맨드로 전송하는 방법에 대해 설명합니다.

### 엔드포인트

- **URL** - `POST /rest/V1/custom-email/send`
- **권한 부여** - **서비스 간 IMS 권한 부여**&#x200B;만 지원됩니다. 호출자는 **API를 통해 사용자 지정 전자 메일 보내기**(`Magento_CustomEmailSend::send_custom_email`) 리소스에 액세스할 수 있어야 합니다. 자세한 내용은 [REST 인증](https://developer.adobe.com/commerce/webapi/rest/authentication/)을 참조하세요.
- **비동기 사용**(권장) - 이 끝점은 동기적으로 구현되지만, 요청이 오래 지속되는 HTTP 연결을 피하고 소비자에 의해 큐 대기 및 처리되도록 **비동기 REST API**&#x200B;를 사용하여 호출하는 것이 좋습니다. [!DNL Adobe Commerce as a Cloud Service]에서 `/async` 이후 `V1`에 경로를 사용할 수 있습니다(예: `POST https://<server>.api.commerce.adobe.com/<tenant-id>/V1/async/custom-email/send`).

  자세한 내용은 [SaaS(비동기 웹 끝점)](https://developer.adobe.com/commerce/webapi/rest/use-rest/asynchronous-web-endpoints/)을 참조하세요.

### 요청 본문

- **templateId**(정수, 필수) - [!UICONTROL **마케팅**] > [!UICONTROL _커뮤니케이션_] > [!UICONTROL **이메일 템플릿**]&#x200B;에서 관리자에 정의된 이메일 템플릿 ID입니다.

- **recipientEmail**(문자열, 필수) - 대상 전자 메일 주소입니다. 유효한 이메일 형식이어야 합니다. 값이 누락되었거나 비어 있으면 유효성 검사 오류가 트리거됩니다.
- **변수**(개체, 선택 사항) - 템플릿에 `UnstructuredArray`(으)로 삽입된 키-값 맵입니다.

  변수를 사용하지 않는 경우 빈 개체를 전달하거나 생략합니다. 전자 메일 템플릿 본문 및 제목에서 변수 구문을 사용하여 변수를 참조합니다(예: `var order_id`). 제목은 [지원되는 템플릿 시나리오](#supported-template-scenarios)에 설명된 것과 동일한 사용자 지정 변수 및 구문을 지원합니다.

### 성공 응답(HTTP 200)

API는 성공적으로 전송하면 HTTP 200을 반환합니다.

### 오류 응답

- **HTTP 400 - 유효성 검사 오류**

  통합은 각 요청에 대해 올바른 `templateId` 및 `recipientEmail`을(를) 제공해야 합니다.

   - `"message": "Invalid recipient email format"` - 받는 사람 주소가 잘못되었거나 잘못되었습니다.
   - `"message": "Recipient email is required."` - 누락되었거나 비어 있는 `recipientEmail`
   - `"message": "Template ID must be a positive integer."` - 누락됨, 0개 또는 잘못된 `templateId`

- **HTTP 404 - 템플릿을 찾을 수 없음**

  예: `"message": "Email template with ID \"999\" does not exist."`

## 지원되는 템플릿 시나리오

다음 템플릿 기능은 **이메일 본문** 및 **템플릿 제목**&#x200B;에서 모두 지원됩니다.

>[!NOTE]
>
>템플릿 제목도 사용자 지정 변수를 지원합니다. 다음 섹션에 설명된 대로 `var variableName` 및 기타 구문을 사용하십시오.

- **Include 지시문** - 전자 메일 헤더와 같은 다른 디자인 서식 파일을 포함합니다.

  ```javascript
  {{template config_path="design/email/header_template"}}
  ```

- **단순 변수** - `var variableName` 또는 `var order_id`과(와) 같은 `var g`을(를) 사용합니다.

  ```javascript
  {{var order.test}}
  {{var g}}
  {{var order_id}}
  ```

- **중첩/점 표기법** - 요청 `variables`에서 전달된 중첩 키의 경우 변환에서 달러 접두사가 있는 이름(예: `$order_data.customer_name`, `$order.increment_id` 또는 `$order_data.frontend_status_label`)을 사용합니다.

  ```javascript
  {{trans "%name," name=$order_data.customer_name}}
  {{trans "Your order #%increment_id has been updated with a status of **%order_status**." increment_id=$order.increment_id order_status=$order_data.frontend_status_label |raw}}
  ```

- **번역(거래)** - 여러 자리 표시자 및 HTML 태그가 있는 매개 변수가 있는 텍스트, 여러 줄 번역.

  ```javascript
  {{trans "%name," name=$order_data.customer_name}}
  {{trans "Your order #%increment_id has been updated with a status of **%order_status**." increment_id=$order.increment_id order_status=$order_data.frontend_status_label |raw}}
  ```

- **원시 출력** - 번역된 콘텐츠 또는 변수 콘텐츠에 HTML(예: `|raw` 또는 `<strong>`)가 포함된 경우 `<a>` 필터를 사용합니다.

  ```javascript
  {{trans "Your order #%increment_id has been updated with a status of **%order_status**." increment_id=$order.increment_id order_status=$order_data.frontend_status_label |raw}}
  ```

- **URL 도우미** - 번역 내 스토어 URL용.

  ```javascript
  {{trans 'You can check the status of your order by [logging into your account](%account_url).' account_url=$this.getUrl($store,'customer/account/',[_nosid:1]) |raw}}
  ```
