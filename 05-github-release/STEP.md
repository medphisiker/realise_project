# Workflow Step: GitHub Release

## Назначение

Создать git tags и GitHub releases для root проекта и changed nested release units по уже зафиксированным версиям из `project/releaseVersionRegistry.json`.

[`release-preparation gate`](../terms.md) должен быть уже пройден на `01-readiness-gate`. На этом шаге branch state валидируется повторно как часть [`release-publication gate`](../terms.md), а release разрешен только из merged HEAD intended release branch каждого release unit.

## Execution scope

- Не учитывай место хранения workflow step artifacts при определении execution scope.
- Шаг выполняется только для root repo и touched nested release units текущего workflow-run.
- Untouched release units не должны получать git tags или GitHub releases.

## Входы

- changed release units;
- release notes;
- project-local git boundaries.
- текущие git branches для root repo и changed nested release units;
- `project/releaseContext.md`;
- `project/gitContext.md`;
- `project/releaseVersionRegistry.json`;
- `04-release-notes-handoff.md`;
- текущий `release-run.md`.

## Действие

- определить, какие repos должны получить новый git tag;
- повторно проверить current branch для root repo и changed nested release units;
- сопоставить его с intended release branch из project-local policy;
- проверить, что target commit для tag/release является merged HEAD intended release branch;
- если branch state больше не соответствует readiness handoff, остановить `release-publication gate` и вернуть workflow к PR/merge alignment вместо публикации из feature/non-release branch;
- прочитать fixed release versions/tags из `project/releaseVersionRegistry.json`;
- создать tag set для root repo и changed nested repos;
- подготовить и/или создать GitHub releases по готовым release notes.

## Что шаг не делает

- не определяет новые version values заново;
- не публикует release из feature branch даже при user pressure;
- не создает tags для untouched release units;
- не готовит release package для repos, которые не являются release units текущего проекта.

## Выходы

- список `repo -> applied tag`;
- список `repo -> current branch`;
- список `repo -> tag target SHA`;
- список `repo -> release note path`;
- GitHub release publishing result;
- обновленный `release-run.md`;
- финальный handoff artifact для завершения workflow.

## Минимальная проверка внутри шага

- каждый applied tag соответствует changed release unit;
- каждый changed release unit проверен на current branch;
- каждый published release сделан из intended release branch, а не из feature branch;
- каждый published release ссылается на merged HEAD intended release branch;
- каждый changed release unit имеет release note path;
- каждый applied tag совпадает со значением из `project/releaseVersionRegistry.json`;
- excluded/non-release units не попали в git tag/GitHub release package.

## DoD

- для каждого changed release unit зафиксирован current branch и verified release branch decision.
- для каждого changed release unit зафиксирован final tag target SHA.
- для каждого changed release unit создан git tag и подготовлен/создан GitHub release по зафиксированным версиям только после `release-publication gate`.
- `release-run.md` отражает завершение шага.
- подготовлен финальный handoff artifact workflow-run.

## Связанный skill

- [`SKILL.md`](./SKILL.md)
