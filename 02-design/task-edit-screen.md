# Task Edit Screen

## Status

Fixed for first macOS prototype

## Scope

Milestone 1의 할일 수정 화면입니다. 할일 추가 화면과 같은 필드 구조를 사용하되, 기존 Task 값을 불러와 수정합니다.

## Related Screens

- `02-design/task-create-screen.md`
- `prototypes/task-create-macos.html`

## Prototype

`prototypes/task-edit-macos.html`

## Entry Points

- macOS 홈 화면 우측 상세 패널의 `편집` 버튼
- 할일 리스트에서 선택 후 Enter
- 할일 상세 영역에서 편집 액션

## Presentation

macOS에서는 홈 화면 위에 modal 형태로 표시합니다.

할일 추가 화면과 같은 modal 레이아웃을 재사용합니다.

## Fields

| Field | Required | UI | Initial Value | Notes |
| --- | --- | --- | --- | --- |
| `title` | Yes | 단일 행 텍스트 입력 | 기존 Task의 `title` | 할일의 간단한 요약 |
| `memo` | No | 여러 행 텍스트 입력 | 기존 Task의 `memo` | 할일의 구체적인 내용 |
| `progress` | Yes | segmented control | 기존 Task의 `progress` | `todo`, `inProgress`, `done` |
| `schedule.startAt` | No | 날짜/시간 입력 | 기존 Task의 `schedule.startAt` | 시작기간 |
| `schedule.dueAt` | No | 날짜/시간 입력 | 기존 Task의 `schedule.dueAt` | 마감기한 |

## Field Rules

수정 화면의 필드 규칙은 할일 추가 화면과 동일합니다.

- title은 비어 있을 수 없습니다.
- memo는 비어 있을 수 있습니다.
- progress는 항상 하나의 값을 가져야 합니다.
- startAt과 dueAt은 둘 다 비워둘 수 있습니다.
- startAt만 입력할 수 있습니다.
- dueAt만 입력할 수 있습니다.
- 둘 다 입력된 경우 startAt은 dueAt보다 늦을 수 없습니다.

## Initial Values

수정 화면은 새 기본값을 만들지 않고, 선택된 Task의 현재 값을 그대로 표시합니다.

| Case | Initial Value |
| --- | --- |
| title 있음 | 기존 title |
| memo 없음 | 빈 입력 |
| progress 있음 | 기존 progress |
| startAt 없음 | 빈 입력 |
| dueAt 없음 | 빈 입력 |

## Actions

### Save

기존 Task를 수정하고 화면을 닫습니다.

#### Enabled When

- `title`이 비어 있지 않음
- `startAt`과 `dueAt`의 순서가 유효함
- 기존 값과 비교해 변경사항이 있음

#### Result

- 기존 Task가 업데이트됩니다.
- Task의 `id`는 바뀌지 않습니다.
- 홈 화면의 리스트, 요약 값, 상세 패널이 갱신됩니다.
- 수정된 Task는 선택 상태를 유지합니다.

### Cancel

변경사항을 버리고 화면을 닫습니다.

#### Unsaved Changes

기존 값과 다른 입력값이 있으면 닫기 전에 확인이 필요합니다.

확인 문구는 후속 UI 문구 작업에서 확정합니다.

## Difference From Create

| Area | Create | Edit |
| --- | --- | --- |
| Screen title | 새 할일 | 할일 수정 |
| Data source | 빈 값과 기본값 | 기존 Task 값 |
| Save result | 새 Task 생성 | 기존 Task 업데이트 |
| id | 저장 시 새로 생성 | 기존 id 유지 |
| Save enabled | 유효한 입력값 | 유효한 입력값과 변경사항 |

## MVP Decisions

- 수정 화면은 할일 추가 화면의 필드와 레이아웃을 재사용합니다.
- 수정 중에는 사용자가 id를 볼 수 없고 수정할 수도 없습니다.
- 일정이 비어 있는 기존 Task는 시작기간과 마감기한 입력이 모두 비어 있는 상태로 표시합니다.
- 홈 화면 날짜는 수정 화면의 일정 값에 영향을 주지 않습니다.
