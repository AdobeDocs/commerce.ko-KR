---
title: 온보딩
description: ' [!DNL Product Recommendations]에서 요구 사항 및 지원되는 플랫폼에 대해 알아봅니다.'
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 0%

---

# 온보딩

[!DNL Product Recommendations]에 대한 온보딩 프로세스는 서버의 명령줄에 액세스해야 하며 다음 단계로 구성됩니다. 명령줄 작업에 익숙하지 않은 경우 개발자 또는 시스템 통합자에게 도움을 요청하십시오.

- [구현 워크플로](implementation-workflow.md)
- [설치 및 구성](install-configure.md)
- [설정](settings.md)
- [확인](verify.md)
- [스테이징 환경](staging-environment.md)

## 요구 사항

- Adobe Commerce 2.4.4+
- PHP 8.1, 8.2
- 작성기 2

### 지원되는 플랫폼

- Adobe Commerce 온-프레미스(EE) : 2.4.4+
- ECE(Adobe Commerce on Cloud) : 2.4.4+

## 엔드포인트

[!DNL Product Recommendations]은(는) `https://catalog-service.adobe.io/graphql`의 끝점을 통해 통신합니다.

### 페이지 빌더 지원

[!DNL Product Recommendations]을(를) 페이지 빌더 콘텐츠 형식으로 페이지에 추가할 수 있습니다. 제품 권장 사항에 Page Builder 지원을 추가하려면 [설치 및 구성](install-configure.md)을 참조하세요.

[!DNL Page Builder] 콘텐츠에 [!DNL Product Recommendations]을(를) 추가하는 방법에 대한 지침은 [[!DNL Page Builder] 통합](page-builder.md)을 참조하세요.

### SaaS 가격 인덱싱

제품 추천 고객은 [SaaS 가격 인덱싱](../price-index/price-indexing.md)를 사용할 수 있으며, 이를 통해 가격 변경 업데이트 및 동기화 시간이 빨라집니다.

### B2B 지원 {#b2bsupport}

B2B 스토어프론트에는 각 쇼핑객 또는 고객 그룹에 대한 제품 가시성 및 가격을 지정하는 복잡한 논리가 필요한 경우가 많습니다. [!DNL Product Recommendations] 이제 [범주 권한](https://experienceleague.adobe.com/docs/commerce-admin/catalog/categories/category-permissions.html), [공유 카탈로그](https://experienceleague.adobe.com/docs/commerce-admin/b2b/shared-catalogs/catalog-shared.html) 및 [고객 그룹별 가격](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html)을 준수하여 이 기능을 [지원](release-notes.md)합니다. 예를 들어 소매 고객 세그먼트에서 특정 카테고리를 숨긴 경우 해당 세그먼트의 쇼핑객에게는 해당 카테고리의 제품에 대한 권장 사항이 표시되지 않습니다. 또한 특정 고객 그룹 및 회사에 대한 공유 카탈로그를 정의하면 해당 쇼핑객은 액세스할 수 있는 제품에 대한 추천만 볼 수 있습니다. 모든 추천 제품은 각 구매자의 고객 그룹에 따라 올바른 고객 그룹별 가격을 반영합니다.

>[!NOTE]
>
>판매자는 [카탈로그 서비스](../catalog-service/overview.md) 상점 첫 화면 API를 사용하여 위젯 또는 상점 첫 화면 요소를 사용자 지정하고 확장할 수 있지만 Adobe 지원 팀에서는 사용자 지정을 사용할 수 없습니다.
