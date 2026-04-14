# Workflow Step: Readiness Gate

## Назначение

Подтвердить, что release можно начинать: taskset завершен, white spots закрыты, а relevant knowledge уже перенесено в Engineering Documentation SoT.

## Execution scope

- Не учитывай место хранения workflow step artifacts при определении execution scope.
- Шаг выполняется для корневого проекта, который запускает release workflow.
- Текущий workflow-run materialize-ится в `operational_scope/realise_project/<release-id>/`.
- Шаг определяет approved release scope, touched release units и explicit exclusions для текущего прогона.

## Входы

- completed taskset;
- project-local SoT;
- operational artifacts текущего изменения.
- `project/releaseContext.md`;
- `project/gitContext.md`;
- текущий `release-run.md`, если он уже materialized для workflow-run.

## Действие

- проверить, что release scope завершен;
- проверить, что `docs/` уже отражает реализованное состояние;
- проверить, что remaining operational artifacts не содержат незакрытых архитектурных unknowns.

## Что шаг не делает

- не начинает Docker build или compose cutover;
- не пишет release notes;
- не удаляет operational artifacts;
- не готовит tags;
- не включает в release scope units, которые не подтверждены текущим run-specific анализом.

## Выходы

- подтвержденный readiness state;
- список touched release units;
- список canonized artifacts, на которые будет опираться release.
- обновленный `release-run.md`;
- handoff artifact для шага `02-docker-cutover`.

## Минимальная проверка внутри шага

- relevant taskset completed для approved release scope;
- relevant `docs/` already reflect implemented behavior;
- touched release units и explicit exclusions clearly identified;
- remaining operational artifacts не содержат blocking white spots для approved release scope.

## DoD

- можно безопасно перейти к Docker cutover без architectural uncertainty.
- `release-run.md` отражает завершение шага.
- подготовлен handoff artifact для следующего шага.

## Связанный skill

- [`SKILL.md`](./SKILL.md)
