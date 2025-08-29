---
source-git-commit: 39977196f322cac571ecdb0219f006970aff3575
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 5%

---
# Adobe Commerce 기술 설명서

커뮤니티의 콘텐츠 제공과 설명서 팀 외부 Adobe 직원의 콘텐츠 제공도 환영합니다.

## Adobe Open Source 행동 수칙

이 프로젝트에서는 [Adobe OOCT(Open Source Code of Conduct)](code-of-conduct.md) 또는 [.NET Foundation Code of Conduct](https://dotnetfoundation.org/code-of-conduct)가 채택되었습니다. 자세한 내용은 [기여](contributing.md) 문서를 참조하십시오.

## Adobe 콘텐츠에 대한 귀하의 기여 관련 정보

[Adobe 문서 기여자 안내서](https://experienceleague.adobe.com/docs/contributor/contributor-guide/introduction.html)를 참조하세요.

기여 방식은 기여자 및 기여 하고자 하는 변경 사항의 종류에 따라 다릅니다.

### 사소한 변경 사항

부분 업데이트에 기여하는 경우 문서를 방문하여 문서 하단에 나타나는 피드백 영역을 클릭하고 **자세한 피드백 옵션**&#x200B;을 클릭한 다음 **편집 제안**&#x200B;을 클릭하여 GitHub의 Markdown 소스 파일로 이동하십시오. GitHub UI를 사용하여 업데이트를 만듭니다. 자세한 내용은 일반 [Adobe 문서 기여자 안내서](https://experienceleague.adobe.com/docs/contributor/contributor-guide/introduction.html)를 참조하십시오.

이 저장소의 설명서 및 코드 샘플에 대해 사용자가 제출하는 부분 수정 또는 설명은 Adobe 사용 약관의 적용을 받습니다.

### 커뮤니티 구성원의 주요 변경 사항 또는 새 문서

Adobe 커뮤니티에 소속되어 있고 새 문서를 만들거나 주요 변경 사항을 제출하려는 경우 Git 리포지토리의 문제 탭을 사용하여 문제를 제출하면 설명서 팀과 대화를 시작할 수 있습니다. 플랜에 동의하면 직원과 협력하여 공용 및 개인 리포지토리에서 작업을 결합하여 새로운 콘텐츠를 제공할 수 있습니다.

### Adobe 직원의 주요 변경 사항

Adobe Experience Cloud 솔루션에 대한 제품 팀의 테크니컬 라이터, 프로그램 관리자 또는 개발자이고 기술 문서에 기여하거나 기술 문서를 작성하는 것이 본인의 직무인 경우 개인 리포지토리(`https://git.corp.adobe.com/AdobeDocs`)를 사용해야 합니다.

## 도구 및 설정

커뮤니티 기여자는 기본 편집에 GitHub UI를 사용하거나 리포지토리를 포크하여 크게 기여할 수 있습니다.

자세한 내용은 [Adobe 문서 기여자 안내서](https://experienceleague.adobe.com/docs/contributor/contributor-guide/introduction.html)를 참조하십시오.

## Markdown을 사용하여 주제 서식을 지정하는 방법

이 저장소의 모든 문서는 GitHub 버전의 Markdown을 사용합니다. Markdown에 익숙하지 않은 경우 다음을 참조하십시오.

- [Markdown 기본 사항](https://help.github.com/articles/getting-started-with-writing-and-formatting-on-github/)
- [인쇄 가능한 Markdown 치트시트](https://guides.github.com/pdfs/markdown-cheatsheet-online.pdf)

## 이미지 최적화를 위한 사전 커밋 후크

이 저장소에는 커밋하기 전에 이미지를 최적화하는 자동화된 사전 커밋 후크가 포함됩니다. **일관된 이미지 최적화와 저장소 크기를 줄이려면 모든 기여자가 이러한 후크를 사용하도록 설정해야 합니다**.

### 빠른 설정

저장소를 복제한 후 다음을 실행합니다.

```bash
.githooks/setup-hooks.sh
```

### 후크가 수행하는 작업

- 스테이징된 이미지 파일(PNG, JPG, JPEG, GIF, SVG) 자동 감지
- `image_optim`을(를) 실행하여 이미지 압축 및 최적화
- 최적화된 이미지 자동 재스테이지
- 커밋된 모든 이미지가 올바르게 최적화되었는지 확인

### 이점

- 저장소 크기 감소
- 설명서를 위한 빠른 페이지 로드
- 모든 기여자에서 일관된 이미지 품질
- 수동 최적화 불필요

자세한 설정 지침, 문제 해결 및 구성은 [`.githooks/README.md`](.githooks/README.md)을(를) 참조하십시오.
