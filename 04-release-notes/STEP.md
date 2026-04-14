# Workflow Step: Release Notes

## Назначение

Подготовить release-ready notes для root проекта и changed nested release units.

## Execution scope

- Не учитывай место хранения workflow step artifacts при определении execution scope.
- Шаг выполняется для root проекта и touched nested release units текущего workflow-run.
- Release notes пишутся только для реально changed release units.

## Входы

- touched release units;
- canonized SoT;
- фактический scope изменений.
- `project/releaseContext.md`;
- `01-readiness-gate-handoff.md`;
- `03-artifact-cleanup-handoff.md`;
- текущий `release-run.md`.

## Действие

- определить, какие release units реально изменялись;
- для каждого changed unit подготовить краткий release note/changelog;
- разместить notes в project-local release documentation locations.

## Что шаг не делает

- не пишет release notes для untouched release units;
- не подменяет release notes engineering SoT документами;
- не подготавливает tags;
- не меняет compose contour.

## Выходы

- release notes для root проекта;
- release notes для changed nested release units.
- обновленный `release-run.md`;
- handoff artifact для шага `05-tag-prep`.

## Минимальная проверка внутри шага

- для каждого changed release unit есть отдельный release note path;
- release notes отражают canonized SoT и approved release scope;
- untouched release units не получили лишние release notes.

## DoD

- для каждого changed release unit есть отдельный release note в project-local release documentation location.
- `release-run.md` отражает завершение шага.
- подготовлен handoff artifact для следующего шага.

## Связанный skill

- [`SKILL.md`](./SKILL.md)
