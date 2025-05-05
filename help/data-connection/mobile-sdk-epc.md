---
title: Adobe Experience Platform Mobile SDK과 Commerce 통합
description: Headless 또는 사용자 지정 Commerce 상점 첫 화면에서 Adobe Experience Platform Mobile SDK을 사용하는 방법에 대해 알아봅니다.
role: Admin, Developer
feature: Personalization, Integration, Eventing
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---

# Adobe Experience Platform Mobile SDK과 Commerce 통합

>[!IMPORTANT]
>
>iOS용 Adobe Experience Platform Mobile SDK은 iOS 11 이상을 지원합니다.

[Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/home/)를 Commerce 모바일 앱과 통합하면 판매자가 Commerce [이벤트 데이터](events.md)를 Experience Platform Edge로 보낼 수 있습니다.

에지에서 Commerce 이벤트 데이터를 사용할 수 있으면 다른 Adobe Experience Cloud 애플리케이션에서 액세스할 수 있습니다. 예를 들어 데이터를 사용하여 Real-Time CDP에서 대상을 만든 다음 [해당 대상을 사용](https://experienceleague.adobe.com/docs/commerce-admin/customers/audience-activation.html?lang=ko)하여 Commerce 모바일 앱을 개인화할 수 있습니다.

## 구성

Commerce과 함께 Adobe Experience Platform Mobile SDK을 사용하려면 Experience Platform에서 SDK을 설치하고 구성하십시오. 그런 다음 Commerce에서 구성을 완료합니다.

### Experience Platform

1. [모바일 앱의 Adobe Experience Cloud 자습서](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/overview.html?lang=ko)를 검토하여 모바일 앱 기능에 대해 알아봅니다.

1. Experience Platform에서 SDK을 [설치 및 구성](https://developer.adobe.com/client-sdks/documentation/getting-started/)합니다.

   >[!NOTE]
   >
   >Experience Platform에서 만들고 구성하는 스키마는 Commerce 모바일 앱의 애플리케이션 코드에서 사용하는 것과 동일한 스키마입니다.

### Commerce

Experience Platform에 대한 SDK 구성을 완료한 후 SDK 구성을 Commerce에 추가합니다.

1. SDK을 통해 Commerce 이벤트 데이터를 Experience Platform으로 전송하려면 애플리케이션 코드에 XDM 스키마를 제공해야 합니다. 이 스키마는 Experience Platform의 SDK에 대해 [구성됨](https://developer.adobe.com/client-sdks/home/getting-started/set-up-schemas-and-datasets/) 스키마와 일치해야 합니다.

   다음 예제에서는 전자 메일 필드를 사용하여 `web.webpagedetails.pageViews` 이벤트를 추적하고 `identityMap`을(를) 설정하는 방법을 보여 줍니다.

   ```swift
   let stateName = "luma: content: ios: us: en: home"
   var xdmData: [String: Any] = [
       "eventType": "web.webpagedetails.pageViews",
       "web": [
           "webPageDetails": [
               "pageViews": [
                   "value": 1
               ],
               "name": "Home page"
           ]
       ]
   ]
   
   let experienceEvent = ExperienceEvent(xdm: xdmData)
   Edge.sendEvent(experienceEvent: experienceEvent)
   
   // Adobe Experience Platform - Update Identity
   
   let emailLabel = "mobileuser@example.com"
   
   let identityMap: IdentityMap = IdentityMap()
   identityMap.add(item: IdentityItem(id: emailLabel), withNamespace: "Email")
   Identity.updateIdentities(with: identityMap)
   ```

1. Commerce Cloud 환경에 연결합니다.

   프로젝트의 빌드 설정에서 Commerce GraphQL 엔드포인트에 URL을 추가합니다. 예:

   - 디버그: http://_debug_.commercesite.cloud/graphql/
   - 릴리스: http://_릴리스_.commercesite.cloud/graphql/

1. Commerce GraphQL 끝점에서 데이터를 검색하려면 먼저 [아폴로 코드 생성기](https://www.apollographql.com/docs/ios/)를 사용하여 프로젝트에 필요한 파일과 디렉터리를 생성합니다.

   1. 프로젝트 디렉터리에서 [설치](https://www.apollographql.com/docs/ios/get-started#1-install-the-apollo-frameworks) Apollo iOS입니다.

   1. Apollo Codegen CLI를 [초기화](https://www.apollographql.com/docs/ios/code-generation/codegen-cli/#initialize).

      `apollo-codegen-configuration.json` 파일이 만들어집니다.

   1. `apollo-codegen-configuration.json` 파일의 내용을 다음 내용으로 바꾸어 프로젝트에 필요한 GraphQL 파일 및 디렉터리를 생성합니다.

      ```json
      {
      "schemaName" : "MagentoAPI",
      "input" : {
          "operationSearchPaths" : [
          "**/*.graphql"
          ],
          "schemaSearchPaths" : [
          "**/*.graphqls"
          ]
      },
      "output" : {
          "testMocks" : {
          "none" : {
          }
          },
          "schemaTypes" : {
          "path" : "../MagentoAPI",
          "moduleType" : {
              "swiftPackageManager" : {
              }
          }
          },
          "operations" : {
          "inSchemaModule" : {
          }
          }
      },
      "schemaDownloadConfiguration": {
          "downloadMethod": {
              "introspection": {
                  "endpointURL": "http://magento24.com/graphql/",
                  "httpMethod": {
                      "POST": {}
                  },
                  "includeDeprecatedInputValues": false,
                  "outputFormat": "SDL"
              }
          },
          "downloadTimeout": 60,
          "headers": [],
          "outputPath": "magento.graphqls"
      }
      }
      ```

   1. Commerce GraphQL 스키마를 [가져오기](https://www.apollographql.com/docs/ios/code-generation/codegen-cli/#fetch-schema).

      경로가 Commerce GraphQL 스키마에 대한 참조가 포함된 `./apollo-codegen-config.json` 파일에 대한 경로인지 확인하십시오.

   1. 소스 코드를 [생성](https://www.apollographql.com/docs/ios/code-generation/codegen-cli/#generate)합니다.

      필요한 파일 및 디렉터리를 생성하기 위한 구성 정보가 포함된 `./apollo-codegen-config.json` 파일에 대한 경로인지 확인합니다.

   1. 새로 만든 **GraphQLGgenerated** 폴더 내에서 GraphQL 유형을 추가하거나 편집하십시오. 예를 들어 다음 콘텐츠로 `DynamicBlocks.graphql` 형식을 추가할 수 있습니다.

      ```graphql
      query dynamicBlocks($input: DynamicBlocksFilterInput){
          dynamicBlocks(input: $input)
          {
              items {
                  content {
                      html
                  }
              }
          }
      }
      ```

   이제 Adobe Experience Platform 모바일 SDK을 Commerce 모바일 앱과 통합했습니다. 이벤트 데이터는 앱에서 Experience Platform 에지로 이동합니다.

## 모바일 애플리케이션에서 생성된 Commerce 이벤트를 구분하는 방법

모든 [이벤트](events.md)에 이름이 `channel`인 필드가 있습니다. `channel` 필드에는 Luma 상점 첫 화면의 네임스페이스 값이 각각 `"https://ns.adobe.com/xdm/channels/web"` 및 `"https://ns.adobe.com/xdm/channel-types/web"`인 `channel._id` 및 `channel._type`이(가) 포함되어 있습니다. 그러나 모바일 상점의 경우 네임스페이스 값은 각각 `"https://ns.adobe.com/xdm/channels/mobile-app"` 및 `"https://ns.adobe.com/xdm/channel-types/mobile"`입니다.

## 다음 단계

모바일 Commerce 앱에서 Real-Time CDP 대상자를 검색하여 장바구니 가격 규칙, 동적 블록 및 관련 제품 규칙을 알리는 방법에 대해 알아보려면 [Audience Activation](https://experienceleague.adobe.com/docs/commerce-admin/customers/audience-activation.html?lang=ko#retrieve-audiences-using-the-adobe-experience-platform-mobile-sdk)을(를) 참조하십시오.
