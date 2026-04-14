---
name: release-artifact-cleanup
description: Удаляет completed tasks/plans, уже канонизированные в SoT, и синхронизирует task index.
version: 1.0.0
---

# Навык: Release Artifact Cleanup

## Назначение

Навык очищает operational layer после канонизации знаний и перед финализацией релиза.

## Алгоритм

1. Прочитай project-local release binding из `project/releaseContext.md`.
2. Найди completed task artifacts и completed plan artifacts, относящиеся к текущему release scope.
3. Для каждого artifact проверь, что relevant knowledge уже canonized в `docs/`.
4. Удали только те artifacts, которые дублируют уже поднятое SoT.
5. Синхронизируй `operational_scope/tasks_map.md` или project-local task index.

## Выход

- очищенный operational layer;
- синхронизированный task index.

## Ограничения

- Не удалять artifacts с незакрытыми знаниями, even if status accidentally marked completed.
- Не удалять artifacts, которые проект сознательно хранит как history evidence.
