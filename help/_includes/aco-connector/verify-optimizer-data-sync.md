---
source-git-commit: 3d05a7307e58ea2758ac4b6f2b70d24b8ea7a5ac
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---
# Optimizer 데이터 동기화 확인

Commerce 관리자에서 데이터를 내보냈는지, 데이터가 [!DNL Commerce Optimizer]에 전달되었는지 확인합니다. Commerce 관리에서 내보내기로 시작한 다음 [!DNL Commerce Optimizer]에서 배달을 확인합니다.

1. **Commerce 관리자의 동기화 상태 확인:**

   **[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Feed Sync Status]**(으)로 이동합니다.

   ![피드 항목 상태를 보고하는 데이터 피드 동기화 상태 페이지](/help/aco-connector/assets/data-feed-sync-status.png){width="700" zoomable="yes"}

   동기화가 실행 중일 때 피드 데이터에 성공적으로 전송된 레코드가 표시됩니다. 세부 정보를 보거나 동기화 문제를 해결하려면 피드를 선택하십시오.

1. **확인 데이터가 [!DNL Commerce Optimizer]:**(으)로 전달되었습니다.

   [!DNL Commerce Optimizer] 메뉴에서 **[!UICONTROL Data Sync]**&#x200B;을(를) 선택합니다.

   ![동기화된 카탈로그 데이터를 표시하는 Adobe Commerce Optimizer의 데이터 동기화 페이지](/help/aco-connector/assets/data-sync.png){width="700" zoomable="yes"}

   예상 제품, 가격 및 속성이 표시되는지 확인합니다.

동기화가 예상대로 작동하는 경우:

- **[!UICONTROL Data Feed Sync Status]**&#x200B;은(는) 해결되지 않은 항목 수준 오류가 없는 커넥터 피드에 대해 성공적으로 전송된 레코드를 표시합니다.
- [!DNL Commerce Optimizer]의 **[!UICONTROL Data Sync]**&#x200B;은(는) 필요한 카탈로그 원본, 제품, 가격 및 특성을 나열합니다.

>[!TIP]
>
>데이터 동기화에 문제가 있는 경우 [문제 해결](/help/aco-connector/troubleshooting.md) 안내서를 참조하십시오.
