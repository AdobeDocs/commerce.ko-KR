---
title: 제품에 파일 추가
description: ' [!DNL Adobe Commerce as a Cloud Service]의 파일 형식 제품 특성을 사용하여 PDF, 설명서 및 Data Sheet와 같은 파일을 제품에 첨부하는 방법을 알아봅니다.'
feature: Catalog Management, Products, Integration
role: Admin, Developer
level: Intermediate
badgeSaas: label="SaaS만" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Service 및 Adobe Commerce Optimizer 프로젝트에만 적용됩니다(Adobe 관리 SaaS 인프라)."
source-git-commit: 14c4178338859d55a7391139033d51d1aa6f7678
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 0%

---

# 제품에 파일 추가

[!DNL Adobe Commerce as a Cloud Service]은(는) 판매자가 PDF, 설명서, 인증서 및 데이터 시트와 같은 파일을 제품에 직접 첨부할 수 있도록 하는 &quot;파일&quot; [제품 특성 입력 유형](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/attributes-input-types){target="_blank"}을 지원합니다. 파일은 Amazon S3 미디어 저장소에 저장되며 GraphQL을 사용하는 상점 또는 REST API를 사용하는 통합을 통해 액세스할 수 있습니다.

파일을 제품 파일 속성에 업로드하는 방법에는 세 가지가 있습니다.

* [관리자 UI](#upload-files-through-the-admin) - 제품 편집 페이지에서 수동으로 파일을 업로드합니다.
* [REST API](#upload-through-the-rest-api) - S3 사전 서명된 URL을 사용하여 REST API를 통해 파일을 업로드합니다.
* [제품 가져오기](#upload-through-product-import) - 외부 URL을 CSV로 제공하여 파일을 일괄적으로 가져옵니다.

## 사전 요구 사항

파일을 업로드하기 전에 파일 속성을 만들고 속성 세트에 지정해야 합니다.

* [파일 특성을 만듭니다](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/create/attribute-product-create){target="_blank"} - **[!UICONTROL Catalog Input Type for Store Owner]**&#x200B;을(를) **[!UICONTROL File]**(으)로 설정합니다.

* [특성을 특성 집합에 할당](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/create/attribute-sets#create-an-attribute-set){target="_blank"} - 새 파일 특성을 원하는 그룹으로 끌어 옵니다.

* [제품 파일 특성](https://experienceleague.adobe.com/en/docs/commerce-admin/config/catalog/product-file-attributes) 구성에서 허용되는 파일 형식 및 크기를 구성하십시오.

## 관리자를 통해 파일 업로드

[파일 특성을 만들고](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/create/attribute-product-create){target="_blank"}특성 집합에 할당하면 제품 편집 페이지에서 직접 파일을 업로드할 수 있습니다.

1. _관리자_ 사이드바에서 **[!UICONTROL Catalog]** > **[!UICONTROL Products]**(으)로 이동합니다.

1. 편집할 제품을 엽니다.

1. 파일 특성 필드를 찾아 **[!UICONTROL Upload]**&#x200B;을(를) 클릭하여 파일을 선택합니다.

![관리자의 파일 업로드 단추](./assets/upload-file.png){width="600" zoomable="yes"}

1. **[!UICONTROL Save]**&#x200B;을(를) 클릭합니다.

파일을 바꾸려면 기존 파일을 삭제하고 새 파일을 업로드합니다. 업로드된 파일은 Amazon S3 미디어 저장소에 저장됩니다.

## REST API를 통해 업로드

[S3 사전 서명된 URL 흐름](https://developer.adobe.com/commerce/webapi/rest/saas-integrations/s3-uploads/){target="_blank"}을 사용하여 REST API를 통해 프로그래밍 방식으로 파일을 업로드하십시오. 이 프로세스는 카테고리 이미지 및 고객 속성 파일과 같은 다른 미디어 유형의 제품 파일 속성과 동일한 방식으로 작동합니다.

이 프로세스에는 다음 네 가지 단계가 있습니다.

1. 파일 이름으로 `POST V1/media/initiate-upload`을(를) 호출하고 제품 파일 특성에 대해 `media_resource_type`을(를) 호출합니다.
1. 반환된 사전 서명된 URL을 사용하여 파일을 Amazon S3에 직접 `PUT`합니다.
1. 업로드를 확인하려면 `POST V1/media/finish-upload`을(를) 호출하십시오.
1. 반환된 키를 `PUT /V1/products/{sku}`을(를) 통해 제품의 파일 특성에 할당하여 [사용자 지정 특성](https://developer.adobe.com/commerce/webapi/rest/modules/custom-attributes/) 값으로 전달합니다.

## 제품 가져오기를 통해 업로드

[API 가져오기](https://developer.adobe.com/commerce/webapi/rest/modules/import/){target="_blank"} 또는 관리자 가져오기 UI를 사용하여 제품에 파일을 일괄적으로 첨부할 수 있습니다. 제품 파일 특성은 외부 URL에서만 가져오기를 지원하며, 이는 제품 이미지 가져오기에 대한 [메서드 2](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/import/data-import-product-images#method-2-import-images-from-external-server){target="_blank"}와 동일한 접근 방식을 따릅니다. Commerce은 제공된 URL에서 파일을 다운로드하여 S3 미디어 저장소에 저장합니다.

>[!NOTE]
>
>직접 파일 시스템 액세스가 없으므로 [!DNL Adobe Commerce as a Cloud Service]에서 로컬 서버 경로(메서드 1)에서 파일을 가져올 수 없습니다.

### 전용 열에 URL 제공

속성 코드를 CSV 열 헤더로 사용하고 전체 URL을 값으로 사용합니다. 예를 들어 특성 코드가 `file_upload`이면 CSV는 다음과 같이 표시됩니다.

```csv
sku,name,file_upload
ADB112,"My Product",https://example.com/files/manual.pdf
```

### `additional_attributes`에 URL 제공

또는 `additional_attributes` 열에 파일 특성을 포함합니다.

```csv
sku,name,additional_attributes
ADB112,"My Product",file_upload=https://example.com/files/manual.pdf
```

두 경우 모두 URL을 공개적으로 액세스할 수 있어야 하며 파일 확장자와 크기는 [구성된 제한 사항](https://experienceleague.adobe.com/en/docs/commerce-admin/config/catalog/product-file-attributes){target="_blank"}을 준수해야 합니다.

## GraphQL을 통해 파일 검색

[!DNL Adobe Commerce as a Cloud Service]에서 [카탈로그 서비스 GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/){target="_blank"} 끝점은 제품 데이터를 제공합니다. 파일 특성은 `attributes`의 `ProductView` 필드에 나타나며 `value`에는 파일에 대한 전체 공개 URL이 들어 있습니다.

```graphql
{
  products(skus: ["ADB112"]) {
    sku
    name
    attributes(roles: []) {
      name
      label
      value
    }
  }
}
```

응답에는 공용 URL에 파일 속성이 포함됩니다.

```json
{
  "data": {
    "products": [
      {
        "sku": "ADB112",
        "name": "Example product",
        "attributes": [
          {
            "name": "file",
            "label": "FILE",
            "value": "https://<host>/media/catalog/product_file/manual.pdf",
          }
        ]
      }
    ]
  }
}
```

>[!NOTE]
>
>이 쿼리에는 `Magento-Website-Code` 및 `Magento-Store-View-Code` 헤더가 필요합니다. 자세한 내용은 [카탈로그 서비스 제품 쿼리](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/){target="_blank"}를 참조하세요.

## REST API를 통해 파일 검색

[REST API](https://developer.adobe.com/commerce/webapi/reference/rest/saas/){target="_blank"}(`GET /V1/products/{sku}`)을(를) 통해 제품을 검색할 때 파일 특성이 파일 이름을 값으로 하여 `custom_attributes` 배열에 나타납니다.

```json
{
  "custom_attributes": [
    {
      "attribute_code": "file_upload",
      "value": "manual_7aa0b2d63f6d3dbf.pdf"
    }
  ]
}
```
