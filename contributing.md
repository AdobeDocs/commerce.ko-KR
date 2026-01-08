---
source-git-commit: 4ddab6bbd62a3cc7c6dff089745c1b5ef5c20f70
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 1%

---
# 기여

기여해 주셔서 감사합니다!

다음은 이 프로젝트에 기여할 때 따라야 할 지침입니다.

## 행동 수칙

이 프로젝트는 Adobe [수행 코드](code-of-conduct.md)를 준수합니다. 참여함으로써,
이 코드를 준수해야 합니다. 부적절한 행동 보고 대상
[Grp-opensourceoffice@adobe.com](mailto:Grp-opensourceoffice@adobe.com).

## 기여자 안내서 설명서

[기여자 안내서](https://experienceleague.adobe.com/docs/contributor/contributor-guide/introduction.html)를 참조하세요.

## 질문이 있습니까?

문제 제기를 시작하십시오. 이 프로젝트에 대한 기존 기여자는 다음 위치에 도달해야 합니다.
필요한 경우 문제 스레드 내에서 프로젝트 방향 및 문제 솔루션에 대한 합의.

## 기여자 라이선스 계약

이 프로젝트에 대한 모든 타사 기여도는 서명된 기여자를 동반해야 합니다
사용권 계약. 이를 통해 Adobe에 기여도를 재배포할 수 있는 권한을 부여합니다
을 프로젝트의 일부로 사용합니다. [CLA에 서명](https://opensource.adobe.com/cla.html)하세요. 본인
Adobe CLA를 한 번만 제출하면 됩니다. 이전에 제출한 적이 있다면,
가도 좋다!

## 코드 검토

모든 제출 사항은 끌어오기 요청 양식으로 제출해야 하며 검토해야 합니다
프로젝트 기여자별. [GitHub의 끌어오기 요청 설명서](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests) 읽기
끌어오기 요청 전송에 대한 자세한 내용.

마지막으로 다음과 같은 경우 [가져오기 요청 템플릿](PULL_REQUEST_TEMPLATE.md)을(를) 따르십시오.
가져오기 요청을 제출하는 중입니다!

## 참여자에서 커미터로

커뮤니티의 콘텐츠 제공이 좋습니다! 참여자를 넘어 한 걸음 더 나아가고 싶다면
프로젝트에서 전체 쓰기 액세스 권한과 발언권을 가진 커미터가 되려면
프로젝트에 초대를 받습니다. 기존 기여자는 내부 지정을 사용합니다
초대 전에 소극적 합의(침묵이 승인)에 도달해야 하는 프로세스
발급되었습니다. 당신이 자격이 있다고 생각하고 더 깊이 관여하고 싶다면
이 문제에 대해 대화하기 위해 기존 기여자에게 언제든지 연락하십시오.

## 보안 문제

보안 문제를 보고하려면 [보안 전문가에게 문제를 제출하세요](https://helpx.adobe.com/security/alertus.html).

## 새로운 기능

변경 사항으로 인해 강조 표시해야 하는 새로운 주제, 중요한 업데이트 또는 수정 사항이 있는 경우 끌어오기 요청 본문에서 바로 [새로운 기능 섹션](https://experienceleague.adobe.com/en/docs/commerce/user-guides/home#whats-new)에 간단한 설명을 추가할 수 있습니다.

새로운 기능 강조 표시를 추가하려면:

1. 끝에 적절한 설명이 있는 `whatsnew` 태그를 끌어오기 요청 본문에 포함하십시오. 설명은 변경에 대한 컨텍스트와 대상 주제 링크를 제공해야 합니다. 다음 형식을 사용하십시오(코드 블록 인용은 표시용으로만 사용되며, 가져오기 요청 본문에 포함하지 않음).

   ```text
   whatsnew
   Short description of the change in the [target topic](https://experienceleague.adobe.com/en/docs/commerce/target-topic.html).
   ```

   또는 여러 주제가 있는 경우:

   ```text
   whatsnew
   Short description of the changes in the [first target topic](https://experienceleague.adobe.com/en/docs/commerce/target-topic.html), [second target topic](https://experienceleague.adobe.com/en/docs/commerce/second-target-topic.html), and [third target topic](https://experienceleague.adobe.com/en/docs/commerce/third-target-topic.html).
   ```

   여러 강조 표시에 목록을 사용할 수도 있습니다.

   ```text
   whatsnew
   - Short description of the first change in the [first topic](https://experienceleague.adobe.com/en/docs/commerce/first-topic.html).
   - Short description of the second change in the [second topic](https://experienceleague.adobe.com/en/docs/commerce/second-topic.html).
   ```

   ```text
   whatsnew
   The following changes were made to the documentation:
   - Short description of the first change in the [first topic](https://experienceleague.adobe.com/en/docs/commerce/first-topic.html).
   - Short description of the second change in the [second topic](https://experienceleague.adobe.com/en/docs/commerce/second-topic.html).
   ```

1. 변경 유형을 나타내는 지원되는 레이블을 추가합니다. 지원되는 레이블에는 다음과 같은 각 변경 유형에 대한 레이블이 포함됩니다.

   - `new-topic` - 새 주제
   - `major-update` - 콘텐츠, 구조 또는 기능에 중요한 변경 내용이 포함될 수 있는 주요 업데이트용
   - `technical` - 주요 업데이트로 간주되지 않지만 주의가 필요한 기술 변경

**중요:**

1. `whatsnew` 파트는 `whatsnew` 태그에서 시작하여 끌어오기 요청 본문의 맨 끝에 있어야 합니다.
1. 변경 사항에 대한 설명에는 작업 링크가 포함되어야 합니다. 링크가 올바르고 의도한 주제로 이어졌는지 확인하십시오. 새로운 항목인 경우 끌어오기 요청을 병합하고 새 항목을 게시한 후 링크가 작동하는지 확인하십시오. 끌어오기 요청이 병합된 후에 링크를 수정해도 됩니다.

예를 들어, 저장소에서 닫힌 끌어오기 요청을 검색하여 기존 하이라이트의 서식을 확인하고, 이를 [새로운 기능 섹션](https://experienceleague.adobe.com/en/docs/commerce/user-guides/home#whats-new)과 비교하여 설명서에 어떻게 표시되는지 확인하십시오.
