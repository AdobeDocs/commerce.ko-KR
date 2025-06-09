---
title: Adobe Commerce SaaS와 PaaS 비교
description: Adobe Commerce SaaS와 PaaS 모델을 비교하여 비즈니스 요구 사항에 가장 적합한 구현 접근 방식을 결정합니다.
role: Architect
exl-id: c8c9a0b4-f47c-46ec-bc9d-39dee9641f59
source-git-commit: 395def94181016b12a00ce675bb15ef6c8f10309
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 0%

---

# 기능 비교

{{accs-early-access}}

Adobe Commerce은 세 가지 배포 모델을 제공합니다.

- [!BADGE SaaS만 해당]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."} [Adobe Commerce as a Cloud Service](overview.md)(SaaS)
- [!BADGE PaaS만]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce 온 클라우드 프로젝트(Adobe 관리 PaaS 인프라) 및 온프레미스 프로젝트에만 적용됩니다."} [클라우드의 Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/overview)&#x200B;(PaaS)
- [Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/overview)&#x200B;(온-프레미스)

이 비교는 상거래 구현에 대해 다양한 수준의 맞춤화, 확장성 및 제어를 제공하는 SaaS(Software-as-a-Service)와 PaaS(Platform-as-a-Service) 모델의 차이점에 중점을 둡니다.

>[!NOTE]
>
>온-프레미스 모델은 PaaS 모델과 유사한 기능을 공유하므로 SaaS와 온-프레미스 구현을 고려할 때도 이 비교가 적용됩니다.

## 스토어 관리 기능

[Commerce 관리 UI](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/guide-overview)는 백엔드 저장소 작업, 인벤토리, 가격, 프로모션 및 고객 상호 작용을 관리하는 기능에 액세스하기 위한 기본 인터페이스입니다. 그러나 [!DNL Adobe Commerce as a Cloud Service]은(는) Adobe Commerce on Cloud 및 온-프레미스 프로젝트에서 사용할 수 있는 잘 알려진 기능 중 일부를 대체하는 고유한 솔루션을 제공합니다.

다음 표에서는 [!DNL Adobe Commerce as a Cloud Service]에서 사용할 수 있는 기능 및 대체 솔루션을 설명합니다.

<table>
    <thead>
        <tr>
            <th>PaaS 모델 [!BADGE PaaS 전용]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud 프로젝트(Adobe 관리 PaaS 인프라) 및 온프레미스 프로젝트에만 적용됩니다."}</th>
            <th>SaaS 모델 [!BADGE SaaS 전용]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."}</th>
            <th>세부 사항</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/wysiwyg/gallery/media-gallery-asset-management">디지털 자산 관리</a></td>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/aem-asset-management/aem-assets-integration">제품 시각화</a></td>
            <td>리치 미디어 콘텐츠를 관리하기 위해 Adobe Experience Manager과 통합된 강력한 DAM(디지털 에셋 관리) 시스템입니다. 또는 기본 디지털 파일 및 에셋 관리 기능은 디지털 에셋을 저장하고 관리하기 위한 기본 에셋 관리 도구를 제공합니다.</td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/guide-overview">컨텐츠 관리 시스템(CMS)</a></td>
            <td rowspan="3"><a href="https://experienceleague.adobe.com/developer/commerce/storefront/merchants/get-started/">Storefront Builder</a></td>
            <td rowspan="3">사용자가 문서 작성 또는 시각적 편집기를 사용하여 상점 컨텐츠를 쉽게 만들고 관리할 수 있도록 하며 기본 실험 기능이 포함된 CMS.</td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/page-builder/guide-overview">페이지 빌더</a></td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/seo/url-rewrites/url-rewrite">URL 재작성</a></td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/staging/content-staging">컨텐츠 스테이징</a></td>
            <td rowspan="2"><a href="../catalog-service/overview.md">카탈로그 서비스</a></td>
            <td rowspan="2">카탈로그 데이터를 관리하고 제품 관련 상점 경험을 렌더링하기 위한 풍부한 보기 모델(읽기 전용) 서비스입니다.</td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/merchandising/visual-merch/visual-merchandiser">Visual Merchandiser</a></td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/payments/payments">결제</a></td>
            <td><a href="../payment-services/guide-overview.md">결제 서비스</a></td>
            <td>안전하고 효율적인 거래를 용이하게 하는 통합 결제 서비스입니다.</td>
        </tr>
    </tbody>
</table>

## 확장성 및 플랫폼 기능

다음 표는 플랫폼 기능과 확장성 기능을 비교하여 차이점을 이해하고 구현을 시작하기 전에 비즈니스 요구 사항에 가장 적합한 모델을 정보에 입각한 결정을 내리는 데 도움이 됩니다.

<table>
    <thead>
        <tr>
            <th>기능</th>
            <th>PaaS 모델 [!BADGE PaaS 전용]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud 프로젝트(Adobe 관리 PaaS 인프라) 및 온프레미스 프로젝트에만 적용됩니다."}</th>
            <th>SaaS 모델 [!BADGE SaaS 전용]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."}</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>플랫폼 기능</strong></td>
        </tr>
        <tr>
            <td>B2B 기능</td>
            <td>설치 후 사용할 수 있는 전체 B2B 기능</td>
            <td>핵심 B2B 기능과 함께 사전 설치<sup>1</sup></td>
        </tr>
        <tr>
            <td>실험</td>
            <td>특정 계층의 추가 기능</td>
            <td>참여 및 전환을 최적화하기 위한 A/B 테스트</td>
        </tr>
        <tr>
            <td>기능 및 보안 업데이트</td>
            <td>수동 업그레이드 및 패치 필요</td>
            <td>자동 배포됨</td>
        </tr>
        <tr>
            <td>호스팅 인프라</td>
            <td>단일 임차인</td>
            <td>다중 임차인</td>
        </tr>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>Commerce 관리자 사용자 지정</strong></td>
        </tr>
        <tr>
            <td>확장 가능한 코어 관리 화면</td>
            <td>전체 레이아웃 및 기능 사용자 정의</td>
            <td>사전 설정 필터, 가시성 컨트롤</td>
        </tr>
        <tr>
            <td>확장 가능한 새 관리 화면</td>
            <td>표준 관리 UI 통합 및 외부 앱 삽입(관리 UI SDK)</td>
            <td>외부 앱 삽입(관리 UI SDK)</td>
        </tr>
        <tr>
            <td>사용자 지정 가능한 관리자 테마</td>
            <td>확장 가능한 테마 프레임워크</td>
            <td>테마 프레임워크 없음</td>
        </tr>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>확장성</strong></td>
        </tr>
        <tr>
            <td>확장성 모델</td>
            <td>In-process(PHP 사용자 지정) 및 out-of-process(API, 이벤트, App Builder)</td>
            <td>처리 중지 전용(API, 이벤트, App Builder)</td>
        </tr>
        <tr>
            <td>확장 가능한 웹 API</td>
            <td>사용자 지정 확인자를 통한 기본 REST/GraphQL 확장성 및 API Mesh</td>
            <td>사용자 정의 확인자를 사용한 API Mesh</td>
        </tr>
        <tr>
            <td>데이터 모델 확장성</td>
            <td>전체 데이터 모델 사용자 정의</td>
            <td>코어 및 B2B 엔터티의 사용자 지정 특성<sup>2</sup></td>
        </tr>
        <tr>
            <td>기술</td>
            <td>CSS, CLI, HTML, JS, PHP, XML</td>
            <td>CSS, CLI, HTML, JS, 노드</td>
        </tr>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>데이터 및 스토리지</strong></td>
        </tr>
        <tr>
            <td>색인 사용자 정의 검색</td>
            <td>기본 검색 사용자 지정</td>
            <td>타사 솔루션 필요</td>
        </tr>
        <tr>
            <td>사용자 정의 이메일 유형</td>
            <td>전체 이메일 사용자 정의</td>
            <td>표준 이메일 템플릿만</td>
        </tr>
        <tr>
            <td>사용자 지정 데이터 저장소</td>
            <td>DB, 파일, 캐시, 큐</td>
            <td>App Builder 상태 라이브러리(파일만)<sup>3</sup></td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td colspan="3">
                회사 관리 및 견적 처리와 같은 <sup>1</sup> 핵심 <a href="https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/guide-overview">B2B 기능</a>은(는) SaaS에서 즉시 사용할 수 있습니다. 그러나 업계별 사용자 지정 사항에 대해서는 추가적인 구현 고려 사항이 필요할 수 있습니다.
                <br><br>
                SaaS의 <sup>2</sup> 데이터 모델 확장성은 B2B 엔터티를 포함하여 제품 및 고객 이상으로 <a href="https://developer.adobe.com/commerce/services/cloud/guides/custom-attributes/">핵심 엔터티 확장</a>을 지원합니다. 하지만 업계별 데이터 모델(예: 딜러별 속성)에는 추가적인 아키텍처 고려 사항이 필요할 수 있습니다.
                <br><br>
                <sup>3</sup> Adobe은 SaaS에 대한 지속적인 스토리지 요구 사항을 해결하기 위해 문서 DB 통합 작업을 진행 중입니다. 현재 장기적인 데이터 스토리지가 필요한 구현에는 추가 인프라를 프로비저닝하고 유지해야 할 수 있습니다.
            </td>
        </tr>
    </tfoot>
</table>

>[!NOTE]
>
>SaaS로의 마이그레이션을 고려할 때 Adobe은 다음을 권장합니다.
>
>- 가능한 경우 적절한 기능을 프로세스 외부 확장성으로 이동합니다.
>- 변환이 필요한 표면적을 줄입니다.
>- API 기능을 확장하려면 API Mesh 를 고려하십시오.
>- Adobe의 지속적인 플랫폼 발전 및 새로운 기능 릴리스를 모니터링합니다.
>- 사용 가능한 확장성 옵션과 비교하여 업종별 데이터 모델 요구 사항을 평가합니다.
>- 채널 및 정책을 기반으로 하는 [머천다이징 서비스](../optimizer/catalog/overview.md)를 채택해 보십시오.
