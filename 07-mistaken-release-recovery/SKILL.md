---
name: mistaken-release-recovery
description: Выполняет remediation flow для mistaken release и подготавливает безопасный возврат к publication gate.
version: 1.0.0
---

# Навык: Mistaken Release Recovery

## Назначение

Навык materialize-ит exception/remediation branch workflow после ошибочной публикации релиза.

## Алгоритм

1. Прочитай `06-github-release-handoff.md`, `mistaken-release-recovery.md`, `project/releaseContext.md` и `project/gitContext.md`.
2. Зафиксируй invalid publication state и policy violation.
3. Удали erroneous release/tag artifacts when applicable.
4. Зафиксируй remediation status для Docker/external artifacts when applicable.
5. Направь workflow в corrective PR/merge alignment.
6. Подготовь evidence для возврата к `05-release-publication-gate`.

## Выход

- completed or blocked remediation artifact;
- return path to publication gate.

## Ограничения

- Не трактовать этот шаг как обязательный шаг happy path.
- Не скрывать incident/remediation details.
- Не публиковать corrected release без возврата к publication gate.
