---
source-git-commit: 80c4b41ceb0d8809f82db61ce9c3df6b7e1d7102
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---
# 레이크 라이브러리 파일

이 디렉터리에는 기능별로 구성된 레이크 작업 정의가 포함되어 있습니다. 레이크는 이 디렉터리에 있는 모든 `.rake`개의 파일을 자동으로 로드합니다.

## 파일 구성

### `adobe-docs-tasks.rake`

Experience League 설명서 저장소 레이크 작업에서 Adobe Commerce에 대한 일반적인 요구 사항, 공유 기능 및 네임스페이스가 지정되지 않은 작업이 포함됩니다.

- `whatsnew` - 뉴스 다이제스트에 대한 데이터 생성(기본값: 마지막 업데이트 이후)
- `render` - 템플릿 파일 렌더링 및 유지 관리에 포함

### `includes.rake`

`:includes` 네임스페이스에 구성된 포함 관리 작업을 포함합니다.

- `includes:maintain_relationships` - Markdown 파일에서 포함 관계 검색 및 유지 관리
- `includes:maintain_timestamps` - 포함 파일 변경 내용에 따라 타임스탬프 추가/업데이트
- `includes:maintain_all` - 두 작업을 순서대로 실행합니다.
- `includes:unused` - 사용하지 않은 포함 파일 찾기

### `images.rake`

`:images` 네임스페이스로 구성된 이미지 관리 작업을 포함합니다.

- `images:optimize` - 수정된 커밋되지 않은 파일의 이미지 최적화
- `images:unused` - 프로젝트에서 사용하지 않는 이미지 찾기

## 작동 방식

Rake는 `.rake` 디렉터리에 있는 `rakelib/`개의 파일을 자동으로 검색하여 로드합니다. 이를 통해 다음과 같은 작업을 수행할 수 있습니다.

1. **기능별로 작업 구성** - 관련 작업을 함께 그룹화
2. **기본 Rakefile을 정리합니다** - 핵심 프로젝트 작업에 집중
3. **새 작업 그룹을 쉽게 추가** - 새 `.rake`개 파일만 만들기
4. **문제 분리 유지** - 각 파일이 특정 도메인을 처리합니다.

## 새 작업 그룹 추가

관련 작업의 새 그룹을 추가하려면 다음을 수행합니다.

1. 이 디렉터리에 새 `.rake` 파일 만들기
2. 설명 네임스페이스 사용(예: 이미지 관련 작업의 경우 `namespace :images`)
3. 네임스페이스 내에서 작업 정의
4. 레이크가 자동으로 로드됨

## 예제 구조

```ruby
namespace :your_namespace do
  desc 'Description of what this task does'
  task :task_name do
    # Task implementation
  end
end
```

## 사용

작업은 생성 후 즉시 사용할 수 있습니다.

```bash
rake your_namespace:task_name
```

## 이점

- **모듈성**: 각 파일은 특정 영역에 중점을 둡니다.
- **유지 관리**: 특정 작업 그룹을 더 쉽게 찾고 수정할 수 있습니다.
- **확장성**: 기본 Rakefile을 어지럽히지 않고 많은 작업 그룹을 추가할 수 있습니다.
- **팀 개발**: 다른 개발자가 다른 작업 그룹에서 작업할 수 있습니다.
