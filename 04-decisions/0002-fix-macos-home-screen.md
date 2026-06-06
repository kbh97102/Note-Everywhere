# ADR 0002: Fix macOS Home Screen Direction

## Status

Accepted

## Context

noteEveryWhere의 첫 번째 플랫폼별 화면으로 macOS 홈 화면 프로토타입을 만들었습니다. 이 화면은 오늘의 일정 리스트와 선택된 일정의 상세 패널을 동시에 보여주는 구조입니다.

## Decision

`prototypes/macos-home.html`을 macOS 홈 화면의 첫 기준 디자인으로 고정합니다.

홈 화면은 다음 구조를 유지합니다.

- 좌측 사이드바
- 중앙 오늘 일정 리스트
- 우측 선택 일정 상세 패널
- 상단 날짜 이동과 새 일정 버튼
- 요약 항목은 일정 수와 할 일 수만 표시

## Excluded

- 집중 시간 요약은 홈 화면 초기 범위에서 제외합니다.
- 오전, 오후 그룹 옆의 설명 문구는 표시하지 않습니다.

## Consequences

- 이후 macOS 홈 화면 기획과 Compose UI 구현은 이 프로토타입을 기준으로 합니다.
- iOS와 Android는 같은 정보 구조를 공유하되, 화면 폭에 맞춰 상세 패널을 별도 화면 또는 bottom sheet로 전환할 수 있습니다.
- 홈 화면 기능 상세 기획은 `02-design/macos-home-feature-spec.md`에서 관리합니다.

