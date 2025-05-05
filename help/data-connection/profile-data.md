---
title: Commerce 데이터 수집을 위한 프로필 레코드 스키마 업데이트
description: 스키마, 데이터 세트 및 데이터스트림을 만들어 Commerce 프로필 레코드 데이터를 수집하고 Experience Platform으로 전송하는 방법에 대해 알아봅니다.
role: Admin, Developer
feature: Personalization, Integration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 0%

---

# Commerce 데이터 수집을 위한 프로필 레코드 스키마 업데이트

쇼핑객이 Commerce 사이트에서 프로필을 만들면 프로필 레코드가 생성되고 데이터가 캡처됩니다. 해당 프로필 데이터를 Experience Platform에 스트리밍하려면 먼저 해당 프로필 레코드와 관련된 스키마 및 데이터 세트를 만들어야 합니다.

1. [스키마를 만들고](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/ui/resources/schemas) 클래스를 **개인 프로필**(으)로 설정합니다.

1. 다음 프로필별 필드 그룹을 [추가](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/ui/resources/schemas)합니다.

   - identityMap
   - 인구 통계 세부 정보
   - 개인 연락처 세부 정보
   - 사용자 계정 세부 정보

1. 프로필에 대한 스키마를 [사용](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/ui/resources/schemas)합니다.

   프로필에 대해 스키마를 활성화하면 이 스키마에서 만든 모든 데이터 세트가 Real-Time CDP에 참여하며, 이 데이터 세트는 개별 소스의 데이터를 병합하여 각 고객에 대한 전체 보기를 구성합니다.

1. 만들거나 업데이트한 스키마를 기반으로 [데이터 집합을 만듭니다](https://experienceleague.adobe.com/ko/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform).

   데이터 집합은 데이터 수집을 위한 저장 및 관리 구성으로서, 일반적으로 스키마(열) 및 필드(행)를 포함하는 테이블입니다. 데이터 세트에는 저장하는 데이터의 다양한 측면을 설명하는 메타데이터도 포함됩니다.

1. 다음 값으로 Experience Platform에 [사용자 지정 이름 공간](https://experienceleague.adobe.com/ko/docs/experience-platform/identity/features/namespaces#create-namespaces)을 만듭니다.

   - **표시 이름**: _Commerce 고객 ID_
   - **ID 기호**: _CustomerId_
   - **유형**: _개별 교차 장치 ID_

   ![사용자 지정 네임스페이스 만들기](assets/custom-namespace.png){width="700" zoomable="yes"}

   **[!UICONTROL Create]**&#x200B;을(를) 클릭합니다. 사용자 지정 네임스페이스는 통합 프로필 서비스에서 프로필 조각을 함께 결합하는 데 사용됩니다.

고객 프로필 레코드 데이터에 대해 스키마, 데이터 세트 및 사용자 지정 이름 공간을 구성하면 해당 데이터를 수집하여 Experience Platform으로 보내도록 Commerce 인스턴스를 [구성](connect-data.md#data-collection)할 수 있습니다.

동작 및 백 오피스 이벤트 데이터에 대한 스키마, 데이터 세트 및 데이터 스트림을 만들려면 [Commerce 데이터 수집을 위한 시계열 이벤트 스키마 업데이트](update-xdm.md)를 참조하십시오.
