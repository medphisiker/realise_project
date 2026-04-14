---
name: release-tag-prep
description: Готовит tags и release text для root проекта и changed nested release units по project-local git/release context.
version: 1.0.0
---

# Навык: Release Tag Prep

## Назначение

Навык подготавливает tag/release package для ручной финализации релиза.

## Алгоритм

1. Прочитай `project/releaseContext.md` и `project/gitContext.md`.
2. Определи changed release units.
3. Подготовь список repos, для которых нужен новый tag.
4. Для каждого changed release unit свяжи proposed tag с соответствующим release note.
5. Подготовь release text payload для ручной публикации на GitHub.

## Выход

- `repo -> proposed tag`;
- `repo -> release note path`;
- release text для ручной вставки в GitHub release/tag UI.

## Ограничения

- Не хардкодить fixed subproject list внутри skill.
- Не готовить tags для untouched release units.
- Учитывать project-local git boundaries и не смешивать repo contexts.
