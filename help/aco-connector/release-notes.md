---
title: '[!DNL Adobe Commerce Optimizer Connector] 릴리스 정보'
description: 새로운 기능, 버그 수정, 카탈로그 동기화 및 내보내기에 대한 알려진 문제 등  [!DNL Adobe Commerce Optimizer Connector] 릴리스 정보에 대해 알아봅니다.
autotag-review: '2026-06-17T15:08:59.000Z'
feature: Release Notes
TQID: 'https://experienceleague.adobe.com/6NeLAfThvIWIyV4Y6OWtL8V9mC7lPy7UH-Zli8E-WEk'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2:
  - id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
subfeature_v2:
  - id: dad884f1-e840-49a1-970e-2f965bdbc410
  - id: a40ebd6b-b542-4432-a730-1803ef74518d
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 4eb33526927e1c5a81612aab0de0ce4bc7746368
workflow-type: tm+mt
source-wordcount: 366
ht-degree: 0%

---

# Adobe Commerce Optimizer Connector 릴리스 노트

이 릴리스 노트는 [!DNL Adobe Commerce Optimizer Connector]에 대한 모든 릴리스를 설명하며 다음을 포함합니다.

새 기능 ![개](../assets/new.svg)개
![해결된 문제](../assets/fix.svg) 수정 사항 및 개선 사항
![알려진 문제](../assets/bug.svg)알려진 문제

## 2026 릴리스

### 1.0.15 릴리스

_2026년 7월 10일_

![수정](../assets/fix.svg) 범주 피드에 정렬 지원을 추가했습니다. <!--MDEE-1409-->

### 1.0.14 릴리스

_2026년 6월 11일_

![수정](../assets/fix.svg) **PHP 8.5 호환성** - 이제 [!DNL Adobe Commerce Optimizer Connector]이(가) PHP 8.5를 지원하므로 커넥터 기능이나 카탈로그 동기화를 중단하지 않고 [!DNL Adobe Commerce] 환경을 업그레이드할 수 있습니다. <!--MDEE-1388-->

![수정](../assets/fix.svg) **통화 변경 후 가격 장부가 업데이트됨** - 업데이트된 가격은 통화 변경 후 Adobe Commerce Optimizer에 자동으로 반영됩니다. <!--MDEE-1384-->

![수정](../assets/fix.svg) **탐색에서 사용하지 않거나 숨겨진 상위 범주를 따릅니다** - 사용하지 않거나 숨겨진 범주 계층의 제품이 더 이상 탐색 경험에 예기치 않게 표시되지 않습니다.<!--MDEE-1385-->

![수정](../assets/fix.svg) **스테이징 업데이트 후 일관된 범주 URL** - 스테이징 업데이트가 적용된 후에도 범주 링크 및 탐색이 정확하게 유지됩니다. <!--MDEE-1395-->

### 1.0.13 릴리스

_2026년 5월 6일_

![수정](../assets/fix.svg) **향상된 [!DNL Adobe Commerce Optimizer Connector] 구성 지침** - _[!DNL Adobe Commerce Optimizer Connector]통합 가이드에 연결하도록 Commerce 관리자의 [!DNL Adobe Commerce Optimizer] 구성 페이지를 업데이트했습니다_.


![수정](../assets/fix.svg) **[!DNL Adobe Commerce Optimizer Connector]메타데이터 개선** - 이제 [!DNL Adobe Commerce Optimizer Connector]에 설치된 버전이 메타데이터 헤더에 포함됩니다. 이 개선 사항을 통해 팀은 문제 해결 또는 지원 참여 중에 사용 중인 커넥터 버전을 빠르게 식별할 수 있습니다.<!--MDEE-1323-->

### 1.0.12 릴리스

_2026년 4월 2일_

![새로 만들기](../assets/new.svg) **`saas:resync` 명령에 범주 피드에 대한 지원이 추가되었습니다**-이제 `saas:resync` CLI 명령을 사용하여 최신 범주 데이터를 쉽게 새로 고치고 볼 수 있습니다.

```shell
bin/magento saas:resync --feed=categories
```

### 1.0.11 릴리스

_2026년 3월 10일_

![문제 해결](../assets/fix.svg) [!DNL Adobe Commerce Optimizer Connector]이(가) [!DNL Adobe Commerce] 인스턴스에 설치된 경우 Commerce 관리 **[!UICONTROL System]** 및 **[!UICONTROL Configuration]** 메뉴에서 [!DNL Commerce Services Connector] 구성 페이지에 대한 액세스를 차단하는 호환성 문제를 해결했습니다.  이제 두 확장이 모두 설치되면 [!DNL Commerce Services Connector] 구성 페이지에 액세스할 수 있습니다. <!--MDEE-1322-->


### 1.0.10 릴리스

_2026년 3월 9일_

![수정](../assets/fix.svg) 커넥터 구성을 완료하기 전에 **[!UICONTROL Data Feed Sync Status]** 페이지에 액세스하면 이제 자동으로 커넥터 구성 페이지로 리디렉션됩니다. 이 안내식 흐름을 사용하면 커넥터 설정이 완료되고 구성 설정 누락으로 인해 상태 항목이 실패하거나 불완전할 수 있는 오류를 방지할 수 있습니다.<!--MDEE-1296-->

### v1.0.9 릴리스

_2026년 3월 1일_

[!DNL Adobe Commerce Optimizer Connector]의 일반 가용성 릴리스입니다.

>[!NOTE]
>
>[!DNL Adobe Commerce Optimizer Connector]에 대한 Beta 프로그램에 참여했으며 이전 버전의 확장이 설치되어 있는 경우 일반 가용성 버전으로 업그레이드하여 최신 업데이트를 받으십시오.
