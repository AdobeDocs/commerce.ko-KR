---
title: 미디어 파일을 AEM으로 마이그레이션
description: Adobe Commerce 또는 외부 소스에서 AEM Assets DAM으로 미디어 파일을 마이그레이션합니다.
feature: CMS, Media, Integration
source-git-commit: b6e190e883087a942630f0a27781654cd2c68781
workflow-type: tm+mt
source-wordcount: '734'
ht-degree: 0%

---


# 미디어 파일을 AEM Assets DAM으로 마이그레이션

Adobe Commerce과 Adobe Experience Manager(AEM) 모두 Commerce에서 AEM Assets **DAM(디지털 에셋 관리 시스템)**&#x200B;으로 미디어 파일 마이그레이션을 간소화하기 위한 기본 기능을 제공합니다. 다른 소스에서 미디어 파일을 마이그레이션할 수도 있습니다.

## 사전 요구 사항

| 범주 | 요구 사항 |
|----------|-------------|
| **시스템 요구 사항** | <ul><li>AEM Assets으로 프로비저닝된 AEM as a Cloud Service 환경</li><li>충분한 스토리지 용량</li><li>대용량 파일 전송을 위한 네트워크 대역폭</li></ul> |
| **필요한 액세스 및 권한** | <ul><li>AEM Assets as a Cloud Service에 대한 관리자 액세스</li><li>미디어 파일이 저장된 소스 시스템(Adobe Commerce 또는 외부 시스템)에 액세스</li><li>클라우드 스토리지 서비스에 액세스할 수 있는 적절한 권한</li></ul> |
| **클라우드 저장소 계정** | <ul><li>AWS S3 또는 Azure Blob 스토리지 계정</li><li>비공개 컨테이너/버킷 구성</li><li>인증 자격 증명</li></ul> |
| **Source 컨텐츠** | <ul><li>마이그레이션할 준비가 된 미디어 파일 구성</li><li>AEM Assets에서 지원하는 <a href="https://experienceleague.adobe.com/ko/docs/experience-manager-cloud-service/content/assets/file-format-support#image-formats">형식의 이미지 및 비디오 파일</a>.</li><li>정리되고 중복된 에셋</li></li> |
| **메타데이터 준비** | <ul><li><a href="https://experienceleague.adobe.com/ko/docs/commerce-admin/content-design/aem-asset-management/getting-started/aem-assets-configure-aem">Commerce 자산에 대해 구성된 AEM Assets 메타데이터 프로필</a></li><li>각 자산에 대해 매핑된 메타데이터 값</li><li>CSV 파일 편집기(예: Microsoft Excel)</li></ul> |

## 마이그레이션 모범 사례

1. 사용하지 않거나 중복된 콘텐츠를 제거하여 마이그레이션 전에 자산을 조정합니다.

1. 크기, 형식 또는 사용 사례별로 에셋을 논리적으로 구성합니다.

1. 대규모 마이그레이션을 더 작은 배치로 나누는 것이 좋습니다.

1. 사용량이 적은 시간 동안 리소스 집약적인 가져오기를 예약합니다.

1. 전체 가져오기 전에 메타데이터 매핑의 유효성을 검사합니다.

## 마이그레이션 워크플로

마이그레이션 작업 과정을 따라 Adobe Commerce 또는 다른 외부 시스템에서 미디어 파일을 내보내고 AEM Assets DAM으로 가져옵니다.

### 1단계: 기존 데이터 소스에서 컨텐츠 내보내기

[!BADGE PaaS만]{type=Informative tooltip="Adobe Commerce on Cloud 프로젝트에만 적용됩니다(Adobe 관리 PaaS 인프라)."}

Adobe Commerce 판매자의 경우 **원격 저장소 모듈**&#x200B;을(를) 통해 미디어 파일을 쉽게 가져오고 내보낼 수 있습니다. 이 모듈을 통해 기업은 AWS S3와 같은 원격 스토리지 서비스를 사용하여 미디어 파일을 저장하고 관리할 수 있습니다. Commerce 인스턴스에 대한 원격 저장소를 설정하려면 **Commerce 구성 안내서**&#x200B;에서 [원격 저장소 구성](https://experienceleague.adobe.com/ko/docs/commerce-operations/configuration-guide/storage/remote-storage/remote-storage-aws-s3)을(를) 참조하십시오.

Adobe Commerce 외부에 저장된 미디어 파일이 있는 경우 AEM as a Cloud Service에서 지원하는 [데이터 소스](https://experienceleague.adobe.com/ko/docs/experience-manager-cloud-service/content/assets/assets-view/bulk-import-assets-view#prerequisites) 중 하나로 직접 업로드하십시오.

### 2단계: 메타데이터 매핑을 위한 CSV 파일 빌드

미디어 파일을 내보낸 후 CSV 파일을 만들어 이러한 에셋을 자동화에 필요한 메타데이터와 매핑합니다. CSV에는 **제품**, **위치** 및 **역할 매핑**&#x200B;에 대한 필드가 포함되어야 하며 [AEM Assets 메타데이터 프로필](configure-aem.md#configure-a-metadata-profile)과의 정렬을 보장합니다.

마이그레이션하려는 각 미디어 파일에 대해 다음 표에 설명된 대로 [Commerce 에셋용 AEM Assets 메타데이터 프로필](configure-aem.md)에 포함된 메타데이터 필드의 값을 제공하십시오.

| 메타데이터 | 설명 | 값 |
|-------|-------------|--------|
| assetPath | AEM Assets 저장소에 에셋이 저장되는 전체 경로입니다.<br><br>경로를 사용하여 Commerce 자산을 구성할 하위 폴더를 만드십시오. 예: `content/dam/commerce/<brand>/<type>` | `/content/dam/commerce/<sub-folder>/..<filename>` |
| commerce:position | 제품 갤러리에서 에셋의 위치/순서 | 파이프로 구분된 여러 숫자 값(csv 파일 참조) |
| commerce:isCommerce | 자산이 상거래에 사용되는지 보여 주는 플래그 | `Yes` |
| commerce:skus | 이 자산과 연결된 제품 SKU | 파이프로 구분된 여러 문자열 값(csv 파일 참조) |
| commerce:roles | 에셋의 역할 또는 이미지 유형(예: `thumbnail`, `main image`, `swatch`) | 세미콜론으로 구분된 여러 값(예: &quot;thumbnail; image; swatch_image; small_image&quot;) |

+++CSV 코드

이 샘플 CSV 코드를 사용하여 코드 편집기 또는 Microsoft Excel과 같은 스프레드시트 애플리케이션에서 파일을 생성합니다.

```csv
assetPath,commerce:positions{{Number: multi}},commerce:isCommerce{{String}},commerce:skus{{String: multi}},commerce:roles{{String: multi}}
/content/dam/commerce/sample1.jpg,1,Yes,sku1,thumbnail; image; swatch_image; small_image
/content/dam/commerce/sample2.jpg,1|1|1,Yes,sku1|sku2|sku3,thumbnail; image; swatch_image; small_image|image|image; small_change
```

+++

### 3단계: Assets을 AEM Assets으로 일괄 가져오기

메타데이터 매핑 파일을 만든 후 AEM Assets 일괄 가져오기 도구를 사용하여 에셋을 가져옵니다.

다음은 도구 사용에 대한 높은 수준의 개요입니다.

1. [AEM Assets as a Cloud Service 작성자 환경에 로그인](https://experienceleague.adobe.com/ko/docs/experience-manager-cloud-service/content/onboarding/journey/aem-users#login-aem).

1. Experience Manager 도구 보기에서 **[!UICONTROL Assets]** > **[!UICONTROL Bulk Import]**&#x200B;을(를) 선택합니다.

   ![AEM Assets 작성](../assets/aem-assets-bulk-import-selection.png){width="600" zoomable="yes"}

1. 일괄 가져오기 구성에서 **[!UICONTROL Create]**&#x200B;을(를) 선택하여 구성 양식을 엽니다.

   ![AEM Assets 작성](../assets/aem-assets-bulk-import-configuration.png){width="600" zoomable="yes"}

1. 구성을 설정하고 저장합니다.

   다음이 필요합니다.

   * 데이터 소스에 대한 인증 자격 증명
   * 가져온 파일이 저장될 AEM Assets의 대상 폴더
   * 선택 사항입니다. 가져오기 구성을 사용자 정의하기 위한 MIME 유형, 파일 크기 및 기타 매개 변수에 대한 정보입니다
   * 클라우드 스토리지 인스턴스에 업로드한 메타데이터 매핑 CSV 파일의 경로입니다.

   자세한 단계는 *AEM Assets as a Cloud Service 사용 안내서*&#x200B;에서 [일괄 가져오기 도구 구성](https://experienceleague.adobe.com/ko/docs/experience-manager-cloud-service/content/assets/manage/add-assets#configure-bulk-ingestor-tool)을 참조하십시오.

1. 구성을 저장한 후 일괄 가져오기 도구를 사용하여 가져오기 작업을 테스트하고 실행합니다.

>[!MORELIKETHIS]
>
> [일괄 가져오기 도구 비디오 데모](https://experienceleague.adobe.com/ko/docs/experience-manager-cloud-service/content/assets/manage/add-assets#asset-bulk-ingestor)
> &#x200B;> [팁, 모범 사례 및 제한 사항](https://experienceleague.adobe.com/ko/docs/experience-manager-cloud-service/content/assets/manage/add-assets#tips-limitations)
> &#x200B;> [API](https://experienceleague.adobe.com/ko/docs/experience-manager-cloud-service/content/assets/admin/developer-reference-material-apis#asset-upload)을(를) 사용하여 에셋 업로드 또는 수집
