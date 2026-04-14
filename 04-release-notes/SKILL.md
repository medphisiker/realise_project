---
name: release-notes-writer
description: Готовит release notes для root проекта и changed nested release units по project-local release binding.
version: 1.0.0
---

# Навык: Release Notes Writer

## Назначение

Навык готовит release-ready markdown notes/changelog для проекта и его changed nested release units.

## Алгоритм

1. Прочитай `project/releaseContext.md` и `project/gitContext.md`.
2. Определи changed release units из фактического scope релиза.
3. Для root проекта и каждого changed nested release unit подготовь отдельный markdown release note.
4. Размести notes в project-local release documentation locations.
5. Не создавай notes для release units, которые не изменялись.

## Ожидаемый результат

- один release note для root проекта;
- по одному release note для каждого changed nested release unit.

## Ограничения

- Не хардкодить список subprojects внутри skill.
- Список release units всегда брать из project-local context.
