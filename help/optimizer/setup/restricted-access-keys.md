---
title: 제한된 액세스 키
description: 제한된 액세스 키가 B2B 공유 카탈로그에 대해 자동으로 만들어지거나 수동으로 관리되는 [!DNL Adobe Commerce Optimizer]의 카탈로그 보기를 보호하는 방법에 대해 알아봅니다.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="SaaS만" type="Positive" url="https://experienceleague.adobe.com/ko/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 [!DNL Adobe Commerce Optimizer] 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."
TQID: https://experienceleague.adobe.com/Jmze0Pq3kSNMIXqkkML-hmmlZnv-XKgeEgRB8Q8NZ6s
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
    internal-label: Optimization
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
nudge: true
source-git-commit: f93bd673624c58050696da772ce733874ce594e5
workflow-type: tm+mt
source-wordcount: '1251'
ht-degree: 0%
---
# 제한된 액세스 키

제한된 액세스 키를 사용하면 권한 있는 클라이언트 응용 프로그램에서 [개인 카탈로그 보기](catalog-view.md)에 액세스할 수 있습니다. 할당된 키에서 올바른 서명된 토큰을 포함하는 요청만 카탈로그 데이터를 검색할 수 있습니다. 이 카탈로그 보기에 대한 액세스 권한이 명시적으로 부여되지 않은 쇼핑객의 요청 및 API를 검사하는 스크립트를 포함한 다른 모든 요청은 거부됩니다.

제한된 액세스 키는 다음 두 가지 방법 중 하나로 제공됩니다.

- [!BADGE Private Beta]{type=Caution tooltip="현재 비공개 베타에 있는 Adobe Commerce Optimizer 커넥터 B2B 확장이 필요합니다."} **B2B 공유 카탈로그에 대해 자동으로**—[!DNL Adobe Commerce Optimizer Connector for B2B]과(와) 통합된 배포의 경우 커넥터가 초기 키를 프로비저닝하고 할당합니다. 그런 다음 Commerce 관리자로부터 키 및 키 할당을 관리합니다. *Commerce 관리 안내서**에서 [카탈로그 보기 인증](https://experienceleague.adobe.com/ko/docs/commerce-admin/b2b/shared-catalogs/catalog-views-manage)을 참조하십시오.

- **카탈로그 보기에 대해 수동으로**—파트너 포털 또는 시험판 미리 보기와 같이 카탈로그 보기를 직접 보호하려면 [제한된 액세스 키를 만듭니다](#create-a-restricted-access-key). 이 항목의 단계를 따르십시오.

## 제한된 액세스 키 사용 사례

[!DNL Adobe Commerce Optimizer]에서 **[!UICONTROL Price Book ID]**&#x200B;은(는) 요청이 볼 수 있는 가격을 결정합니다. 가격에는 제한이 있지만 요청을 할 수 있는 사람은 없습니다. 카탈로그 보기의 ID 및 가격 장부 ID를 알고 있는 모든 클라이언트는 머천다이징 API를 통해 해당 데이터를 검색할 수 있습니다. 제한된 액세스 키는 별도의 보완 제어를 추가합니다. 이들은 적용되는 가격 장부에 관계없이 카탈로그 보기에 액세스할 수 있는 사용자의 범위를 지정합니다.

제한된 액세스 키는 일반적으로 다음에 사용됩니다.

- **계약 기반 B2B 가격 책정**—협상된 가격 장부에 연결된 카탈로그 보기를 제한하여 구매자만 이를 쿼리할 수 있도록 합니다. 다른 구매 조직과 대중은 할 수 없습니다. B2B 공유 카탈로그의 경우 자동으로 설정됩니다. [키 관리 및 순환](#key-management-and-rotation)을 참조하세요.
- **파트너 및 리셀러 포털** - 머천다이징 API와 직접 통합하는 승인된 파트너로 카탈로그 하위 집합을 제한합니다.
- **프리릴리스 미리 보기** - 신뢰할 수 있는 내부 또는 파트너 시스템에서 예정된 제품을 공개하기 전에 미리 볼 수 있습니다.

## 제한된 액세스 키 작동 방식

제한된 액세스 키는 RSA 키 쌍의 공개 구성 요소입니다. 클라이언트 애플리케이션은 이 키를 생성하여 사용하여 개인 카탈로그 보기를 읽을 수 있는 권한을 부여합니다. 이 컨텍스트에서 _클라이언트 응용 프로그램_&#x200B;은(는) 상점 프런트 엔드 자체가 아닌 쇼핑객(예: [!DNL Adobe Commerce]의 사용자 지정 논리 또는 타사 백엔드)을 인증하는 백 엔드 시스템을 참조합니다.

다음 단계에서는 키 쌍과 서명된 토큰이 B2B 공유 카탈로그의 일부가 아닌 카탈로그 보기에 대한 만들기에서 유효성 검사로 이동하는 방법을 설명합니다.

1. 클라이언트 애플리케이션은 RSA 키 쌍을 생성하고 개인 키를 유지합니다.
1. [!DNL Commerce Optimizer]의 **public** 키를 제한된 액세스 키로 등록했습니다.
1. 클라이언트 애플리케이션은 개인 키로 JSON 웹 토큰(JWT)에 서명하고 개인 카탈로그 보기에 대한 각 요청과 함께 이 토큰을 포함합니다.
1. [!DNL Commerce Optimizer]이(가) 등록된 공개 키에 대해 토큰 서명을 확인하고, 유효한 경우 요청된 카탈로그 데이터를 반환합니다.

## 제한된 액세스 키 만들기

>[!NOTE]
>
>이 섹션과 다음 세 섹션에서는 수동 [!DNL Adobe Commerce Optimizer] Studio 흐름에 대해 설명합니다. [!DNL Adobe Commerce Optimizer Connector B2B extension]과(와) 함께 B2B 공유 카탈로그를 사용하는 경우 Commerce 관리자의 키를 관리합니다. _Adobe Commerce Optimizer 커넥터_ 설명서에서 [제한된 액세스 키](../../aco-connector/restricted-access-keys.md)를 참조하십시오.

개인 카탈로그 보기의 초기 테스트를 수행하려면 [!DNL OpenSSL]과(와) 같은 도구를 사용하여 키 쌍을 생성하십시오. 개인 키 비밀을 유지하십시오. 공개 키만 [!DNL Commerce Optimizer]에 업로드됩니다.

```bash
openssl genrsa -out private-key.pem 2048
openssl rsa -in private-key.pem -pubout -out public-key.pem
```

키 크기는 2048비트와 8192비트 사이여야 합니다. `public-key.pem`에 아래 **[!UICONTROL Public key]** 필드에 붙여 넣은 값이 있습니다.

## [!DNL Commerce Optimizer]에 제한된 액세스 키 추가

1. [!DNL Adobe Commerce Optimizer Studio]의 왼쪽 메뉴에서 **[!UICONTROL Store setup]**(으)로 이동한 다음 **[!UICONTROL Restricted access keys]**&#x200B;을(를) 클릭합니다.

   ![제한된 액세스 키 목록(제한된 액세스 키 추가 단추 포함)](../assets/restricted-access-keys.png){width="70%" zoomable="yes"}

1. **[!UICONTROL Add Restricted Access Key]**&#x200B;을(를) 클릭합니다.

1. 주요 세부 정보 입력:

   ![제목, 만료 날짜 및 공개 키 필드가 있는 제한된 액세스 키 양식 추가](../assets/restricted-access-keys-add.png){width="70%" zoomable="yes"}

   - **[!UICONTROL Title]** - 키 목록 및 카탈로그 보기 키 선택기에 표시되는 키를 식별하는 레이블입니다(예: `ACME Corp wholesale portal — Tier 1 pricing`).
   - **[!UICONTROL Expiration date]**—아직 만료되지 않은 토큰의 경우에도 키 사용이 중지되는 날짜 및 시간(UTC).
   - **[!UICONTROL Public key]** - `-----BEGIN PUBLIC KEY-----` 및 `-----END PUBLIC KEY-----` 마커를 포함하여 SPKI(주체 공개 키 정보) 형식의 PEM 인코딩 RSA 공개 키입니다. 환경 전체에서 고유해야 합니다.

1. **[!UICONTROL Save]**&#x200B;을(를) 클릭합니다.

키를 만든 후에는 변경할 수 없습니다. 값을 변경하려면 키를 삭제하고 새 값을 만듭니다. 액세스 중단 없이 이 작업을 수행하려면 [키 회전](#rotate-a-key)을 참조하십시오.

## 카탈로그 보기에 키 할당

제한된 액세스 키는 **[!UICONTROL Catalog Protection]**&#x200B;이(가) 활성화된 카탈로그 보기에 할당된 후에만 액세스를 인증합니다. 설치 단계는 [카탈로그 보기 보호](private-catalog-view.md#protect-a-catalog-view)를 참조하십시오.

## 키 삭제

1. **[!UICONTROL Restricted access keys]** 페이지에서 제거할 키를 찾아 **[!UICONTROL Delete]**&#x200B;을(를) 클릭합니다.

   하나 이상의 카탈로그 보기에 키를 할당하면 해당 키를 사용하는 클라이언트 응용 프로그램에 대한 액세스 권한이 상실된다는 경고가 표시됩니다. 카탈로그 뷰 자체는 보호되어 있으므로 공개적으로 액세스할 수 없습니다.

1. 삭제를 확인합니다.

## 키 관리 및 순환

제한된 액세스 키는 카탈로그 보호를 사용하는 방법에 따라 다음 두 가지 방법 중 하나로 관리됩니다.

- **B2B 공유 카탈로그에 대해 자동으로**—[!BADGE Private Beta]{type=Caution tooltip="현재 비공개 베타에 있는 Adobe Commerce Optimizer 커넥터 B2B 확장이 필요합니다."} [!DNL Adobe Commerce Optimizer Connector for B2B]과(와) 통합된 배포에 대해 서비스는 카탈로그 보기를 만들 때 첫 번째 제한된 액세스 키를 자동으로 생성하고 할당합니다. 각 카탈로그 보기는 자체 키를 받습니다. 그런 다음 공유 카탈로그 또는 회사 계정 페이지에서 각 키를 관리할 수 있습니다. Commerce 관리 **제한된 액세스 키** 페이지(**시스템** > **데이터 전송**)에서 키를 보고 관리할 수도 있습니다. [카탈로그 보기 구성 관리](https://experienceleague.adobe.com/ko/docs/commerce-admin/b2b/shared-catalogs/catalog-views-manage)를 참조하세요.

  공유 카탈로그와 이 공유 카탈로그가 할당된 스토어 보기의 각 조합은 별도의 카탈로그 보기로 투영됩니다. 프로젝션은 커넥터가 해당 조합에 대해 [!DNL Adobe Commerce Optimizer]&#x200B;(으)로 내보내는 카탈로그 보기, 정책, 가격 장부 참조 및 제한된 액세스 키 구성 데이터입니다. 따라서 여러 저장소 보기에 할당된 공유 카탈로그는 각각 고유한 키를 가진 여러 카탈로그 보기를 생성합니다. 다른 항목에 영향을 주지 않고 한 카탈로그 보기에 대한 키를 편집하거나 회전합니다.

  키는 기본적으로 만료 기간이 깁니다. 키를 회전해야 하는 경우 관리자에서 교체를 추가하고 이전 키를 제거할 때까지 두 키를 모두 활성 상태로 유지합니다. [B2B 공유 카탈로그 변경 내용](/help/aco-connector/get-started.md#monitor-b2b-shared-catalog-changes)을 참조하세요.

- **수동으로 모든 카탈로그 보기**—Adobe Commerce 백엔드의 B2B 공유 카탈로그와 연결되어 있지 않은 카탈로그 보기의 경우, 키 생성, 토큰 서명 및 순환은 구매자를 인증하는 백 엔드 클라이언트 응용 프로그램에서 완전히 관리됩니다. [!DNL Adobe Commerce Optimizer]이(가) 사용자를 대신하여 이 키를 생성하거나 회전하지 않습니다. 이 항목의 앞 단계를 사용하여 키를 만들고, 추가하고, 삭제합니다. 키를 회전하려면 [키 회전](#rotate-a-key)을 참조하세요.

### 키 회전

액세스 중단 없이 키를 회전하려면 카탈로그 보기에서 최대 3개의 키를 한 번에 할당할 수 있습니다.

1. 새 키 쌍을 생성하고 새 공개 키를 새 제한된 액세스 키로 추가합니다.
1. 기존 키와 함께 새 키를 카탈로그 보기에 할당합니다.
1. 새 개인 키로 새 토큰에 서명을 시작하여 키 롤오버를 완료합니다.
1. 새 키에서 모든 클라이언트 응용 프로그램이 확인되면 이전 키를 제거하고 삭제합니다.

## 제한

[카탈로그 보기 및 정책 제한](../boundaries-limits.md#catalog-views-and-policies)을 참조하세요.

## 다음과 같음

- [비공개 카탈로그 보기](private-catalog-view.md)—제한된 액세스 키로 카탈로그 보기를 보호하는 방법에 대해 알아봅니다.
- [B2B 공유 카탈로그 변경](/help/aco-connector/get-started.md#monitor-b2b-shared-catalog-changes)—[!DNL Adobe Commerce Optimizer Connector]이(가) B2B 공유 카탈로그에 대한 키 관리를 자동화하는 방법을 알아봅니다.

