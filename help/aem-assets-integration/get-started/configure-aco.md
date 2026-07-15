---
title: Commerce Optimizer용 AEM Assets 구성
description: ' [!DNL Adobe Commerce Optimizer]에 대한 AEM Assets 통합을 구성하는 방법을 알아봅니다.'
feature: CMS, Media, Configuration, Integration
source-git-commit: 0c2e50338cbf286704239b6d1f628180e85a3bef
workflow-type: tm+mt
source-wordcount: '1244'
ht-degree: 0%

---


# [!DNL Adobe Commerce Optimizer]에 대한 AEM Assets 구성

[!BADGE SaaS만]{type=Positive tooltip="Adobe Commerce Optimizer 프로젝트에만 적용됩니다."}

[!DNL Adobe Commerce Optimizer]용 AEM Assets 통합을 통해 판매자는 제품 이미지에 대한 중앙 집중식 디지털 에셋 관리 솔루션으로 AEM Assets을 사용할 수 있습니다. 이 안내서에서는 [!DNL Commerce Optimizer]과(와) 관련된 구성을 다룹니다.

다음 다이어그램은 [!DNL Adobe Commerce Optimizer]과(와) AEM Assets 통합 간의 제품 동기화에 대한 개요입니다.

![AEM Assets에서 [!DNL Commerce Optimizer] 흐름으로](../assets/aco-asset-sync-architecture.png){width="700"}

이 통합에는 두 개의 독립된 이벤트 흐름이 있습니다. 두 방법 모두 [Adobe I/O Events](https://developer.adobe.com/events/docs/)을(를) 사용하여 이벤트를 Assets 통합 서비스로 전송하지만 각 방향에서는 고유한 이벤트 공급자를 사용합니다.

* **AEM Assets에서 Assets 통합 서비스로**: 에셋이 승인, 거부 또는 제거되면 이벤트가 Assets 통합 서비스로 전달됩니다. 이 서비스는 `match-by-SKU`(메타데이터 기반) 또는 [사용자 지정 선택기(App Builder)](../synchronize/custom-match.md){target=_blank}를 사용하여 제품에 자산을 일치시킨 다음 `product-asset` 매핑을 [!DNL Commerce Optimizer]에 보내고, 여기서 제품 계층으로 저장됩니다.

  >[!NOTE]
  >
  >온보딩 중에 통합에서 사용하는 `AEM-Assets` 카탈로그 레이어가 자동으로 만들어집니다. 미리 만들 필요는 없습니다. 카탈로그 레이어의 작동 방식과 AEM-Assets 레이어의 동작 방식에 대한 배경은 [AEM-Assets 레이어](../../optimizer/setup/catalog-layer.md#aem-assets-layer)를 참조하십시오.

* **[!DNL Adobe Commerce Optimizer]에서 Assets 통합 서비스로**: [!DNL Commerce Optimizer]에서 제품을 업데이트하면 이벤트가 Assets 통합 서비스로 전달됩니다. 서비스가 일치하는 모든 자산 매핑을 다시 [!DNL Commerce Optimizer]&#x200B;(으)로 동기화합니다.

## 제한 사항

[!DNL Commerce Optimizer] 통합에는 다음과 같은 제한 사항이 있습니다.

### 레이어 관련 제한 사항

* AEM Assets 컨텐츠에 전용 레이어를 사용합니다.

  AEM Assets에서 전송된 페이로드는 Commerce Optimizer 카탈로그 계층을 채웁니다. 해당 레이어의 값은 필드가 제공되는 기본 카탈로그 속성을 덮어씁니다. 통합에서 페이로드의 필드를 생략하면 해당 레이어의 해당 값을 빈 값으로 덮어쓸 수 있습니다. 관련 없는 Commerce 워크플로우와 레이어를 공유하거나 AEM이 아닌 Assets 제품 데이터를 이미 저장하는 레이어를 다시 사용하면 **의도하지 않은 데이터 손실**&#x200B;이 발생하거나 덮어쓰기를 혼동할 수 있습니다. 주로 AEM 기반 제품 이미지 동기화를 위해 레이어 이름(예: 기본 **`AEM-Assets`**)을 예약합니다.

* 통합은 테넌트당 하나의 카탈로그 소스(단일 로케일과 하나의 명명된 레이어)를 지원합니다. 동일한 테넌트에 대해 여러 AEM-Assets 레이어 또는 여러 로케일을 구성하는 것은 현재 지원되지 않습니다.

* 기존 레이어를 다시 사용하거나 관련 없는 워크플로우와 레이어를 공유하는 것은 예방 가능한 지원 사례의 빈번한 원인입니다.

### 기타 제한 사항

* **이미지만**: 이 단계에서 통합은 비디오 또는 다른 미디어 형식을 지원하지 않습니다.
* **범주 이미지가 없습니다**: 범주 이미지 동기화를 사용할 수 없습니다. Assets 선택기(UI 삽입)에 대한 AEM Assets의 카테고리 이미지가 지원되지 않습니다.
* **다중 사이트 구분 없음**: 통합에서 다중 사이트를 처리하지 않습니다. 제품과 연결된 이미지가 모든 채널 및 정책에 동일하게 표시됩니다.
* **이미지 위치/순서 지정**: 이미지 위치와 순서 지정은 지원되지 않습니다.
* **제품이 있어야 함**: 제품이 [!DNL Commerce Optimizer]에 없는 경우 해당 제품-자산 매핑에 대한 레이어가 만들어지지 않습니다.

## 사전 요구 사항

통합을 구성하기 전에 다음을 확인합니다.

* **제품 시각화** 권한이 있는 활성 [!DNL Adobe Commerce Optimizer] 인스턴스(OpenAPI 기능 + [AEM Assets Prime](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-prime))나 Dynamic Media가 활성화된 고객 제공 AEM Assets 라이선스(예: **AEM Assets Ultimate**)입니다.
* AEM Assets as a Cloud Service 환경에 액세스합니다.
* [!DNL Commerce Optimizer]과(와) AEM Assets이 모두 동일한 Adobe IMS 조직에 있습니다.
* AEM Assets 환경에서 OpenAPI를 사용하는 Dynamic Media(활성화 단계는 [AEM Assets 프로젝트 구성](configure-aem.md#prerequisites) 참조).

### 먼저 AEM Assets 구성

통합을 지원하려면 [!DNL Commerce Optimizer]과(와) 함께 AEM Assets 통합을 온보딩하는 프로세스를 시작하기 전에 AEM Assets 프로젝트 및 환경을 구성하십시오. 여기에는 OpenAPI 기능을 통해 Dynamic Media 활성화 및 Commerce 메타데이터 스키마, 이벤트 및 UI를 AEM 프로젝트에서 사용할 수 있도록 하는 작업이 포함됩니다.

* [!BADGE 권장]{type=Positive} AEM 릴리스 `2026.5.26309` 이상에서는 코드 배포 없이 Cloud Manager에서 통합을 사용하도록 설정하십시오. [Commerce 통합 사용(셀프 서비스)](configure-aem.md#enable-aem-commerce-self-service)을 참조하세요.

* 이전 AEM 릴리스에서는 `assets-commerce` 패키지를 수동으로 배포합니다.
[자산 상거래 패키지를 수동으로 설치](configure-aem.md#install-the-assets-commerce-package-manually)를 따르십시오.

>[!TIP]
>
> 오른쪽 상단 메뉴에서 현재 AEM 버전을 확인할 수 있습니다. **[!UICONTROL Help]** > **[!UICONTROL About AEM]**.

## 온보딩

>[!IMPORTANT]
>
>[!DNL Commerce Optimizer]과의 통합을 사용하도록 설정하는 지원 티켓을 제출하기 전에 [AEM Assets 구성](#configure-aem-assets-first) 프로세스를 완료하십시오. 지원을 사용하려면 메타데이터 및 이벤트에 대한 `assets-commerce` 패키지(또는 이에 상응하는 셀프 서비스 패키지)의 배포를 포함하여 AEM Commerce 통합을 지원하도록 AEM Assets 환경 및 프로젝트를 구성해야 합니다. AEM이 구성되기 전에 티켓을 열면 온보딩이 지연될 수 있습니다.

[!DNL Commerce Optimizer]과(와) AEM Assets 통합을 온보딩하려면 Adobe 지원에서 Assets 통합 서비스에 Adobe Commerce Optimizer 인스턴스를 등록하고 구독해야 합니다.

* AEM Assets 이벤트(자산 승인, 업데이트, 제거됨)
* [!DNL Commerce Optimizer]개의 카탈로그 이벤트(제품 생성, 업데이트)

이 프로세스를 시작하려면 다음 정보가 포함된 [지원 티켓을 만드세요](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket).

* **[!DNL Adobe Commerce Optimizer]테넌트 ID**(인스턴스 ID)이(가) [!DNL Commerce Optimizer] URL 또는 Commerce Cloud Manager UI에 있습니다.
* [통합을 위해 AEM Assets을 구성](#configure-aem-assets-first)할 때 설정한 **AEM 프로그램 ID 및 환경 ID**.
* **일치 규칙**: SKU 또는 [외부 일치 항목(App Builder)](../synchronize/custom-match.md){target=_blank}별로 일치합니다.
* **계층**: 테넌트를 등록할 카탈로그 계층 이름입니다(**계층 관련 제약 조건** 참조). 의도적인 경우에만 사용자 지정 이름을 지정하십시오. 그렇지 않으면 기본값 **`AEM-Assets`**&#x200B;이(가) 사용됩니다.
* **로케일**: 테넌트를 등록할 카탈로그 원본 로케일(예: `en-US`)입니다. 이 로케일은 카탈로그 보기 및 제품 카탈로그 데이터에서 사용하는 로케일과 일치해야 합니다.

### 카탈로그 보기 구성

[!DNL Commerce Optimizer] 테넌트가 등록된 후 상점 및 API가 AEM 기반 이미지 데이터를 나타내도록 카탈로그 보기를 구성합니다.

* **카탈로그 원본(로케일)을 선택하십시오** — 지원 티켓에 지정한 것과 동일한 로케일을 선택하십시오(예: **`en-US`**). 통합은 테넌트당 하나의 로케일을 등록합니다. 불일치로 인해 동기화된 이미지가 의도한 카탈로그 보기에 표시되지 않습니다.
* **카탈로그 레이어 할당** — **`AEM-Assets`** 레이어(또는 티켓의 사용자 지정 레이어 이름)를 해당 카탈로그 보기에 할당합니다.

로케일 또는 레이어가 올바르게 할당되지 않으면 동기화가 업스트림에서 성공했더라도 이미지 데이터가 **표시되지 않거나** 예기치 않게 동작합니다.

## 동기화

구성이 완료되면 통합은 `product-asset` 매핑을 자동으로 동기화합니다.

자세한 내용은 [사용자 지정 자동 일치](../synchronize/custom-match.md)를 참조하십시오.

### SKU별 일치 워크플로우 예

새 제품에 기존 에셋을 추가할 때의 일반적인 흐름:

1. API 또는 데이터 수집을 통해 [!DNL Commerce Optimizer]에서 제품을 만듭니다. 처음에 이 제품은 이미지 없이 존재할 수 있습니다.

1. AEM Assets에서 제품에 매핑할 자산을 엽니다.

1. 제품 SKU를 **commerce:skus** 메타데이터에 추가하고 이미지 역할(예: `thumbnail`, `image`)을 할당합니다.

1. 게재할 자산을 승인합니다. 이렇게 하면 Assets 통합 서비스가 처리하는 이벤트가 트리거됩니다.

1. Assets 통합 서비스가 [!DNL Commerce Optimizer]&#x200B;(으)로 제품 이미지 매핑을 보냅니다. [!DNL Commerce Optimizer]의 제품이 자산의 이미지로 업데이트되었습니다.

1. 이미지가 표시되는지 확인합니다. 동기화가 완료될 때까지 몇 분 정도 기다린 다음 [!DNL Commerce Optimizer] UI에서 제품을 확인하거나 상점 API를 쿼리하여 이미지가 반환되었는지 확인합니다.

## 이미지 역할 처리

제품에 동일한 이미지 역할을 사용하는 여러 에셋이 있는 경우(예: `thumbnail` 역할을 가진 두 에셋) 통합에서는 하나의 에셋만 해당 역할을 유지하여 [!DNL Commerce Optimizer] 계층의 역할 중복 및 예기치 않은 상점 첫 번째 동작을 방지합니다.

**동작:** AEM Assets에서 업데이트를 보낼 때 가장 최근에 업데이트된 에셋이 이미지 역할(예: `thumbnail`)을 받고 해당 역할이 있는 이전 에셋에서 제거됩니다. 이렇게 하면 중복 이미지 역할이 상점 앞에 표시되지 않습니다.

## 다음과 같음

* [제품 시각화](../../optimizer/setup/product-visuals.md)
* [AEM Assets 프로젝트 구성](configure-aem.md)
* [사용자 지정 자동 일치](../synchronize/custom-match.md)
* [AEM Assets 통합 개요](../overview.md)
