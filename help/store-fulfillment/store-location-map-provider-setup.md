---
title: 저장 위치 및 매핑 시스템 구성
description: 상점 UI에서 저장소 위치 매핑을 지원하도록 거리 공급자를 구성합니다. 스토어 이행 솔루션은 소매 스토어 검색 및 전체 이행 워크플로우를 위한 기타 매핑 및 스케줄링 기능을 사용할 수 있도록 거리 공급 업체를 필요로 합니다.
role: Admin
level: Intermediate
feature: Shipping/Delivery, Integration, Tools and External Services, Configuration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# 저장소 위치 및 매핑 설정

소매 저장소 위치를 검색하도록 [거리 공급자](https://experienceleague.adobe.com/ko/docs/commerce-admin/inventory/configuration/distance-priority-algorithm)를 구성하여 저장소 이행 시 저장소 위치 및 매핑 기능을 사용하도록 설정하십시오.

**요구 사항**

구성 프로세스 중에 Google 맵 플랫폼에 Google API 키를 제공합니다. 항목이 없으면 [Google 지도 플랫폼에서 항목을 생성](https://experienceleague.adobe.com/ko/docs/commerce-admin/inventory/configuration/distance-priority-algorithm#configure-google-maps)합니다.

거리 공급자를 구성하려면:

1. 관리자의 **[!UICONTROL Stores > General]** 구성에서 맵 콘텐츠 형식에 대한 Google 맵 통합을 추가합니다.

   - **[!UICONTROL Stores > Configuration  > General > Content Management]**(으)로 이동합니다.

   - **[!UICONTROL Google Maps API Key]** 필드에 Google API 키를 추가합니다.

1. 관리자의 **[!UICONTROL Stores > Inventory]** 구성에서 스토어 이행 거리 공급자를 선택합니다.

   - **[!UICONTROL Stores > Configuration > Catalog > Inventory]**(으)로 이동합니다.

   - **[!UICONTROL Distance Provider for Distance Based SSA]** 섹션을 확장합니다.

   - **공급자**&#x200B;를 **Google 맵**(으)로 설정합니다.

1. **[!UICONTROL Google Distance Provider]**&#x200B;에 대한 설정을 구성합니다.

   - **Google API 키**&#x200B;를 추가합니다.

   - **[!UICONTROL Computation Mode]**&#x200B;을(를) `Driving`(으)로, **[!UICONTROL Value]**&#x200B;을(를) `Distance`(으)로 설정
