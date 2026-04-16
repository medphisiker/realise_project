# Workflow Step: Release Publication Gate

## Назначение

Проверить, что workflow может войти в `release-publication stage`: touched release units merged в configured release branch, branch state соответствует project-local publication policy, а финальная publication допустима.

## Execution scope

- Не учитывай место хранения workflow step artifacts при определении execution scope.
- Шаг выполняется для root проекта и touched nested release units текущего workflow-run.
- Шаг materialize-ит decision point перед финальными publication artifacts.

## Входы

- changed release units;
- branch matrix и readiness handoff из `01-readiness-gate`;
- `04-release-notes-handoff.md`;
- текущие git branches для root repo и changed nested release units;
- `project/releaseContext.md`;
- `project/gitContext.md`;
- текущий `release-run.md`.

## Действие

- повторно проверить current branch для root repo и changed nested release units;
- сопоставить его с configured release branch из project-local policy;
- проверить, что required PR/merge alignment завершен для touched release units;
- если publication branch state не готов, остановить workflow и вернуть его к PR/merge alignment;
- если publication branch state готов, зафиксировать `release-publication gate` как passed и подготовить handoff для финальной publication.

## Что шаг не делает

- не создает git tags;
- не создает GitHub releases;
- не определяет новые versions/tags;
- не публикует Docker images сам по себе.

## Выходы

- `repo -> current branch`;
- `repo -> release branch`;
- `repo -> PR URL` when applicable;
- `repo -> merge commit SHA` when applicable;
- publication gate decision;
- обновленный `release-run.md`;
- handoff artifact для шага `06-github-release`.

## Минимальная проверка внутри шага

- каждый changed release unit проверен на current branch;
- publication gate passed only when changed release units satisfy configured release branch policy;
- if publication gate is blocked, workflow does not continue to final release publication.

## DoD

- publication eligibility зафиксирована как explicit workflow decision.
- `release-run.md` отражает результат `release-publication gate`.
- подготовлен handoff artifact для следующего шага.

## Связанный skill

- [`SKILL.md`](./SKILL.md)
