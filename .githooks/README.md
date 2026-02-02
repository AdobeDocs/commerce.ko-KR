---
source-git-commit: 65313a91d28d199c142e33f9b77b7e59bbb512ac
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 0%

---
# 이미지 최적화를 위한 사전 커밋 후크

이 디렉토리에는 이미지를 저장소에 커밋하기 전에 자동으로 최적화하는 사전 커밋 후크가 포함되어 있습니다.

## 후크가 수행하는 작업

- **스테이징된 이미지 파일(PNG, JPG, JPEG, GIF)**&#x200B;개 자동 감지
- **`image_optim`**&#x200B;을(를) 실행하여 이미지 압축 및 최적화
- **최적화된 이미지 다시 스테이징** 자동
- **커밋된 모든 이미지가 올바르게 최적화되었는지 확인**

## 이점

- 저장소 크기 감소
- 설명서를 위한 빠른 페이지 로드
- 모든 기여자에서 일관된 이미지 품질
- 수동 최적화 불필요

## 사전 요구 사항

- Ruby 3.0 이상
- 번들러
- Git

## 설정

### 자동 설정(권장)

```bash
.githooks/setup-hooks.sh
```

### 수동 설정

```bash
git config core.hooksPath .githooks
chmod +x .githooks/*
```

### 프로젝트 설정 완료

1. 저장소 복제:

   ```bash
   git clone <repository-url>
   cd commerce-admin.en
   ```

2. 사전 커밋 후크 활성화:

   ```bash
   .githooks/setup-hooks.sh
   ```

3. Jekyll 종속성 설치:

   ```bash
   cd _jekyll
   bundle install
   ```

## 후크 테스트

1. 저장소에 이미지 파일 추가
2. 스테이징: `git add <image-file>`
3. 커밋 시도: `git commit -m 'test'`
4. 후크는 이미지를 자동으로 최적화합니다

### 예상 출력

```bash
Found 1 staged image(s). Running optimization...
Optimizing: path/to/your/image.png
Re-staged optimized image: path/to/your/image.png
Image optimization complete!
```

## 이미지 지침

- **PNG**: 스크린샷 및 UI 요소에 사용합니다(자동으로 최적화됨).
- **JPEG**: 사진에 사용(자동으로 최적화됨)
- **GIF**: 애니메이션에 사용(자동으로 최적화됨)
- **SVG**: 아이콘 및 단순 그래픽(후크에서 처리하지 않음, 그대로 커밋)에 사용합니다.

사전 커밋 후크는 커밋 시 PNG, JPEG 및 GIF 이미지를 자동으로 최적화합니다.

## 수동 최적화

수동 이미지 최적화:

```bash
cd _jekyll
bundle exec rake images:optimize path=../path/to/images
```

## 구성

후크는 구성 파일 `_jekyll/.image_optim.yml`을(를) 사용하여 최적화 설정을 사용자 지정합니다.

- **PNG**: `advpng`, `optipng` 및 `pngquant` 사용
- **JPEG**: `jhead`, `jpegoptim` 및 `jpegtran` 사용
- **GIF**: `gifsicle` 사용
- **SVG**: 처리되지 않음(벡터 그래픽과 애니메이션을 유지하기 위해 검색에서 제외)

## 문제 해결

### 후크가 실행 중이 아님

- 후크 구성 확인: `git config core.hooksPath`
- 후크 파일이 실행 가능한지 확인합니다. `chmod +x .githooks/pre-commit`
- `_jekyll` 디렉터리가 있는 올바른 리포지토리에 있는지 확인합니다.

### 최적화 실패

- `bundle install` 디렉터리에서 `_jekyll`이(가) 실행되었는지 확인
- `adobe-comdox-exl-rake-tasks` gem이 설치되어 있는지 확인합니다(`image_optim` 제공).
- `.image_optim.yml` 구성 파일 검토

### 성능 문제

- `_jekyll/.image_optim.yml`에서 스레드 수 조정
- 자세한 오류 정보를 보려면 `DEBUG=1` 환경 변수를 설정하십시오.

## 작동 방식

1. **사전 커밋 트리거**: `git commit`을(를) 실행하면 후크가 자동으로 실행됩니다
2. **이미지 검색**: 이미지 확장에 대해 준비된 파일을 검사합니다.
3. **최적화**: 각 준비된 이미지에서 `image_optim`을(를) 실행합니다.
4. **다시 스테이징**: 최적화된 이미지를 스테이징 영역에 자동으로 다시 추가합니다.
5. **커밋 진행**: 최적화가 성공하면 커밋은 정상적으로 계속됩니다

## 지원되는 이미지 형식

- **PNG**(`.png`) - 무손실 및 손실 압축
- **JPEG**(`.jpg`, `.jpeg`) - 메타데이터 정리 시 손실 압축
- **GIF**(`.gif`) - 애니메이션 및 정적 최적화
- **SVG**(`.svg`) - 후크에서 처리되지 않음(품질을 유지하기 위해 있는 그대로 커밋)

## 우수 사례

1. **후크 테스트**: 작은 이미지를 먼저 커밋하여 작동하는지 확인하십시오
2. **변경 내용 검토**: git 차이를 확인하여 최적화 결과를 확인하십시오.
3. **성능 모니터링**: 큰 이미지를 최적화하는 데 시간이 걸릴 수 있습니다.
4. **버전 제어**: 후크가 이 `.githooks/` 디렉터리에 저장됩니다.

## 지원

사전 커밋 후크가 있는 문제의 경우:

1. 후크 출력에 오류 메시지 확인
2. `image_optim` 설정이 작동하는지 확인
3. 수동 레이크 작업으로 먼저 테스트
4. 후크 로그 및 구성 검토
5. 후크 구성 확인: `git config core.hooksPath`
