# Task Swipe Delete

## Status

Fixed for first macOS prototype

## Scope

Milestone 1의 할일 삭제 액션입니다. 리스트 항목을 왼쪽으로 밀면 오른쪽에 삭제 버튼이 드러나는 방식으로 제공합니다.

## Prototype

`prototypes/task-swipe-delete-macos.html`

## Entry Points

- 홈 화면 할일 리스트의 Task 카드

## Presentation

macOS에서도 리스트 항목을 왼쪽으로 밀어 삭제 액션을 노출합니다.

기본 상태에서는 삭제 버튼을 보이지 않습니다. 사용자가 항목을 왼쪽으로 밀면 카드가 왼쪽으로 이동하고, 오른쪽에 destructive style의 `삭제` 버튼이 나타납니다.

## Content

| Area | Content |
| --- | --- |
| Swipe target | Task 카드 전체 |
| Revealed action | `삭제` |
| Action position | 카드 오른쪽 |
| Action style | destructive |

## Behavior

### Reveal

- 사용자가 Task 카드를 왼쪽으로 밀면 삭제 버튼을 노출합니다.
- 한 번에 하나의 Task만 삭제 버튼 노출 상태가 될 수 있습니다.
- 다른 Task를 선택하거나 다른 영역을 클릭하면 노출 상태를 닫습니다.

### Delete

- 노출된 `삭제` 버튼을 누르면 해당 Task를 삭제합니다.
- 별도 확인 dialog는 표시하지 않습니다.
- 삭제 후 홈 화면 리스트와 요약 값을 갱신합니다.
- 삭제된 Task가 선택 중이었다면 다음 Task를 선택합니다.
- 다음 Task가 없으면 빈 상태를 표시합니다.

## Rules

- 삭제 버튼은 destructive style로 표시합니다.
- 삭제 버튼에는 `삭제` 텍스트를 사용합니다.
- Task의 id는 사용자에게 표시하지 않습니다.
- Milestone 1에서는 삭제 확인 팝업을 사용하지 않습니다.

## Deferred

- 삭제 후 undo toast
- 키보드 기반 삭제 액션
- 우클릭 context menu 삭제

