---
title: Commerce 설명서 거버넌스
description: Commerce Insights의 내부 거버넌스 모델에 대해 알아봅니다. Experience League에 게시되지 않음 - 의도적으로 TOC.md에서 누락되었습니다.
source-git-commit: 1da6d9753acbeadf3a0df5fae86a9386643c6d6d
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---


# Commerce 설명서 거버넌스

설명서 팀의 내부 참조입니다. `TOC.md`에 나열되어 있지 않으므로 빌드되거나 Experience League에 게시되지 않습니다. 제어하는 콘텐츠에 가깝게 유지되도록 여기에 보관하십시오.

## 소유권

Commerce Insights 문서는 문서 정확도 및 통화 유지를 담당하는 게시 작성자 또는 팀이 소유합니다. 이러한 문서는 현재 `commerce.en` 리포지토리에서 호스팅됩니다. Commerce 설명서 팀은 콘텐츠 품질을 보장하고 문서를 프로덕션에 게시하는 데 도움이 됩니다.

## Commerce Insights의 속성

- **여기에 속함**: 실제 시나리오를 기반으로 구현 지침을 다루는 Commerce 솔루션에 대한 전략적 지침 및 백서. 지원을 위해 관련 Commerce 설명서 페이지에 대한 링크를 포함합니다.

- **대신 제품 리포지토리에 속함**: 단계별 구성, 튜토리얼, 참조 자료(API/CLI/config 참조) 및 문제 해결. 여기에서 게시물이 이러한 종류의 세부 정보를 누적하기 시작하는 경우 해당 제품 안내서로 이동하고 대신 링크하십시오.

## 새 콘텐츠 추가

게시할 문서에 대한 COMDOX JIRA 티켓을 만듭니다. 티켓 설명에 `[templates/comdox-intake-template.md](templates/comdox-intake-template.md)`을(를) 복사하고 채우십시오. 이 요청은 요청자에게 대상을 식별하고, 콘텐츠가 임시적인지(만료 날짜가 있음) 플래그를 지정하고, 콘텐츠가 Commerce 제품 설명서가 아닌 Insights 가이드에 속하는지 확인합니다.

티켓의 범위가 지정되면 `templates/`의 템플릿에서 문서를 시작하십시오(`whitepaper-template.md`, `security-guidance-template.md`, `insight-perspective-template.md`—게시되지 않음, 관련 파일을 대상 파일에 복사하고 템플릿의 자체 frontmatter 자리 표시자 주석을 삭제하십시오). 콘텐츠를 게시할 준비가 되면 `TOC.md` 항목을 추가하십시오.

- **새로운 최상위 섹션**(예: 인사이트 > 카탈로그 관리)은 가이드의 탐색 모양을 변경하므로 추가하기 전에 IA 검토가 필요합니다. 스토리나 작업에 대한 Commerce IA 리뷰를 소유하고 있는 모든 사용자를 반복합니다.

- **TOC에 추가** - 게시하기 전에 TOC에 새 주제를 추가합니다. 필요한 경우 메타데이터 숨김을 사용하여 링크가 있는 사용자만 액세스할 수 있는 숨겨진 문서를 게시합니다. ExL 작성자 안내서의 [콘텐츠 숨기기](https://experienceleague.adobe.com/en/docs/authoring-guide/using/authoring/hiding-files)를 참조하십시오.

## 케이던스 검토

새 Commerce 솔루션의 이름이 변경되거나 업데이트되거나 통찰력이 더 이상 관련이 없는 경우 문서 콘텐츠를 검토하십시오.
