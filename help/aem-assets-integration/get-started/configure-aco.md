---
title: Commerce Optimizer용 AEM Assets 구성
description: ' [!DNL Adobe Commerce Optimizer]에 대한 AEM Assets 통합을 구성하는 방법을 알아봅니다.'
feature: CMS, Media, Configuration, Integration
source-git-commit: 2cc7b70a6923687c74fe3f4b88448eaada6d16af
workflow-type: tm+mt
source-wordcount: '1453'
ht-degree: 0%

---


# [!DNL Adobe Commerce Optimizer]에 대한 AEM Assets 구성

[!BADGE SaaS만]{type=Positive tooltip="Adobe Commerce Optimizer 프로젝트에만 적용됩니다."}

[!DNL Adobe Commerce Optimizer]용 AEM Assets 통합을 통해 판매자는 제품 이미지에 대한 중앙 집중식 디지털 에셋 관리 솔루션으로 AEM Assets을 사용할 수 있습니다. 이 안내서에서는 [!DNL Commerce Optimizer]과(와) 관련된 구성을 다룹니다.

Adobe Commerce(PaaS) 또는 [!DNL Adobe Commerce as a Cloud Service]과(와) 달리 [!DNL Commerce Optimizer]에는 관리자 구성 UI가 없습니다. 통합을 사용하려면 [!DNL Adobe Commerce Optimizer] 및 AEM Assets 세부 정보로 지원 티켓을 만드십시오. Adobe 지원은 통합을 구성하고 테넌트를 Assets 통합 서비스에 등록합니다.

**티켓을 제출하기 전에 AEM Assets을 준비합니다.** 테넌트 등록은 AEM 측을 Commerce에 사용할 수 있다고 가정합니다. 예를 들어, 메타데이터 및 이벤트가 설명된 대로 작동하도록 AEM Commerce `assets-commerce` 패키지를 배포한 후 **AEM이 구성되기 전에 티켓을 열면 온보딩이 지연될 수 있습니다.**

다음 다이어그램은 [!DNL Adobe Commerce Optimizer]과(와) AEM Assets 통합 간의 제품 동기화에 대한 개요입니다.

![AEM Assets에서 [!DNL Commerce Optimizer] 흐름으로](../assets/aco-asset-sync-architecture.png){width="700"}

이 통합에는 다음과 같은 두 가지 기본 흐름이 있습니다.

* **AEM Assets에서**: 에셋이 승인, 거부 또는 제거되면 이벤트가 Adobe 파이프라인을 통해 Assets 통합 서비스로 흐릅니다. 이 서비스는 `match-by-SKU`(메타데이터 기반) 또는 [사용자 지정 선택기(App Builder)](../synchronize/custom-match.md){target=_blank}를 사용하여 제품에 자산을 일치시킨 다음 `product-asset` 매핑을 Commerce Optimizer에 보내 제품 계층으로 저장합니다.

* **시작[!DNL Adobe Commerce Optimizer]**: [!DNL Commerce Optimizer]에서 제품을 업데이트하면 이벤트가 Adobe 파이프라인을 통해 Assets 통합 서비스로 이동합니다. 서비스가 일치하는 모든 자산 매핑을 다시 [!DNL Adobe Commerce Optimizer]&#x200B;(으)로 동기화합니다.

## 사전 요구 사항

통합을 구성하기 전에 다음을 확인합니다.

* 제품 시각화 권한이 있는 활성 [!DNL Adobe Commerce Optimizer] 인스턴스 또는 Dynamic Media가 있는 모든 AEM Assets 라이선스.
* AEM Assets as a Cloud Service 환경에 액세스합니다.
* [!DNL Commerce Optimizer]과(와) AEM Assets이 모두 동일한 Adobe IMS 조직에 있습니다.
* AEM Assets 환경에서 OpenAPI를 사용하는 Dynamic Media(활성화 단계는 [AEM Assets 프로젝트 구성](configure-aem.md#prerequisites) 참조).

## 먼저 AEM Assets 구성

테넌트 등록을 위해 [지원 티켓을 열기](#onboarding)하는 동안 **이전**&#x200B;의 AEM Assets 단계를 완료합니다. 설치 패턴은 Adobe Commerce as a Cloud Service과 일치합니다. [Commerce 메타데이터를 지원하도록 AEM Assets 프로젝트 구성](configure-aem.md)을 참조하십시오.

### 1단계: AEM Commerce 패키지 배포

Commerce 메타데이터 스키마, 이벤트 및 UI를 사용할 수 있도록 AEM 프로젝트에 `assets-commerce` 패키지를 설치하고 배포합니다.

[패키지 `assets-commerce`설치](configure-aem.md#step-1-install-the-assets-commerce-package)에서 전체 절차를 완료합니다. 지원 티켓을 열기 전에 다음 단계를 따르십시오.

1. Cloud Manager Git 저장소를 복제하고 [AEM Assets Commerce 저장소](https://github.com/ankumalh/assets-commerce) 코드를 프로젝트에 복사합니다.

1. 프로젝트의 모든 `filter.xml` 및 `pom.xml` 파일에서 모든 &lt;my-app>을 사용자의 앱 이름으로 바꾸십시오.

1. 배포 파이프라인을 커밋, 푸시, 실행하고 자산 속성에 **[!UICONTROL Commerce]** 탭이 표시되는지 확인합니다.

**[!UICONTROL Commerce]** 탭이 누락된 경우 Cloud Manager 스크린샷, 파이프라인 단계 및 문제 해결을 위해 [패키지 설치](configure-aem.md#step-1-install-the-assets-commerce-package)를 참조하십시오.`assets-commerce`

### 2단계: OpenAPI를 사용하여 Dynamic Media 활성화

AEM Assets 환경에서 OpenAPI 기능을 사용하는 Dynamic Media를 활성화해야 합니다. 셀프서비스 경로(예: 제품 비주얼을 위한 Cloud Manager) 및 Adobe 지원 경로는 [AEM Assets 프로젝트 구성](configure-aem.md#prerequisites)에 설명되어 있습니다.

### 3단계: Commerce 메타데이터 적용 및 에셋 승인

Commerce 메타데이터를 AEM Assets의 제품 이미지에 추가합니다. 필드 정의는 [AEM Commerce 패키지 내용](configure-aem.md#aem-commerce-assets-commerce-package-contents)을 참조하십시오.

데이터 동기화를 트리거하려면 자산이 **승인됨** 상태여야 합니다. 메타데이터만 저장해도 이벤트가 트리거되지 않습니다.

### 4단계: 선택 사항 - Commerce 메타데이터 프로필 구성

AEM 메타데이터 프로필을 사용하여 작성을 간소화하는 경우 패키지가 배포된 후 **후**&#x200B;에 구성하면 팀이 필수 Commerce 필드를 이해합니다. 이는 **AEM Assets 프로젝트 구성**&#x200B;과(와) 동일한 선택적 패턴입니다.

[메타데이터 프로필 구성](configure-aem.md#step-2-optional-configure-a-metadata-profile)을 참조하십시오.

## 제한 사항

[!DNL Commerce Optimizer] 통합에는 다음과 같은 제한 사항이 있습니다.

### 레이어 관련 제한 사항

이 섹션 **이전**&#x200B;을(를) 읽고 지원 티켓에서 카탈로그 계층 이름을 선택하십시오. 이 컨텍스트 없이 레이어를 선택하거나 공유하면 예방 가능한 지원 사례가 자주 발생합니다.

**AEM Assets 컨텐츠에 전용 레이어를 사용합니다.** AEM Assets에서 보낸 페이로드는 Commerce Optimizer 카탈로그 **레이어**&#x200B;를 채웁니다. 해당 레이어의 값은 필드가 제공되는 기본 카탈로그 특성을 **덮어씁니다**. 통합이 페이로드의 필드를 생략하면 해당 레이어의 해당 값을 빈 값으로 덮어쓸 수 있습니다. 관련 없는 Commerce 워크플로우와 레이어를 공유하거나 AEM이 아닌 Assets 제품 데이터를 이미 저장하는 레이어를 다시 사용하면 **의도하지 않은 데이터 손실**&#x200B;이 발생하거나 덮어쓰기를 혼동할 수 있습니다. 지원 티켓을 열기 전에 **먼저** 계층 선택을 계획하고 주로 AEM 기반 제품 이미지 동기화를 위해 해당 계층 이름(예: 기본 **`AEM-Assets`**)을 예약하십시오.

>[!IMPORTANT]
>
>통합은 테넌트당 **1개의 카탈로그 원본**(단일 로케일 및 **1개의 명명된 레이어**)을 지원합니다. 동일한 테넌트에 대해 여러 AEM-Assets 레이어 또는 여러 로케일을 구성하는 것은 현재 지원되지 않습니다.

### 기타 제한 사항

* **이미지만**: 이 단계에서 통합은 비디오 또는 다른 미디어 형식을 지원하지 않습니다.
* **범주 이미지가 없습니다**: 범주 이미지 동기화를 사용할 수 없습니다. Assets 선택기(UI 삽입)에 대한 AEM Assets의 카테고리 이미지가 지원되지 않습니다.
* **다중 사이트 구분 없음**: 통합에서 다중 사이트를 처리하지 않습니다. 제품과 연결된 이미지가 모든 채널 및 정책에 동일하게 표시됩니다.
* **이미지 위치/순서 지정**: 이미지 위치와 순서 지정은 지원되지 않습니다.
* **제품이 있어야 함**: 제품이 [!DNL Commerce Optimizer]에 없는 경우 해당 제품-자산 매핑에 대한 레이어가 만들어지지 않습니다.

## 온보딩

[!DNL Commerce Optimizer]과(와) AEM Assets 통합을 온보딩하려면 [지원 티켓을 만들기](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket)해야 합니다.

Adobe 지원에서는 티켓의 정보를 사용하여 테넌트를 Assets 통합 서비스에 등록하고 통합을 구성합니다.

티켓을 제출하기 전에 [먼저 AEM Assets 구성](#configure-aem-assets-first)을 완료했는지 확인하십시오.

지원 티켓에 다음 정보를 포함하십시오.

* **[!DNL Adobe Commerce Optimizer]테넌트 ID**(인스턴스 ID)이(가) [!DNL Commerce Optimizer] URL 또는 Commerce Cloud Manager UI에 있습니다.
* **AEM 프로그램 ID**.
* **AEM 환경 ID**.
* **일치 규칙**: SKU 또는 [외부 일치 항목(App Builder)](../synchronize/custom-match.md){target=_blank}별로 일치합니다.
* **계층**: 테넌트를 등록할 카탈로그 계층 이름입니다(**계층 관련 제약 조건** 참조). 의도적인 경우에만 사용자 지정 이름을 지정하십시오. 그렇지 않으면 기본값 **`AEM-Assets`**&#x200B;이(가) 사용됩니다.
* **로케일**: 테넌트를 등록할 카탈로그 원본 로케일(예: `en-US`)입니다. 이 로케일은 카탈로그 보기 및 제품 카탈로그 데이터에서 사용하는 로케일과 일치해야 합니다.

Adobe 지원에서 티켓을 처리하면 통합이 구성되고 테넌트가 Assets 통합 서비스에 등록됩니다.

온보딩이 완료되면:

1. **Assets Integration Service에 등록**: [!DNL Commerce Optimizer] 테넌트가 티켓에 제공된 [!DNL Adobe Commerce Optimizer] 테넌트 ID, AEM 프로그램 ID, AEM 환경 ID, 일치하는 규칙, 로케일 및 레이어 이름을 사용하여 Assets Integration Service에 등록됩니다.

1. **이벤트 구독**: Assets Integration Service는 다음을 구독합니다.

   * AEM Assets 이벤트(자산 승인, 업데이트, 제거됨)
   * [!DNL Commerce Optimizer]개의 카탈로그 이벤트(제품 생성, 업데이트)

상점 및 API에서 AEM 기반 이미지 데이터를 표시하도록 [카탈로그 보기](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/catalog-view)를 구성합니다.

* **카탈로그 원본(로케일)** — 지원 티켓에 지정한 것과 동일한 로케일을 선택합니다(예: **`en-US`**). 통합은 테넌트당 하나의 로케일을 등록합니다. 불일치로 인해 동기화된 이미지가 의도한 카탈로그 보기에 표시되지 않습니다.
* **카탈로그 레이어** — **`AEM-Assets`** 레이어(또는 티켓의 사용자 지정 레이어 이름)를 해당 카탈로그 보기에 할당합니다.

로케일 또는 레이어가 올바르게 할당되지 않은 경우 동기화가 업스트림에서 성공하더라도 이미지 데이터가 **나타나지 않거나** 예기치 않게 동작할 수 있습니다.

## 동기화

구성이 완료되면 통합은 `product-asset` 매핑을 자동으로 동기화합니다.

자세한 내용은 [사용자 지정 자동 일치](../synchronize/custom-match.md)를 참조하십시오.

### SKU별 일치 워크플로우 예

새 제품에 기존 에셋을 추가할 때의 일반적인 흐름:

1. API 또는 데이터 수집을 통해 [!DNL Commerce Optimizer]에서 제품을 만듭니다. 처음에 이 제품은 이미지 없이 존재할 수 있습니다.

1. AEM Assets에서 제품에 매핑할 자산을 엽니다.

1. 제품 SKU를 **commerce:skus** 메타데이터에 추가하고 이미지 역할(예: `thumbnail`, `image`)을 할당합니다.

1. 게재할 자산을 승인합니다. 이렇게 하면 Assets 통합 서비스가 처리하는 이벤트가 트리거됩니다.

1. Assets Integration Service가 제품-이미지 매핑을 [!DNL Commerce Optimizer]에 보냅니다. [!DNL Commerce Optimizer]의 제품이 자산의 이미지로 업데이트되었습니다.

1. 이미지가 표시되는지 확인합니다. 동기화가 완료될 때까지(일반적으로 몇 분 이내) 기다린 다음 [!DNL Commerce Optimizer] UI에서 제품(예: 데이터 동기화 또는 카탈로그 보기)을 확인하거나 상점 API(카탈로그 서비스, 라이브 검색, 상점 GraphQL API)를 쿼리하여 이미지가 반환되는지 확인하십시오.

## 이미지 역할 처리

제품에 동일한 이미지 역할을 사용하는 여러 에셋이 있는 경우(예: `thumbnail` 역할을 가진 두 에셋) 통합에서는 하나의 에셋만 해당 역할을 유지하여 [!DNL Commerce Optimizer] 계층의 역할 중복 및 예기치 않은 상점 첫 번째 동작을 방지합니다.

**동작:** AEM Assets에서 업데이트를 보낼 때 가장 최근에 업데이트된 에셋이 이미지 역할(예: `thumbnail`)을 받고 해당 역할이 있는 이전 에셋에서 제거됩니다. 이렇게 하면 중복 이미지 역할이 상점 앞에 표시되지 않습니다.

## 다음과 같음

* [제품 시각화](../../optimizer/setup/product-visuals.md)
* [AEM Assets 프로젝트 구성](configure-aem.md)
* [사용자 지정 자동 일치](../synchronize/custom-match.md)
* [AEM Assets 통합 개요](../overview.md)
