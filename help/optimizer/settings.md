---
title: 설정
description: ' [!DNL Adobe Commerce Optimizer]에 대한 설정을 구성합니다.'
badgeSaas: label="SaaS만" type="Positive" url="https://experienceleague.adobe.com/ko/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."
source-git-commit: 3020386cd051b4453ed6b90d2c694a5bb31dfb24
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---

# 설정

*설정* 작업 영역을 사용하여 가격 패싯 범위 및 간격과 제품 검색에 대한 기본 언어를 구성하십시오.

가격 팩시팅은 가격 범위 그룹의 수와 가격 값이 이들 그룹 간에 분배되는 방식을 지정합니다.

**언어** 설정은 인덱스를 작성할 때 예상할 언어를 [!DNL Adobe Commerce Optimizer]에 알려줍니다.

## 가격 결정

가격 범위 그룹의 수와 가격 값이 이들 그룹 간에 분배되는 방법을 지정할 수 있습니다. 각 가격대는 이전 그룹과 하나씩 겹칩니다. 예를 들어 간격이 20인 5개의 그룹은 0-20, 20-40, 40-60, 60-80 및 >80의 가격 범위를 생성합니다. 카탈로그에 정의된 모든 범위를 채울 제품이 충분하지 않은 경우 사용 가능한 그룹의 표시가 적절하게 조정됩니다. 예: 0-20, 60-80, >80.

1. **설정** 작업 영역에서 **[!UICONTROL Search]**&#x200B;을(를) 선택한 다음 **가격 결정**&#x200B;에서 다음을 수행합니다.
   - 사용할 수 있는 **선택 항목 수** 또는 가격 그룹화를 입력하십시오. 최대 50개의 가격 그룹화를 정의할 수 있습니다.
   - **간격 값** 또는 각 그룹의 가격 범위를 입력하십시오. 최대값은 40,000,000입니다.
1. **저장**&#x200B;을 클릭합니다.

   상점에서 업데이트된 설정을 사용할 수 있기까지는 약 15분이 소요됩니다.

### 필드 설명

| 필드 | 설명 |
|--- |--- |
| 선택 항목 수 | 상점 첫 화면에서 검색 필터로 사용할 수 있는 가격 범위 그룹화 수를 지정합니다. 기본값: 8, 최대값: 50 |
| 간격 값 | 각 그룹의 가격 범위 간격을 지정합니다. 예를 들어 간격 값이 20인 5개의 선택 항목을 선택하면 0-20, 20-40, 40-60, 60-80 및 >80의 5개 그룹이 생성됩니다. 기본값: 5, 최대값: 40,000,000 |

## 언어

언어 설정은 카탈로그를 읽고 색인을 작성할 때 예상할 언어를 [!DNL Adobe Commerce Optimizer]에 알려줍니다.

언어에는 문법에 대한 다양한 규칙 세트, 예를 들어 단어 분리 방법, 동사 문장 및 단어 형태가 있습니다.
언어 설정을 사용하면 색인화 메커니즘에 올바른 규칙 집합이 적용됩니다.

언어 설정을 카탈로그의 기본 언어로 설정합니다. 색인의 언어를 변경할 때 카탈로그의 크기와 복잡성에 따라 상점 변경 사항을 반영하는 데 5분에서 60분이 걸릴 수 있습니다.

| 언어 | 코드 |
|----|----|
| 아랍어 | ar |
| 아르메니아어 | hy |
| 바스크어 | eu |
| 벵골어 | bn |
| 브라질어 | pt-br |
| 불가리아어 | bg |
| 카탈로니아어 | ca |
| 중국어(간체) | zh-cn |
| 중국어(번체) | zh-tw |
| 체코어 | cs |
| 덴마크어 | da |
| 네덜란드어 | nl |
| 영어 | en |
| 에스토니아어 | et |
| 핀란드어 | fi |
| 프랑스어 | fr |
| 갈리시아어 | gl |
| 독일어 | de |
| 그리스어 | el |
| 힌디어 | 안녕하세요 |
| 헝가리어 | hu |
| 인도네시아어 | id |
| 아일랜드어 | ga |
| 이탈리아어 | it |
| 일본어(가타카나) | ja |
| 한국어 | ko |
| 라트비아어 | lv |
| 리투아니아어 | lt |
| 노르웨이어 | 아니요 |
| 페르시아어 | fa |
| 포르투갈어 | pt |
| 루마니아어 | ro |
| 러시아어 | ru |
| 소라니 | ku |
| 스페인어 | es |
| 스웨덴어 | sv |
| 터키어 | tr |
| 태국인 | 번째 |
