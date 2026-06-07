# ADR 0006: Development Architecture and Planning Rules

## Status

Accepted

## Context

noteEveryWhere는 Compose Multiplatform으로 Android, iOS, macOS를 지원합니다. Milestone 1 기획과 HTML 프로토타입이 이미 작성되어 있으므로, 개발은 이 기준을 따라야 합니다.

## Decision

개발은 다음 구조로 진행합니다.

- Compose Multiplatform
- MVI
- Clean Architecture
- presentation 계층 추가 모듈화
- DesignSystem 모듈 분리
- 기능별 UI 모듈 분리

Android, iOS, macOS는 하나의 DesignSystem을 공유합니다. 플랫폼별 별도 color, typography, shape 체계는 만들지 않습니다.

기획서와 초안 디자인은 구현의 기준입니다. 개발 중 더 좋은 기획 방향이 떠오르더라도 기존 기획서 내용을 임의로 변경하지 않습니다.

변경이 필요하면 반드시 사용자 컨펌을 받은 뒤 문서와 ADR을 수정합니다.

## UI Implementation Rule

한 화면은 큰 section으로 나누고, section 내부를 작은 컴포넌트로 분리합니다.

한 파일에 많은 컴포넌트를 몰아넣지 않습니다.

## Consequences

- 개발자는 구현 전에 관련 기획 문서와 프로토타입을 확인해야 합니다.
- 기획 변경은 구현 중 임의로 처리하지 않습니다.
- presentation 모듈은 DesignSystem과 기능별 UI로 나뉩니다.
- Task Create와 Task Edit은 UI form을 공유할 수 있지만 MVI contract는 분리합니다.
- 플랫폼별 차이는 같은 DesignSystem token을 사용하는 adaptive layout으로 처리합니다.
