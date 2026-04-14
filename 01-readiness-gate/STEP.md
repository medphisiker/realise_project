# Workflow Step: Readiness Gate

## Назначение

Подтвердить, что release можно начинать: taskset завершен, white spots закрыты, а relevant knowledge уже перенесено в Engineering Documentation SoT.

## Входы

- completed taskset;
- project-local SoT;
- operational artifacts текущего изменения.

## Действие

- проверить, что release scope завершен;
- проверить, что `docs/` уже отражает реализованное состояние;
- проверить, что remaining operational artifacts не содержат незакрытых архитектурных unknowns.

## Выходы

- подтвержденный readiness state;
- список touched release units;
- список canonized artifacts, на которые будет опираться release.

## DoD

- можно безопасно перейти к Docker cutover без architectural uncertainty.

## Связанный skill

- [`SKILL.md`](./SKILL.md)
