---
title: 비공개 카탈로그 보기
description: 비공개 카탈로그 보기가 B2B 공유 카탈로그에 대해 자동으로 생성되거나 카탈로그 보호로 수동으로 구성된 카탈로그 데이터 액세스를 제한하는 방법에 대해 알아봅니다.
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="SaaS만" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 [!DNL Adobe Commerce Optimizer] 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."
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
source-git-commit: f93bd673624c58050696da772ce733874ce594e5
workflow-type: tm+mt
source-wordcount: '903'
ht-degree: 0%
---
# 비공개 카탈로그 보기

기본적으로 [카탈로그 보기](catalog-view.md)는 공개 보기입니다. 유효한 서명 토큰이 있는 요청만 해당 데이터를 검색할 수 있도록 카탈로그 보기에 대한 액세스를 제한합니다.

카탈로그 보기는 다음 두 가지 방법 중 하나로 비공개가 됩니다.

- [!BADGE Private Beta]{type=Caution tooltip="현재 비공개 베타에 있는 Adobe Commerce Optimizer 커넥터 B2B 확장이 필요합니다."} **B2B 공유 카탈로그에 대해 자동으로**—B2B 확장과 [!DNL Adobe Commerce Optimizer Connector] 통합을 사용하는 Commerce 배포의 경우 [!DNL Adobe Commerce]의 공유 카탈로그 구성에 따라 개인 카탈로그 보기가 자동으로 만들어지고 구성됩니다. B2B 공유 카탈로그에 대한 [자동 비공개 카탈로그 보기](#automatic-private-catalog-views-for-b2b-shared-catalogs)를 참조하세요.

- **모든 카탈로그 보기에 대해 수동으로**—B2C 카탈로그 보기를 포함하여 공개되는 카탈로그 보기에 대한 액세스를 제한하려면 [카탈로그 보기 보호](#protect-a-catalog-view)의 단계를 따르십시오. 파트너 포털 및 시험판 미리 보기와 같은 예는 [제한된 액세스 키 사용 사례](restricted-access-keys.md#restricted-access-key-use-cases)를 참조하십시오.

카탈로그 보호는 선택한 카탈로그 보기에만 적용됩니다. 보기의 정책 또는 계층은 변경되지 않습니다. 단일 가격 장부로 보기를 제한합니다. [개인 카탈로그 보기에 대한 가격 장부 제한](#price-book-restriction-on-private-catalog-views)을 참조하세요.

## 보호 경계 이해

카탈로그 보호는 활성화된 카탈로그 보기에만 적용됩니다. 이 기능은 카탈로그 및 검색 요청을 보호하지만 보기의 정책이나 계층을 변경하거나 다른 카탈로그 보기를 보호하거나 장바구니, 체크아웃 또는 주문 작업을 보호하지 않습니다.

연결된 상거래 백엔드는 독립적으로 구매 자격을 적용해야 합니다.

## 개인 카탈로그 보기에 대한 가격 책자 제한

비공개 카탈로그 보기는 하나의 가격 장부만 참조할 수 있습니다. 이는 여러 가격 장부를 사용할 수 있는 공개 카탈로그 보기와는 다릅니다.

[!UICONTROL Catalog Protection]을(를) 사용하도록 설정하면 카탈로그 보기 양식의 가격 장부 선택기가 다중 선택 컨트롤에서 단일 선택(라디오 단추) 컨트롤로 전환됩니다.

![비공개 카탈로그 가격 목록 보기 제한](../assets/catalog-view-private-pricebook-restrictions.png)

- 가격 장부가 여러 개 할당된 카탈로그 보기에서 [!UICONTROL Catalog Protection]을(를) 사용하도록 설정하면 가격 장부를 하나만 제외한 모든 항목을 제거할 때까지 보기를 저장할 수 없습니다.
- 이 제한이 존재하기 전에 가격 장부 지정을 여러 개 사용하여 개인 카탈로그 뷰를 이전에 저장한 경우 카탈로그 뷰 구성이 자동으로 변경되지 않습니다. 그러나 다음에 보기를 편집할 때는 업데이트를 저장하기 전에 하나의 가격 장부를 제외한 모든 가격 장부를 제거해야 합니다.

이러한 각 경우에 [!DNL Adobe Commerce Optimizer]은(는) 다음 유효성 검사 메시지를 표시합니다. `A protected catalog view can use only one price book. Select 'Single price book only' to continue.`

공개 카탈로그 보기는 이 제한의 영향을 받지 않으며 여러 가격 장부를 계속 참조할 수 있습니다.

## B2B 공유 카탈로그에 대한 자동 비공개 카탈로그 보기

[!BADGE Private Beta]{type=Caution tooltip="현재 비공개 베타에 있는 Adobe Commerce Optimizer 커넥터 B2B 확장이 필요합니다."}

공유 카탈로그를 지원하기 위해 [!DNL Adobe Commerce Optimizer Connector for B2B]과(와) 통합된 배포의 경우, 확장 기능은 [!DNL Adobe Commerce]의 공유 카탈로그 구성에 따라 개인 카탈로그 보기를 자동으로 만들고 구성합니다. 이 구성에는 카탈로그 보기, 정책, 초기 제한 액세스 키 및 가격 장부 참조가 포함됩니다. 이 구성을 통해 Commerce 관리 **제한된 액세스 키** 페이지(**시스템** > **데이터 전송**)에서 제한된 액세스 키를 관리합니다. 자세한 내용은 *[!DNL Adobe Commerce Optimizer Connector]통합 안내서*&#x200B;의 [B2B 공유 카탈로그 변경 내용](/help/aco-connector/get-started.md#monitor-b2b-shared-catalog-changes)을 참조하세요.

B2B 공유 카탈로그를 사용하지 않는 경우(예: 파트너 포털 또는 프리릴리스 미리 보기에 대한 카탈로그 보기를 보호하려면 [카탈로그 보기 보호](#protect-a-catalog-view)의 지침을 사용하여 수동으로 구성해야 합니다.

## 카탈로그 보기 보호

>[!NOTE]
>
>[!DNL Adobe Commerce Optimizer Connector for B2B]에서 관리하는 B2B 공유 카탈로그와 연결된 카탈로그 보기에 대해서는 이 절차를 건너뜁니다. B2B 공유 카탈로그에 대한 [자동 비공개 카탈로그 보기](#automatic-private-catalog-views-for-b2b-shared-catalogs)를 참조하세요.

시작하기 전에 클라이언트 응용 프로그램에서 생성한 공개 키에서 [제한된 액세스 키를 만듭니다](restricted-access-keys.md).

1. 카탈로그 보기 만들기 또는 편집 양식에서 **[!UICONTROL Catalog Protection]**&#x200B;을(를) **[!UICONTROL Enabled]**(으)로 전환합니다.

1. **[!UICONTROL Restricted Access Keys]**&#x200B;에서 이 카탈로그 보기에 할당할 최대 3개의 [제한된 액세스 키](restricted-access-keys.md)를 선택하십시오.

   ![카탈로그 보기 편집 양식에 제한된 액세스 키가 할당된 카탈로그 보호가 활성화됨](../assets/catalog-view-protected.png){width="70%" zoomable="yes"}

1. **[!UICONTROL Save catalog view]**&#x200B;을(를) 클릭합니다.

   이제 카탈로그 보기가 보호됩니다. 할당된 키에서 유효한 서명된 토큰을 전달하는 요청만 해당 데이터를 검색할 수 있습니다.

   >[!NOTE]
   >
   >카탈로그 보호 구성 변경 사항이 적용되는 데 최대 5분이 소요됩니다.

## 액세스가 적용되었는지 확인

비공개 카탈로그 보기가 권한 없는 요청을 거부하는지 확인하려면 다음 헤더를 사용하여 서명된 토큰을 사용하거나 사용하지 않고 해당 [GraphQL 끝점](../get-started.md#get-instance-details)을 호출합니다.

| 머리글 | 목적 |
| --- | --- |
| `AC-View-ID` | 쿼리할 카탈로그 보기입니다. |
| `AC-Price-Book-ID` | 적용할 가격 장부입니다. |
| `AC-Catalog-View-Access-Token` | 카탈로그 보기에 대한 인증을 증명하는 서명된 JWT입니다. |

유효한 토큰이 없는 요청은 카탈로그 데이터 대신 GraphQL 오류를 반환합니다. 예:

```json
{
  "errors": [
    {
      "message": "Access key validation failed: Missing token",
      "extensions": { "x-commerce-exception": "access-key-invalid" }
    }
  ]
}
```

만료되지 않은 할당된 키로 서명된 토큰을 전달하는 요청은 카탈로그 데이터를 예상대로 반환합니다. JWT에 서명하고 머천다이징 API를 호출하는 방법에 대한 자세한 내용은 [개발자 설명서](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/using-the-api#authentication)를 참조하십시오.

## 제한된 액세스 키 관리

[!UICONTROL Catalog Protection]을(를) 사용하도록 설정하고 할당된 모든 키가 만료되면 카탈로그 보기에 액세스할 수 없게 됩니다. 이 카탈로그 보기에 의존하는 상점 영역은 데이터를 제공할 수 없습니다. 액세스 권한을 복원하려면 만료되지 않은 새 키를 할당하십시오. 자세한 내용은 [키 회전](restricted-access-keys.md#rotate-a-key)을 참조하세요.

>[!NOTE]
>
>[!DNL Adobe Commerce Optimizer Connector for B2B] 확장과 통합된 배포의 경우 Commerce 관리 **제한된 액세스 키** 페이지(**시스템** > **데이터 전송**)에서 액세스 키를 관리합니다. 자세한 내용은 *[!DNL Adobe Commerce Optimizer Connector]통합 안내서*&#x200B;의 [제한된 액세스 키 관리](../../aco-connector/restricted-access-keys.md)를 참조하십시오.

## 다음과 같음

- [카탈로그 보기](catalog-view.md) - 카탈로그 보기가 비즈니스 구조, 정책 및 가격별로 제품 카탈로그를 구성하는 방법을 알아봅니다.
- [제한된 액세스 키](restricted-access-keys.md)—카탈로그 보호를 위해 토큰을 서명하는 데 사용되는 키를 만들고, 할당하고, 회전합니다.
