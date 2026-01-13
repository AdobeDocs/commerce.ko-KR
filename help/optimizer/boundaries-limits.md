---
title: 제한 및 경계
description: ' [!DNL Adobe Commerce Optimizer] 제한 및 경계를 파악하여 용량을 계획하고 성능 문제를 방지하십시오.'
role: Admin, Developer
badgeSaas: label="SaaS만" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."
exl-id: 58d94da9-8d48-4513-8b6a-8e8c7c27a2a5
source-git-commit: f9ac230d448f071e6e8e6368b940f0c415abb02b
workflow-type: tm+mt
source-wordcount: '1350'
ht-degree: 0%

---

# 제한 및 경계

[!DNL Adobe Commerce Optimizer]에 두 가지 제한 유형이 있습니다.

- **라이선스 제한**—구입한 용량에 따라 추가 패키지를 구입하여 확장할 수 있습니다.
- **시스템 경계** - 시스템 리소스를 보호하고 모든 사용자의 안정적인 성능을 보장하는 제한을 해결했습니다.

사용은 이러한 제한 내에서 유지되어야 합니다. 이를 초과하면 지연 시간 증가 및 요청 조절 문제가 발생할 수 있습니다.

## 추가 용량 요청

[라이선스 제한 및 시스템 경계](#license-limits-and-system-boundaries) 섹션에서 설명한 라이선스 패키지를 구입하거나 고유한 사용 사례에 대해 사용자 지정 라이선스를 협상하여 라이선스 제한을 늘릴 수 있습니다. 요구 사항에 대해 논의하려면 Adobe 계정 담당자에게 문의하십시오.

시스템 경계에 대한 질문이 있으면 [Adobe 지원](https://experienceleague.adobe.com/home?lang=en#support)에 문의하십시오.

## 성능 문제 방지

다음 모범 사례에 따라 한도를 유지하고 운영 문제를 방지하십시오.

- **제한 검토**—새 상점 또는 캠페인을 시작하기 전에 [용량 제한](#license-limits-and-system-boundaries)을 이해합니다.
- **사용량 추적** - 기본 제공 지표 대시보드 또는 CDN 로그를 사용합니다.

## 라이선스 제한 및 시스템 경계

다음 표에는 용량 영역별로 라이센스 제한 및 시스템 경계가 요약되어 있으며, 해당되는 경우 용량을 확장하기 위해 라이센스를 추가하는 방법에 대한 정보가 포함되어 있습니다.

### 환경 제한

| **환경** | **설명** | **기본 할당** | **확장 가능 여부** |
| --- | --- | --- | --- |
| **샌드박스 환경** | 포함된 샌드박스 환경 수 | 인스턴스당 2개 | 예<p>인스턴스당 추가 환경 라이센스 추가</p> |
| **프로덕션 환경** | 포함된 프로덕션 환경 수 | 인스턴스당 1개 | 라이선스<p>인스턴스당 추가 환경 라이센스 추가</p> |

{style="table-layout:auto"}

### 카탈로그

| **기능** | **설명** | **기본 할당** | **확장 가능 여부** |
| --- | --- | --- | --- |
| 제품 수집 비율 | 만들거나 업데이트한 제품 수 | 분당 1K 업데이트<p>하루에 최대 10만 건의 업데이트</p> | 예<p>라이선스 팩 1개 추가:</p><ul><li>분당 5K 업데이트<br>하루에 최대 50K 업데이트</li> <li>분당 10K 업데이트<br>하루에 최대 1M 업데이트</li></ul><p>데이터 수집을 위한 최대 용량은 하루에 1M 업데이트입니다.</p> |
| 제품 페이로드 크기 | API를 사용하여 제품 정보를 생성, 업데이트 또는 수집할 때 허용되는 최대 데이터 양입니다 | 200KB | 아니요 |
| 카탈로그 변형 | Storefront 사용자가 사용할 수 있는 카탈로그 보기 횟수<p>(*카탈로그 보기 수 × 가격 책자 수*)로 계산됩니다.</p> | 100개 변형 | 예<p>100개의 카탈로그 변형 라이선스 팩 추가</p> |
| 단일 카탈로그 소스의 제품 | 카탈로그에서 지원되는 SKU | 25만개의 SKU | 예<p>100K SKU 라이선스 팩 추가</p> |
| 제품별 변형 | 제품당 허용되는 제품 변형(크기, 색상 조합) 수 | 10K | 아니요 |
| 카탈로그 소스 | 카탈로그 데이터 컨텍스트 수(예: 로케일 또는 PIM 및 ERP와 같은 데이터 소스) | 50 | 아니요 |

{style="table-layout:auto"}

### 가격 장부

| **기능** | **설명** | **기본 할당** | **확장 가능 여부** |
| --- | --- | --- | --- |
| 가격 장부 | 인스턴스당 허용되는 가격 장부 수 | [카탈로그 변형](#catalog)의 수를 기반으로 함 | 예<br>카탈로그 변형 늘리기 |
| 가격 기록당 할인 | 단일 가격표 내에서 제품 가격에 적용할 수 있는 할인 횟수 | 10 | 아니요 |

{style="table-layout:auto"}

### AEM Assets 기반 제품 비주얼

| **기능** | **설명** | **기본 할당** | **확장 가능 여부** |
| --- | --- | --- | --- |
| 제품 비주얼의 고급 사용자 | AI 도구, Adobe Express/Firefly 통합, Content Hub 공유, 핵심 DAM 작업 처리 및 최적의 효율성을 위한 고급 클라우드 기반 기능 등 전체 디지털 에셋 관리 기능을 갖춘 라이센스 사용자입니다. | 2 | 예<p>AEM Assets 라이선스로 업그레이드</p> |
| 제품 시각화 공동 작업자 사용자 | AEM Commerce 통합을 통해 에셋에 액세스하고 작업하며 Adobe Express 및 Firefly을 사용하여 콘텐츠를 만들고 편집하고, 활성화된 경우 Content Hub 포털을 통해 승인된 에셋을 활용합니다. | 2 | 예<p>AEM Assets 라이선스로 업그레이드</p> |
| 제품 비주얼 스토리지 | 에셋에 할당된 스토리지 공간 | 1TB 스토리지 | 아니요 |
| Dynamic Media 사용 | 다음을 포함하는 Dynamic Media 처리 작업을 허용합니다.<ul><li>이미지 게재</li><li>스마트 이미징</li><li>비디오 게재</li></ul><p>자세한 내용은 아래의 *Dynamic Media 사용량 계산*&#x200B;을 참조하십시오. | GMV 기반<p>최소 할당: 5M 작업/월</p> | 예<ul><li>추가 작업을 위한 라이선스 구매</li><li>AEM Assets 라이선스로 업그레이드</li></ul> |
| 비디오 게재 | 비디오 게재 또는 다운로드 허용 | 300개 비디오, 비디오당 1분 | 예<p>AEM Assets 라이선스로 업그레이드</p> |
| 자산 생성 | 이미지 생성을 위한 Adobe Express 및 Adobe Firefly 생성 AI에 액세스 | 없음 | Generative AI 크레딧을 별도로 구매하십시오 |

{style="table-layout:auto"}


>[!NOTE]
>
>**고급 사용자**&#x200B;는 직접 또는 Adobe Commerce Optimizer 내에서 Adobe Express에 액세스할 수 있습니다. **Collaborator 사용자**&#x200B;는 Adobe Express 애플리케이션에 직접 액세스할 수 있습니다. 사용은 [Firefly 제품별 라이선스 약관이 있는 Adobe Express](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/PSLT-AdobeExpressWFirefly-WW-2025v1.pdf)의 적용을 받습니다.


>[!BEGINSHADEBOX &quot;Dynamic Media 사용 계산&quot;]

Dynamic Media 사용은 Adobe Commerce Optimizer 내의 제품 시각화 구성 요소로 들어오는 API 요청을 추적하여 다음 작업 중 하나를 용이하게 합니다.

- **이미지 게재에서 다음 항목이 발생할 때마다 하나의 Dynamic Media 작업을 사용합니다**.
   - 크기 조정, 크기 조정, 포맷 변환, 압축 또는 자르기 작업과 같은 디지털 에셋의 **기본 이미지 변환**.
   - 해당 디지털 자산 또는 디지털 자산 렌디션 중 **정적 이미지 제공 또는 다운로드**(비디오 제외)
- **스마트 이미지 게재는 최종 사용자의 장치 및 브라우저에 가장 적합한 이미지 렌디션을 자동으로 생성하여 단일 디지털 에셋의 최적화된 각 게재에 대해 20개의 Dynamic Media 작업을 사용합니다**.
- **비디오 게재는 단일 비디오 게재 또는 다운로드 또는 변환된 비디오 변형에 20개의 Dynamic Media 작업을 사용합니다**.

>[!ENDSHADEBOX]


### 카탈로그 보기 및 정책

| **기능** | **설명** | **기본 할당** | **확장 가능 여부** |
| --- | --- | --- | --- |
| 카탈로그 보기 | 마스터 카탈로그의 구성 가능한 하위 집합 수 | [카탈로그 변형](#catalog)의 수를 기반으로 함 | 예<br>카탈로그 변형 늘리기 |
| 카탈로그 보기별 정책 | 허용되는 데이터 필터 수 | 10 | 아니요 |
| 정책의 속성 값 | 필터링을 구성할 수 있는 제품 특성 수입니다 | 100 | 아니요 |

{style="table-layout:auto"}

### 카탈로그 상점

카탈로그 상점 기능에 대한 기본 할당은 GMV 계층을 기반으로 결정됩니다. 이 표는 각 기능에 대한 최소 할당을 나타냅니다.

| **기능** | **설명** | **기본 할당** | **확장 가능 여부** |
| --- | --- | --- | --- |
| 카탈로그 검색률 | 카탈로그에서 데이터를 검색하기 위해 시스템(상점, 트랜잭션 시스템, ERP 또는 기타)에서 매월 카탈로그 API를 호출한 횟수입니다 | GMV 계층 기반<p>최소 할당: 10M/월</p> | 예<p>월별 요청 1백만 개 라이선스 팩 추가</p> |
| 콘텐츠 요청 | HTML 페이지 조회수 또는 JSON API 호출을 위해 Commerce Storefront에 대한 요청. 1개의 페이지 보기 또는 5개의 API 호출로 계산됩니다. | GMV 계층 기반<p>최소 할당: 2M/월</p> | 예<p>월별 1M 라이선스 팩 추가</p> |
| Storefront GenAI 변형 | 텍스트 기반 콘텐츠 생성 허용 | GMV 계층 기반<p>최소 할당: 1K 변형/월</p> | 예<p>Generative AI 크레딧을 별도로 구매하십시오</p> |

{style="table-layout:auto"}

>[!NOTE]
>
>이미지를 생성하려면 Adobe Firefly과 동일한 IMS 조직에 Adobe Commerce Optimizer 라이선스가 프로비저닝되어야 합니다.


### 제품 검색

| **기능** | **설명** | **기본 할당** | **확장 가능 여부** |
| --- | --- | --- | --- |
| 검색 요청당 제품 수 | 검색 결과에서 페이지당 반환되는 최대 제품 수 | 100 | 아니요 |
| 필터링 가능한 속성 | 레이어 탐색 및 패싯에 사용할 수 있는 제품 특성(색상, 크기, 브랜드 또는 재질)의 수입니다 | 200 | 아니요 |
| 검색 가능한 속성 | 제품 카탈로그 검색 서비스와 함께 사용하도록 구성할 수 있는 제품 특성의 수입니다 | 200 | 아니요 |
| 정렬 가능한 속성 | 검색 결과 값의 순서를 결정하기 위해 구성할 수 있는 제품 특성 수 | 50 | 아니요 |
| 검색 페이지 매김 깊이 | 페이지 매김 을 통해 액세스할 수 있는 최대 제품 수(예: 100페이지 × 100개 제품/페이지) | 10K | 아니요 |
| 패싯 | 쇼핑객이 검색 결과를 구체화하고 범주를 탐색하는 데 도움이 되도록 구성할 수 있는 필터링 가능한 제품 특성(예: 브랜드, 색상, 크기, 가격)의 수 | 100<p>필터링 가능한 속성이어야 합니다.</p> | 아니요 |
| 패싯당 옵션 | 쇼핑객이 목록에서 선택할 수 있는 필터링 가능한 제품 속성 값(예: 색상은 &quot;빨간색&quot;, &quot;파란색&quot;, 크기는 &quot;작은&quot;, &quot;Medium&quot;)의 수 | 100 | 예<p>지원 요청을 통해 증가 가능</p> |

{style="table-layout:auto"}

### 권장 사항

제품 권장 사항에 사용할 수 있는 기능은 다음과 같습니다. 다른 Adobe Commerce 제품에서 사용할 수 있는 일부 기능은 [!DNL Adobe Commerce Optimizer]에서 지원되지 않습니다.

| **기능** | **설명** | **기본 할당** | **확장 가능 여부** |
| --- | --- | --- | --- |
| 활성 추천 단위 | 상점 첫 화면의 라이브 권장 사항 구성 요소 수(&quot;고객이 본 항목&quot; 또는 &quot;당신도 좋아할 수 있음&quot;) | 50 | 아니요 |
| 범주 또는 속성 포함/제외 | 제품을 권장 사항에 적합한 특정 세트로 필터링 | 지원되지 않음 | |
| 권장 사항 미리보기 | 게시하기 전에 상점 첫 화면에 권장 사항이 어떻게 표시되는지 미리 보기 | 지원되지 않음 | |

{style="table-layout:auto"}

### 확장성

| **기능** | **설명** | **기본 할당** | **확장 가능 여부** | **메모** |
| --- | --- | --- | --- | --- |
| Adobe Developer App Builder | 클라우드 기반 확장 및 통합 구축 용량 | GMV 계층 기반<p>최소 할당: 1팩/년</p> | 예<p>추가 팩 추가</p> | 팩당 정의된 제한에 대해서는 다음을 참조하십시오.<ul><li>팩당 정의된 제한에 대한 [App Builder 제품 설명](https://helpx.adobe.com/legal/product-descriptions/adobe-developer-app-builder.html).</li><li>[App Builder 런타임 가이드](https://developer.adobe.com/app-builder/docs/guides/runtime_guides/system-settings)의 *시스템 설정 및 제한*.</li><li>[App Builder 저장소 요구 사항](https://developer.adobe.com/app-builder/docs/guides/app_builder_guides/storage/)</li></ul> |

{style="table-layout:auto"}

<!--## How to size your solution

Ask your Adobe representative for a list of available packages to determine which most closely matches your project

To accurately size your Adobe Commerce Optimizer solution, follow these steps:

1. Review the available packages, and start with a package that most closely matches your requirements.
1. Review the capabilities and metrics to ensure they align with your business requirements.
1. Purchase add-on packages for any metrics where you require additional capacity.

This approach ensures your solution is accurately sized for your business needs.

### Example use cases

1. **Seasonal Catalog Expansion**

   * Need: +20K SKUs
   * Add-On: 2 × SKU Packs (10K each)

1. **High Traffic Surge**

   * Need: +3M content requests/month
   * Add-On: 3 × content request packs (1M each)

1. **Global Presence**

   * Need: Additional environments for testing
   * Add-On: +1 Production, +2 Sandbox instances

1. **GenAI or Media Needs**

   * Need: +10M dynamic media ops/month
   * Add-On: 10 × dynamic media packs (1M each) -->
