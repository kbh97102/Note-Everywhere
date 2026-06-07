# Module Structure

## Status

Draft

## Direction

Compose Multiplatform 프로젝트는 기능과 계층을 함께 고려해 모듈화합니다.

특히 presentation 계층은 DesignSystem과 기능별 UI 모듈로 나눕니다.

## Proposed Modules

```text
:shared:domain
:shared:data
:shared:presentation:designsystem
:shared:presentation:home
:shared:presentation:task-create
:shared:presentation:task-edit
:shared:presentation:task-swipe-delete
:app:android
:app:ios
:app:macos
```

실제 Gradle 모듈 이름은 프로젝트 생성 시 조정할 수 있지만, 역할 분리는 유지합니다.

## Module Responsibilities

### :shared:domain

- Task entity
- Schedule value object
- TaskProgress enum
- Repository interface
- Use cases

### :shared:data

- Repository implementation
- Local data source
- Persistence model
- Mapper

### :shared:presentation:designsystem

- Color token
- Typography token
- Spacing token
- Common button
- Common text field
- Modal/sheet base
- Progress chip
- Swipe action surface

### :shared:presentation:home

- macOS Home screen
- Today summary
- Task list
- Task detail panel
- Swipe delete state

### :shared:presentation:task-create

- Task create modal
- Task create MVI contract
- Task create validation state

### :shared:presentation:task-edit

- Task edit modal
- Task edit MVI contract
- Existing Task value binding

### :shared:presentation:task-swipe-delete

- Swipe delete UI behavior
- Delete action exposure state
- Delete intent dispatch

## Presentation File Structure

각 기능 UI 모듈은 다음 구조를 권장합니다.

```text
feature/
  Screen.kt
  Contract.kt
  ViewModel.kt
  sections/
  components/
  preview/
```

예시:

```text
home/
  HomeScreen.kt
  HomeContract.kt
  HomeViewModel.kt
  sections/
    HomeSidebarSection.kt
    TaskListSection.kt
    TaskDetailSection.kt
  components/
    TaskRow.kt
    TaskProgressChip.kt
    SwipeDeleteRow.kt
  preview/
    HomePreviewData.kt
```

## Dependency Rules

```text
home -> designsystem
task-create -> designsystem
task-edit -> designsystem
task-swipe-delete -> designsystem
presentation feature -> domain
data -> domain
app -> presentation modules
```

금지:

- DesignSystem이 feature UI에 의존
- domain이 presentation 또는 data에 의존
- feature UI 모듈끼리 직접 강하게 의존
- Composable 안에서 repository 직접 호출

## Reuse Rule

Task Create와 Task Edit은 필드 구조가 같으므로 form component를 공유할 수 있습니다.

공유 후보:

- TaskTitleField
- TaskMemoField
- TaskProgressSelector
- TaskScheduleFields
- TaskFormActions

공유하더라도 create/edit의 MVI contract는 분리합니다.

