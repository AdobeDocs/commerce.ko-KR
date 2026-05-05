---
title: 보안 아키텍처 및 데이터 흐름
description: Adobe Commerce as a Cloud Service의 보안 아키텍처 및 데이터 흐름에 대해 알아봅니다.
role: Admin, Architect, Leader
badgeSaas: label="SaaS만" type="Positive" url="https://experienceleague.adobe.com/ko/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."
source-git-commit: 0343c4f3ecc182145a97e08eca2790bd1512aa27
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---


# 보안 아키텍처 및 데이터 흐름

다음 예제에서는 일반적으로 데이터가 [!DNL Adobe Commerce as a Cloud Service]에서 어떻게 흐르는지 보여 줍니다.

![Adobe Commerce as a Cloud Service 데이터 흐름 다이어그램](../assets/data-flow-1.png)

## 데이터 흐름 이야기

**1단계**: 쇼핑객이 브라우저에 가맹점의 상점 URL을 입력하여 Commerce 상점 URL을 외부 CDN(Content Delivery Network)로 보냅니다.

**2단계**: 사이트 URL이 캐시되면 Storefront CDN이 이 URL을 구매자에게 반환합니다. 리소스에 대한 첫 번째 요청인 경우 발생할 수 있는 아직 캐시되지 않은 경우 외부 CDN이 구매자 요청을 내부 CDN으로 전달하고 후속 요청에 대한 응답을 캐시합니다.

**2a**: 이미지 또는 비디오에 대한 요청인 경우 해당 요청이 [!DNL Product Visuals]&#x200B;(으)로 전송되어 상점 앞으로 반환됩니다.

**3단계**: 사이트 URL이 내부 CDN에 캐시되면 해당 캐시에서 반환됩니다. 그렇지 않은 경우 [!DNL API Mesh]&#x200B;(으)로 전송되며 응답은 후속 요청에 대해 캐시됩니다.

**4단계**: [!DNL API Mesh]은(는) 오케스트레이션 계층 역할을 하며 요청을 [!DNL Adobe Commerce as a Cloud Service] 또는 서드파티 시스템에 보내 요청을 이행할지 여부를 결정합니다.

>[!NOTE]
>
>[!DNL API Mesh]은(는) Mesh 구성을 사용자 지정한 경우에만 서드파티 시스템에 요청을 보냅니다.

**5단계**: [!DNL Adobe Commerce as a Cloud Service]&#x200B;(으)로 전송된 요청은 의심스러운 또는 악의적인 요청을 차단하는 웹 응용 프로그램 방화벽(WAF)을 통과합니다. 요청된 URL이 [!DNL Commerce] CDN에 캐시되면 해당 캐시에서 전달됩니다. 캐시되지 않은 경우 하나 이상의 [!DNL Adobe Commerce as a Cloud Service] 마이크로서비스(예: foundation, search 및 recommendations)에서 반환된 다음 이후 요청에 대해 캐시됩니다.

**5a**: 요청이 서드파티 시스템으로 전송되면 응답이 [!DNL API Mesh]&#x200B;(으)로 반환됩니다.

**5b**: 결제 처리를 위한 요청인 경우 결제 공급자는 쇼핑객이 신용 카드 정보를 안전하게 입력하고 결제 거래를 완료할 수 있도록 iframe을 상점 앞에 렌더링합니다.

**6단계**: [!DNL Adobe Commerce as a Cloud Service] 또는 서드파티 서비스의 응답이 [!DNL API Mesh]에 수신되면 함께 통합 그래프로 결합되어 [!DNL Commerce Storefront]에 반환되어 구매자의 요청을 처리합니다.
