# Workflow Step: Docker Cutover

## Назначение

Подготовить release Docker contour проекта во время `release-preparation stage` и синхронизировать production compose с актуальной логикой development compose без финальной publication.

## Execution scope

- Не учитывай место хранения workflow step artifacts при определении execution scope.
- Шаг выполняется для корневого проекта, который запускает release workflow.
- Project-specific Docker/release binding и instance-specific decisions нужно читать из `project/` и `operational_scope/realise_project/` этого проекта.

## Входы

- touched release units;
- `docker-compose-dev.yml`;
- `docker-compose.yml`;
- project-local release binding.
- `project/dockerReleaseContext.md`;
- `project/releaseVersionRegistry.json`;
- workflow-instance handoff от `01-readiness-gate`;
- текущий `release-run.md`.

## Действие

- определить Docker contour для `release-preparation stage` у touched release units;
- определить новые release versions/tags для touched release units и обновить `project/releaseVersionRegistry.json`;
- локально собрать preparation images с approved release tags для touched release units, чтобы проверить Docker contour до [`release-publication gate`](../terms.md);
- сравнить `docker-compose-dev.yml` и `docker-compose.yml`;
- перенести в `docker-compose.yml` новые image refs и release-relevant runtime logic, которая уже materialized в dev contour;
- обновлять только touched release units; untouched release units не менять;
- сравнивать не только image refs, но и release-relevant runtime fields: environment, command/entrypoint, healthcheck, depends_on, ports, restart policy, volumes и другие поля, влияющие на release contour;
- dev-only mechanics вроде bind mounts, live-reload и локального build flow не переносить в release contour автоматически;
- подготовить release contour для manual verification пользователем;
- зафиксировать, что финальная publication Docker images должна выполняться только после [`release-publication gate`](../terms.md) из intended release branch.

## Что шаг не делает

- не публикует Docker images до manual verification пользователем;
- не выполняет финальный Docker publish из feature/preparation branch;
- не переписывает `docker-compose-dev.yml`, если не возникло реальной необходимости изменить development contour по смыслу;
- не меняет release units вне approved release scope.
- не придумывает image repository naming вне `project/dockerReleaseContext.md`.

## Выходы

- обновленный release compose contour;
- набор локально собранных preparation images, готовых к manual verification и последующей publication re-build/re-check после hard gate.
- обновленный `project/releaseVersionRegistry.json`;
- обновленный `release-run.md`;
- handoff artifact для следующего workflow step.

## Минимальная проверка внутри шага

- локальная сборка touched preparation images должна завершиться успешно;
- `project/releaseVersionRegistry.json` должен отражать новый agreed release version/tag для touched release units;
- release compose contour должен проходить структурную проверку через compose config/render;
- в handoff artifacts не нужно копировать полный вывод команд, если в нем materialize secrets или env values.

## DoD

- `docker-compose.yml` синхронизирован с актуальной release logic и готов к ручной проверке.
- touched preparation images локально собраны с approved release tags.
- `project/releaseVersionRegistry.json` обновлен для touched release units.
- зафиксировано, что финальный publish contour будет materialized только после `release-publication gate`.
- `release-run.md` отражает завершение шага.
- подготовлен handoff artifact для следующего шага.

## Связанный skill

- [`SKILL.md`](./SKILL.md)
