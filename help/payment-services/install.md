---
title: ' [!DNL Payment Services] 설치'
description: 결제 서비스 확장을 설치합니다.
role: Admin
feature: Payments, Checkout, Install, Upgrade
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 0%

---

# [!DNL Payment Services] 설치

[!DNL Adobe Commerce] 및 [!DNL Magento Open Source]에 대한 결제 서비스를 사용하려면 몇 가지 온보딩 단계를 완료해야 합니다.

>[!INFO]
>
> 자세한 내용은 [Adobe Commerce에 대해 구성 [!DNL Payment Services] 구성](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/admin/adobe-commerce-services/configure-adobe-payment-services) 비디오를 참조하십시오.

[!DNL Adobe Commerce] 및 [!DNL Magento Open Source]에 대한 [!DNL Payment Services] 확장을 다운로드하고 설치하는 것은 [!DNL Payment Services]을(를) 사용하기 위한 필수 단계입니다.

## 확장 다운로드

설치하기 전에 먼저 [Commerce Marketplace](https://experienceleague.adobe.com/docs/commerce-admin/start/resources/commerce-marketplace.html)에서 확장을 다운로드해야 합니다.

1. Commerce Marketplace의 [결제 서비스 확장](https://commercemarketplace.adobe.com/magento-payment-services.html)&#x200B;(으)로 이동합니다.
1. 버전 및 버전을 선택하려면 **[!UICONTROL Edition]** 및 **[!UICONTROL Your store version]**&#x200B;을(를) 원하는 선택 항목으로 전환하십시오.
1. **[!UICONTROL Add to Cart]**&#x200B;을(를) 클릭합니다.
1. 체크 아웃을 완료하고 **[!UICONTROL Place Order]**&#x200B;을(를) 클릭합니다.
1. 주문 확인 및 세부 사항은 Marketplace 다운로드와 연결된 이메일을 확인하십시오.

>[!NOTE]
>
> Adobe Commerce 버전 2.4.7 이상의 경우 [!DNL Payment Services]을(를) 즉시 사용할 수 있습니다.

## 확장 설치

등록 프로세스에서 제공된 Commerce 계정 [mageid](https://developer.adobe.com/commerce/marketplace/guides/sellers/profile-information/#access-keys)에 연결된 클라우드 인프라 및 온-프레미스 인스턴스에 모두 [!DNL Adobe Commerce]에 대한 [!DNL Payment Services] 확장을 설치할 수 있습니다.
[!DNL Magento Open Source]명의 고객이 온-프레미스 지침을 사용합니다.

작성기가 [!DNL Adobe Commerce]을(를) 처음 설치하는 동안 또는 작성기 키가 이전에 `auth.json` 파일에 저장되지 않은 상황에서 이 키를 사용합니다.

작성기 키 가져오기에 대한 자세한 내용은 [인증 키 가져오기](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/authentication-keys)를 참조하십시오.

확장을 다운로드하여 설치하기 전에 고려해야 할 사항에 대한 자세한 내용은 [확장 설치](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/extensions)를 참조하십시오.

### 클라우드 인프라의 [!DNL Adobe Commerce]

이 메서드는 Commerce Cloud 인스턴스의 [!DNL Payment Services] 확장을 설치하는 데 사용됩니다.

1. `composer.json` 파일 업데이트:

   ```bash
   composer require magento/payment-services --no-update
   ```

1. 종속성을 업데이트하고 확장을 설치합니다.

   ```bash
   composer update magento/payment-services --with-dependencies
   ```

   `composer update` 명령을 사용하여 모든 루트 종속성을 업데이트합니다.

1. 변경 사항을 커밋하고 푸시합니다.

### 온-프레미스 및 기타 구성

이 메서드는 온-프레미스 인스턴스 및 [!DNL Magento Open Source] 고객의 [!DNL Payment Services] 확장을 설치하는 데 사용됩니다.

1. 확장을 가져오려면 다음 명령을 실행합니다.

   ```bash
   composer require magento/payment-services --no-update
   ```

1. 종속성을 업데이트하고 확장을 설치합니다.

   ```bash
   composer update magento/payment-services --with-dependencies
   ```

   `composer update` 명령을 사용하여 모든 루트 종속성을 업데이트합니다.

1. 인스턴스 업그레이드:

   ```bash
   bin/magento setup:upgrade
   ```

1. 캐시를 지웁니다.

   ```bash
   bin/magento cache:clean
   ```

1. 변경 사항을 커밋합니다.
1. 커밋된 코드가 배포되었는지 확인하려면 인스턴스 를 업데이트합니다.

>[!NOTE]
>
> [!DNL Payment Services] 1.6.1은 PHP 버전 7.x와 호환됩니다. 그러나 최신 [!DNL Payment Services] 버전으로 업데이트하는 것이 좋습니다.

## 확장 업그레이드

[!DNL Payment Services]의 새 버전이 출시되면 확장을 쉽게 업그레이드할 수 있습니다.

1. 패키지의 최신 버전을 얻으려면:

   ```bash
   composer update magento/payment-services --with-dependencies
   ```

   `composer update` 명령을 사용하여 모든 루트 종속성을 업데이트합니다.

1. 작성기 업데이트 후 다음을 실행합니다.

   ```bash
   bin/magento setup:upgrade
   ```

1. 변경 사항을 커밋하고 푸시합니다.

## 문제 해결

[!DNL Payment Services] 확장을 설치하려고 하면 오류가 표시될 수 있습니다. 다음 문제 해결 방법을 사용하여 오류를 해결하십시오.

### 저장소 목록

저장소 목록에 `repo.magento.com`이(가) 있는지 확인합니다.

### 잘못된 작성기 키

잘못된 작성기 키가 있음을 나타내는 다음 오류가 표시되면

```
Could not find a matching version of package magento/payment-services. Check the package spelling, your version constraint and that the package is available in a stability which matches your minimum-stability (stable).
```

작성기 키가 유효하고 다른 Magento 패키지에 액세스할 수 있는지 확인하십시오.

구성된 Composer 키를 보려면 다음 작업을 수행하십시오.

1. `auth.json` 파일의 위치 찾기:

   ```bash
   composer config --global home
   ```

1. `auth.json` 파일 보기:

   ```bash
   cat /path/to/auth.json
   ```

1. [Commerce 계정 `MageID`과(와) 연결된 키](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/authentication-keys)를 확인하세요.

### 메모리가 부족하여 PHP를 사용할 수 없습니다.

PHP에 대한 충분한 메모리가 없다는 것을 나타내는 다음 오류가 표시됩니다.

```
Fatal error: Allowed memory size of 2146435072 bytes exhausted (tried to allocate 4096 bytes) in phar:///usr/local/bin/composer/src/Composer/DependencyResolver/RuleWatchGraph.php on line 52
```

`php.ini`의 환경에서 PHP에 대한 [메모리 제한을 늘립니다](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/app/php-settings#increase-php-memory-limit).

또는 `php -d memory_limit=-1 [path to composer]/composer require magento/payment-services` 명령을 사용하여 메모리 제한을 지정할 수 있습니다.

For example:

```bash
php -d memory_limit=-1 vendor/bin/composer require magento/payment-services
```
