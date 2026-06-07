# Development Guidelines

## Status

Draft

## Core Direction

noteEveryWhere는 Compose Multiplatform 기반으로 Android, iOS, macOS를 지원합니다.

개발 구조는 다음 원칙을 따릅니다.

- Compose Multiplatform
- MVI
- Clean Architecture
- presentation 계층 추가 모듈화
- 기존 기획서와 HTML 프로토타입 우선 준수

## Planning and Design Rules

기획서와 초안 디자인은 구현의 기준입니다.

개발 도중 더 좋은 기획 방향이나 디자인 개선안이 떠오르더라도 기존 기획서 내용을 임의로 변경하지 않습니다.

변경이 필요하다고 판단되면 다음 순서를 따릅니다.

1. 변경 제안 내용을 별도 메모 또는 대화로 정리합니다.
2. 사용자에게 컨펌을 요청합니다.
3. 컨펌을 받은 뒤 기획 문서, 디자인 문서, ADR을 수정합니다.
4. 수정된 문서를 기준으로 구현합니다.

컨펌 없이 변경하면 안 되는 항목은 다음과 같습니다.

- Task 데이터 모델
- Milestone 1 범위
- 화면 구조
- HTML 프로토타입의 주요 레이아웃
- 사용자 플로우
- 삭제, 추가, 수정 등 핵심 액션 방식

## UI Implementation Rules

한 화면은 큰 section 단위로 먼저 나누고, 각 section 내부를 작은 컴포넌트로 분리합니다.

예시:

```text
MacosHomeScreen
- HomeTopBar
- HomeSidebar
- HomeSummarySection
- TaskListSection
- TaskDetailSection
```

section 내부는 다시 작은 컴포넌트로 나눕니다.

```text
TaskListSection
- TaskTimeGroup
- TaskRow
- TaskSwipeDeleteAction
- TaskProgressChip
```

## File Size Rule

한 파일에 너무 많은 컴포넌트를 몰아넣지 않습니다.

권장 기준:

- Screen 파일: 화면 조립 중심
- Section 파일: 화면의 큰 영역
- Component 파일: 재사용 가능한 작은 UI
- State/Intent/Effect 파일: MVI 계약

Screen 파일은 UI 전체 구조를 읽기 쉽게 보여주는 역할만 합니다. 세부 UI 구현이 길어지면 별도 파일로 분리합니다.

## Compose Rules

- 화면 단위 composable은 상태를 직접 만들지 않고 state를 받습니다.
- 사용자 액션은 callback 또는 intent dispatcher로 전달합니다.
- UI는 가능한 한 stateless composable로 유지합니다.
- Preview 또는 sample data는 실제 도메인 로직과 분리합니다.
- 디자인 시스템 토큰을 직접 hardcoding하지 않고 DesignSystem 모듈에서 가져옵니다.

## MVI Rules

각 기능 화면은 MVI 계약을 명확히 둡니다.

```text
State: 화면에 필요한 모든 상태
Intent: 사용자의 의도 또는 입력
Effect: 일회성 이벤트
Reducer: 이전 State와 Intent/Result를 기반으로 새 State 생성
```

화면 composable은 다음 흐름을 따릅니다.

```text
State render
User action
Intent dispatch
State update
Effect handling
```

## Clean Architecture Rules

의존성 방향은 바깥에서 안쪽으로 흐르지 않습니다.

```text
presentation -> domain <- data
```

domain은 presentation과 data를 모릅니다.

presentation은 use case를 호출합니다.

data는 repository 구현체와 local/remote data source를 관리합니다.

## Implementation Priority

Milestone 1 구현 순서는 다음을 우선합니다.

1. Task 데이터 모델
2. DesignSystem 기초 토큰과 공통 컴포넌트
3. macOS Home 화면
4. Task Create modal
5. Task Edit modal
6. Task Swipe Delete
7. 로컬 저장소

