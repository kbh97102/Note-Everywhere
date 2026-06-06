# ADR 0005: Defer Search and Add Swipe Delete

## Status

Accepted

## Context

Milestone 1은 간단한 할일 관리 기능을 여러 플랫폼에서 완성하고 출시하는 것을 목표로 합니다. 검색은 유용하지만 첫 출시의 핵심 흐름에는 포함하지 않습니다. 반면 삭제는 기본적인 데이터 관리 동작이므로 리스트에서 빠르게 실행할 수 있어야 합니다.

## Decision

검색 기능과 검색 결과 없음 상태는 다음 마일스톤으로 넘깁니다.

Milestone 1에는 리스트 항목 스와이프 삭제를 포함합니다.

`prototypes/task-swipe-delete-macos.html`을 macOS 스와이프 삭제 상태의 첫 기준 디자인으로 사용합니다.

## Consequences

- 현재 macOS 홈 화면에는 검색 입력과 Search 네비게이션 항목을 표시하지 않습니다.
- Task 카드를 왼쪽으로 밀면 삭제 버튼을 노출합니다.
- 삭제 확인 dialog는 Milestone 1에서 사용하지 않습니다.
- 스와이프 삭제 상세 기획은 `02-design/task-swipe-delete.md`에서 관리합니다.
