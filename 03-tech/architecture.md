# Architecture

## Status

Draft

## Overview

noteEveryWhere는 Clean Architecture와 MVI를 함께 사용합니다.

```text
presentation
  -> domain
  -> data
```

의존성 방향은 presentation에서 domain으로, data에서 domain으로 향합니다. domain은 가장 안쪽 계층으로 유지합니다.

## Layers

### Domain

비즈니스 규칙을 담습니다.

포함 항목:

- Entity
- Value object
- Repository interface
- Use case

예시:

```text
Task
Schedule
TaskProgress
TaskRepository
CreateTaskUseCase
UpdateTaskUseCase
DeleteTaskUseCase
ObserveTodayTasksUseCase
```

### Data

데이터 접근과 저장소 구현을 담당합니다.

포함 항목:

- Repository implementation
- Local data source
- DTO 또는 database model
- Mapper

Milestone 1에서는 local first를 우선합니다.

### Presentation

화면 상태, 사용자 입력, Compose UI를 담당합니다.

presentation은 한 번 더 모듈화합니다.

```text
presentation
- DesignSystem
- Home UI
- Task Create UI
- Task Edit UI
- Task Swipe Delete UI
```

## MVI Contract

각 화면 또는 기능 단위는 다음 계약을 둡니다.

```text
State
Intent
Effect
```

예시:

```text
TaskCreateState
TaskCreateIntent
TaskCreateEffect
```

## State Ownership

화면 상태는 presentation의 ViewModel 또는 Presenter가 소유합니다.

Composable은 state를 받아 렌더링하고, 사용자 액션을 intent로 전달합니다.

Composable 내부에서 도메인 로직을 처리하지 않습니다.

## Error Handling

Milestone 1에서는 복잡한 에러 정책을 만들지 않습니다.

필수 검증:

- title은 비어 있을 수 없음
- startAt은 dueAt보다 늦을 수 없음

검증 결과는 State에 반영하고 UI가 표시합니다.

## Data Flow

```text
User action
-> Intent
-> ViewModel
-> UseCase
-> Repository
-> State update
-> Compose render
```

## Planning Boundary

아키텍처 구현 중 기획과 충돌하는 더 좋은 아이디어가 생겨도 기획 문서를 바로 수정하지 않습니다.

변경은 사용자 컨펌 이후 ADR과 기획 문서를 함께 수정합니다.

