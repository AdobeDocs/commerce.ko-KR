---
title: 카탈로그 동기화
description: ' [!DNL Commerce] 서버에서  [!DNL Commerce Services](으)로 제품 데이터를 내보내는 방법에 대해 알아봅니다.'
feature: Catalog Management, Data Import/Export, Catalog Service
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 0%

---


# 카탈로그 동기화

>[!NOTE]
>
> 카탈로그 동기화 대시보드가 이제 데이터 관리 대시보드입니다. 이렇게 개선된 대시보드는 이제 [[!DNL Product Recommendations]](../product-recommendations/guide-overview.md) v6.0.0+, [[!DNL Live Search]](../live-search/overview.md) v4.1.0+ 및 [[!DNL Catalog Service]](../catalog-service/overview.md) v1.17+를 지원합니다. 고객은 해당 서비스 중 하나의 최신 버전으로 업데이트하여 데이터 관리 대시보드를 가져올 수 있습니다. 자세한 내용은 [데이터 관리 대시보드](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-dashboard.html) 설명서를 참조하세요. 이 현재 항목은 아직 업그레이드하지 않았으며 여전히 카탈로그 동기화 대시보드가 있는 사용자에게 남아 있습니다.

Adobe Commerce은 인덱서를 사용하여 카탈로그 데이터를 표로 컴파일합니다. 이 프로세스는 제품 가격 또는 재고 수준 변경과 같은 [이벤트](https://experienceleague.adobe.com/docs/commerce-admin/systems/tools/index-management.html#events-that-trigger-full-reindexing)에 의해 자동으로 트리거됩니다.

카탈로그 동기화 서비스는 데이터를 최신 상태로 유지하기 위해 제품 데이터를 [!DNL Adobe Commerce] 인스턴스에서 [!DNL Commerce Services] 플랫폼으로 지속적으로 이동합니다. 예를 들어 [[!DNL Product Recommendations]](/help/product-recommendations/overview.md)은(는) 올바른 이름, 가격 및 가용성으로 권장 사항을 정확하게 반환하기 위해 현재 카탈로그 정보가 필요합니다. _카탈로그 동기화_ 대시보드를 사용하여 동기화 프로세스 또는 명령줄 인터페이스를 관찰하고 관리하여 카탈로그 동기화를 트리거하고 [!DNL Commerce Services]에서 사용할 제품 데이터를 다시 인덱싱합니다. _SaaS 데이터 내보내기_ 안내서의 [명령줄 인터페이스 참조](../data-export/data-export-cli-commands.md)를 참조하십시오.

## 카탈로그 동기화 대시보드 액세스

카탈로그 동기화 대시보드에 액세스하려면 **시스템** > _데이터 전송_ > **카탈로그 동기화**&#x200B;를 선택하십시오.

**카탈로그 동기화** 대시보드를 사용하여 다음을 수행할 수 있습니다.

- 동기화 상태 보기(**진행 중**, **성공**, **실패**)
- 동기화된 총 제품 수 보기
- 동기화된 제품을 검색하여 현재 상태 보기
- 이름, SKU 등을 기준으로 한 검색 스토어 카탈로그
- 동기화 불일치를 진단하는 데 도움이 되도록 JSON에서 동기화된 제품 세부 정보 보기
- 동기화 프로세스 다시 시작

### 마지막 동기화

다음의 동기화 상태를 보고합니다.

- **성공** - 동기화가 성공한 날짜와 시간, 업데이트된 제품 수를 표시합니다.
- **실패** - 동기화를 시도한 날짜와 시간을 표시합니다.
- **진행 중** - 마지막으로 성공한 동기화의 날짜와 시간을 표시합니다.

카탈로그 동기화 프로세스는 매시간 자동으로 실행됩니다. 상점 앞에 예상 제품이 표시되지 않거나 제품이 최근 변경 사항을 반영하지 않는 경우 [카탈로그 동기화 문제](#resolvesync)를 해결할 수 있습니다.

### 제품 동기화됨

[!DNL Commerce] 카탈로그에서 동기화된 총 제품 수를 표시합니다. 초기 동기화 후에는 변경된 제품만 동기화해야 합니다.

## 다시 동기화 {#resync}

시간별 예약된 동기화가 발생하기 전에 카탈로그 재동기화를 시작해야 하는 경우 강제로 재동기화를 수행할 수 있습니다.

>[!NOTE]
>
> 재동기화를 강제로 수행하면 전체 제품 카탈로그가 재동기화되어 하드웨어 리소스에 대한 부하가 증가할 수 있습니다.

1. _카탈로그 동기화_ 대시보드에서 **설정**&#x200B;을 선택합니다.

   _카탈로그 동기화 설정_ 페이지가 나타납니다.

1. _데이터 다시 동기화_ 섹션에서 [!UICONTROL Resync]을(를) 클릭합니다.

   [!DNL Commerce]이(가) 다음에 예약된 동기화 기간 동안 카탈로그를 동기화합니다. 카탈로그 크기에 따라 이 작업은 시간이 오래 걸릴 수 있습니다.

## 동기화된 카탈로그 제품

**동기화된 카탈로그 제품** 테이블에는 다음 정보가 표시됩니다.

| 필드 | 설명 |
|---|---|
| ID | 제품에 대한 고유 식별자 |
| 이름 | 제품의 상점 이름 |
| 유형 | 단순, 구성 가능 또는 다운로드 가능 등 제품 유형 식별 |
| 마지막으로 내보냄 | 제품을 카탈로그에서 마지막으로 성공적으로 내보낸 날짜 |
| 마지막 수정일 | 카탈로그에서 제품이 마지막으로 수정된 날짜 |
| SKU | 제품에 대한 재고 유지 단위를 표시합니다. |
| 가격 | 제품 가격 |
| 가시성 | [!DNL Commerce] 카탈로그에 정의된 제품의 가시성 설정 |

## 카탈로그 동기화 문제 해결 {#resolvesync}

_SaaS 데이터 내보내기 안내서_&#x200B;에서 [로그 및 문제 해결](../data-export/troubleshooting-logging.md#troubleshooting)을 참조하십시오.
