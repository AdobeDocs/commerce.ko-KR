---
title: 판매점 구성
description: 향상된 Inventory management 소스를 판매점으로 설정합니다.
role: Admin
level: Experienced
feature: Shipping/Delivery, Inventory, Configuration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '1227'
ht-degree: 0%

---

# 가맹점(Source) 구성

이 솔루션은 판매자를 위한 운영 중심 기능으로 재고 소스를 확장하여 기본 Inventory management 기능을 강화합니다.

- 스토어 위치에 대한 지리적 좌표 추가
- 원본을 [!DNL Store Pickup Location]&#x200B;(으)로 지정하고 사용 가능한 배송 기능(배달 대상 저장소, 배달 대상 저장소)을 지정하십시오.
- 사용 가능한 픽업 옵션(매장 또는 커브사이드), 사용자 정의된 픽업 지침 및 기타 정보를 지정하여 고객에게 픽업 세부 정보 및 지침을 전달합니다

_소스_ 및 _가맹점 위치_&#x200B;라는 용어가 서로 교환하여 사용됩니다. 모든 레코드는 재고 출처이지만 구성 설정에 따라 출처가 가맹점 위치일 수도 있습니다.

관리자의 가맹점 구성 관리: **[!UICONTROL Stores > Inventory > Sources >  Edit Source]**.

>[!NOTE]
>
>설정 프로세스 중에 소스를 생성하거나 기존 소스를 업데이트한 후 캐시를 플러시해야 할 수 있습니다.

## **일반**

<table>
<tbody>
<tr>
<th>필드</th>
<th>설명</th>
<th>범위</th>
<th>필수</th>
</tr>
<tr>
<td><strong>[!UICONTROL Latitude]</strong></br><code>Base Attribute: latitude</code></td>
<td>가맹점 위치의 위도 좌표. 이 필수 정보는 상점 앞의 위치 검색 및 맵 배치에 사용됩니다. 유효성 검사를 통과하려면 값이 저장소의 정확한 주소와 일치해야 합니다.</td>
<td>글로벌</td>
<td>예</td>
</tr>
<tr>
<td><strong>[!UICONTROL Longitude]</strong></br><code>Base Attribute: Longitude</code></td>
<td>가맹점 위치의 세로 좌표. 이 필수 정보는 상점 앞의 위치 검색 및 맵 배치에 사용됩니다. 유효성 검사를 통과하려면 값이 저장소의 정확한 주소와 일치해야 합니다.</td>
<td>글로벌</td>
<td>예</td>
</tr>
<tr>
<td><strong>[!UICONTROL Use as Pickup Location]</br></strong><code>Base Attribute: is_pickup_location_active</code></td>
<td>소스를 사용 가능한 스토어 픽업 위치로 지정합니다. 이 설정은 소스가 동기화되어 방문자에게 표시되는지 여부를 결정합니다.</td>
<td>글로벌</td>
<td>아니요</td>
</tr>
<tr>
<td><strong>[!UICONTROL Enable Ship to Store]</strong><br><code>Extension Attribute: allow_ship_to_store</code></td>
<td>소스 수준에서 납품처 저장 기능을 구성합니다. 자세한 내용은 [일반 구성](enable-general.md) 옵션 <strong>[!UICONTROL Enable Ship To Store]을(를) 참조하십시오
</tr>
<tr>
<td><strong>[!UICONTROL Latitude]</strong></br><code>Base Attribute: latitude</code></td>
<td>가맹점 위치의 위도 좌표. 이 필수 정보는 상점 앞의 위치 검색 및 맵 배치에 사용됩니다. 유효성 검사를 통과하려면 값이 저장소의 정확한 주소와 일치해야 합니다.</td>
<td>글로벌</td>
<td>예</td>
</tr>
<tr>
<td><strong>[!UICONTROL Longitude]</strong></br><code>Base Attribute: Longitude</code></td>
<td>가맹점 위치의 세로 좌표. 이 필수 정보는 상점 앞의 위치 검색 및 맵 배치에 사용됩니다. 유효성 검사를 통과하려면 값이 저장소의 정확한 주소와 일치해야 합니다.</td>
<td>글로벌</td>
<td>예</td>
</tr>
<tr>
<td><strong>[!UICONTROL Use as Pickup Location]</br></strong><code>Base Attribute: is_pickup_location_active</code></td>
<td>소스를 사용 가능한 스토어 픽업 위치로 지정합니다. 이 설정은 소스가 동기화되어 방문자에게 표시되는지 여부를 결정합니다.</td>
<td>글로벌</td>
<td>아니요</td>
</tr>
<tr>
<td><strong>[!UICONTROL Enable Ship to Store]</strong></br> <code>Extension Attribute: [!DNL allow_ship_to_store]</code></td>
<td>소스 수준에서 납품처 저장 기능을 구성합니다. 자세한 내용은 [일반 구성](enable-general.md) 옵션 <strong>[!UICONTROL Enable Ship To Store]</strong>을(를) 참조하십시오.</td>
<td>글로벌</td>
<td>아니요</td>
</tr>
<tr>
<td><strong>[!UICONTROL Enable Ship From Store]</strong></br><code>Extension Attribute: [!DNL use_as_shipping_source]</code></td>
 <td>소스 수준에서 출고처(Ship-from-Store) 기능을 구성합니다. 자세한 내용은 [일반 구성](enable-general.md) 옵션 [!UICONTROL Enable Ship From Store]을(를) 참조하십시오.</td>
<td>글로벌</td>
<td>아니요</td>
</tr>
<tr>
<td>글로벌</td>
<td>아니요</td>
</tr>
<tr>
<td><strong>[!UICONTROL Enable Ship From Store]</strong><code></br><code>Extension Attribute: [!DNL use_as_shipping_source]</code></td>
<td>소스 수준에서 출고처(Ship-from-Store) 기능을 구성합니다. 자세한 내용은 [일반 구성](enable-general.md) 옵션 [!UICONTROL Enable Ship From Store]을(를) 참조하십시오.</td>
<td>글로벌</td>
<td>아니요</td>
</tr>
</tbody>
</table>



| **필드** | **설명** | **범위** | **필수** |
|--------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|--------------|
| **[!UICONTROL Latitude]**</br>`Base Attribute: latitude` | 가맹점 위치의 위도 좌표. 이 필수 정보는 상점 앞의 위치 검색 및 맵 배치에 사용됩니다. 유효성 검사를 통과하려면 값이 저장소의 정확한 주소와 일치해야 합니다. | 글로벌 | 예 |
| **[!UICONTROL Longitude]**</br>`Base Attribute: Longitude` | 가맹점 위치의 세로 좌표. 이 필수 정보는 상점 앞의 위치 검색 및 맵 배치에 사용됩니다. 유효성 검사를 통과하려면 값이 저장소의 정확한 주소와 일치해야 합니다. | 글로벌 | 예 |
| **[!UICONTROL Use as Pickup Location]**</br>`Base Attribute:[!DNL is_pickup_location_active]` | 소스를 사용 가능한 스토어 픽업 위치로 지정합니다. 이 설정은 소스가 동기화되어 방문자에게 표시되는지 여부를 결정합니다. | 글로벌 | 아니요 |
| **[!UICONTROL Enable Ship to Store]**</br>`Extension Attribute: [!DNL allow_ship_to_store]` | 소스 수준에서 납품처 저장 기능을 구성합니다. 자세한 내용은 [일반 구성](enable-general.md) 옵션 **[!UICONTROL Enable Ship To Store]**&#x200B;을(를) 참조하십시오. | 글로벌 | 아니요 |
| **[!UICONTROL Enable Ship From Store]**</br>`Extension Attribute: [!DNL use_as_shipping_source]` | 소스 수준에서 출고처(Ship-from-Store) 기능을 구성합니다. 자세한 내용은 [일반 구성](enable-general.md) 옵션 [!UICONTROL Enable Ship From Store]을(를) 참조하십시오. | 글로벌 | 아니요 |

{style="table-layout:auto"}

## 픽업 위치 구성

| **필드** | **설명** | **범위** | **필수** |
|-----------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|--------------|
| **[!UICONTROL Allow In-Store Pickup]**</br>`Extension Attribute: [!DNL store_pickup_enabled]` | 두 가지 픽업 옵션 중 하나. [!DNL In-Store Pickup]은(는) 고객이 주문을 검색하기 위해 가맹점 위치를 입력할 수 있는 기능을 의미합니다. </br></br>이 옵션을 활성화하면 체크아웃 중에 이 옵션이 고객에게 제공될 수 있습니다. </br></br>이 옵션은 또한 [!UICONTROL In-store Pickup]에 대해 [!UICONTROL Delivery Method]에 구성된 [!UICONTROL Enable In-store Pickup]&#x200B;(으)로 전역 구성을 재정의합니다. | 글로벌 | 아니요 |
| **매장 내 픽업 지침**</br>`Extension Attribute: store_pickup_instructions` | **스토어에서 주문 준비 완료** 전자 메일 알림을 통해 고객에게 사용자 지정 가능한 메시지가 전달되었습니다. | 글로벌 | 아니요 |
| **커브사이드 허용**</br>`Extension Attribute: curbside_enabled` | 두 가지 픽업 옵션 중 하나. 커브사이드 배송은 고객이 가맹점 위치의 지정된 장소에 차량을 주차할 수 있다. 이 시나리오에서 주문은 스토어 제휴자가 고객에게 전달합니다. </br></br>이 옵션을 활성화하면 체크아웃 중에 이 옵션이 고객에게 제공될 수 있습니다. 또한, 체크인 과정에서 고객이 자신의 차량과 주차 장소를 설명하도록 요청할 수 있습니다. </br></br>이 옵션은 또한 **매장 내 픽업**&#x200B;에 대해 **게재 메서드**&#x200B;에 구성된 **커브사이드 픽업 사용**&#x200B;에 전역 구성을 재정의합니다 | 글로벌 | 아니요 |
| **[!UICONTROL Curbside Instructions]**</br>`Extension Attribute: curbside_instructions` | [!UICONTROL Order Ready For Pickup in Store] 전자 메일 알림에서 고객에게 사용자 지정 가능한 메시지를 전달합니다. | 글로벌 | 아니요 |
| **[!UICONTROL Estimated Pickup Lead Time]**</br>`Extension Attribute: pickup_lead_time` | 주문을 받고 선택하고 가져올 준비가 되기까지의 시간(분). </br></br>이 정보는 웹 사이트의 고객에 대한 주문 픽업의 예상 시간을 표시하는 데 사용됩니다.</br></br> 이 옵션을 설정하면 **매장 내 픽업** 구성에서 **배달 메서드**&#x200B;에 대해 구성된 **예상 픽업 리드 타임**&#x200B;에 대한 전역 구성이 재정의됩니다. | 글로벌 | 아니요 |
| **[!UICONTROL Estimated Pickup Time Label]**</br>`Extension Attribute: pickup_time_label` | 주문을 받을 준비가 될 때까지의 시간(분)을 표시하는 레이블입니다.</br></br> 이 레이블을 사용자 지정할 때 %1 코드를 사용하여 **예상 픽업 리드 타임**&#x200B;을 삽입할 수 있습니다.</br></br> 이 옵션을 설정하면 [!UICONTROL In-store Pickup]의 [!UICONTROL Delivery Method]에 대해 구성된 [!UICONTROL Estimated Pickup Time Label]에 대한 전역 구성이 재정의됩니다. | 글로벌 | 아니요 |

### **운영 시간**

| **필드** | **설명** | **범위** | **필수** |
|------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|--------------|
| **[!UICONTROL Location Timezone]**</br>`Extension Attribute: timezone` | 가맹점 위치의 시간대. 매일 시작 및 종료 시간을 설정합니다.</br></br>이러한 설정은 예상 픽업 시간을 최적화하고 이행 서비스 보고를 수행하는 데 사용됩니다. | 글로벌 | 예 |
| **[!UICONTROL Opening Hours]**</br>`Internal Attribute: inventory_source_opening_hours_dynamic_rows` | 가맹점 위치의 운영 시간. </br></br>이 정보를 사용하여 예상 픽업 시간을 최적화하고 이행 서비스 보고를 수행할 수 있습니다. | 글로벌 | 예 |

### 체크인 경험 인터페이스 옵션 구성



| **필드** | **설명** | **범위** | **필수** |
|---------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|--------------|
| **[!UICONTROL Use Parking Spots]**</br>`Extension Attribute: parking_spots_enabled` | 가맹점 위치에 측면 픽업용 지정 주차 공간이 있는지 여부를 지정합니다. </br></br>사용 가능한 주차 공간을 구성할 수 있습니다. | 글로벌 | 아니요 |
| **[!UICONTROL Is Parking Spot a Mandatory Field?]**</br>`Extension Attribute: parking_spot_mandatory` | 쇼핑 경험 중에 고객에게 주차 장소 식별이 필요한지 여부를 지정합니다.</br></br>활성화하면 도착 시 주차 장소를 지정하라는 메시지가 표시됩니다. 비활성화된 경우 고객은 이 입력을 건너뛸 수 있습니다. | 글로벌 | 아니요 |
| **[!UICONTROL Parking Spots List]**</br> `Internal Attribute: inventory_source_parking_spot_dynamic_rows` | 이 상점의 위치에서 이용 가능한 주차 공간은 커브사이드 픽업을위한. 제공된 인터페이스를 사용하여 각 지점의 이름을 지정합니다.</br></br> 모든 주차 공간의 이름을 지정할 필요는 없으며, 길가에 지정된 위치만 지정할 수 있습니다. 예를 들어, A-G행의 주차가 가능할 수 있지만, A 행의 처음 8개 지점만 측면 픽업으로 지정됩니다. 이 시나리오에서는 A1, A2, A3 등 8개의 지점을 정의할 수 있습니다. | 글로벌 | 아니요 |
| **[!UICONTROL Allow "Other" Parking Spot Field]**</br>`Extension Attribute: custom_parking_spot_enabled` | 이 설정을 사용하면 체크인 중에 고객이 주차 공간을 설명할 수 있습니다. | 글로벌 | 아니요 |
| **[!UICONTROL Use Car Color]**</br>`Extension Attribute: use_car_color` | 체크인 시 고객의 차량 색상 수집을 지원할지 여부를 지정합니다. </br></br> [!UICONTROL Car Color]에 대해 사용 가능한 선택 항목이 체크 인 환경의 관리 [시스템 설정](check-in-experience-setup.md)에 구성되어 있습니다. | 글로벌 | 아니요 |
| **[!UICONTROL Is Car Color a Mandatory Field?]**</br>`Extension Attribute: car_color_mandatory` | 체크인 시 고객에 대해 차량 색상 식별이 필요한지 여부를 지정합니다.</br></br>활성화된 경우 도착 시 차량 색상을 지정하라는 메시지가 표시됩니다. 비활성화된 경우 고객은 이 입력을 건너뛸 수 있습니다. | 글로벌 | 아니요 |
| **[!UICONTROL Use Car Make]** </br>`Extension Attribute: use_car_make` | 체크인 시 고객으로부터 차량 제조물 수거 지원 여부를 지정합니다.</br></br> [!UICONTROL Car Make]에 대해 사용 가능한 선택 항목이 체크 인 환경의 관리 [시스템 설정](check-in-experience-setup.md)에 구성되어 있습니다. | 글로벌 | 아니요 |
| **[!UICONTROL Is Car Make a Mandatory Field?]**</br>`Extension Attribute: car_make_mandatory` | 체크인 시 고객에 대해 차량 ID가 필요한지 여부를 지정합니다.</br></br>활성화된 경우 도착 시 차량 제조사를 지정하라는 메시지가 표시됩니다. 비활성화된 경우 고객은 이 입력을 건너뛸 수 있습니다. | 글로벌 | 아니요 |
| **[!UICONTROL Use Additional Information]**</br> `Extension Attribute: use_additional_information` | 체크인 시 고객의 추가 정보 수집을 지원할지 여부를 지정합니다. | 글로벌 | 아니요 |
| **[!UICONTROL Is Additional Information a Mandatory Field?]**</br>`Extension Attribute: additional_information_mandatory` | 체크인 시 고객에 대해 추가 정보가 필요한지 여부를 지정합니다. </br></br>활성화된 경우 도착 시 추가 정보를 입력하라는 메시지가 표시됩니다. 비활성화된 경우 고객은 이 입력을 건너뛸 수 있습니다. | 글로벌 | 아니요 |
