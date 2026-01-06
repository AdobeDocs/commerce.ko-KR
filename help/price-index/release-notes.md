---
title: '[!DNL Catalog Adapter] 릴리스 정보'
description: Adobe Commerce의  [!DNL Catalog Adapter] 에 대한 최신 릴리스 정보입니다.
feature: Services, Release Notes
recommendations: noCatalog
roles: Admin, Developer
exl-id: d4dd0288-8853-43fe-9103-1aead8d3b56e
source-git-commit: 47419e7e19611dc4a045c195f259e2126ab77372
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# [!DNL Catalog Adapter] 확장 릴리스 노트

이 릴리스 노트는 [!DNL Catalog Adapter] 확장의 최신 버전에 대해 설명합니다. 현재 주요 릴리스 버전에 대한 지원이 제공됩니다. 이전 버전에 대한 릴리스 노트는 참조를 위해 제공됩니다.

업데이트에는 다음이 포함됩니다.

새 기능 ![개](../assets/new.svg)개
![수정](../assets/fix.svg) 수정 사항 및 개선 사항
![버그](../assets/bug.svg) 알려진 문제


>[!NOTE]
>
>[카탈로그 어댑터 확장](catalog-adapter.md)이(가) Adobe Commerce 가격 인덱싱을 사용하지 않도록 설정합니다. 설치한 경우 composer를 사용하여 시스템에 설치된 버전을 확인할 수 있습니다. 경우에 따라 Commerce 서비스 버전을 업데이트하지 않고 시스템에서 카탈로그 어댑터 확장을 업그레이드하여 수정 사항이나 새 기능을 선택할 수 있습니다.

## 현재 메이저 버전

## 1.0.10 릴리스

![수정](../assets/fix.svg) 시스템이 올바른 유효한 SKU 대신 조회에 연결된 SKU를 사용하려고 시도했기 때문에 가져온 또는 새로 만든 번들 제품의 가격 쿼리로 인해 내부 서버 오류가 발생할 수 있는 문제가 수정되었습니다. 이제 번들 제품의 가격 쿼리가 적절한 SKU를 사용하며 올바르게 해결됩니다.<!--MDEE-1040-->

## 1.0.9 릴리스

![수정](../assets/fix.svg) PHP 8.4에 대한 호환성을 추가했습니다. <!--MDEE-941-->

## 1.0.8 릴리스

![수정](../assets/fix.svg) 숫자 SKU를 사용하는 구성 가능한 제품 변형을 위시리스트에 추가할 때 예외 로그에 오류가 발생하는 문제를 해결했습니다. <!--MDEE-876-->
