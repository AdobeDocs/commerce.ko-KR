---
title: 레벨 2 및 레벨 3 처리
description: ' [!DNL Payment Services] 거래 내의 카드 결제 처리 수준입니다.'
role: Admin
feature: Payments, Paas, Saas
exl-id: db8993fe-dd6f-48b5-9e7b-69a0f2e08552
source-git-commit: 870c2497a2d6dcfc4066c07f20169fc9040ae81a
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 0%

---

# 레벨 2 및 레벨 3 처리

[!DNL Payment Services]은(는) 상인이 결제 거래를 최적화하고 교환 수수료를 낮출 수 있도록 고급 카드 처리 기능을 제공합니다. 각각 다른 거래 데이터 요구 사항을 가진 세 가지 수준의 카드 처리를 사용할 수 있습니다.

>[!CAUTION]
>
> [Fastlane](payments-options.md#fastlane-button) 주문에는 레벨 2/레벨 3 데이터, 라인 항목 및 금액 분류가 포함되지 않습니다.

## 처리 수준별 데이터 요구 사항

![트랜잭션 보고서](assets/level-processing-details.png){width="500" zoomable="yes"}

[!DNL Payment Services]에서 이 데이터를 수집하고 결제 거래에 대한 자세한 보고를 제공합니다.

## 카드 네트워크별 사용 가능한 처리 수준

![카드 세부 정보](assets/cards-details-level-processing.png){width="500" zoomable="yes"}

자세한 내용은 PayPal 개발자 설명서에서 [결제 처리](https://developer.paypal.com/docs/checkout/advanced/processing/){target=_blank}를 참조하십시오.

### 레벨 1

레벨 1이 가장 일반적이고, 필요한 정보가 적기 때문에 일반적으로 기업 및 구매 신용카드와 관련된 레벨 2 또는 레벨 3 데이터로 처리된 거래에 비해 높은 교환 수수료가 발생합니다.

### 레벨 2 및 레벨 3

Interchange Plus(IC++)의 [!DNL Payment Services] 가맹점은 카드 네트워크에 추가 거래 세부 정보를 제공하고 특정 자격 기준을 충족하는 경우 레벨 2/레벨 3 처리 자격을 얻을 수 있습니다. 이러한 수준은 상당한 구매 또는 법인 카드 볼륨을 처리하는 가맹점에 특히 유용합니다. 그 결과 상당한 비용 절감이 발생할 수 있기 때문입니다. 자세한 레벨 2 또는 레벨 3 데이터를 제공하면 다음과 같은 작업을 수행할 수 있습니다.

* 처리 비용 절감 및 전체 비용 최적화
* 사기 방지, 프로세서 위험 감소
* 트랜잭션 보안 강화

[IC란++? 참조자세한 내용은 PayPal 개발자 설명서의 &#x200B;](https://www.paypal.com/us/brc/article/what-is-interchange-plus-plus){target=_blank}을 참조하십시오.

## [!DNL Payment Services]의 레벨 2 및 레벨 3 카드 결제 거래

레벨 2 또는 레벨 3 처리의 자격을 얻으려면 상인은 이전 정보를 전송해야 하지만, 카드 네트워크가 거래를 처리할 때 최종적으로 어느 레벨에 자격이 있는지를 결정합니다.

자세한 내용은 PayPal 개발자 설명서에서 [결제 처리 FAQ](https://www.paypal.com/us/cshelp/article/ts2278?_ga=1.131773126.875104296.1712843492){target=_blank}를 참조하십시오.

매장 수준의 [!DNL Payment Services] 가맹점에 대해 기본적으로 수준 2 및 수준 3 처리가 비활성화되어 있습니다.

이미 IC++ 가격을 사용하고 있다면 레벨 2 및 레벨 3 처리를 사용할 수 있습니다. 이 기능을 사용하려면 [명령줄 인터페이스(CLI](configure-cli.md))를 통해 이 작업을 수행할 수 있습니다.

>[!IMPORTANT]
>
>질문이 있는 경우 [!DNL Payment Services] 계정 관리자에게 문의하십시오.
