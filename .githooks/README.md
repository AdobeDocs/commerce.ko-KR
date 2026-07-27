---
source-git-commit: 9de8e747353a9042d5b6d7c150688e705c21d2c6
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 0%

---
# 이미지 최적화를 위한 사전 커밋 후크

이 디렉토리에는 이미지를 저장소에 커밋하기 전에 자동으로 최적화하는 사전 커밋 후크가 포함되어 있습니다.

## 후크가 수행하는 작업

- **준비된 이미지 파일 `.png`, `.jpeg`, `.jpg`, `.gif`, `.svg` 자동 검색**
- **래스터 이미지(`.png`, `.jpeg`, `.jpg`, `.gif`)를 압축하고 최적화하려면`image_optim`**&#x200B;을(를) 실행하십시오.
- **최적화된 이미지 다시 스테이징** 자동
- **커밋된 모든 래스터 이미지가 올바르게 최적화되었는지 확인**
- **크기 제한에 대해 준비된 SVG**&#x200B;을(를) 확인하고 `help/`의 모든 파일에서 크기가 큰 SVG을 참조하는 경우 커밋을 중단합니다(그렇지 않으면 경고하십시오).

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

Checking images ...
path/to/your/image.png    100.00%
Pre-commit image checks complete!
```

### 단위 테스트

후크의 SVG 링크 감지 논리(`help/`에서 크기가 큰 SVG을 참조하는지 여부를 결정하는 논리)는 Ruby의 번들 `minitest`만 필요한 단위 테스트에서 다룹니다(gems 없음 또는 `_jekyll` 설정 없음).

```bash
ruby .githooks/test/svg_link_checker_test.rb
```

## 이미지 지침

- **PNG**: 스크린샷 및 UI 요소에 사용합니다(자동으로 최적화됨).
- **JPEG**: 사진에 사용(자동으로 최적화됨)
- **GIF**: 애니메이션에 사용(자동으로 최적화됨)
- **SVG**: 아이콘 및 간단한 그래픽에 사용됩니다(최적화되지 않았지만 크기 제한에 따라 선택됨. 크기가 큰 SVG이 `help/`에서 연결되어 있는 경우에만 커밋이 실패함).

사전 커밋 후크는 커밋 시 `.png`, `.jpeg`/`.jpg` 및 `.gif` 이미지를 자동으로 최적화하고 크기 제한(140KB)에 대해 준비된 SVG를 확인합니다.

준비된 SVG이 한도를 초과하여 `help/`의 파일에서 참조되면 커밋이 중단됩니다. `help/`의 어느 곳에서든 대형 SVG이 참조되지 않으면 후크에서 경고만 인쇄하고 커밋이 진행됩니다. 대신 크기를 초과한 SVG를 PNG 로 변환합니다.

```bash
cd _jekyll
bundle exec rake images:svg_to_png path=../help/assets/image.svg
```

경로가 `_jekyll`을(를) 기준으로 하므로 `help/` 아래의 이미지가 `../help/...`(으)로 참조됩니다.

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
- **SVG**: 최적화되지 않았지만(벡터 그래픽과 애니메이션을 보존하기 위해 `image_optim`에서 제외) 140KB 크기 제한에 대해 확인되었습니다.

## 문제 해결

### 후크가 실행 중이 아님

- 후크 구성 확인: `git config core.hooksPath`
- 후크 파일이 실행 가능한지 확인합니다. `chmod +x .githooks/pre-commit`
- `_jekyll` 디렉터리가 있는 올바른 리포지토리에 있는지 확인합니다.

### 최적화 실패

- `_jekyll` 디렉터리에서 `bundle install`이(가) 실행되었는지 확인
- `adobe-comdox-exl-rake-tasks` gem이 설치되어 있는지 확인합니다(`images:optimize`, `images:check_size` 및 `images:svg_to_png` 레이크 작업을 후크에서 제공함).
- `.image_optim.yml` 구성 파일 검토

### SVG이 크기 제한을 초과합니다.

- 준비된 SVG이 140KB를 초과하고 `help/`의 파일에서 참조되면 커밋이 중단됩니다. 그렇지 않으면 후크만 경고되고 커밋이 진행됩니다.
- SVG을 PNG로 변환: `cd _jekyll && bundle exec rake images:svg_to_png path=../help/assets/image.svg`(경로는 `_jekyll`에 상대적이므로 `help/` 아래의 이미지가 `../help/...`(으)로 참조됨)
- 그런 다음 SVG 대신 PNG를 준비하고 다시 커밋합니다

### 성능 문제

- `_jekyll/.image_optim.yml`에서 스레드 수 조정
- 자세한 오류 정보를 보려면 `DEBUG=1` 환경 변수를 설정하십시오.

## 작동 방식

1. **사전 커밋 트리거**: `git commit`을(를) 실행하면 후크가 자동으로 실행됩니다
2. **이미지 검색**: 이미지 확장에 대해 준비된 파일을 검사합니다.
3. **최적화**: 준비된 각 PNG, JPEG 또는 GIF에서 `image_optim`을(를) 실행합니다.
4. **다시 스테이징**: 최적화된 이미지를 스테이징 영역에 자동으로 다시 추가합니다.
5. **SVG 크기 확인**: 140KB 크기 제한에 대해 준비된 각 SVG을 확인합니다.
6. **커밋 진행**: 최적화가 성공하고 `help/`에서 크기가 큰 SVG이 참조되지 않으면 커밋이 정상적으로 계속됩니다. 그렇지 않으면 커밋이 중단됩니다(`help/`에서 크기가 큰 SVG이 참조되지 않으면 경고만 트리거됨).

## 지원되는 이미지 형식

- **PNG**(`.png`) - 무손실 및 손실 압축
- **JPEG**(`.jpg`, `.jpeg`) - 메타데이터 정리 시 손실 압축
- **GIF**(`.gif`) - 애니메이션 및 정적 최적화
- **SVG** (`.svg`) - 최적화되지 않았지만(품질을 유지하기 위해 있는 그대로 커밋) 140KB 크기 제한에 대해 확인되었습니다. 제한을 초과하고 `help/`에서 SVG을 참조하면 커밋이 중단됩니다(그렇지 않으면 후크만 경고됨).

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
