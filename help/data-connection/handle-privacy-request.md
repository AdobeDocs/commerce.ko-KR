---
title: ' [!DNL Commerce] Services에서 개인 정보 요청을 처리하는 방법'
description: ' [!DNL Commerce] 서비스에서 데이터 액세스 및 삭제 요청을 처리하는 방법에 대해 알아봅니다.'
role: Admin, Leader
feature: Security, Compliance
exl-id: 1408ca77-6956-4519-93a6-bc9be9bffeff
TQID: https://experienceleague.adobe.com/KhsveSMPR0tKmNzViEaWWHDu8fWve0GZjwsl2oyvx1k
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b5f00040-57a0-4a6d-a39e-383b1936c2c9id: ba9e5be9-7de1-4f71-a5d2-baead0e425eeid: c1256247-af4b-46d8-9dca-0c654ecfa157
subfeature_v2: id: bcbf87e7-9b75-4596-bffe-0f376b4c73a7
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: f8a45b24-4be7-4f1b-909b-60d06b483a20
topic_v2: id: d00e9f03-e50b-4162-b143-0c0817c937c2id: d095671a-1355-40aa-8b5f-06c33c68080bid: e0eb8757-182f-49f3-94a4-1587d16f5094id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 595
ht-degree: 1%

---

# 개인 정보 보호 요청

Adobe Experience Platform Privacy Service은 고객 데이터 요청을 관리하는 데 도움이 되는 RESTful API 및 사용자 인터페이스를 제공합니다. Privacy Service을 사용하면 Adobe Experience Cloud 애플리케이션에서 개인 고객 데이터에 액세스하고 삭제하는 요청을 제출할 수 있으므로 법적 및 조직의 개인 정보 보호 규정을 자동으로 준수할 수 있습니다.

Privacy Service에 대한 자세한 내용 및 개인 정보 보호 요청을 만들고 관리하는 방법은 Adobe Experience Platform 설명서를 참조하십시오.

* [Privacy Service 개요](https://experienceleague.adobe.com/en/docs/experience-platform/privacy/home)
* [Privacy Service UI에서 개인 정보 작업 관리](https://experienceleague.adobe.com/en/docs/experience-platform/privacy/ui/user-guide)

## 개별 데이터 개인 정보 보호 요청 관리

다음 두 가지 방법으로 [!DNL Commerce]에서 소비자 데이터에 액세스하고 삭제하도록 개별 요청을 제출할 수 있습니다.

* **Privacy Service UI**&#x200B;를 통해. 설명서를 [여기](https://experienceleague.adobe.com/en/docs/experience-platform/privacy/ui/user-guide#_blank)에서 확인하세요.
* **Privacy Service API**&#x200B;를 통해. 설명서 [여기](https://developer.adobe.com/experience-platform-apis/references/privacy-service/#_blank) 및 API 정보 [여기](https://developer.adobe.com/experience-platform-apis/#_blank)를 참조하세요.

Privacy Service에서는 **데이터 액세스** 및 **데이터 삭제** 요청의 두 가지 유형을 지원합니다.

>[!NOTE]
>
>이 문서는 [!DNL Commerce]에 대한 개인 정보 보호 요청을 하는 데 중점을 둡니다. [플랫폼 데이터 레이크](https://experienceleague.adobe.com/en/docs/experience-platform/catalog/privacy), [실시간 고객 프로필](https://experienceleague.adobe.com/en/docs/experience-platform/profile/privacy) 또는 [ID 서비스](https://experienceleague.adobe.com/en/docs/experience-platform/identity/privacy)에 대한 개인 정보 보호 요청을 하려는 경우 해당 사용 안내서를 참조하세요. Commerce에 대한 개인 정보 보호 요청은 이러한 모든 시스템에서 데이터를 제거하지 않으므로 삭제 및 액세스 요청은 각 시스템에 개별적으로 해야 합니다.

## 데이터 액세스

**액세스 요청**&#x200B;에 대해 UI에서 &quot;Commerce(Personalization)&quot;를 지정하거나 `commerceMarketingData`을(를) API의 제품 코드로 지정하십시오.

## 데이터 삭제

삭제 요청의 경우 Privacy Service은 마케팅 목적으로 Commerce SaaS 서비스에 저장된 [!DNL Commerce]개의 데이터를 삭제합니다. 즉, 데이터 주체의 프로필 및 주문이 더 이상 캠페인 및 고객 여정에 사용하기 위해 Adobe 마케팅 애플리케이션으로 전송되지 않습니다. 그러나 Privacy Service에서는 판매자 트랜잭션 요구 사항에 필요할 수 있으므로 [!DNL Commerce] 응용 프로그램의 데이터를 삭제하지 않습니다. 판매자는 [!DNL Commerce] 응용 프로그램에서 데이터 삭제/액세스 요청을 담당합니다. 자세한 내용은 [공유 권한 보안 및 운영 모델](https://experienceleague.adobe.com/en/docs/commerce-operations/security-and-compliance/shared-responsibility)을 참조하세요.

[!DNL Commerce]이(가) 특정 데이터의 삭제를 요청하는 데이터 주체에 대한 정보를 보내어 상인에게 삭제 요청에 대해 알립니다.

## 액세스 및 삭제 요청을 만드는 방법

### 사전 요구 사항

Adobe [!DNL Commerce]에 대한 데이터에 액세스하고 삭제를 요청하려면 다음을 수행해야 합니다.

* ims 조직 ID
* 작업을 수행할 사람의 ID 식별자와 해당 네임스페이스입니다. Adobe [!DNL Commerce] 및 Experience Platform의 ID 네임스페이스에 대한 자세한 내용은 [ID 네임스페이스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/identity/features/namespaces)를 참조하십시오.

### GDPR 요청/삭제 액세스 예:

**액세스 요청**&#x200B;의 경우 UI에서 &quot;Commerce(Personalization)&quot;(또는 &quot;commerceMarketingData&quot;를 API의 제품 코드로 지정)을 지정하십시오.

**삭제 요청**&#x200B;에 대해 &quot;Commerce(Personalization)&quot; 확인란이 활성화되어 있는지 확인하십시오. 또한 고객 프로필 및 주문 데이터를 [!DNL Commerce]에서 Adobe Experience Platform으로 이미 보낸 경우 삭제 요청을 다음 다운스트림 서비스에 제출해야 합니다.

* 프로필(제품 코드: &quot;profileService&quot;)
* AEP 데이터 레이크(제품 코드: &quot;AdobeCloudPlatform&quot;)
* ID(제품 코드: &quot;id&quot;)

Privacy API를 통해 액세스 및 삭제 요청을 전송하려면 Privacy Service에 대한 권한을 인증하고 관리해야 합니다.

* [Privacy Service API 인증 및 액세스](https://experienceleague.adobe.com/en/docs/experience-platform/privacy/api/getting-started)
* [Privacy Service에 대한 권한 관리](https://experienceleague.adobe.com/en/docs/experience-platform/privacy/permissions)

**필수 헤더**

```bash
curl --location --request POST 'https://platform.adobe.io/data/core/privacy/jobs' \
--header 'Content-Type: application/json' \
--header 'x-api-key: {{CLIENT_ID}}' \
--header 'x-gw-ims-org-id: {{IMS_ORGID}}' \
--header 'Authorization: Bearer {{ACCESS_TOKEN}}' \
```

**요청**

```json
{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{{IMS_ORGID}}"
      }
    ],
    "users": [
      {
        "key": "sampleUserKey1",
        "action": ["access"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "dsmith@sample.com",
            "type": "standard"
          }
        ]
      },
      {
        "key": "sampleUserKey2",
        "action": ["access","delete"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "ajones@sample.com",
            "type": "standard"
          }
        ]
      }
    ],
    "include": ["commerceMarketingData"],
    "expandIds": false,
    "priority": "normal",
    "regulation": "gdpr"
}
```

**응답**

```json
{
    "requestId": "17284033173196154RX-223",
    "totalRecords": 3,
    "jobs": [
        {
            "jobId": "a52ca032-858e-11ef-bbb4-27391388a0a6",
            "customer": {
                "user": {
                    "key": "sampleUserKey1",
                    "action": [
                        "access"
                    ],
                    "userIDs": [
                        {
                            "namespace": "email",
                            "value": "dsmith@sample.com",
                            "type": "standard",
                            "namespaceId": 6,
                            "isDeletedClientSide": false
                        }
                    ]
                }
            }
        },
        {
            "jobId": "a52ca034-858e-11ef-bbb4-d5d952d69769",
            "customer": {
                "user": {
                    "key": "sampleUserKey2",
                    "action": [
                        "delete"
                    ],
                    "userIDs": [
                        {
                            "namespace": "email",
                            "value": "ajones@sample.com",
                            "type": "standard",
                            "namespaceId": 6,
                            "isDeletedClientSide": false
                        }
                    ]
                }
            }
        },
        {
            "jobId": "a52ca033-858e-11ef-bbb4-8361a5022341",
            "customer": {
                "user": {
                    "key": "sampleUserKey2",
                    "action": [
                        "access"
                    ],
                    "userIDs": [
                        {
                            "namespace": "email",
                            "value": "ajones@sample.com",
                            "type": "standard",
                            "namespaceId": 6,
                            "isDeletedClientSide": false
                        }
                    ]
                }
            }
        }
    ]
}
```
