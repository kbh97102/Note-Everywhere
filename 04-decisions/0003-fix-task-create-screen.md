# ADR 0003: Fix Task Create Screen Direction

## Status

Accepted

## Context

Milestone 1에서는 할일 추가 화면을 최소 필드로 제한합니다. 할일은 Task가 본체이고, 일정은 Task 안의 시간 조건으로 다룹니다.

## Decision

`prototypes/task-create-macos.html`을 macOS 할일 추가 화면의 첫 기준 디자인으로 고정합니다.

화면은 홈 화면 위에 modal로 표시합니다.

포함 필드는 다음으로 제한합니다.

- 제목
- 메모
- 진행 정도
- 시작기간
- 마감기한

새 할일의 시작기간과 마감기한은 기본적으로 비어 있습니다. 홈 화면에서 보고 있던 날짜는 자동으로 입력하지 않습니다.

## Excluded

- 태그
- 우선순위
- 알림
- 반복
- 하위 작업
- 연결 문서
- 저장 조건 안내 영역
- 필드 하단 description 문구

## Consequences

- 이후 macOS 할일 추가 UI 구현은 이 프로토타입을 기준으로 합니다.
- iOS와 Android는 같은 필드 구조를 유지하되, 플랫폼에 맞게 sheet 또는 full-screen form으로 바꿀 수 있습니다.
- 할일 추가 화면의 상세 기획은 `02-design/task-create-screen.md`에서 관리합니다.
