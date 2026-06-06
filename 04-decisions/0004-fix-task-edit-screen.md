# ADR 0004: Fix Task Edit Screen Direction

## Status

Accepted

## Context

Milestone 1의 할일 수정 화면은 할일 추가 화면과 같은 필드 구조를 사용합니다. 차이는 기존 Task 값을 불러와 수정하고, 저장 시 새 Task를 만들지 않고 기존 Task를 업데이트한다는 점입니다.

## Decision

`prototypes/task-edit-macos.html`을 macOS 할일 수정 화면의 첫 기준 디자인으로 고정합니다.

화면은 홈 화면 위에 modal로 표시합니다.

할일 추가 화면과 같은 레이아웃을 재사용하며, 다음 차이만 둡니다.

- 화면 제목은 `할일 수정`
- 기존 Task 값이 입력된 상태로 표시
- 진행 정도는 기존 Task의 progress를 선택 상태로 표시
- 저장 버튼 문구는 `변경 저장`
- 저장 시 기존 Task의 id를 유지

## Excluded

- 수정 화면 내 삭제 기능
- id 노출
- 태그
- 우선순위
- 알림
- 반복
- 하위 작업
- 연결 문서

## Consequences

- 이후 macOS 할일 수정 UI 구현은 이 프로토타입을 기준으로 합니다.
- 할일 추가/수정 화면은 같은 컴포넌트를 공유할 수 있습니다.
- iOS와 Android는 같은 필드 구조를 유지하되, 플랫폼에 맞게 sheet 또는 full-screen form으로 바꿀 수 있습니다.
- 할일 수정 화면의 상세 기획은 `02-design/task-edit-screen.md`에서 관리합니다.
