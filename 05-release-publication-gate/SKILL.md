---
name: release-publication-gate
description: Проверяет publication eligibility текущего release run и materialize-ит explicit decision перед финальной публикацией release artifacts.
version: 1.0.0
---

# Навык: Release Publication Gate

## Назначение

Навык materialize-ит `release-publication gate` как отдельный workflow-step.

## Алгоритм

1. Прочитай `project/releaseContext.md`, `project/gitContext.md` и текущий `release-run.md`.
2. Используй readiness baseline и release-notes handoff как входной контекст для publication decision.
3. Для root проекта и каждого changed nested release unit проверь current branch и configured release branch.
4. Проверь, что required PR/merge alignment завершен.
5. Если publication policy не выполняется, останови workflow и верни его к PR/merge alignment.
6. Если policy выполняется, зафиксируй `release-publication gate` как passed.
7. Подготовь handoff для `06-github-release`.

## Выход

- `repo -> current branch`;
- `repo -> release branch`;
- `repo -> PR URL` when applicable;
- `repo -> merge commit SHA` when applicable;
- publication gate decision.

## Ограничения

- Не создавать release artifacts внутри этого шага.
- Не подменять этим шагом сам `06-github-release`.
- Не публиковать release из branch, который не проходит configured publication policy.
