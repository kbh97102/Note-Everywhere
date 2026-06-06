# macOS Home Screen

## Status

Fixed for first macOS prototype

## Prototype

`prototypes/macos-home.html`

## Purpose

macOS 앱의 홈 화면은 오늘의 일정과 할 일을 빠르게 확인하고, 선택한 일정의 상세 내용을 오른쪽 패널에서 바로 검토하는 화면입니다.

## Layout

- 상단: macOS 타이틀바와 날짜 이동, 새 일정 버튼
- 좌측: 앱 네비게이션, 미니 캘린더, 동기화 상태
- 중앙: 오늘의 일정 리스트
- 우측: 선택된 일정 상세 정보와 체크리스트

## Summary Items

- 일정 수
- 할 일 수

## Notes

- 집중 시간 요약은 현재 홈 화면 범위에서 제외합니다.
- macOS에서는 넓은 화면을 활용해 리스트와 상세 패널을 동시에 보여줍니다.
- iOS와 Android에서는 같은 정보 구조를 유지하되 상세 패널은 별도 화면 또는 bottom sheet로 전환하는 방향을 검토합니다.

## Feature Spec

상세 기능 기획은 `02-design/macos-home-feature-spec.md`에서 관리합니다.
