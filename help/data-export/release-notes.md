---
title: '[!DNL SaaS Data Export Extension] 릴리스 정보'
description: Adobe Commerce의  [!DNL Data Export Extension] 에 대한 최신 릴리스 정보입니다.
feature: Services, Release Notes
recommendations: noCatalog
exl-id: 8ae51d3d-8c12-4607-b7e5-985033143a84
source-git-commit: eb55055653717cef4b6e568a36593177d821a743
workflow-type: tm+mt
source-wordcount: '2012'
ht-degree: 0%

---

# [!DNL SaaS Data Export] 확장 릴리스 노트

이 릴리스 노트는 [!DNL SaaS data export] 확장의 최신 버전에 대해 설명합니다. 현재 주요 릴리스 버전에 대한 지원이 제공됩니다. 이전 버전에 대한 릴리스 노트는 참조를 위해 제공됩니다.

업데이트에는 다음이 포함됩니다.

새 기능 ![개](../assets/new.svg)개
![수정](../assets/fix.svg) 수정 사항 및 개선 사항
![버그](../assets/bug.svg) 알려진 문제


>[!NOTE]
>
>SaaS 데이터 내보내기 확장은 라이브 검색, 제품 권장 사항 및 카탈로그 서비스와 함께 자동으로 설치되는 모듈 컬렉션입니다. Composer를 사용하여 시스템에 설치된 버전을 확인할 수 있습니다. 경우에 따라 Commerce 서비스 버전을 업데이트하지 않고 시스템에서 데이터 내보내기 확장 기능을 업그레이드하여 수정 사항이나 새 기능을 선택할 수 있습니다.

## 현재 메이저 버전

## 103.4.18 릴리스

![수정](../assets/fix.svg) 업데이트 중에 항목 배치가 허용된 한도를 초과하여 데이터를 `items_limit_exceeded`Commerce 서비스[&#x200B; 또는 &#x200B;](https://experienceleague.adobe.com/ko/docs/commerce/user-guides/home)Adobe Commerce Optimizer[과(와) 동기화할 때 &#x200B;](https://experienceleague.adobe.com/ko/docs/commerce/optimizer/setup/data-sync) 오류가 발생하는 문제를 해결했습니다. <!--MDEE-1264-->
![수정](../assets/fix.svg) 번들 제품 옵션 수집 중에 실패한 항목을 등록하는 논리를 추가하여 제품 데이터 내보내기의 안정성을 개선했습니다. <!--CCSAAS-4458-->

## 103.4.17 릴리스   

![수정](../assets/fix.svg) 더 이상 필요하지 않은 `magento/module-data-exporter` 종속성을 제거하기 위해 데이터 내보내기 확장(`magento/module-analytics`)을 업데이트했습니다.<!--MDEE-1260--> 
![수정](../assets/fix.svg) 제품의 계층 가격을 업데이트해도 이전 값이 제거되지 않아 계층 가격 항목이 중복되거나 오래된 문제가 해결되었습니다. 이제 업데이트 후 현재 계층 가격만 표시됩니다. <!--MDEE-1157-->  
![수정](../assets/fix.svg) $0 가격 또는 100% 할인된 제품이 상점 앞에 무료로 표시되지 않는 문제를 해결했습니다. Storefront 및 장바구니 가격은 이제 일관적입니다. <!--MDEE-1159-->  
![수정](../assets/fix.svg) Symfony 7.4 LTS 호환성이 향후 업그레이드 및 통합을 지원하기 위해 데이터 내보내기 확장에 추가되었습니다. <!--MDEE-1272-->   

## 103.4.16 릴리스   

![수정](../assets/fix.svg) 여러 인덱서에서 ActionInterface 구현이 누락되어 설치 또는 업그레이드 중에 특정 인덱서가 `Update On Schedule` 모드로 전환되지 않는 문제를 해결했습니다. 이 수정 사항을 통해 인덱서 관련 오류가 발생하지 않고 확장 프로그램을 성공적으로 설치 및 업그레이드할 수 있습니다. <!--MDEE-1235-->

## 103.4.15 릴리스

![새로운 기능](../assets/new.svg) Adobe Commerce에서 연결된 서비스(카탈로그 서비스, Live Search 및 제품 권장 사항)로의 데이터 전송을 모니터링하고 문제를 해결하기 위해 데이터 피드 동기화 상태 확장 기능에 대한 지원을 추가했습니다. 이 확장 기능 설치 및 사용에 대한 자세한 내용은 [Commerce 관리 안내서](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status.html?lang=ko)의 *데이터 피드 동기화 상태 모니터링*&#x200B;을 참조하십시오. <!--MDEE-954-->

## 103.4.14 릴리스

![수정](../assets/fix.svg) [&#x200B; 테이블이 없으면 &#x200B;](https://developer.adobe.com/commerce/php/development/components/indexing/#mview)mview 인덱서`cde_product_overrides_feed_cl` 작업이 실패할 수 있는 문제를 해결했습니다. 이 수정 사항으로 인해 안정적인 리인덱싱이 가능하며 다중 테넌트 환경에서 이 테이블과 관련된 작업 오류가 발생하지 않습니다.&quot; <!--MDEE-1175-->

## 103.4.13 릴리스

![수정](../assets/fix.svg) 웹 구성 설정을 편집하여 제품 피드 색인이 재설정되는 문제가 해결되었습니다. <!--MDEE-1154-->
![수정](../assets/fix.svg) 특히 여러 스토어 또는 웹 사이트에 할당된 제품에 대해 번들 제품 옵션 및 변형이 카탈로그 서비스 응답에 여러 번 나타날 수 있는 문제를 해결했습니다. 이 수정 사항으로 각 번들 옵션/변형은 이제 제품당 한 번만 반환되어 판매자와 고객 모두에게 정확하고 일관된 상점 전면이 표시됩니다. <!--MDEE-1167-->

## 103.4.12 릴리스

![수정](../assets/fix.svg) 고객 그룹 가격 책정 시 PDP(제품 세부 정보 페이지)에 카탈로그 가격 규칙 할인이 표시되지 않는 문제를 해결했습니다. 이제 PDP가 최저가를 올바르게 표시합니다.<!--MDEE-1158-->

## 103.4.11 릴리스

![새로 만들기](../assets/new.svg) [!BADGE PaaS만 해당]{type=Informative url="https://experienceleague.adobe.com/ko/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce 온 클라우드 프로젝트(Adobe 관리 PaaS 인프라) 및 온프레미스 프로젝트에만 적용됩니다."}
제품 피드에 Commerce 제품 구성의 세금 클래스, 속성 세트 및 재고 데이터를 포함하도록 추가 제품 속성에 대한 지원을 추가했습니다. 제품 내보내기 피드에 이러한 속성을 포함하려는 고객은 추가 제품 속성 모듈을 Adobe Commerce 프로젝트에 추가해야 합니다. [세금 클래스, 특성 집합 및 재고 특성 추가](add-tax-attribute-set-inventory-attributes.md)를 참조하십시오.<!--MDEE-1135-->
![수정](../assets/fix.svg) 전체 제품 색인 중에 오류가 발생한 경우 삭제된 제품 업데이트에 대해 잘못 동기화되는 문제를 해결했습니다. 이제 인덱싱 프로세스 중에 오류가 발생하더라도 모든 제품 삭제가 올바르게 동기화됩니다. <!--MDEE-1144-->

## 103.4.10 릴리스

![수정](../assets/fix.svg) 동적으로 만든 일부 특성에 대해 잘못된 유형(`text` 대신 `OBJECT`)이 반환되는 문제를 해결했습니다. 이제 올바른 유형 정보가 일관되게 반환되므로 수동으로 다시 동기화하거나 해결할 필요가 없습니다.<!--MDEE-1131-->
![수정](../assets/fix.svg) LowStock 인벤토리 공급자의 오류로 인해 부분 동기화 중 제품 데이터 수집이 실패할 수 있는 문제를 해결했습니다. 이 수정 사항을 통해 제품 데이터를 안정적으로 내보내고 LowStock 관련 오류로 인해 제품 ID를 건너뛸 수 없습니다.<!--MDEE-1132-->

## 103.4.9 릴리스

![수정](../assets/fix.svg) 제품이 삭제되거나 제품 SKU가 변경된 경우 제품 가격 피드가 다시 생성되지 않는 문제가 해결되었습니다.<!--MDEE-1125-->
![수정](../assets/fix.svg) 이전에 삭제된 제품과 동일한 SKU로 새로 만든 제품을 업데이트할 때 변경 내용이 정확하게 반영되도록 제품 업데이트 처리가 개선되었습니다. 이제 제품 동기화는 업데이트된 제품 ID를 올바르게 사용하므로 정확하고 안정적인 데이터 내보내기가 보장됩니다.<!--MDEE-1126-->
![수정](../assets/fix.svg) 특성 삭제 후 제품 업데이트 이벤트가 게시되도록 하여 카탈로그 서비스가 구성 가능한 제품에 대한 오래된 변형 데이터를 반환할 수 있는 문제를 해결했습니다.<!--MDEE-1127-->

## 103.4.8 릴리스

![새로 만들기](../assets/new.svg) 가격 피드에 계층 가격 정보가 추가되었습니다. <!--MDEE-1070-->
![수정](../assets/fix.svg) 이제 데이터 내보내기 확장은 웹 사이트 범위 번들 선택 가격을 올바르게 내보내 &quot;카탈로그 가격 범위&quot; 구성에 따라 상점 가격이 정확한 값을 반영하도록 합니다.<!--MDEE-1115-->
![수정](../assets/fix.svg) 이전에는 임계값 구성으로 Inventory management(다중 소스 Inventory management)를 사용할 때 제품이 잘못된 `lowStock=true` 상태로 동기화되었습니다. 이 문제는 정확한 낮은 재고 보고를 위해 해결되었습니다.<!--MDEE-1113-->

## 103.4.7 릴리스

![수정](../assets/fix.svg) 제품에 대한 범주 권한을 저장한 오래된 테이블을 제거했습니다. <!--MDEE-1065-->

## 103.4.6 릴리스

![수정](../assets/fix.svg) Adobe Commerce Optimizer에서 사용할 `ac_downloadable` 특성을 사용하여 Adobe Commerce 다운로드 가능한 제품 데이터를 내보냅니다. <!--MDEE-1043-->
![수정](../assets/fix.svg) Adobe Commerce 버전 2.4.4에 대한 중요한 설치 오류 수정. <!--MDEE-1074-->

## 103.4.5 릴리스

![새로 만들기](../assets/new.svg) SaaS 데이터 내보내기가 이제 Adobe Commerce `giftcard` 제품 형식을 지원합니다. 데이터 피드에서 기프트 카드 제품을 제품 특성 유형이 `ac_giftcard`인 간단한 제품으로 내보냅니다. <!--MDEE-1042-->
![수정](../assets/fix.svg) 데이터 내보내기 오류 보고가 개선되었습니다. 이제 로그에는 오류를 더 쉽게 디버깅하고 추적할 수 있도록 원본 기술 세부 정보를 포함하여 더 자세한 오류 메시지가 포함됩니다. <!--MDEE-1064-->

## 103.4.4 릴리스

![새로 만들기](../assets/new.svg) `cleanup-feed` 인수를 `saas:resync` CLI 명령에 추가할 때 표시되는 경고 메시지가 추가되었습니다. `--cleanup-feed` 옵션은 환경 정리 후나 `--dry-run` 옵션과 같은 특정 시나리오에서만 주의해서 사용해야 합니다. 다른 경우에 사용하면 데이터가 손실되고 동기화 문제가 발생할 수 있습니다. <!--MDEE-1047-->
![수정](../assets/fix.svg) 추적 가능성을 개선하기 위해 서버 응답에서 `x-request-id`을(를) 추가했습니다. <!--MDEE-1041-->
![수정](../assets/fix.svg) 전체 피드 배치에 대해 동기화 상태가 저장되지 않아 다시 동기화되지 않는 문제를 해결했습니다. <!--MDEE-1049-->
![수정](../assets/fix.svg) 한 피드에 오류가 있는 경우 동기화 중에 피드 배치의 모든 피드를 건너뛰는 문제를 해결했습니다. <!--MDEE-976-->
![수정](../assets/fix.svg) 범주 권한 인덱서에서 차원에 대한 지원이 추가되었습니다. <!--MDEE-654-->

## 103.4.3 릴리스

![수정](../assets/fix.svg) EAV 특성이 누락되어 데이터 내보내기 프로세스 중에 제품을 건너뛰던 문제를 해결했습니다. <!--MDEE-970-->

## 103.4.2 릴리스

![수정](../assets/fix.svg) `saas-export.log` 환경 변수와 함께 `saas:resync --dry-run` 명령을 사용하여 테스트 다시 동기화를 실행할 때 `EXPORTER_EXTENDED_LOG=1`에서 엔터티 페이로드를 수집하는 기능이 추가되었습니다. <!--MDEE-1023-->

## 103.4.1 릴리스

![수정](../assets/fix.svg) 다른 모듈과의 이름 지정 충돌을 방지하기 위해 QueryXml 캐시 키에 접두사를 추가했습니다. <!--MDEE-1019-->

## 103.4.0 릴리스

![수정](../assets/fix.svg) 제품이 범주에 할당되지 않은 경우 제품 재정의 피드가 더 이상 권한을 보내지 않습니다.<!--MDEE-449-->

## 103.3.21 릴리스

![수정](../assets/new.svg) 지정된 제품 SKU 목록을 기반으로 `products`, `productOverrides` 및 `productAttributes` 피드를 부분적으로 동기화하는 기능이 추가되었습니다. CLI 다시 동기화 명령에 `--by-ids` 옵션을 추가하여 새 기능을 사용합니다. <!--MDEE-606-->

```shell
bin/magento saas:resync --feed=<FEED_NAME> --by-ids='<SKU1>,<SKU2>,<SKU3>
```

![수정](../assets/fix.svg) 더 이상 사용되지 않는 기능을 해결하여 PHP 8.4의 잠재적인 호환성 문제를 줄였습니다. <!--MDEE-1002-->

## 103.3.20 릴리스

![해결](../assets/fix.svg) 카탈로그 데이터 내보내기 cron 작업 실패와 관련된 오류에 대한 메시지를 개선하여 `BulkException`에서 추적 불가능한 `cron.log` 오류를 해결했습니다.<!--MDEE-966-->
![수정](../assets/fix.svg) 스토어 보기 수가 많은 인스턴스에서 제품 재동기화 프로세스의 성능이 향상되었습니다. <!--MDEE-974-->

## 103.3.19 릴리스

![수정](../assets/fix.svg) 피드 확장성을 개선하기 위해 데이터 내보내기 확장을 업데이트했습니다. <!--MDEE-936-->
![수정](../assets/fix.svg) 이제 데이터 내보내기 프로세서에서 전체 재동기화 전에 인덱서 상태를 확인하여 피드 테이블에서 실수로 데이터가 손실되지 않도록 합니다.

## 103.3.18 릴리스

![수정](../assets/fix.svg) 제품 및 범주 엔터티에 대한 스테이징 업데이트가 데이터 내보내기 데이터 업데이트 시 올바르게 트리거됩니다.<!--MDEE-963-->

## 103.3.17 릴리스

![수정](../assets/fix.svg) PHP 8.4에 대한 호환성을 추가했습니다. <!--MDEE-941-->

## 103.3.16 릴리스

![수정](../assets/fix.svg) 옵션 값은 여러 스토어 보기에 대해 구성 가능한 제품의 경우 비워 둘 수 있습니다. <!--MDEE-926-->

## 103.3.15 릴리스

![수정](../assets/fix.svg) 이전 구성에 대한 통합 테스트의 안정적인 작동을 확인했습니다. <!--MDEE-869-->
![수정](../assets/fix.svg) 불필요한 특성 옵션 전달을 중지합니다. <!--MDEE-882-->
![수정](../assets/fix.svg) 데이터 직렬화가 실패하면 데이터 내보내기 로그로 전송되는 오류 메시지를 수정했습니다. <!--MDEE-913-->
![수정](../assets/fix.svg) 추가 테스트 범위를 통해 간단한 제품 업데이트의 안정성을 개선했습니다. <!--MDEE-886-->

## 103.3.14 릴리스

![수정](../assets/fix.svg) 내보내기 인덱서가 이제 종속 인덱서에 대한 올바른 상태를 유지합니다. 이전에는 이러한 색인이 잘못 무효화되었으며 색인화 성능을 느리게 하는 추가 확인 및 유효성 검사가 필요했습니다. <!--MDEE-866-->

## 103.3.13 릴리스

![수정](../assets/fix.svg) 특성 옵션 데이터에 대한 로컬 캐시를 추가하여 데이터 동기화 프로세스의 성능을 개선했습니다.<!--MDEE-864-->

## 103.3.12 릴리스

![수정](../assets/fix.svg) 단순 및 가상 제품에 대한 동기화 시간이 증가하는 문제를 해결했습니다. <!--MDEE-861-->

## 103.3.11 릴리스

![수정](../assets/fix.svg) 이제 데이터 내보내기 서비스에서 번들 제품에 대한 특별 가격 데이터를 백분율로 보내어, 최종 가격으로 전송된 이전 문제를 해결합니다. <!--MDEE-854-->
![수정](../assets/fix.svg) 모노로그 3과의 호환성을 위해 모노로그 구현을 업데이트했습니다. <!--MDEE-858-->

## 103.3.10 릴리스

![수정](../assets/fix.svg) 제품 사용자 지정 옵션 피드에 대한 여러 저장소 보기 필터링을 수정했습니다. <!--MDEE-842-->
![수정](../assets/fix.svg) 피드의 해시 값이 변경될 때까지 잘못된 피드가 다시 제출되지 않습니다.<!--MDEE-848-->

## 103.3.9 릴리스

![수정](../assets/fix.svg) 엔터티가 삭제되면 이제 `deleted` 플래그가 웹 사이트(`scopesWebsite`) 및 고객 그룹(`scopesCustomerGroup`)의 범위 서비스 피드에 대해 전파됩니다.<!--MDEE-839-->

## 103.3.8 릴리스

![수정](../assets/fix.svg) 비활성화된 구성 옵션은 더 이상 활성 옵션으로 내보내지 않습니다.<!--MDEE-812-->
![수정](../assets/fix.svg) 이제 하위 제품에 변경 사항이 적용되면 구성 가능한 제품에 대한 옵션 및 값이 업데이트됩니다. <!--MDEE-835-->
![새로 만들기](../assets/new.svg) 제품 특성 피드에 추가 시스템 특성 데이터를 포함하는 기능이 추가되었습니다.

## 103.3.7 릴리스

![수정](../assets/fix.svg)이(가) InventoryDataExporter 모듈에서 불필요한 종속성을 제거했습니다.
![수정](../assets/fix.svg) Adobe Commerce 버전 2.4.4를 지원하도록 CatalogInventoryDataExporter 모듈에 포함된 인벤토리 모듈에 대한 필수 버전을 변경했습니다.

## 103.3.6 릴리스

![수정](../assets/fix.svg) 다중 스레드 모드에서 피드를 다시 인덱싱하는 동안 발생한 교착 상태를 해결했습니다. 이제 쿼리가 삽입 및 업데이트 작업으로 구분됩니다.
![수정](../assets/fix.svg) 많은 웹 사이트가 있는 큰 카탈로그의 가격 쿼리를 최적화했습니다.
![새로 만들기](../assets/new.svg) 교착 상태가 발생할 때 실패한 트랜잭션을 다시 실행하기 위한 다시 시도 논리를 추가했습니다.

## 103.3.5 릴리스

![수정](../assets/fix.svg) SaaS 공통 모듈에 대해 호환되는 최신 데이터 내보내기 버전에 대한 종속성을 설정합니다.

![수정](../assets/fix.svg)이(가) 다른 서비스 구성을 지원하기 위해 `ScopeConfig` 인스턴스를 `ServiceConfigInterface`(으)로 대체했습니다.

## 103.3.4 릴리스

![수정](../assets/fix.svg) Commerce 인스턴스에서 Commerce 서비스로 데이터를 전송할 때마다 `data_sent_outside` 이벤트를 발송하는 메커니즘을 추가하여 데이터 전송 감사 로깅에 대한 지원을 추가했습니다. <!--MDEE-785-->

## 103.3.3 릴리스

![새로 만들기](../assets/new.svg) SaaS 데이터 내보내기가 이제 특성 메타데이터 쿼리에 대해 EAV(Entity-Attribute-Value) 특성을 캐시합니다.

![수정](../assets/fix.svg) 제품을 삭제한 경우 다시 시도할 때 `InventoryStockStatus` 피드가 저장되지 않는 문제를 해결했습니다.

## 103.3.2 릴리스

![수정](../assets/fix.svg) 제거된 엔터티 피드에서 `modifiedAt` 필드가 누락되는 문제를 해결했습니다.

## 103.3.1 릴리스

![수정](../assets/fix.svg) 페이지 빌더를 설치할 때 제품 피드를 다시 인덱싱하는 동안 `Invalid Template File` 메시지가 표시되는 문제를 해결했습니다.

## 103.3.0 릴리스

![새로 만들기](../assets/new.svg) 바로 내보내기 피드 테이블을 통합 구조로 마이그레이션했습니다.
`id`, `source_entity_id`, `feed_id`, `modified_at`, `is_deleted`, `status`, `feed_data`, `feed_hash`, `errors`

![새로 만들기](../assets/new.svg) 카탈로그 및 인벤토리 피드를 즉시 내보내기 솔루션으로 마이그레이션했습니다.

![새로 만들기](../assets/new.svg) 피드를 즉시 내보내는 크론 작업이 `*_feed_resend_failed_items`(으)로 이름이 변경되었습니다.

![새로 만들기](../assets/new.svg) 즉각적인 내보내기 피드, 인덱서 보기 ID 및 변경 로그 테이블의 이름이 변경되었습니다.

- 피드 테이블(및 인덱서 보기 ID):

   - `catalog_data_exporter_products` -> `cde_products_feed`
   - `catalog_data_exporter_product_attributes` -> `cde_product_attributes_feed`
   - `catalog_data_exporter_categories` -> `cde_categories_feed`
   - `catalog_data_exporter_product_prices` -> `cde_product_prices_feed`
   - `catalog_data_exporter_product_variants` -> `cde_product_variants_feed`
   - `inventory_data_exporter_stock_status` -> `inventory_data_exporter_stock_status_feed`

- 로그 테이블 이름 변경 - 피드 테이블과 동일한 이름 지정 패턴을 따르지만 로그 테이블 이름 변경에는 `_cl` 접미사가 추가됩니다.  예: `catalog_data_exporter_products_cl`-> `cde-products_feed_cl`

이러한 엔티티를 참조하는 사용자 지정 코드가 있는 경우 코드가 계속 제대로 작동하도록 참조를 새 이름으로 업데이트하십시오.

![수정](../assets/fix.svg) 필요한 피드에 대해서만 피드 데이터의 `modified_at` 필드를 설정합니다.

![수정](../assets/fix.svg) 제품 특성만 검색하려면 `productAttributes` 쿼리를 수정하십시오.

## 103.2.6 릴리스

![수정](../assets/fix.svg) 테이블에 접두사가 있을 때 피드가 다시 인덱싱되지 않는 문제를 해결했습니다.

## 103.2.5 릴리스

![수정](../assets/fix.svg) 가격 쿼리를 최적화했습니다.

## 103.2.4 릴리스

![수정](../assets/fix.svg) Commerce Inventory management이 활성화된 경우 제품에 대해 표시되는 잘못된 재고 상태를 수정했습니다.

## 103.2.3 릴리스

![수정](../assets/fix.svg) 웹 사이트 수준의 특별 가격을 수정했습니다.
![수정](../assets/fix.svg) 처리되는 모든 피드에 대해 뮤텍스를 추가했습니다.


## 103.2.2 릴리스

![수정](../assets/fix.svg) 큰 카탈로그에 대한 피드 일괄 처리 전략을 개선했습니다. 이제 배치 테이블이 메모리 사용을 줄이기 위해 제한된 수의 ID로 채워집니다.

![수정](../assets/fix.svg)으로 인해 MSI 모듈에 대한 CommerceInventoryDataExporter의 엄격한 종속성이 제거되었습니다.

![수정](../assets/fix.svg) 더 많은 정보를 수집하고 여러 내보내기 단계로 구성할 수 있도록 `commerce-data-exporter` 로그를 개선했습니다.

## 103.2.1 릴리스

- 업데이트된 버전이 릴리스되었습니다.

## 103.2.0 릴리스

- 제품 및 가격에 대한 다중 스레드 데이터 동기화를 추가했습니다.
