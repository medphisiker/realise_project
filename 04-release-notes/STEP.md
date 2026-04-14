# Workflow Step: Release Notes

## Назначение

Подготовить release-ready notes для root проекта и changed nested release units.

## Входы

- touched release units;
- canonized SoT;
- фактический scope изменений.

## Действие

- определить, какие release units реально изменялись;
- для каждого changed unit подготовить краткий release note/changelog;
- разместить notes в project-local release documentation locations.

## Выходы

- release notes для root проекта;
- release notes для changed nested release units.

## DoD

- для каждого changed release unit есть отдельный release note в project-local release documentation location.

## Связанный skill

- [`SKILL.md`](./SKILL.md)
