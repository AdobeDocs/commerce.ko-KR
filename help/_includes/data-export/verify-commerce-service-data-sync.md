---
source-git-commit: e7d9c056ef8d565b4a143b05ff4e06d607fbfa8e
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 0%

---
# Commerce 서비스 데이터 동기화 확인

데이터 동기화가 작동하는지 확인하려면 [!DNL Adobe Commerce]에서 데이터를 내보내고 연결된 Commerce 서비스로 데이터를 성공적으로 배달했는지 확인하십시오. 배포에 대시보드를 사용하여 두 단계를 모두 확인합니다.

내보내기로 시작한 다음 게재를 확인합니다.

1. Commerce 관리자에서 동기화 상태를 확인합니다.

   **[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Feed Sync Status]**(으)로 이동합니다.

   ![피드 항목 상태를 보고하는 데이터 피드 동기화 상태 페이지](/help/data-export/assets/data-feed-sync-status.png){width="800" zoomable="yes"}

   동기화가 실행 중일 때 피드 데이터에 성공적으로 전송된 레코드가 표시됩니다. 세부 정보를 보거나 동기화 문제를 해결하려면 피드를 선택하십시오.

1. 데이터가 연결된 Commerce 서비스에 전달되었는지 확인합니다.

   Commerce 관리자에서 **[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Management Dashboard]**(으)로 이동합니다.

   ![연결된 Commerce 서비스의 동기화된 카탈로그 데이터를 표시하는 데이터 관리 대시보드](/help/data-export/assets/data-management-dashboard.png){width="700" zoomable="yes"}

   예상 제품, 가격 및 속성이 표시되는지 확인합니다.

>[!TIP]
>
>데이터 동기화에 추가 문제가 있는 경우 [로그 검토 및 문제 해결](/help/data-export/troubleshooting/logging.md)을 참조하세요.

