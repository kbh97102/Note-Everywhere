# ADR 0001: Documentation Workflow

## Status

Accepted

## Context

noteEveryWhere의 기획 문서, 기술 메모, 의사결정 기록을 Obsidian, Codex, Git으로 함께 관리하려고 합니다.

## Decision

Obsidian vault를 Git 저장소로 관리하고, Codex는 같은 폴더의 Markdown 문서를 직접 읽고 수정합니다.

## Consequences

- 문서 변경 이력을 Git commit으로 추적할 수 있습니다.
- Codex가 여러 문서를 기반으로 기획 정리와 기술 초안을 작성할 수 있습니다.
- 충돌을 줄이기 위해 작업 전 `git pull`, 작업 후 `git status`와 commit을 확인해야 합니다.

