# Task Create Screen

## Status

Fixed for first macOS prototype

## Scope

Milestone 1의 할일 추가 화면입니다. 이 화면은 새 Task를 만들기 위한 최소 필드만 제공합니다.

## Prototype

`prototypes/task-create-macos.html`

## Entry Points

- macOS 홈 화면 상단의 `＋ 할일` 버튼
- 키보드 단축키 후보: `Command + N`

## Presentation

macOS에서는 홈 화면 위에 modal 형태로 표시합니다.

- 사용자가 입력 중인 맥락을 유지할 수 있습니다.
- 홈 화면으로 돌아왔을 때 방금 추가한 할일을 리스트에서 바로 확인할 수 있습니다.
- 필드 수가 적어 별도 전체 화면보다 modal이 적합합니다.

## Fields

| Field | Required | UI | Default | Notes |
| --- | --- | --- | --- | --- |
| `title` | Yes | 단일 행 텍스트 입력 | 없음 | 할일의 간단한 요약 |
| `memo` | No | 여러 행 텍스트 입력 | 없음 | 할일의 구체적인 내용 |
| `progress` | Yes | segmented control | `todo` | `todo`, `inProgress`, `done` |
| `schedule.startAt` | No | 날짜/시간 입력 | 없음 | 시작기간 |
| `schedule.dueAt` | No | 날짜/시간 입력 | 없음 | 마감기한 |

## Field Details

### Title

할일을 대표하는 필수 입력값입니다.

#### Rules

- 비어 있으면 저장할 수 없습니다.
- 앞뒤 공백은 저장 전에 제거합니다.
- 한 줄 입력을 기본으로 합니다.

#### Error State

- 저장 시 title이 비어 있으면 title 입력 필드에 오류 상태를 표시합니다.
- 오류 문구는 `제목을 입력하세요.`로 시작합니다.

### Memo

할일에 대한 구체적인 설명을 입력하는 선택값입니다.

#### Rules

- 비어 있어도 저장할 수 있습니다.
- 여러 줄 입력을 허용합니다.
- 첫 출시에서는 서식 없는 plain text로 저장합니다.

### Progress

할일의 진행 정도입니다.

#### Options

- `todo`: 아직 시작하지 않음
- `inProgress`: 진행 중
- `done`: 완료

#### Default

새 할일의 기본값은 `todo`입니다.

#### UI

segmented control을 사용합니다.

표시 문구는 다음과 같습니다.

- 예정
- 진행 중
- 완료

### Schedule

할일의 시간 조건입니다. 일정은 별도 객체가 아니라 Task 안에 포함됩니다.

#### Fields

- 시작기간: `schedule.startAt`
- 마감기한: `schedule.dueAt`

#### Rules

- 둘 다 비워둘 수 있습니다.
- 시작기간만 입력할 수 있습니다.
- 마감기한만 입력할 수 있습니다.
- 둘 다 입력할 수 있습니다.
- 둘 다 입력된 경우 `startAt`은 `dueAt`보다 늦을 수 없습니다.

#### Error State

- `startAt > dueAt`이면 저장할 수 없습니다.
- 오류 문구는 `시작기간은 마감기한보다 늦을 수 없습니다.`로 시작합니다.

## Actions

### Save

새 Task를 생성하고 화면을 닫습니다.

#### Enabled When

- `title`이 비어 있지 않음
- `startAt`과 `dueAt`의 순서가 유효함

#### Result

- Task가 로컬 저장소에 추가됩니다.
- 홈 화면의 리스트와 요약 값이 갱신됩니다.
- 새로 생성된 Task가 선택 상태가 됩니다.

### Cancel

입력값을 버리고 화면을 닫습니다.

#### Unsaved Changes

입력한 값이 있으면 닫기 전에 확인이 필요합니다.

확인 문구는 후속 UI 문구 작업에서 확정합니다.

## Initial Values

홈 화면에서 진입했을 때의 기본값은 다음과 같습니다.

| Field | Value |
| --- | --- |
| `title` | 비어 있음 |
| `memo` | 비어 있음 |
| `progress` | `todo` |
| `schedule.startAt` | 비어 있음 |
| `schedule.dueAt` | 비어 있음 |

홈 화면 날짜는 새 할일의 일정 기본값으로 자동 적용하지 않습니다. 새 할일의 시작기간과 마감기한은 기본적으로 비어 있습니다.

## Empty Schedule Meaning

일정이 비어 있는 Task는 `언젠가 처리할 할일`입니다.

홈 화면에서는 시간 조건이 있는 할일 아래 또는 별도 `시간 없음` 그룹에 표시하는 방안을 검토합니다.

## Validation Summary

| Case | Valid | Message |
| --- | --- | --- |
| title 없음 | No | 제목을 입력하세요. |
| memo 없음 | Yes | 없음 |
| progress 없음 | No | 내부 기본값 `todo` 사용 |
| startAt 없음, dueAt 없음 | Yes | 없음 |
| startAt 있음, dueAt 없음 | Yes | 없음 |
| startAt 없음, dueAt 있음 | Yes | 없음 |
| startAt <= dueAt | Yes | 없음 |
| startAt > dueAt | No | 시작기간은 마감기한보다 늦을 수 없습니다. |

## MVP Decisions

- 첫 출시에서는 태그, 우선순위, 알림, 반복, 하위 작업을 제공하지 않습니다.
- id는 사용자가 입력하지 않습니다. 앱이 저장 시 자동 생성합니다.
- 생성/수정 시간은 Milestone 1 데이터 모델 범위에서 제외되어 있으므로 UI에 노출하지 않습니다.
