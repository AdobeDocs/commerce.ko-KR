---
title: 데이터 동기화
description: Commerce 데이터 원본에서  [!DNL Adobe Commerce Optimizer] (으)로 동기화 중인 카탈로그 데이터를 검토하십시오.
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="SaaS만" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."
exl-id: c0f4664c-6afc-4762-856b-5e26a865d3a2
source-git-commit: e2c3c8a225b2c56985ba48c7efc9ae2c2d059b2e
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 0%

---

# 데이터 동기화

**데이터 동기화** 페이지에는 데이터 원본(기존 Commerce 카탈로그, 제품 정보 관리(PIM) 시스템, ERP(Enterprise Resource Planning) 시스템 등)에서 [!DNL Adobe Commerce Optimizer]&#x200B;(으)로 전송되는 제품 데이터의 동기화 상태에 대한 개요가 표시됩니다.

**데이터 동기화** 페이지에서는 상점 데이터를 사용할 수 있는 지에 대한 중요한 통찰력을 제공하여 쇼핑객에게 즉시 표시되도록 합니다.

**데이터 동기화** 페이지는 *설정* > **데이터 동기화**&#x200B;에 있습니다.

![데이터 동기화](../assets/data-sync.png)

**데이터 동기화** 페이지에 다음 필드가 포함되어 있습니다.

| 필드 | 설명 |
|--- |--- |
| 카탈로그 소스 | 동기화된 데이터에 대한 특정 로케일. |
| [!DNL Catalog Service] | [!DNL Catalog Service]에 대해 동기화된 제품의 최신 동기화 업데이트, 받은 총 제품, 검색 필드 및 테이블을 표시합니다. |
| 제품 검색 | 최신 동기화 업데이트, 받은 총 제품 수, 검색 필드 및 검색을 위해 동기화된 제품 표를 표시합니다. |
| 권장 사항 | 최신 동기화 업데이트, 받은 총 제품 수, 검색 필드 및 Recommendations에 대해 동기화된 제품 표를 표시합니다. |
| 지난 3시간 동안 받은 제품 | 지난 3시간 동안 카탈로그 소스에서 Adobe Commerce Optimizer으로 전송된 제품 수를 표시합니다. 카탈로그를 자주 업데이트하지 않는 경우 이 값은 0인 경우가 많습니다. |
| 카탈로그의 총 제품 수 | Adobe Commerce Optimizer에서 사용할 수 있는 총 카탈로그 제품 수를 반영합니다. |
| 동기화된 제품 | Adobe Commerce Optimizer에 동기화된 제품에 대한 세부 정보를 제공합니다. 기본적으로 이 테이블은 &#39;최근 업데이트&#39;별로 정렬됩니다. 특정 제품을 찾으려면 **[!UICONTROL Search by Name or SKU]** 필드를 사용하십시오. |

## 동기화된 제품 목록

JSON 형식의 동기화된 제품에 대한 세부 정보를 보려면 동기화된 제품 테이블에서 제품 행의 코드 아이콘 ![코드 링크](../assets/data-sync-details.png)를 클릭하십시오.

![제품 세부 정보 동기화](../assets/synced-products.png)

## 카탈로그 데이터 재동기화

**데이터 동기화** 페이지에 특정 제품이 표시되지 않으면 업스트림 시스템에서 재동기화를 시작해야 합니다. 그러나 재동기화를 통해 하드웨어 리소스의 부하를 늘릴 수 있습니다. 그러나 다음 시나리오에서는 카탈로그를 다시 동기화하는 것이 필요할 수 있습니다.

- 새 제품 추가, 제품 세부 사항 업데이트 또는 범주 수정과 같이 제품 카탈로그가 크게 변경되는 경우

- 상점에 제품 데이터를 표시할 때 불일치나 성능 문제가 발생하는 경우

>[!IMPORTANT]
>
>동기화를 완료하는 데 걸리는 시간은 카탈로그 크기와 업데이트된 데이터의 볼륨에 따라 다릅니다.

## 데이터 동기화 상태 모니터링

Adobe Commerce을 업스트림 데이터 소스로 사용하는 프로젝트의 경우 Commerce 관리자의 [데이터 피드 동기화 상태 페이지](../../data-export/data-synchronization.md)에서 데이터 내보내기 프로세스를 모니터링하고 다시 동기화 작업을 시작할 수 있습니다.

