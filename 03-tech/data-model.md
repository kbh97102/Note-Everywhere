# Data Model Draft

## Milestone 1 Direction

첫 출시 목표는 여러 플랫폼에서 간단한 할일 관리 경험을 완성하는 것입니다. 따라서 데이터 모델은 작게 시작합니다.

핵심 개념은 다음과 같습니다.

- `Task`: 사용자가 해야 하는 일의 본체
- `Schedule`: Task 안에 포함되는 시간 조건

즉, 일정은 별도 상위 개념이 아니라 할일이 언제 시작될 수 있고 언제까지 끝나야 하는지를 나타내는 하위 정보입니다.

## Task

| Field | Required | Description |
| --- | --- | --- |
| `id` | Yes | 할일을 식별하기 위한 고유 ID |
| `title` | Yes | 할일의 간단한 요약 |
| `memo` | No | 할일에 대한 구체적인 내용 |
| `progress` | Yes | 할일의 진행 정도 |
| `schedule` | No | 시작기간과 마감기한을 담는 시간 정보 |

## Schedule

| Field | Required | Description |
| --- | --- | --- |
| `startAt` | No | 할일을 시작할 수 있는 시점 또는 기간의 시작 |
| `dueAt` | No | 할일을 끝내야 하는 마감기한 |

## Progress

Milestone 1에서는 진행 정도를 단순한 단계로 표현합니다.

| Value | Meaning |
| --- | --- |
| `todo` | 아직 시작하지 않은 할일 |
| `inProgress` | 진행 중인 할일 |
| `done` | 완료된 할일 |

## Schedule Cases

| startAt | dueAt | Meaning |
| --- | --- | --- |
| 없음 | 없음 | 언젠가 처리할 할일 |
| 있음 | 없음 | 특정 시점부터 시작 가능한 할일 |
| 없음 | 있음 | 마감 전까지 끝내야 하는 할일 |
| 있음 | 있음 | 특정 기간 안에 처리해야 하는 할일 |

## Milestone 1 Task Shape

```text
Task
- id
- title
- memo
- progress
- schedule
  - startAt
  - dueAt
```

## Deferred

아래 항목은 첫 출시 이후 검토합니다.

- 태그
- 우선순위
- 알림
- 반복
- 하위 작업
- 연결 문서
- 동기화 메타데이터
- 생성/수정 시간

## Design Notes

- 첫 출시에서는 기능 수보다 여러 플랫폼에서 안정적으로 동작하는 경험을 우선합니다.
- `id`는 로컬 저장, 수정, 삭제, 향후 동기화의 기준이므로 처음부터 포함합니다.
- `progress`는 완료 여부보다 약간 더 많은 상태를 표현하기 위해 `todo`, `inProgress`, `done` 세 단계로 시작합니다.
- 일정 리스트 화면은 실제로는 Task 목록을 시간 조건에 따라 보여주는 화면입니다.
