---
source-git-commit: a3ade1a31d3c2905b601f71bda118de89c43cf59
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%
---
# [!DNL Commerce Optimizer] 인스턴스 세부 정보 가져오기

[!DNL Commerce Optimizer] 인스턴스 [[!DNL Instance details] 페이지](/help/optimizer/get-started.md#manage-instances)의 _[!DNL Instance Id]_&#x200B;필드 또는 인스턴스에 액세스하는 데 사용된 URL에서_&#x200B;테넌트 ID _을(를) 가져옵니다. 예: `https://experience.adobe.com/#/@<your organization>/in:<tenant>/commerce-optimizer-studio/home`.

1. Commerce 관리자에서 **[!UICONTROL Adobe Commerce Optimizer]**&#x200B;을(를) 선택하여 지침이 포함된 구성 페이지를 표시합니다.

   ![[!DNL Commerce Optimizer] 구성 페이지](/help/aco-connector/assets/aco-connector-admin-installation.png){width="500" zoomable="yes"}

1. 명령줄에서 [SSH를 사용](https://experienceleague.adobe.com/ko/docs/commerce-on-cloud/user-guide/develop/secure-connections)하여 [!DNL Adobe Commerce] 스테이징 환경에 연결합니다.

1. 통합을 구성하려면 다음 [!DNL Adobe Commerce] CLI 명령을 실행하여 자리 표시자 값을 [!DNL Commerce Optimizer] 프로젝트의 값으로 바꿉니다.

   ```shell
   bin/magento aco:config:init --org_id=your-org --tenant_id=your-tenant --client_id=your-client-id --client_secret=your-secret
   ```

1. Commerce 관리자로 돌아가 [!UICONTROL Adobe Commerce Optimizer] 옵션을 선택하여 연결을 확인합니다.

   옵션을 선택하면 새 탭에서 [!DNL Commerce Optimizer] UI가 열립니다.
