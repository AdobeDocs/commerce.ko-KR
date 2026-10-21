---
title: Commerce 정보 센터 거버넌스
description: Commerce 정보 센터의 내부 거버넌스 모델에 대해 알아봅니다. Experience League에 게시되지 않았습니다.
source-git-commit: a91925091da28cd0745923894a3faab0374f0a0c
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 0%
---

# Commerce 정보 센터 거버넌스

설명서 팀에 대한 이 내부 참조는 `TOC.md`에 나열되지 않으므로 Adobe Experience League에 게시되지 않습니다.

## 소유권

Adobe Commerce 설명서 팀은 정보 센터를 소유합니다. `metadata.md`에 `git-repo`(으)로 나열된 리포지토리인 `Adobe-Enterprise-Docs/commerce.en`에서 작성되었습니다.

교차 제품이기 때문에 단일 제품 팀이 소유하지 않습니다. 여기에서 수정하는 대신 소유 제품 팀의 문서 연락처에 대한 제품별 수정 사항을 에스컬레이션하십시오.

## 인포메이션 센터에 있는 것

| 여기에 속함 | 제품 저장소에 속함 |
| --- | --- |
| 제품 선택 지침, 제품 간 구현 여정, 아키텍처 패턴 및 백서와 같이 둘 이상의 제품 또는 서비스에 적용되는 콘텐츠 | 단계별 구성, API/CLI/구성 참조 및 문제 해결 등 단일 제품 콘텐츠 |
| 신뢰할 수 있는 제품 문서에 연결되는 짧은 큐레이션 페이지 | |

- 여기에 페이지에 단일 제품 세부 사항이 누적되어 있는 경우 제품 안내서로 이동하고 링크를 클릭하십시오.
- 정보 센터는 제품 설명서를 통합하거나 마이그레이션하지 않으며 개별 제품 기능을 문서화하지 않습니다. 새로운 내용을 작성하기 전에 기존의 신뢰할 수 있는 콘텐츠에 연결합니다.

## 새 콘텐츠 추가

### 기존 섹션의 문서

1. 섹션과 일치하는 폴더에 파일을 추가합니다.
1. 해당 섹션 아래의 `TOC.md`에 항목을 추가합니다.

일반적인 PR 검토 이후로는 승인이 필요하지 않습니다.

| 목차 섹션 | 폴더 |
| --- | --- |
| Commerce 플랫폼 및 서비스 살펴보기 | `portfolio/`, `storefronts/`, `aem-assets/`, `apis/` |
| 역할별 시작 | `get-started/` |
| 통찰력 및 지침 | `guidance-and-insights/` |
| 아키텍처 | `architecture-options/` |
| 마이그레이션 및 채택 | `migration-adoption/` |
| 구현 안내서 | `implementation-guides/` |

### 인사이트 및 지침 문서

1. `guidance-and-insights/templates/`에서 `guidance-and-insights/`(으)로 `whitepaper-template.md` 또는 `security-guidance-template.md`을(를) 복사합니다. 템플릿이 게시되지 않습니다. COMDOX 접수 티켓을 포함한 전체 작성 프로세스는 [readme.md](guidance-and-insights/readme.md)을(를) 참조하십시오.
1. 템플릿의 자리 표시자 주석을 삭제합니다.
1. 콘텐츠를 게시할 준비가 되면 인사이트 및 지침 아래에 `TOC.md` 항목을 추가합니다.

### 최상위 섹션

`TOC.md`의 새 최상위 그룹이 가이드의 탐색을 변경하므로 IA 검토가 필요합니다. Commerce IA 리뷰를 소유한 사람에게 문의하십시오. 파트너 또는 지원 콘텐츠의 역할별 시작과 같이 기존 섹션을 먼저 재사용합니다.

### 게시된 URL

URL은 안내서 ID, `TOC.md`의 섹션 ID(예: `{#insights-and-guidance}`) 및 파일 이름에서 작성됩니다. 폴더 이름이 URL에 표시되지 않습니다. 각 섹션에 고유 ID를 지정하고 두 문서가 동일한 URL로 확인되지 않도록 합니다.

## 케이던스 검토

- **이벤트 기반** - Commerce 제품의 이름이 바뀌거나, 시작되거나, 사용이 중단되거나, 제품의 가용성이 변경되는 경우 Commerce 플랫폼 및 서비스 탐색, 역할별 시작, 아키텍처, 마이그레이션 및 채택, 구현 안내서 섹션을 검토하십시오. 예를 들어 Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer이 통합되는 경우 검토하십시오. 이러한 페이지는 먼저 오래된 페이지가 됩니다.
- **예약됨** - 오래된 용어, 브랜딩 또는 기술적인 부정확성을 확인하려면 6개월마다 자동화된 콘텐츠 감사 및 검토를 실행하십시오.

## 도움말/랜딩/

`help/landing/`(&quot;Adobe Commerce 서비스 안내서&quot;)은 정보 센터에 속하지 않는 별도의 안내서입니다. Catalog Service, Live Search, Product Recommendations 및 Payment Services와 같은 Commerce 서비스에 중점을 두고 있으며, 자세한 내용은 정보 센터에서 링크를 통해 확인할 수 있습니다. 이 두 가지를 다시 처리하거나 통합하는 것은 이 안내서가 해결하지 못하는 후속 결정입니다.
