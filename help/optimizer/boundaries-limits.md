---
title: 경계 및 제한
description: ' [!DNL Adobe Commerce Optimizer]의 경계 및 제한에 대해 알아봅니다.'
role: Admin, Developer
badgeSaas: label="SaaS만" type="Positive" url="https://experienceleague.adobe.com/ko/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."
source-git-commit: 553490762ef10e43ccce1654acec59aeb83bb5f9
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# 경계 및 제한

다음은 [!DNL Adobe Commerce Optimizer]의 경계 및 제한을 제공합니다.

## 카탈로그

- 카탈로그 수집의 보장 비율은 1000개 제품/분 및 5000개 가격/분입니다.
- 하루 제품 업데이트의 기본 수는 1,000,000개입니다.
- 단일 인스턴스에 허용되는 총 SKU 수는 250,000개입니다. 
- 카탈로그 소스의 최대 수는 50개입니다.
- 제품당 변형 수는 10,000개입니다.
- 제품 크기는 200kb를 초과할 수 없습니다.

## 가격

- 가격 장부의 최대 개수는 1,000개입니다.

## 제품 검색 및 상점

- 단일 검색 요청이 반환할 수 있는 제품 수는 100개입니다.
- 필터링 가능한 속성의 최대 수는 200개입니다.
- 검색 가능한 속성의 최대 수는 200개입니다.
- 정렬 가능한 속성의 최대 수는 50개입니다.
- 최대 패싯 수는 100개입니다. 모든 면은 필터링 가능한 속성이어야 합니다.
- 단일 Facet Cat이 반환하는 최대 옵션 수는 100개이며, 지원 요청당 늘릴 수 있습니다.

## 카탈로그 보기 및 정책

- 테넌트당 최대 카탈로그 보기 수는 1000개입니다.
- 하나의 카탈로그 보기에 할당된 최대 정책 수는 10개입니다.
- 정책에 사용되는 최대 속성 값 수는 100개입니다. 

## 권장 사항

- 카테고리 또는 속성 포함 또는 제외를 지원하지 않습니다.
- [!DNL Adobe Commerce Optimizer]에서 권장 사항을 미리 볼 수 없습니다.
