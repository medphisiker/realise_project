---
name: github-release
description: Создает git tags и GitHub releases для root проекта и changed nested release units по project-local release version registry и release notes после explicit publication gate.
version: 1.0.0
---

# Навык: GitHub Release

## Назначение

Навык materialize-ит финальный git/GitHub release package по уже утвержденным версиям текущего release run.

## Алгоритм

1. Прочитай `project/releaseContext.md`, `project/gitContext.md` и `project/releaseVersionRegistry.json`.
2. Определи changed release units.
3. Прочитай result `release-publication gate` из workflow handoff.
4. Для root проекта и каждого changed nested release unit повторно проверь current branch и intended release branch.
5. Если publication gate не passed или branch state не соответствует intended release branch, не публикуй release.
6. Только после проверки merged HEAD intended release branch прочитай фиксированный tag/version из registry.
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
