# Workflow Step: Tag Prep

## Назначение

Подготовить список tag actions и release text для root проекта и changed nested release units.

## Execution scope

- Не учитывай место хранения workflow step artifacts при определении execution scope.
- Шаг выполняется только для root repo и touched nested release units текущего workflow-run.
- Untouched release units не должны получать tag prep package.

## Входы

- changed release units;
- release notes;
- project-local git boundaries.
- `project/releaseContext.md`;
- `project/gitContext.md`;
- `04-release-notes-handoff.md`;
- текущий `release-run.md`.

## Действие

- определить, какие repos должны получить новый tag;
- подготовить tag set для root repo и changed nested repos;
- подготовить release text payload для ручной публикации на GitHub.

## Что шаг не делает

- не создает tags для untouched release units;
- не готовит release package для repos, которые не являются release units текущего проекта;
- не публикует tags или GitHub releases автоматически.

## Выходы

- список `repo -> proposed tag`;
- список `repo -> release note path`;
- release text payload для ручной вставки на GitHub.
- обновленный `release-run.md`;
- финальный handoff artifact для завершения workflow.

## Минимальная проверка внутри шага

- каждый proposed tag соответствует changed release unit;
- каждый changed release unit имеет release note path;
- excluded/non-release units не попали в tag prep package.

## DoD

- для каждого changed release unit подготовлен tag prep package.
- `release-run.md` отражает завершение шага.
- подготовлен финальный handoff artifact workflow-run.

## Связанный skill

- [`SKILL.md`](./SKILL.md)
