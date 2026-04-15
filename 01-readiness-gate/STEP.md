# Workflow Step: Readiness Gate

## Назначение

Подтвердить, что release можно начинать: taskset завершен, white spots закрыты, relevant knowledge уже перенесено в Engineering Documentation SoT, а touched release units проходят начальный preparation-branch gate.

## Execution scope

- Не учитывай место хранения workflow step artifacts при определении execution scope.
- Шаг выполняется для корневого проекта, который запускает release workflow.
- Текущий workflow-run materialize-ится в `operational_scope/realise_project/<release-id>/`.
- Шаг определяет approved release scope, touched release units и explicit exclusions для текущего прогона.

## Входы

- completed taskset;
- project-local SoT;
- operational artifacts текущего изменения.
- current git branches для root repo и candidate nested release units;
- `project/releaseContext.md`;
- `project/gitContext.md`;
- текущий `release-run.md`, если он уже materialized для workflow-run.

## Действие

- проверить, что release scope завершен;
- проверить, что `docs/` уже отражает реализованное состояние;
- проверить, что remaining operational artifacts не содержат незакрытых архитектурных unknowns.
- определить touched release units и их intended release branches;
- зафиксировать branch matrix для touched release units;
- проверить, что preparation идет в допустимой feature branch `feature-<feature-name>` или в другом явно разрешенном project-local preparation branch;
- если preparation идет прямо в intended release branch, остановить workflow до explicit user confirmation;
- если branch state не проходит preparation policy, остановить workflow и не передавать run дальше в `02-docker-cutover`.

## Что шаг не делает

- не начинает Docker build или compose cutover;
- не пишет release notes;
- не удаляет operational artifacts;
- не готовит tags;
- не включает в release scope units, которые не подтверждены текущим run-specific анализом.

## Выходы

- подтвержденный readiness state;
- список touched release units;
- branch matrix и branch/PR eligibility decision;
- список canonized artifacts, на которые будет опираться release.
- обновленный `release-run.md`;
- handoff artifact для шага `02-docker-cutover`.

## Минимальная проверка внутри шага

- relevant taskset completed для approved release scope;
- relevant `docs/` already reflect implemented behavior;
- touched release units и explicit exclusions clearly identified;
- branch matrix для touched release units зафиксирован;
- каждый touched release unit либо находится в допустимом preparation branch, либо workflow остановлен до clarifying decision;
- remaining operational artifacts не содержат blocking white spots для approved release scope.

## DoD

- можно безопасно перейти к Docker cutover без architectural uncertainty и branch ambiguity for preparation stage.
- `release-run.md` отражает завершение шага.
- подготовлен handoff artifact для следующего шага.

## Связанный skill

- [`SKILL.md`](./SKILL.md)
