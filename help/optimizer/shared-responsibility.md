---
title: 공동 책임
description: ' [!DNL Adobe Commerce Optimizer]  프로젝트에 관련된 각 당사자의 보안 책임에 대해 알아봅니다.'
role: Admin, Architect, Leader
badgeSaas: label="SaaS만" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."
source-git-commit: 7c407bfc2becfb0ba6babe5958bcb790c178f406
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# 공동 책임 보안 및 운영 모델

>[!BEGINSHADEBOX]

다음 요약 테이블은 RACI 모델을 사용하여 Adobe과 고객 간에 공유된 보안 책임을 보여 줍니다.

**R** — 담당
**A** — 책임 있음
**C** — 참조됨
**I** — 알림

>[!ENDSHADEBOX]

| 작업 | Adobe | 고객 |
| --- | --- | --- |
| Adobe Commerce 인프라 패치 적용 | RA | |
| 지원 서비스에 패치 적용 | RA | |
| 백엔드 원본 WAF 규칙 정의 | RA | |
| 백엔드 CDN WAF 규칙 정의 | RA | |
| 백엔드 플랫폼 WAF 규칙 배포 | RA | |
| 백엔드 CDN WAF 규칙 배포 | RA | |
| [!DNL Adobe Commerce Optimizer]에서 버그를 수정하는 중 | RA | I |
| [!DNL Adobe Commerce Optimizer]인프라 패치 릴리스 중 | RA | |
| 확장(인프라) | RA | I |
| 외부 애플리케이션 통합 | | RA |
| App Builder 앱 설치 | | RA |
| 모든 App Builder 앱의 성능 테스트 | | RA |
| 사용자 지정 App Builder 앱의 테마 설정 및 디자인 | | RA |
| 백엔드 DNS 구성 | RA |  |
| 온보딩 백엔드 CDN | RA |  |
| 백엔드 CDN 지원 | RA |  |
| 백엔드 DNS 공급자 가져오기 | RA | |
| 프로덕션 및 샌드박스 환경 프로비저닝 | A | R |
| Adobe Commerce Optimizer용 Dynamics 액세스 | R | C |
| 백엔드 고객 보안 문제 해결 | RA | I |
| 백엔드 CDN 보안 문제 해결 | RA | |
| Adobe의 보안 조사 지원(스캔/감사) | RA | |
| PCI ASV 스캔 수행 | RA | I |
| Adobe Commerce Optimizer 인프라 PCI 스캔 수정 | R | |
| OS 및 플랫폼 비밀 관리 | RA | |
| 백엔드 보안 로그 모니터링 | RA | |
| 고객 지원 및 액세스 제어 | A | R |
| Adobe DR 계획 및 백업 및 복원의 연간 테스트 및 문서화 | RA | |
| 연간 재해 복구 계획 테스트 및 문서화 | RA | |
| 디버깅 및 문제 격리 | R | R |
| 디버깅 및 문제 격리 프로세스를 적시에 지원 | R | R |
| Adobe Commerce Optimizer에 업데이트 및 패치 설치 | RA | I |
| 핵심 Adobe Commerce Optimizer 애플리케이션 품질 | RA | |
