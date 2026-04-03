---
title: '[!DNL Adobe Commerce Optimizer Connector] 릴리스 정보'
description: Adobe Commerce의  [!DNL Adobe Commerce Optimizer Connector] 에 대한 최신 릴리스 정보입니다.
feature: Services, Catalog Service, Release Notes
source-git-commit: 205fca38b379f94027a965b58826ffd922577f61
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# Adobe Commerce Optimizer Connector 릴리스 노트

이 릴리스 노트는 [!DNL Adobe Commerce Optimizer Connector]에 대한 모든 릴리스를 설명하며 다음을 포함합니다.

새 기능 ![개](../assets/new.svg)개
![해결된 문제](../assets/fix.svg) 수정 사항 및 개선 사항
![알려진 문제](../assets/bug.svg)알려진 문제

## 2026 릴리스

### 1.0.12 릴리스

_2026년 4월 2일_

![새로 만들기](../assets/new.svg) **`saas:resync` 명령에 범주 피드에 대한 지원이 추가되었습니다. **-이제 `saas:resync` CLI 명령을 사용하여 최신 범주 데이터를 쉽게 새로 고치고 볼 수 있습니다.

```terminal
bin/magento saas:resync --feed=categories
```

_2026년 3월 10일_

![문제 해결](../assets/fix.svg) Adobe Commerce Optimizer Connector가 Commerce 인스턴스에 설치된 경우 Commerce Admin System 및 Configuration 메뉴에서 Commerce Services Connector 구성 페이지에 대한 액세스를 차단하는 호환성 문제를 해결했습니다.  이제 두 확장이 모두 설치된 경우 Commerce 서비스 커넥터 구성 페이지에 액세스할 수 있습니다. <!--MDEE-1322-->


### v1.0.10 릴리스

_2026년 3월 9일_

![수정](../assets/fix.svg) 커넥터 구성을 완료하기 전에 데이터 피드 동기화 상태 페이지에 액세스하면 이제 자동으로 커넥터 구성 페이지로 리디렉션됩니다. 이 안내식 흐름을 사용하면 커넥터 설정이 완료되고 구성 설정 누락으로 인해 상태 항목이 실패하거나 불완전할 수 있는 오류를 방지할 수 있습니다.<!--MDEE-1296-->

### v1.0.9 릴리스

_2026년 3월 1일_

Adobe Commerce Optimizer 커넥터의 일반 가용성 릴리스입니다.

>[!NOTE]
>
>Adobe Commerce Optimizer Connector용 Beta 프로그램에 참여했고 이전 버전의 확장이 설치되어 있는 경우 일반 가용성 버전으로 업그레이드하여 최신 업데이트를 받으십시오.

