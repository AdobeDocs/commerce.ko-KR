---
title: 마이그레이션 평가
description: Adobe Commerce PaaS 마이그레이션 평가 보고서를 읽고, 상점 및 백엔드 복잡성 신호를 해석하고, Adobe AI 개발자 도구를 사용하여 Adobe Commerce as a Cloud Service에 대한 확장 빌드를 시작하는 방법에 대해 알아봅니다.
feature: Cloud, Migration
role: Developer, Admin
level: Intermediate
TQID: 'https://experienceleague.adobe.com/-OrsBVtHRcEV5EzgHzzP0JVf0aQWfSO2Fu1R5F5jtAw'
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: c32adafa-ed01-4b31-997e-2413013911b0id: cc250cf1-34eb-4863-80d0-d170d45ea067id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
nudge: true1
source-git-commit: 99ad11aa255d35dcee4ffa80b4a38916d0c21766
workflow-type: tm+mt
source-wordcount: 2505
ht-degree: 0%

---


# 마이그레이션 평가

>[!IMPORTANT]
>
> [!DNL Adobe Commerce on Cloud Infrastructure] 또는 [!DNL Adobe Commerce on-premises] 프로젝트를 [!DNL Adobe Commerce as a Cloud Service]&#x200B;(으)로 마이그레이션하는 경우에만 마이그레이션 평가를 사용할 수 있습니다.

Commerce 마이그레이션 평가는 기존 Adobe Commerce 구현에 대한 자동화된 분석입니다. Adobe의 도구 기능은 Commerce 코드베이스를 스캔하고 빌드되거나, 사용자 정의되거나, 수정된 모든 사항을 인벤터리하는 구조화된 보고서를 생성합니다. 그러면 코드베이스에 대한 사용자 지정이 [!DNL Adobe Commerce as a Cloud Service]&#x200B;(으)로의 마이그레이션에 어떤 영향을 미치는지 보여줍니다.

보고서는 모든 브라우저에서 열 수 있는 HTML 파일로 제공됩니다. 프로젝트 코드베이스를 처음 공유하는 경우를 제외하고 프로덕션 환경에 액세스할 필요가 없습니다.

**평가에서 제공하는 항목:**

- 유형 및 영향 수준별로 구성된 스토어의 모든 사용자 정의 모듈에 대한 전체 인벤토리
- 위험 예측 지표에서 계산된 마이그레이션 복잡성 등급(높음, Medium 또는 낮음)
- 마이그레이션 계획이 필요한 가장 영향력이 큰 백엔드 및 상점 영역에 대한 우선 순위 보기
- Adobe의 AI 개발자 도구에 대한 직접 입력으로 사용할 수 있는 각 사용자 정의 모듈에 대한 설명입니다

## 마이그레이션 평가 보고서 이해

보고서는 **[!UICONTROL Summary]**, **[!UICONTROL Module Reports]**, **[!UICONTROL Report Reliability]** 세 개의 탭으로 구성됩니다.

>[!NOTE]
>
>보고서의 모든 섹션이 모든 스토어에 적용되는 것은 아닙니다. 가능한 모든 사용자 정의 유형 및 복잡성 드라이버에 대해 포괄적으로 평가되도록 설계되었지만 스토어에는 여기에 나열된 섹션의 하위 집합만 있습니다.

## 요약 탭

**[!UICONTROL Summary]** 탭은 다음 영역으로 구성된 주요 신호에 대한 개요를 제공합니다.

- 마이그레이션 복잡성
- 파일 유형 분류
- 가장 큰 영향을 미치는 모듈
- 마이그레이션 드라이버
- 사용자 지정 분류

### 마이그레이션 복잡성

마이그레이션 복잡성 섹션에는 저장소 전체에 대한 평가 등급이 포함되어 있습니다. 점수가 계산된 방식을 설명하고 주요 위험 요소를 강조합니다.

**마이그레이션 복잡성 및 복잡성 점수**

![가중치가 적용된 점수, 주요 위험 요소 및 주요 지표를 보여 주는 마이그레이션 복잡성 섹션](../assets/assessment-migration-complexity.png){width="600" zoomable="yes"}

복잡성 점수는 각 입력에 마이그레이션이 얼마나 어려운지 가중치를 부여합니다. 점수는 고정 임계값을 사용하여 마이그레이션 복잡성 등급에 매핑됩니다.

| 등급 | 점수 범위 | 일반적인 마이그레이션 방식 |
| --- | --- | --- |
| 낮음 | 150 이하 | 표준 마이그레이션 - 결제 제공업체 조정을 통한 직접 마이그레이션 및 데이터 마이그레이션을 병렬 워크스트림으로 처리. |
| Medium | 151-375 | 모듈식 마이그레이션 - 세그먼트에서 마이그레이션되어 영향력이 큰 사용자 정의 모듈을 평가합니다. |
| 높음 | 375 이상 | 12~24개월 동안 지속되는 단계적 마이그레이션 |

**사용자 지정 모듈 비율**

![사용자 지정 모듈 비율, 타사 모듈, 사용자 지정 테마 수, 중요 후크, 총 파일 및 PHP 코드베이스 크기를 표시하는 사용자 지정 모듈 비율 지표 행](../assets/assessment-custom-module-ratio.png){width="600" zoomable="yes"}

구현을 위해 특별히 빌드된 모듈의 비율입니다. 비율이 높을수록 더 많은 사용자 지정 코드를 감사하고 마이그레이션해야 합니다. 평균 고객의 사용자 정의 모듈 비율은 약 62%입니다.

>[!TIP]
>
>사용자 정의 모듈 비율은 복잡성 신호가 아닌 범위 신호입니다. 사용자 정의 모듈이 80% 격리되고 위험도가 낮은 스토어는 40% 높은 위험 사용자 정의 모듈이 있는 스토어보다 쉽게 마이그레이션할 수 있습니다. 복잡성 점수 와 체인 충돌 수를 사용하여 어려움을 평가합니다. 사용자 정의 모듈 비율을 사용하여 볼륨을 추정합니다.

**파일 형식 분류**

![파일 개수 및 코드 줄이 있는 파일 확장자를 나열하는 파일 형식 분석 표](../assets/assessment-file-type-breakdown.png){width="600" zoomable="yes"}

코드베이스에 있는 파일 수를 유형별로 정리한 목록.

**가장 영향이 큰 모듈**

![모듈 이름, 설명, 영향 등급 및 후크 수를 보여 주는 가장 영향이 큰 모듈 목록](../assets/assessment-highest-impact-modules.png){width="600" zoomable="yes"}

가장 많은 마이그레이션에 주의가 필요한 저장소의 특정 모듈에 대한 선별된 목록입니다. 이러한 모듈은 종종 체크아웃, 결제 또는 주문 관리와 상호 작용하는 모듈입니다. 영향을 많이 받는 각 모듈에는 고유한 마이그레이션 계획이 필요합니다. 이 목록은 기술 팀과의 대화에 가장 좋은 시작점입니다.

### Storefront 복잡성

![사용자 지정 테마 네임스페이스, 총 블록 수, 레이아웃 XML 파일, 코어 핸들 재정의 및 실행 가능한 신호를 보여주는 Storefront 복잡성 섹션](../assets/assessment-storefront-complexity.png){width="600" zoomable="yes"}

Storefront 복잡성 섹션은 스토어의 프론트엔드 프레젠테이션 레이어를 마이그레이션하는 데 필요한 노력을 나타냅니다. 이 워크플로우는 백엔드 코드 마이그레이션과 구별되는 워크플로우는 프론트엔드 개발자가 처리하며 일반적으로 별도의 계획 대화가 필요합니다.

>[!NOTE]
>
>스토어는 낮은 백엔드 복잡성과 높은 스토어프런트 복잡성을 가질 수 있습니다. 마이그레이션 작업의 범위를 지정하기 전에 항상 두 섹션을 모두 검토하십시오.

- 사용자 지정 테마 - 스토어 사용자 지정 테마의 네임스페이스(예: BrandName_Theme). 사용자 지정 테마가 있으면 [!DNL Adobe Commerce as a Cloud Service]에 전체 테마를 다시 빌드해야 합니다. 사용자 정의 테마 네임스페이스가 있는 모든 평가 스토어는 전용 프론트엔드 마이그레이션 워크스트림을 계획해야 합니다.

- 총 블록 수 - 스토어에 있는 블록 및 템플릿(.phtml) 파일 수입니다. 블록은 기본 서버측 렌더링 아티팩트이며, 각각은 개별 마이그레이션 작업을 나타냅니다.

| 블록 수 | 작업량 |
| --- | --- |
| 100세 미만 | 초기 계획 - 표준 작업량 |
| 100-300 | Medium - 구조화된 프론트엔드 웨이브 계획 |
| 300개 이상 | 높음 - 전용 워크스트림으로 우선 순위 지정 |

### 마이그레이션 드라이버

![사용자 지정 설치 공간, 플러그인 및 관찰자, 노력 등급이 있는 클래스 환경 설정 카드를 표시하는 마이그레이션 드라이버 섹션](../assets/assessment-migration-drivers.png){width="600" zoomable="yes"}

마이그레이션 드라이버 섹션에는 복잡성 평가를 유도하는 주요 요인이 표시됩니다.

| 드라이버 | 정의 |
| --- | --- |
| 사용자 지정 공간 | 총 구현 대비 사용자 지정 코드의 전체 볼륨 |
| 플러그인 및 옵저버 | 런타임 시 핵심 플랫폼 동작을 가로채는 코드 |
| 클래스 환경 설정 | 핵심 클래스를 완전히 대체하고 업그레이드 시 자동으로 중단되는 취약한 맞춤화 패턴 |
| 데이터 모델 | 사용자 지정 및 수정된 데이터베이스 구조 |
| 통합 | 스토어에 연결된 외부 시스템 |

각 드라이버는 높음, Medium 또는 낮음으로 표시됩니다. 범위 지정 및 계획 시 가장 높은 등급의 드라이버를 먼저 해결합니다.

### 데이터 모델

![사용자 지정 테이블, 핵심 테이블 수정 및 중요 EAV 특성 수를 보여 주는 데이터 모델 섹션](../assets/assessment-data-model.png){width="600" zoomable="yes"}

데이터 모델 섹션에는 사용자 지정 테이블 수, [!DNL Adobe Commerce] 코어 데이터베이스 테이블에 대한 수정 사항 및 중요한 EAV(Entity-Attribute-Value) 특성이 표시됩니다.

핵심 테이블 수정 사항은 특정 플랫폼 스키마 버전에 대한 종속성을 만들고 복잡성 점수 공식에 높은 영향을 미치기 때문에 마이그레이션하기 가장 어려운 범주입니다.

>[!TIP]
>
>보고서에 15개가 넘는 핵심 테이블 수정 사항이 표시되면 백엔드 모듈 마이그레이션의 범위를 설정하기 전에 전용 데이터 마이그레이션 워크스트림을 계획하십시오.

## 사용자 지정 분류

![카운트 및 영향 지표가 있는 모든 사용자 지정 범주를 나열하는 사용자 지정 분류 섹션](../assets/assessment-customization-breakdown.png){width="600" zoomable="yes"}

사용자 지정 분류 섹션은 스토어의 모든 사용자 지정 카테고리에 대한 세부 지표를 제공합니다.

>[!NOTE]
>
>모든 보고서에 모든 하위 섹션이 나타나는 것은 아니며 코드 베이스에서 감지된 카테고리만 표시됩니다.
>
>프론트엔드 프레젠테이션 레이어에 영향을 주는 하위 섹션은 백엔드 코드 마이그레이션과 구별되는 작업 스트림이며 일반적으로 별도의 계획 대화가 필요합니다.
>
>스토어는 낮은 백엔드 복잡성과 높은 프론트엔드 복잡성을 가질 수 있습니다. 마이그레이션 작업의 범위를 지정하기 전에 항상 백엔드 및 상점 관련 하위 섹션을 검토하십시오.

### 레이아웃 XML

레이아웃 XML 파일의 수와 총 작업 수입니다. 레이아웃 XML은 블록이 나타나는 블록, 해당 블록이 나타나는 컨테이너, 해당 블록이 속한 페이지 유형을 포함하여 모든 페이지의 구조를 정의합니다.

많은 작업에서 파일 수가 많으면 다시 설계해야 하는 상당한 페이지 구조 사용자 지정이 표시됩니다.

### 코어 핸들 재정의

레이아웃 XML이 핵심 [!DNL Adobe Commerce] 페이지 핸들을 재정의하는 위치(예: `checkout_cart_index` 또는 `catalog_product_view`)의 수입니다. 코어 핸들 재정의는 플랫폼 수준에서 페이지 구조를 수정하고 명시적인 재구성이 필요하므로 가장 위험도가 높은 레이아웃 신호입니다.

| 재정의 수 | 작업량 |
| --- | --- |
| 0 | 코어 레이아웃 재정의 없음 |
| 1-3 | 런타임 위험 - 각 재정의에 명시적 레이아웃 재구성이 필요합니다. |
| 4개 이상 | 중요 - 전용 레이아웃 마이그레이션 스프린트에 대한 계획 |

### 블록

스토어에 있는 블록 및 템플릿(`.phtml`)의 파일 수입니다. 블록은 기본 서버측 렌더링 객체입니다. 각 블록은 개별 마이그레이션 작업을 나타냅니다.

| 블록 수 | 작업량 |
| --- | --- |
| 100세 미만 | 초기 계획 - 표준 작업량 |
| 100-300 | Medium - 구조화된 프론트엔드 웨이브 계획 |
| 300개 이상 | 높음 - 전용 워크스트림으로 우선 순위 지정 |

### 고위험 블록

체크아웃 렌더링, 장바구니 표시 및 이와 유사한 프런트 엔드 표면과 같이 코어 렌더링 경로를 연결하는 블록입니다. 위험이 높은 블록은 스케줄링하기 전에 개별 마이그레이션 평가가 필요합니다.

### 테마 및 이메일 템플릿

스토어의 사용자 지정 테마 네임스페이스(예: `BrandName_Theme`)입니다. 사용자 지정 테마가 있으면 전체 테마를 다시 빌드해야 합니다. 사용자 정의 테마 네임스페이스가 있는 모든 평가 스토어는 전용 프론트엔드 마이그레이션 워크스트림을 계획해야 합니다.

### 템플릿 재정의(핵심 수정됨)

재정의된 코어 [!DNL Adobe Commerce] `.phtml` 템플릿의 수입니다. 각 핵심 템플릿 무시는 해당 템플릿의 특정 버전에 대한 종속성을 만듭니다. 템플릿을 변경하는 플랫폼 업데이트로 무시가 자동으로 중단됩니다.

### 드롭인 마이그레이션 필요

[!DNL Adobe Commerce as a Cloud Service]은(는) 체크아웃, 장바구니 및 제품 세부 사항을 포함한 상점 표면에 대해 모듈식 드롭인 구성 요소 아키텍처를 사용합니다. 이러한 서피스에 대한 커스터마이제이션은 드롭인 구성 요소로 다시 빌드해야 합니다. 이러한 사용자 지정에서는 사용자 지정 체크아웃 단계 추가, 장바구니 표시 논리 수정 또는 제품 세부 사항 페이지 확장과 같은 다양한 기능을 사용할 수 있습니다.

[!UICONTROL Drop-in migration required] 필드는 끌어 놓기 재빌드가 필요한 상점 영역을 나타냅니다.

>[!IMPORTANT]
>
>**체크아웃**&#x200B;이(가) 드롭인 마이그레이션 요구 사항으로 나열되는 경우 전용 체크아웃 드롭인 워크스트림을 계획하십시오. 이 작업은 가장 복잡하고 비즈니스 크리티컬한 Storefront 마이그레이션 작업입니다.

## 모듈 보고서 탭

![영향 필터 및 자세한 모듈 분석 패널이 있는 검색 가능한 모듈 목록을 표시하는 모듈 보고서 탭](../assets/assessment-module-reports-tab.png){width="600" zoomable="yes"}

**[!UICONTROL Module Reports]** 탭에는 스토어의 모든 사용자 지정 모듈에 대한 전용 항목이 포함되어 있습니다. 이 정보를 기술 팀과 공유합니다.

각 모듈에 대해 다음과 같은 보고서가 표시됩니다.

| 필드 이름 | 정의 |
| --- | --- |
| 기능 | 사용자 정의 모듈의 목적 및 비즈니스 기능에 대한 설명 |
| 영향 수준 | 모듈이 터치하는 상거래 동작에 따라 **높음**, **Medium** 또는 **낮음**&#x200B;에 영향을 줍니다. |
| 후크 수 | 이 모듈이 핵심 플랫폼 동작을 가로채는 위치의 수를 나타내는 웹 후크 수입니다. |
| 마이그레이션 권장 사항 | **다시 빌드**, **리팩터링**, **기본 기능으로 바꾸기** 또는 **제거** |
| 종속성 | 이 모듈이 마이그레이션 시퀀싱을 알릴 수 있는 상호 작용하는 다른 모듈 |

**워크플로**

1. 먼저 **영향력이 큰** 모듈로 필터링하십시오. 따라서 가장 많은 마이그레이션 노력과 비용이 듭니다.
1. 각 사용자 정의 모듈에 대해 다음 질문에 대한 답변을 결정하십시오.
   - 이 모듈이 여전히 활발히 사용되고 있습니까?
   - 모듈을 네이티브 [!DNL Adobe Commerce as a Cloud Service] 기능으로 바꿀 수 있습니까?
   - 모듈을 다시 빌드해야 하는 경우 교체에서 제공해야 하는 기능은 무엇입니까?
1. 사용 중지 또는 교체할 수 있는 사용자 정의 모듈을 식별합니다. 각 코드는 코드를 작성하기 전에 마이그레이션 범위를 줄입니다.
1. **다시 빌드** 마이그레이션 권장 사항을 사용하여 각 사용자 지정 모듈의 설명을 복사합니다. 이러한 설명은 Adobe의 AI 개발자 도구에 직접 지정할 수 있습니다. 자세한 내용은 [Commerce 확장성을 위한 AI 개발자 도구](#ai-developer-tools-for-commerce-extensibility)를 참조하십시오.

## 참조: 주요 용어

| 용어 | 정의 |
| --- | --- |
| **모듈** | 사용자 지정된 자체 포함 기능 패키지입니다. 당신의 가게는 모듈 스무 개에서 수백 개까지 가질 수 있습니다. |
| **플러그 인(인터셉터)** | Commerce 함수를 실행하기 전, 실행 중 또는 후에 가로채고 해당 동작을 변경하는 코드입니다. |
| **관찰자** | &quot;주문&quot;과 같은 특정 플랫폼 이벤트를 수신하고 해당 이벤트가 실행될 때 사용자 지정 논리를 실행하는 코드입니다. |
| **기본 설정(클래스 재정의)** | 핵심 Commerce 클래스를 완전히 대체하는 취약한 사용자 정의 유형으로, 플랫폼에서 해당 클래스를 업그레이드할 때 자동으로 중단됩니다. |
| **체인 충돌** | 두 개 이상의 플러그인이 동일한 함수를 가로채고 한 플러그인이 다음 플러그인으로 컨트롤을 전달하지 못하는 경우. 이로 인해 오류 메시지 없이 기능이 자동으로 작동하지 않을 수 있습니다. |
| **핵심 테이블 수정** | 특정 플랫폼 스키마 버전에 대해 비가역적인 종속성을 만드는 Commerce의 기본 제공 데이터베이스 테이블의 구조적 변경. 이는 복잡성 점수 공식에서 가장 높은 가중치를 갖습니다. |
| **EAV(Entity-Attribute-Value)** | 제품 또는 고객에 추가된 유연한 사용자 정의 필드(예: 사용자 정의 &quot;보증 기간&quot; 필드). 높은 EAV 수는 데이터 마이그레이션 복잡성을 증가시킵니다. |
| **후크 밀도** | 모듈당 평균 플러그인 및 관찰자 수. 밀도가 높을수록 핵심 플랫폼에 맞춤화가 더욱 긴밀하게 결합되어 있음을 의미합니다. |
| **드롭인** | 상점 첫 화면 구성 요소에 대한 [!DNL Adobe Commerce's] 모듈식 접근 방식(체크아웃, 장바구니 및 제품 세부 사항 페이지 포함). [!DNL Adobe Commerce on Cloud Infrastructure] 또는 [!DNL Adobe Commerce on Premises]의 사용자 지정 체크아웃 동작을 사용하려면 일반적으로 [!DNL Adobe Commerce as a Cloud Service]에 드롭인 다시 빌드가 필요합니다. |
| **App Builder** | Adobe의 프로세스 외부 확장성 플랫폼과 사용자 정의 기능을 빌드하는 데 권장되는 방법으로, 프로세스 내 PHP 확장을 대체합니다. |
| **레이아웃 XML** | 페이지에 나타나는 블록을 정의하는 구성 파일입니다. [!DNL Adobe Commerce as a Cloud Service's] 페이지 구조에 대해 사용자 지정 레이아웃 XML을 다시 빌드해야 합니다. |
| **코어 핸들 재정의** | 핵심 Commerce 페이지 구조를 전체적으로 수정하는 레이아웃 XML 사용자 정의입니다. 가장 위험도가 높은 마이그레이션 레이아웃 패턴을 갖고 있습니다. |

## Commerce 확장성을 위한 AI 개발자 도구

**[!UICONTROL Module Reports]** 탭의 모듈 설명을 Adobe AI 개발자 도구에 대한 프롬프트로 사용할 수 있습니다. 이 도구를 사용하면 [!DNL Adobe Commerce as a Cloud Service]과(와) 호환되는 대체 확장을 빌드하고 배포하는 데 도움이 됩니다.

### 도구에서 제공하는 사항

Adobe의 [Commerce 확장성을 위한 AI 개발자 도구](https://developer.adobe.com/commerce/extensibility/developer-agent/)에는 두 가지 기본 기능이 포함됩니다.

- [!DNL Adobe Commerce] [!DNL App Builder] MCP 서버 - AI 코딩 도우미를 [!DNL Adobe Commerce] 설명서, API 및 App Builder 개발 패턴에 직접 연결하는 MCP(모델 컨텍스트 프로토콜) 통합입니다. 개발자는 빌드할 내용을 설명할 수 있으며 MCP 서버는 IDE 내에서 Commerce 인식 코드 생성, 아키텍처 지침 및 배포 자동화를 제공합니다.
- 에이전트 기술 - REST API, 체크아웃 확장, 상점 구성 요소 및 이벤트 기반 통합과 같은 일반적인 Commerce 확장성 패턴을 다루는 사전 빌드된 AI 기술. [!DNL Adobe Commerce as a Cloud Service] 및 [!DNL App Builder]과(와) 관련된 아키텍처, 구현, 테스트 및 배포 단계를 통해 AI를 안내합니다.

#### AI 도구 설치

전체 지침 및 특정 IDE 구성은 [AI 개발자 도구 설치](https://developer.adobe.com/commerce/extensibility/developer-agent/coding-tools)를 참조하십시오.

**사전 요구 사항:** Node.js 22.x, npm 9.0.0 이상, Adobe I/O CLI.

설치 명령:

```bash
aio commerce extensibility tools-setup
```

### 평가 보고서에서 프롬프트 생성

평가는 개발에 대한 청사진을 제공하지만, AI 도구를 사용하면 전체 마이그레이션 계획이 완료되기 전에 팀이 즉시 빌드를 시작할 수 있습니다.

1. **[!UICONTROL Module Reports]** 탭을 열고 **다시 빌드** 권장 사항이 있는 영향 높은 모듈을 찾습니다.
1. 모듈의 설명을 읽어 보십시오. 예:

```shell-session
Manages custom shipping rate calculations based on customer account tier and order    weight thresholds.
```

1. Commerce 확장성 MCP 서버가 활성화된 상태에서 IDE(예: GitHub Copilot, Cursor 또는 Cloud)를 엽니다.
1. 모듈 설명을 사용하여 AI 에이전트를 묻는 메시지를 표시합니다.
1. 스캐폴딩한 [!DNL App Builder] 응용 프로그램을 검토하고 에이전트를 반복하여 구현을 구체화합니다.

## 다음 단계

1. **[!UICONTROL Summary]** 탭을 엽니다. 마이그레이션 복잡성 및 가장 큰 영향을 미치는 모듈을 검토한 다음 사용자 지정 분류 하위 섹션을 확인하십시오. 스토어에 사용자 지정 테마, 고위험 블록 또는 체크아웃 드롭인이 나열되어 있는 경우 백엔드 마이그레이션과 함께 병렬 프론트엔드 워크스트림을 계획합니다.
1. **[!UICONTROL Module Reports]** 탭을 기술 팀이나 개발 파트너와 공유합니다. 더 이상 사용되지 않거나 [!DNL Adobe Commerce as a Cloud Service] 기능으로 대체할 수 있는 사용자 지정 모듈에 플래그를 지정하도록 요청하십시오.
1. 사용자 지정 빌드를 시작합니다. 모듈 설명을 AI 도구 입력으로 사용하여 호환되는 확장 스캐폴딩을 시작합니다.
1. Adobe 계정 팀과 연습 호출을 예약합니다. Adobe은 사용자와 함께 결과를 검토하고 특정 모듈 및 상점 내 신호에 대한 질문에 답변하며 복잡성 프로필에 대한 마이그레이션 접근 방식을 매핑하는 데 도움이 됩니다.

## 리소스

- [!DNL Adobe Commerce as a Cloud Service]
   - [개요](../overview.md)
   - [마이그레이션 개요](./overview.md)
   - [등급 확장 튜토리얼](../tutorials/ratings-extension.md)
   - [배송 방법 자습서](../tutorials/shipping-method-extension.md)
- 확장성
   - [개요](https://developer.adobe.com/commerce/extensibility/)
   - [AI 개발자 도구](https://developer.adobe.com/commerce/extensibility/developer-agent/)
      - [우수 사례](https://developer.adobe.com/commerce/extensibility/developer-agent/best-practices)
      - [설정](https://developer.adobe.com/commerce/extensibility/developer-agent/coding-tools)
      - [스킬 및 프롬프트](https://developer.adobe.com/commerce/extensibility/developer-agent/skills-and-prompts)
      - [사용 사례](https://developer.adobe.com/commerce/extensibility/developer-agent/use-cases)
   - [App Builder 개요](https://developer.adobe.com/app-builder/docs/intro_and_overview/)
   - [Adobe Commerce용 App Builder](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/extensibility/adobe-developer-app-builder/introduction-to-app-builder)
   - 스타터 키트
      - [백엔드 통합 시작 키트](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/)
      - [체크아웃 스타터 키트](https://developer.adobe.com/commerce/extensibility/starter-kit/checkout/)
- Storefront 개발
   - [개요](https://experienceleague.adobe.com/developer/commerce/storefront/)
   - [Storefront AI 기술](https://experienceleague.adobe.com/developer/commerce/storefront/boilerplate/ai-agent-skills/)

>[!TIP]
>
>기존 인스턴스에 대한 마이그레이션 평가를 요청하려면 솔루션 계정 관리자에게 문의하십시오.
