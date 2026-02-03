---
title: Adobe Commerce SaaS와 PaaS 비교
description: Adobe Commerce SaaS와 PaaS 모델을 비교하여 비즈니스 요구 사항에 가장 적합한 구현 접근 방식을 결정합니다.
feature: App Builder, GraphQL, Integration, Saas
role: Developer, Admin, Leader
level: Intermediate
exl-id: c8c9a0b4-f47c-46ec-bc9d-39dee9641f59
source-git-commit: e8e0c9f6a14232abc1332b48df7ae8bc3b955900
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 0%

---

# 기능 비교

Adobe Commerce은 세 가지 배포 모델을 제공합니다.

- [!BADGE SaaS만 해당]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."} [Adobe Commerce as a Cloud Service](overview.md)(SaaS)
- [!BADGE PaaS만]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce 온 클라우드 프로젝트(Adobe 관리 PaaS 인프라) 및 온프레미스 프로젝트에만 적용됩니다."} [클라우드의 Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/overview)&#x200B;(PaaS)
- [Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/overview)&#x200B;(온-프레미스)

이 비교에서는 SaaS(Software-as-a-Service) 모델과 PaaS(Platform-as-a-Service) 모델의 차이점에 중점을 둡니다. 이러한 모델은 Commerce 구현에 대해 다양한 수준의 맞춤화, 확장성 및 제어를 제공합니다.

>[!NOTE]
>
>온-프레미스 모델은 PaaS 모델과 유사한 기능을 공유하므로 SaaS와 온-프레미스 구현을 고려할 때도 이 비교가 적용됩니다.

## 스토어 관리 기능

[Commerce 관리 UI](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/guide-overview)는 백엔드 저장소 작업, 인벤토리, 가격, 프로모션 및 고객 상호 작용을 관리하는 기능에 액세스하기 위한 기본 인터페이스입니다. 그러나 [!DNL Adobe Commerce as a Cloud Service]은(는) [!DNL Adobe Commerce on Cloud] 및 온-프레미스 프로젝트에서 사용할 수 있는 잘 알려진 기능 중 일부를 대체하는 고유한 솔루션을 제공합니다.

다음 표에서는 [!DNL Adobe Commerce as a Cloud Service]에서 사용할 수 있는 기능 및 대체 솔루션을 설명합니다.

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
            <td>디지털 자산 관리</td>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/wysiwyg/gallery/media-gallery-asset-management">미디어 갤러리</a></td>
            <td><a href="../aem-assets-integration/overview.md">제품 시각화</a></td>
        </tr>
        <tr>
            <td>콘텐츠 관리</td>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/guide-overview">콘텐츠 관리 시스템(CMS)</a>, <a href="https://experienceleague.adobe.com/en/docs/commerce-admin/page-builder/guide-overview">페이지 빌더</a>, <a href="https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/seo/url-rewrites/url-rewrite">URL 다시 쓰기</a></td>
            <td><a href="https://experienceleague.adobe.com/developer/commerce/storefront/merchants/get-started/">Storefront Builder</a></td>
        </tr>
        <tr>
            <td>카탈로그 머천다이징</td>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/staging/content-staging">콘텐츠 스테이징</a>, <a href="https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/merchandising/visual-merch/visual-merchandiser">시각적 머천다이저</a></td>
            <td><a href="../catalog-service/overview.md">카탈로그 서비스</a></td>
        </tr>
        <tr>
            <td>결제</td>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/payments/payments">결제 솔루션</a></td>
            <td><a href="../payment-services/guide-overview.md">결제 서비스</a></td>
        </tr>
        <tr>
            <td>B2B 기능</td>
            <td>설치 후 사용할 수 있는 전체 B2B 기능</td>
            <td>핵심 B2B 기능과 함께 사전 설치<sup>1</sup></td>
        </tr>
        <tr>
            <td>실험</td>
            <td>특정 계층의 추가 기능</td>
            <td>참여 및 전환을 최적화하는 기본 A/B 테스트</td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td colspan="3">
                회사 관리 및 견적 처리와 같은 <sup>1</sup> 핵심 <a href="https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/guide-overview">B2B 기능</a>은(는) SaaS에서 즉시 사용할 수 있습니다. 그러나 업계별 사용자 지정 사항에 대해서는 추가적인 구현 고려 사항이 필요할 수 있습니다.
            </td>
        </tr>
    </tfoot>
</table>

## 확장성 및 플랫폼 기능

다음 표는 플랫폼 기능과 확장성 기능을 비교하여 차이점을 이해하고 구현을 시작하기 전에 비즈니스 요구 사항에 가장 적합한 모델을 결정하는 데 도움이 됩니다.

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
            <td>기능 및 보안 업데이트</td>
            <td>수동 업그레이드 및 패치가 필요합니다. 연간 패치 릴리스 6개와 마이너 릴리스 1개.</td>
            <td>버전이 없는 SaaS 모델을 통해 Adobe에서 자동으로 업그레이드됨</td>
        </tr>
        <tr>
            <td>호스팅 인프라</td>
            <td>단일 임차인</td>
            <td>다중 임차인</td>
        </tr>
        <tr>
            <td>성능 및 확장성</td>
            <td>확장 가능한 아키텍처를 위한 수평 자동 확장 확장되지 않은 아키텍처를 포함하여 모든 판매자에 대해 조기 액세스 시 롤아웃되는 웹 계층에 대한 수직 자동 확장.</td>
            <td>스택 전체에서 전체 Auto-Scaling을 지원하는 다중 테넌트 클라우드 네이티브 애플리케이션</td>
        </tr>
        <tr>
            <td>가시성</td>
            <td>[!DNL New Relic] 고객이 환경을 모니터링 및 관리할 수 있도록 액세스</td>
            <td>Adobe 관리. 고객은 [!DNL OpenTelemetry]개 앱에 대해 [!DNL App Builder]을(를) 사용하고 상점가에 대해 RUM 대시보드를 사용할 수 있습니다. [!DNL New Relic] 라이선스가 포함되지 않았습니다. 고객은 자신의 [!DNL API Mesh] 계정으로 데이터를 보내도록 [!DNL App Builder] 및 [!DNL New Relic]을(를) 구성할 수 있습니다.</td>
        </tr>
        <tr>
            <td>CDN</td>
            <td>[!DNL Fastly] 포함됨</td>
            <td>완전히 관리되는 Edge CDN은 Commerce Storefront와 밀접하게 연결되어 있습니다. BYO-CDN도 지원됩니다.</td>
        </tr>
        <tr>
            <td>보안 및 규정 준수</td>
            <td>호스팅 공급업체당 SOC2, PCI, ISO 인증, HIPAA</td>
            <td>SOC2, PCI, ISO, GDPR. 현재 HIPAA를 사용할 수 없습니다.</td>
        </tr>
        <tr>
            <td>재해 복구 및 SLA</td>
            <td>99.99% 인프라, 99.9% 애플리케이션(Managed Services)</td>
            <td>99.9%(인프라 및 애플리케이션), 더 빠른 RPO/RTO</td>
        </tr>
        <tr>
            <td>호스팅 영역</td>
            <td>Azure(24개 위치), AWS(22개 위치), GCP(표준이 아닌 8개 위치)</td>
            <td>전역적으로 사용 가능합니다. 지역의 프로덕션 환경에 대한 자세한 내용은 고객 서비스 담당자에게 문의하십시오. 수요에 따라 추가 위치가 롤아웃되었습니다.</td>
        </tr>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>Commerce 관리자 사용자 지정</strong></td>
        </tr>
        <tr>
            <td>Admin Console 확장성</td>
            <td>PHP 사용자 지정 및 테마, App Builder 확장성(권장)</td>
            <td>App Builder 확장성</td>
        </tr>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>확장성</strong></td>
        </tr>
        <tr>
            <td>확장성 모델</td>
            <td>In-process(PHP 사용자 지정) 및 out-of-process(권장:API, 이벤트, App Builder)</td>
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
            <td>코어 및 B2B 엔터티의 사용자 지정 특성<sup>1</sup></td>
        </tr>
        <tr>
            <td>기술</td>
            <td>CSS, CLI, HTML, JS, PHP, XML</td>
            <td>CSS, CLI, HTML, JS, 노드</td>
        </tr>
        <tr>
            <td>앱 마켓플레이스</td>
            <td>[!DNL App Builder] 앱용 [Magento Marketplace](https://marketplace.magento.com/)(PHP 확장 기능) 및 [Exchange Marketplace](https://commercemarketplace.adobe.com)(권장)</td>
            <td>[!DNL App Builder] [[!DNL Exchange Marketplace]]의 앱(https://commercemarketplace.adobe.com)</td>
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
            <td>App Builder 상태 라이브러리(파일만 해당)<sup>2 - <a href="https://developer.adobe.com/app-builder/docs/guides/app_builder_guides/storage/database">App Builder용 데이터베이스 저장소</a>가 현재 조기 액세스 상태입니다.</sup></td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td colspan="3">
                SaaS의 <sup>1</sup> 데이터 모델 확장성은 B2B 엔터티를 포함하여 제품 및 고객 이상으로 <a href="https://developer.adobe.com/commerce/webapi/graphql/schema/attributes/mutations/">핵심 엔터티 확장</a>을 지원합니다. 하지만 업계별 데이터 모델(예: 딜러별 속성)에는 추가적인 아키텍처 고려 사항이 필요할 수 있습니다.
                <br><br>
                <sup>2</sup> Adobe은 SaaS에 대한 지속적인 스토리지 요구 사항을 해결하기 위해 문서 DB 통합 작업을 진행 중입니다. 현재 장기적인 데이터 스토리지가 필요한 구현에는 추가 인프라를 프로비저닝하고 유지해야 할 수 있습니다.
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
>- API 기능을 확장하려면 [!DNL API Mesh]을(를) 고려하십시오.
>- Adobe의 지속적인 플랫폼 발전 및 새로운 기능 릴리스를 모니터링합니다.
>- 사용 가능한 확장성 옵션과 비교하여 업종별 데이터 모델 요구 사항을 평가합니다.
>- 카탈로그 보기 및 정책을 기반으로 하는 [머천다이징 서비스](../optimizer/setup/catalog-view.md)를 채택해 보십시오.
