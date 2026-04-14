# Workflow Step: Tag Prep

## Назначение

Подготовить список tag actions и release text для root проекта и changed nested release units.

## Входы

- changed release units;
- release notes;
- project-local git boundaries.

## Действие

- определить, какие repos должны получить новый tag;
- подготовить tag set для root repo и changed nested repos;
- подготовить release text payload для ручной публикации на GitHub.

## Выходы

- список `repo -> proposed tag`;
- список `repo -> release note path`;
- release text payload для ручной вставки на GitHub.

## DoD

- для каждого changed release unit подготовлен tag prep package.

## Связанный skill

- [`SKILL.md`](./SKILL.md)
