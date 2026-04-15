---
name: github-release
description: Создает git tags и GitHub releases для root проекта и changed nested release units по project-local release version registry и release notes только после branch/PR gate.
version: 1.2.0
---

# Навык: GitHub Release

## Назначение

Навык materialize-ит финальный git/GitHub release package по уже утвержденным версиям текущего release run.

## Алгоритм

1. Прочитай `project/releaseContext.md`, `project/gitContext.md` и `project/releaseVersionRegistry.json`.
2. Определи changed release units.
3. Используй branch/PR eligibility result из `01-readiness-gate` как baseline для release run.
4. Для root проекта и каждого changed nested release unit повторно проверь current branch и intended release branch.
5. Если changed repo находится на feature/non-release branch или уже не совпадает с readiness handoff, не публикуй release; верни workflow в PR/merge alignment до intended release branch.
6. Только после merge/readiness на intended release branch и проверки merged HEAD прочитай фиксированный tag/version из registry.
7. Свяжи каждый release unit с соответствующим release note.
8. Создай git tags и подготовь/создай GitHub releases по готовым release notes.

## Выход

- `repo -> applied tag`;
- `repo -> current branch`;
- `repo -> tag target SHA`;
- `repo -> release note path`;
- результат GitHub release publication.

## Ограничения

- Не определять новые version values внутри этого шага.
- Не публиковать release из feature branch.
- Не создавать tag/release не из merged HEAD intended release branch.
- Не хардкодить fixed subproject list внутри skill.
- Не готовить releases для untouched release units.
- Учитывать project-local git boundaries и не смешивать repo contexts.
