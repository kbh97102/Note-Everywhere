# Data Model Draft

## Event

- id
- title
- startAt
- endAt
- timezone
- note
- recurrenceRule
- createdAt
- updatedAt

## Task

- id
- title
- dueAt
- completedAt
- priority
- note
- createdAt
- updatedAt

## Routine

- id
- title
- recurrenceRule
- active
- createdAt
- updatedAt

## Design Notes

- 일정과 할 일을 하나의 상위 타입으로 묶을지 검토가 필요합니다.
- 반복 규칙은 초기부터 별도 모델로 관리하는 편이 확장에 유리합니다.
- 동기화 가능성을 고려하면 모든 주요 엔티티에 stable id와 updatedAt이 필요합니다.

