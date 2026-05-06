---
title: 통합 제한 및 경계
description: Commerce을 사용하는 LLM Optimizer에 대한 서드파티 카탈로그, 자동 수정 범위, 크롤링 사전 요구 사항, 엔터프라이즈 규모 고려 사항 및 제한된 베타 액세스 제한에 대해 알아봅니다.
role: Admin, User, Leader
recommendations: noCatalog
badgePaas: label="PaaS만" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce 온 클라우드 프로젝트(Adobe 관리 PaaS 인프라) 및 온프레미스 프로젝트에만 적용됩니다."
source-git-commit: 47348a44ff7c5f890c10594f44cae6e771be046f
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---

# 통합 제한 및 경계

>[!IMPORTANT]
>
>이 통합에 대한 액세스가 제한됩니다. 자세한 내용은 기술 계정 관리자에게 문의하십시오.

이 항목을 사용하여 [!DNL Adobe Commerce] 및 [!DNL Adobe LLM Optimizer] 통합이 자동화할 수 있는 사항, 책임감을 유지하는 위치 및 아직 진화하고 있는 제한 사항에 대한 기대를 설정하십시오.

## 타사 카탈로그 제한 사항 {#third-party-catalog}

카탈로그 **이(가) [!DNL Adobe Commerce]에 있지**&#x200B;않은 경우:

- LLM Optimizer은 설정에 따라 미러링되거나 가져온 카탈로그 데이터를 사용하여 문제를 식별하고 개선 사항을 제안할 수 있습니다.
- 상인의 상거래 플랫폼에 대한 **직접 자동 수정**&#x200B;은(는) 상인의 원본 카탈로그에 작성하는 것과 동일하지 않습니다. 변경 사항을 적용하려면 미러 카탈로그, 내보내기/가져오기 또는 파트너 자동화가 필요할 수 있습니다.

Commerce 호스팅 카탈로그의 경우 승인된 이름 및 설명 업데이트는 Commerce 기록 시스템으로 이동합니다. [Adobe Commerce과 함께 LLM Optimizer 사용](get-started/use-llmo-with-commerce.md)을 참조하세요.

## 확장 및 기술 제한 {#scale-limits}

큰 카탈로그와 높은 URL 수는 크롤링의 스트레스, 분석 및 에지 배포 패턴을 분석할 수 있습니다.

## 크롤링 및 봇 가독성 {#crawling}

의미 있는 카탈로그 및 PDP 인사이트는 LLM 관련 **봇이 중요한 URL에 액세스**&#x200B;할 수 있으며 자동 분석이 신뢰할 수 있도록 페이지가 구성되어 있다고 가정합니다. 로봇 규칙, 인증, 지리 차단 및 과도한 개인화를 통해 적용 범위를 줄일 수 있습니다.

## 관련 항목

- [통합 개요](overview.md)
- [Adobe Commerce을 LLM Optimizer에 연결](get-started/connect-to-llmo.md)
- [Adobe Commerce과 함께 LLM Optimizer 사용](get-started/use-llmo-with-commerce.md)
