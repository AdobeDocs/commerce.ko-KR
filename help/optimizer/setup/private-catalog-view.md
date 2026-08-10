---
title: 비공개 카탈로그 보기
description: 유효한 서명 토큰이 있는 요청만 제품 및 가격 데이터를 검색할 수 있도록 카탈로그 보호를 활성화하여 개인 카탈로그 보기를 만드는 방법에 대해 알아봅니다.
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="SaaS만" type="Positive" url="https://experienceleague.adobe.com/ko/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 [!DNL Adobe Commerce Optimizer] 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 38fa0734562a631fdcdd7510580571c5d37cb598
workflow-type: tm+mt
source-wordcount: 467
ht-degree: 0%

---

# 비공개 카탈로그 보기

기본적으로 [카탈로그 보기](catalog-view.md)는 공개 보기입니다. 유효한 서명된 토큰이 포함된 요청에 대한 액세스를 제한하려면 카탈로그 보기에서 카탈로그 보호를 사용하도록 설정하십시오.

카탈로그 보호는 선택한 카탈로그 보기에만 적용됩니다. 보기의 정책, 레이어 또는 가격 장부는 변경되지 않습니다.

카탈로그 보기를 보호할 시기에 대한 예는 [제한된 액세스 키 사용 사례](restricted-access-keys.md#restricted-access-key-use-cases)를 참조하세요.

## 보호 경계 이해

카탈로그 보호는 활성화된 카탈로그 보기에만 적용됩니다. 이 기능은 카탈로그 및 검색 요청을 보호하지만 보기의 정책이나 가격 장부를 변경하거나 다른 카탈로그 보기를 보호하거나 장바구니, 체크아웃 또는 주문 작업을 보호하지는 않습니다.

연결된 상거래 백엔드는 독립적으로 구매 자격을 적용해야 합니다.

## 카탈로그 보기 보호

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

[!UICONTROL Catalog Protection]을(를) 사용하도록 설정하고 할당된 모든 키가 만료되면 카탈로그 보기에 액세스할 수 없게 됩니다. 이 카탈로그 보기에 의존하는 상점은 데이터를 제공할 수 없습니다. 액세스 권한을 복원하려면 만료되지 않은 새 키를 할당하십시오. 자세한 내용은 [키 회전](restricted-access-keys.md#rotate-a-key)을 참조하세요.

>[!IMPORTANT]
>
>Adobe Commerce 및 Adobe Commerce Optimizer 커넥터를 통한 자동 키 생성 및 관리는 아직 사용할 수 없습니다.

## 다음과 같음

- [카탈로그 보기](catalog-view.md) - 카탈로그 보기가 비즈니스 구조, 정책 및 가격별로 제품 카탈로그를 구성하는 방법을 알아봅니다.
- [제한된 액세스 키](restricted-access-keys.md)—카탈로그 보호를 위해 토큰을 서명하는 데 사용되는 키를 만들고, 할당하고, 회전합니다.
