---
title: ' [!DNL Commerce] 서비스에 대한 HIPAA 준비'
description: ' [!DNL Data Connection] 확장을 사용하여 Experience Platform과 데이터를 공유 [!DNL Commerce] 하고 HIPAA 규정을 준수하는 방법을 알아봅니다.'
role: Admin, Leader
feature: Security, Compliance
exl-id: 8851e6d2-c466-4d8e-bfa4-20d0ad6522b5
source-git-commit: 290e3310bd7940c4ccd11317d273b75cc974223b
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# [!DNL Commerce] 서비스에 대한 HIPAA 준비

[!DNL Data Connection] 확장을 사용하면 [!DNL Commerce] 백 오피스 이벤트 데이터를 Experience Platform과 공유하고 HIPAA 준수를 유지할 수 있습니다.

>[!IMPORTANT]
>
>Storefront 이벤트는 클라이언트측에서 생성되므로 판매자는 [Storefront 이벤트 데이터를 Experience Platform으로 보내지 마십시오](connect-data.md#data-collection).

이 문서에서는 다음을 학습합니다.

- 설치 방법
- Experience Platform에 전송된 데이터가 HIPAA에 준비되는지 확인하는 방법
- [!DNL Commerce]의 데이터 암호화

## 설치

Adobe [!DNL Commerce]용 의료 서비스 추가 기능을 구입한 경우 [HIPAA 지원 확장](https://experienceleague.adobe.com/ko/docs/commerce-admin/start/compliance/hipaa-ready-service/overview#installation)을 이미 설치했을 수 있습니다. [!DNL Commerce] 백오피스 이벤트 데이터가 HIPAA를 사용할 수 있도록 하려면 추가 [!DNL Data Connection]데이터 서비스 HIPAA **확장을 사용하여** 확장 프로그램을 설치해야 합니다. **데이터 서비스 HIPAA** 확장을 사용하면 Experience Platform으로 보내는 모든 백 오피스 데이터를 HIPAA에서 사용할 수 있습니다. [확장 설치 방법](install.md#install-the-data-services-hipaa-extension)을 알아보세요.

>[!IMPORTANT]
>
>**데이터 서비스 HIPAA** 확장을 설치하면 라이브 검색 및 제품 추천에서 사용하는 상점 이벤트 데이터가 더 이상 캡처되지 않습니다. 이는 storefront 이벤트 데이터가 클라이언트측에서 생성되기 때문입니다. 상점 이벤트 데이터를 계속 캡처하고 보내려면 이러한 서비스에 대한 이벤트 수집을 다시 활성화하십시오. 자세한 내용은 [일반 구성](https://experienceleague.adobe.com/ko/docs/commerce-admin/config/general/general#data-services)을 참조하세요.

## Experience Platform에 전송된 데이터가 HIPAA에 준비되는지 확인하는 방법

[!DNL Data Connection] 확장에서 Experience Platform으로 보내는 모든 백 오피스 이벤트 데이터는 [!DNL Commerce] 내에서 중요한 것으로 간주됩니다. 그러나 특정 데이터를 중요한 것으로 명시적으로 식별하기 위해 Experience Platform의 [!DNL Commerce] 스키마에 데이터 사용 레이블을 적용하는 것은 판매자의 책임입니다. 데이터 사용 레이블을 스키마에 직접 적용하면 해당 레이블이 해당 스키마를 기반으로 하는 기존 및 향후 모든 데이터 세트에 전파됩니다.

데이터 거버넌스 프레임워크 내에서 데이터 사용 레이블 및 해당 역할에 대한 개요는 Experience Platform 설명서의 [데이터 사용 레이블 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/data-governance/labels/overview)를 참조하십시오.

### [!DNL Commerce] 필드에 데이터 사용 레이블 적용

[스키마에 대한 데이터 사용 레이블 관리](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/tutorials/labels) 자습서의 단계에 따라 [!DNL Commerce] 스키마에 레이블을 적용하는 방법을 알아보십시오.

[&#x200B; 스키마의 필드에 적용할 수 있는 사용 가능한 레이블에 대한 자세한 내용은 &#x200B;](https://experienceleague.adobe.com/ko/docs/experience-platform/data-governance/labels/reference#sensitive)중요 레이블의 용어집[!DNL Commerce]을 참조하세요. 예를 들어 레이블 `RHD`은(는) Adobe에서 계약상 업로드할 수 있는 PHI(보호 상태 정보) 또는 환자에 대한 정보를 식별합니다.

[!DNL Commerce] 데이터가 중요 데이터로 레이블이 지정되면 정책 위반을 구성하는 데이터 작업을 방지하기 위해 정책을 적용할 수 있습니다. Experience Platform의 [정책 적용](https://experienceleague.adobe.com/ko/docs/experience-platform/data-governance/enforcement/overview)에 대해 자세히 알아보세요.

## Commerce의 데이터 암호화

Adobe [!DNL Commerce]은(는) 블록 수준 암호화를 사용합니다. 저장의 경우 [!DNL Commerce]에서 Amazon Elastic Block Store(EBS)를 사용합니다. 모든 EBS 볼륨은 AES-256 알고리즘을 사용하여 암호화됩니다. 즉, 데이터가 저장 시 암호화됩니다. 전송 중인 [!DNL Commerce] 데이터는 HTTPS [TLS v1.2](https://datatracker.ietf.org/doc/html/rfc5246)을(를) 사용하여 암호화된 보안 연결을 통해 수행됩니다.

>[!IMPORTANT]
>
>Commerce은 데이터가 유휴 상태이거나 서버 간에 전송되지 않을 때 열 또는 행 수준 암호화 또는 암호화를 지원하지 않습니다.

### Experience Platform의 데이터 암호화

판매자가 Experience Platform으로 데이터를 보낼 때 HTTPS TLS v1.2를 사용하여 해당 데이터가 전송됩니다. [Experience Platform](https://experienceleague.adobe.com/ko/docs/experience-platform/landing/governance-privacy-security/encryption)이(가) 데이터를 암호화하는 방법에 대해 자세히 알아보세요.

## [!DNL Commerce]에서 개인 정보 요청을 처리하는 방법

[!DNL Commerce] [개인 정보 보호 요청을 처리하는 방법](handle-privacy-request.md)을 알아보세요.
