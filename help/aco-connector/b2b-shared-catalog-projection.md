---
title: B2B 공유 카탈로그 프로젝션
description: B2B 커넥터가 Adobe Commerce B2B 공유 카탈로그를 보호된 Commerce Optimizer 카탈로그 보기로 프로젝션하는 방법과 상점이 구매자 액세스를 해결하고 권한을 부여하는 방법에 대해 알아봅니다.
feature: Integration, Configuration
role: Admin, Developer
level: Intermediate
TQID: 'https://experienceleague.adobe.com/b37PBjcVQXRSLrB6c7nEf3A3U5cuLs1lQzwPUbp9fdA'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
feature_v2:
  - id: 4067ab89-2e97-5de1-8d98-de8318461a8d
    internal-label: Products
  - id: 4ca54350-01cb-5b22-8966-5f2873dc6d90
    internal-label: Media
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
    internal-label: Security
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
subfeature_v2:
  - id: 3c398179-d35a-51ba-b317-6c5b95feef5e
    internal-label: Logs
  - id: a1d22079-48b9-5e69-9ee6-eb236068ef34
    internal-label: Search
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
source-git-commit: a3ade1a31d3c2905b601f71bda118de89c43cf59
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%
---
# B2B 공유 카탈로그 프로젝션

[!DNL Adobe Commerce Optimizer Connector for B2B] 프로젝트 [!DNL Adobe Commerce]이(가) 카탈로그 및 회사 할당을 보호된 [!DNL Adobe Commerce Optimizer] 카탈로그 보기로 공유했습니다.

## 기본 동기화 및 B2B 투영

기본 [!DNL Adobe Commerce Optimizer Connector]은(는) 카탈로그 및 가격 피드를 동기화하고, 스토어 보기를 카탈로그 소스에 매핑하고, 웹 사이트를 가격 장부에 매핑하고, 고객 그룹을 가격 장부에 매핑합니다.

[!DNL Adobe Commerce Optimizer Connector for B2B]은(는) 각 사용자 지정 공유 카탈로그의 분류와 가격을 보호된 보기로 프로젝션합니다. Adobe Commerce은 구매자의 회사 지정을 사용하여 뷰를 선택합니다. 제한된 액세스 키는 서명된 요청을 확인하지만 카탈로그 액세스를 결정하지 않습니다. Adobe Commerce은 커넥터 관리 카탈로그, 가격 및 B2B 프로젝션 데이터에 대한 기록 시스템입니다. [!DNL Adobe Commerce Optimizer] 구성에서 제품 검색 및 권장 사항을 관리합니다.

## 데이터 매핑

B2B 프로젝션은 동기화된 카탈로그 콘텐츠 및 가격을 공유 카탈로그 분류 및 회사 할당 컨텍스트와 결합합니다.

![다이어그램 매핑 [!DNL Adobe Commerce] 저장소 보기, 가격 책정, 공유 카탈로그 및 회사 할당과 [!DNL Adobe Commerce Optimizer]](./assets/b2b-catalog-projection-mapping.svg){width="800"}의 예상 개인 카탈로그 보기

| [!DNL Adobe Commerce] 데이터 | [!DNL Adobe Commerce Optimizer]개 결과 | 목적 |
| --- | --- | --- |
| 스토어 보기 및 제품 데이터 활성화 | 카탈로그 소스 | 현지화된 제품 콘텐츠를 제공합니다. |
| 웹 사이트 및 고객 그룹 가격 | 가격 장부 | 적용 가능한 가격을 제공하지만 액세스를 승인하지 않습니다. |
| 사용자 지정 공유 카탈로그 분류 | 정책 | 카탈로그 보기를 공유 카탈로그 분류로 필터링합니다. |
| 사용자 지정 공유 카탈로그 및 활성화된 저장소 보기 | 비공개 카탈로그 보기 | 해당 카탈로그 소스, 정책 및 가격 장부를 사용하여 각 조합에 대해 하나의 보호된 보기를 만듭니다. |
| 공유 카탈로그에 회사 할당 | 해결된 구매자 컨텍스트 | 인증된 백엔드가 구매자 회사와 연결된 카탈로그 보기를 확인하도록 합니다. |
| 제한된 액세스 키가 보호된 보기에 할당됨 | 카탈로그 보호 | 보호된 카탈로그 보기에 대한 요청을 승인하지만 가격책정을 선택하지 않습니다. |

각 비공개 카탈로그 보기는 하나의 가격 장부만 참조할 수 있습니다. 동일한 웹 사이트 및 고객 그룹 가격 컨텍스트를 사용하는 스토어 조회수는 현지화된 다양한 카탈로그 소스를 사용하면서 가격 책자를 공유할 수 있습니다. 커넥터가 공유 카탈로그별로 가격 장부를 만들지 않습니다.

기본 공유 카탈로그는 B2B 개인 카탈로그 보기로 투영되지 않습니다.

## 런타임 인증

구매자가 로그인하면 Commerce 백엔드가 세션을 인증하고 구매자의 회사 할당 및 스토어 보기를 사용하여 적절한 카탈로그 보기 및 가격 장부를 해결합니다.

상점은 각 머천다이징 API 요청과 함께 카탈로그 보기 ID, 가격 장부 ID 및 서명된 토큰을 보냅니다. [!DNL Adobe Commerce Optimizer]은(는) 카탈로그 보기에 할당된 제한된 액세스 키에 대해 JWT에 대한 RS256 서명을 확인합니다. 토큰과 키가 유효하고 만료되지 않은 경우에만 카탈로그 데이터를 반환합니다.

![상점 및 Commerce 백엔드를 통해 [!DNL Adobe Commerce Optimizer]](./assets/b2b-catalog-runtime-authorization.svg){width="700"}(으)로 구매자의 B2B 카탈로그 요청에 대한 런타임 인증 흐름

비공개 카탈로그 요청의 경우 다음 헤더를 보냅니다.

| 머리글 | 목적 |
| --- | --- |
| `AC-View-ID` | 카탈로그 보기를 식별합니다. |
| `AC-Price-Book-ID` | 사용할 가격 장부를 식별합니다. |
| `AC-Catalog-View-Access-Token` | 보호된 카탈로그 보기에 대한 액세스 권한을 부여하는 서명된 JWT를 전달합니다. |

전체 요청 및 토큰 요구 사항에 대해서는 [머천다이징 API 인증](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/using-the-api#authentication) 및 [개인 카탈로그 보기에 대한 액세스 확인](/help/optimizer/setup/private-catalog-view.md#verify-access-is-enforced)을 참조하십시오.

## 보호 경계

카탈로그 보호는 카탈로그 및 검색 요청만 포함합니다. 장바구니, 체크아웃 또는 주문 작업을 보호하지 않습니다. Adobe Commerce 또는 연결된 거래 시스템에서 구매 적격성을 적용합니다.

## 프로젝션 설정 및 모니터링

B2B 커넥터는 개인 카탈로그 보기, 정책, 가격표 참조 및 [!DNL Adobe Commerce]의 제한된 액세스 키 구성을 예상합니다. 이러한 커넥터 관리 투영 객체를 수동으로 생성할 필요가 없습니다. 설치 지침은 [B2B 커넥터 시작](get-started-b2b-shared-catalogs.md)을 참조하세요.

예상 카탈로그 보기를 모니터링하고 구성 변경을 조정하려면 [카탈로그 보기 동기화 모니터링](catalog-view-sync-status.md)을 참조하십시오. 할당된 키를 관리하려면 [B2B 공유 카탈로그에 대한 제한된 액세스 키 관리](restricted-access-keys.md)를 참조하세요.
