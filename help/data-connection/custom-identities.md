---
title: 프로필에 사용자 지정 속성 추가
description: 고객 프로필에 사용자 지정 특성을 추가하는 방법을 알아봅니다.
role: Admin, Developer
feature: Personalization, Integration
source-git-commit: 5489910382edc70eea5d7c0ca94da41c653b577d
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---


# 프로필에 사용자 지정 속성 추가

사용자 지정 프로필 속성을 사용하면 기본 `customerId` 및 `emailId` 이상의 추가 식별자를 사용하여 Experience Platform에서 고객 프로필 식별을 향상시킬 수 있습니다. 이러한 추가 식별자를 통해 보다 정밀한 고객 일치를 수행할 수 있으며 Commerce 플랫폼과 Experience Platform 간의 데이터 통합을 향상시킬 수 있습니다.

>[!NOTE]
>
>주문에 [사용자 지정 특성을 추가](custom-attributes.md)하는 방법에 대해 알아봅니다.

## 이점

- 더 나은 고객 일치를 위해 여러 식별자를 사용합니다.
- 비즈니스 요구 사항에 따라 사용자 정의 필드를 ID 속성에 매핑합니다.
- 중복 프로필을 줄이고 고객 데이터 정확도를 향상시킵니다.
- 더 많은 타겟팅된 고객 경험을 사용할 수 있습니다.

## 사전 요구 사항

사용자 지정 ID 속성을 구현하기 전에 다음을 확인하십시오.

- [데이터 연결 확장 설치](install.md)
- [Adobe Experience Platform에 연결](connect-data.md)
- [고객 프로필 데이터 보내기](connect-data.md#send-customer-profile-data)

## 1단계: Experience Platform 스키마 구성

1. Adobe Experience Platform에 로그인하고 Commerce 스키마를 선택합니다.
1. 루트 수준에서 [사용자 지정 ID 필드 추가](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/ui/resources/schemas?lang=en#custom-fields-for-standard-groups):
   - `hashedPID`(문자열) - 기본 ID 해시
   - `hashedSID`(문자열) - 보조 ID 해시
   - `primaryID`(문자열) - 기본 ID 필드 이름
   - `secondaryID`(문자열) - 보조 ID 필드 이름

![Experience Platform 스키마 구성](./assets/aep-schema-configuration.png)

>[!NOTE]
>
>요구 사항에 따라 정확한 필드 이름을 사용자 정의할 수 있습니다. 이 예제에서는 `hashedPID` 및 `hashedSID`을(를) ID 필드로 사용합니다.

## 2단계: 프로세서 클래스 만들기

사용자 정의 모듈에서 다음 PHP 프로세서 클래스를 만듭니다.

### AddressCustomHashedId 클래스

이 프로세서는 고객 주소의 `parent_id` 및 `entity_id`을(를) 해시합니다.

```php
<?php declare(strict_types=1);

namespace Magento\AepCustomerCustomAttributes\Event;
use Magento\AdobeCommerceEventsClient\Event\Event;
use Magento\AdobeCommerceEventsClient\Event\Processor\EventDataProcessorInterface;

class AddressCustomHashedId implements EventDataProcessorInterface
{
    public function process(Event $event, array $eventData): array
    {
        $pid = $eventData['parent_id'] ?? '';
        $sid = $eventData['entity_id'] ?? '';

        $eventData['profileAttributes']['hashedPID'] = hash('sha256', (string)$pid);
        $eventData['profileAttributes']['hashedSID'] = hash('sha256', (string)$sid);
        return $eventData;
    }
}
```

### AddressCustomId 클래스

이 프로세서는 주소 이벤트에 대한 기본 및 보조 ID 필드 이름을 설정합니다.

```php
<?php declare(strict_types=1);

namespace Magento\AepCustomerCustomAttributes\Event;
use Magento\AdobeCommerceEventsClient\Event\Event;
use Magento\AdobeCommerceEventsClient\Event\Processor\EventDataProcessorInterface;

class AddressCustomId implements EventDataProcessorInterface
{
    public function process(Event $event, array $eventData): array
    {
        $eventData['profileAttributes']['primaryID'] = 'hashedPID';
        $eventData['profileAttributes']['secondaryID'] = 'hashedSID';

        // Ensure both IDs are present, otherwise, Commerce will default primary to customerId and secondary to emailId
        if (empty($eventData['profileAttributes']['primaryID']) || empty($eventData['profileAttributes']['secondaryID'])) {
            $eventData['profileAttributes']['primaryID'] = $eventData['customerId'] ?? '';
            $eventData['profileAttributes']['secondaryID'] = $eventData['email'] ?? '';
        }

        return $eventData;
    }
}
```

### CustomHashedId 클래스

이 프로세서는 고객 프로필에 대해 `entity_id` 및 `email`을(를) 해시합니다.

```php
<?php declare(strict_types=1);

namespace Magento\AepCustomerCustomAttributes\Event;
use Magento\AdobeCommerceEventsClient\Event\Event;
use Magento\AdobeCommerceEventsClient\Event\Processor\EventDataProcessorInterface;

class CustomHashedId implements EventDataProcessorInterface
{
    public function process(Event $event, array $eventData): array
    {
        $pid = $eventData['entity_id'] ?? '';
        $sid = $eventData['email'] ?? '';

        $eventData['profileAttributes']['hashedPID'] = hash('sha256', (string)$pid);
        $eventData['profileAttributes']['hashedSID'] = hash('sha256', (string)$sid);
        return $eventData;
    }
}
```

### CustomId 클래스

이 프로세서는 프로필 이벤트에 대한 기본 및 보조 ID 필드 이름을 설정합니다.

```php
<?php declare(strict_types=1);

namespace Magento\AepCustomerCustomAttributes\Event;
use Magento\AdobeCommerceEventsClient\Event\Event;
use Magento\AdobeCommerceEventsClient\Event\Processor\EventDataProcessorInterface;

class CustomId implements EventDataProcessorInterface
{
    public function process(Event $event, array $eventData): array
    {
        $eventData['profileAttributes']['primaryID'] = 'hashedPID';
        $eventData['profileAttributes']['secondaryID'] = 'hashedSID';

        // Ensure both IDs are present, otherwise, Commerce will default primary to customerId and secondary to emailId
        if (empty($eventData['profileAttributes']['primaryID']) || empty($eventData['profileAttributes']['secondaryID'])) {
            $eventData['profileAttributes']['primaryID'] = $eventData['customerId'] ?? '';
            $eventData['profileAttributes']['secondaryID'] = $eventData['email'] ?? '';
        }

        return $eventData;
    }
}
```

>[!NOTE]
>이벤트 데이터에서 `primaryID`과(와) `secondaryID`이(가) 모두 전송되었는지 확인하십시오. 둘 중 하나가 누락된 경우 Commerce의 기본값은 다음과 같습니다.
>
>- primaryID = customerId
>- secondaryID = emailId

>[!BEGINSHADEBOX]

다음 두 단계를 완료하면

- Experience Platform의 Commerce 스키마는 프로필 이벤트 데이터에 대한 사용자 지정 ID를 올바르게 수집할 수 있습니다.
- Commerce PHP 코드의 프로세서 클래스는 프로필 이벤트에서 사용자 지정 식별 정보를 수집합니다.

이제 Commerce에서 보낸 모든 프로필 이벤트 데이터에는 사용자 지정 식별 정보가 포함됩니다.

>[!ENDSHADEBOX]

## 데이터 형식 예

다음 예제에서는 프로필 속성과 전체 고객 프로필 데이터 형식 모두에서 사용자 지정 ID 속성에 대해 예상되는 JSON 구조를 보여 줍니다.

### 프로필 속성 형식

```json
{
  "profileAttributes": {
    "hashedPID": "d80eae6e96d148b3b2abbbc6760077b66c4ea071f847dab573d507a32c4d99a5",
    "hashedSID": "fa7359e288ce3104bd4317a4fb75f08c4a5feec472de2e415b8260fb3567ebe6",
    "warehousecode": "1256",
    "method": "ina2354",
    "source": "commerce",
    "primaryID": "hashedPID",
    "secondaryID": "hashedSID"
  }
}
```

### 전체 고객 프로필 구조

```json
{
  "id": 137,
  "entity_id": "137",
  "created_at": "2025-02-10 20:10:30",
  "updated_at": "2022-02-10 20:10:31",
  "email": "customer@example.com",
  "firstname": "John",
  "lastname": "Doe",
  "dob": "2007-10-01 00:00:00",
  "profileAttributes": {
    "hashedPID": "d80eae6e96d148b3b2abbbc6760077b66c4ea071f847dab573d507a32c4d99a5",
    "hashedSID": "fa7359e288ce3104bd4317a4fb75f08c4a5feec472de2e415b8260fb3567ebe6",
    "primaryID": "137",
    "secondaryID": "customer@example.com"
  },
  "_metadata": {
    "commerceEdition": "Adobe Commerce",
    "commerceVersion": "2.4.6",
    "eventsClientVersion": "1.9.0",
    "storeId": "1",
    "websiteId": "1",
    "storeGroupId": "1",
    "websiteCode": "base",
    "storeCode": "default",
    "storeViewCode": "main_website_store"
  }
}
```

## 문제 해결

### 누락된 primaryID 또는 secondaryID

- **증상:** 데이터는 사용자 지정 값 대신 customerId/emailId로 기본 설정됩니다.
- **솔루션:** `primaryID`과(와) `secondaryID`이(가) 모두 `profileAttributes` 개체에 설정되어 있는지 확인하십시오.

### 잘못된 해시 값

- **증상:** 해시 값이 비어 있거나 형식이 잘못되었습니다.
- **해결 방법:** 해싱하기 전에 원본 필드(`parent_id`, `entity_id`, `email`)에 올바른 데이터가 포함되어 있는지 확인하십시오.

### 프로세서가 실행되지 않음

- **증상:** 사용자 지정 특성이 이벤트 데이터에 표시되지 않습니다.
- **해결 방법:** 프로세서가 `events.xml`에 올바르게 등록되어 있고 모듈이 활성화되어 있는지 확인하십시오.

### Experience Platform 스키마 불일치

- **증상:** 데이터가 Experience Platform 또는 스키마 유효성 검사 오류에 나타나지 않습니다.
- **해결 방법:** Experience Platform 스키마에 올바른 데이터 형식의 사용자 지정 ID 필드가 포함되어 있는지 확인하십시오.
