# Setup Instructions: `realise_project`

## Назначение

Этот документ объясняет, как подключить reusable workflow pack релиза к новому проекту.

Логика такая:

1. пользователь копирует workflow pack;
2. переносит шаблоны из `resources/templates/` в свой проект с сохранением путей;
3. смотрит реальные примеры в `resources/examples/`;
4. заполняет project-local files под свою release policy;
5. после этого workflow pack готов к первому release run.

## Что workflow ожидает от проекта

Workflow pack самодостаточен как sequence of steps, но для работы он ожидает project-local binding в стандартных местах.

Минимально нужны:

- `project/releaseContext.md`
- `project/gitContext.md`
- `project/releaseVersionRegistry.json`
- `operational_scope/realise_project/`
- release note location, согласованная с `project/releaseContext.md`

Рекомендуется дополнительно иметь:

- `project/dockerReleaseContext.md`
- `operational_scope/tasks_map.md`
- canonical SoT entry points в `docs/`

## Как использовать templates

Templates уже разложены по целевой структуре каталогов.

Рекомендуемый flow:

1. Возьми `resources/templates/` как baseline scaffold.
2. Перенеси файлы в свой проект, сохранив относительные пути.
3. Открой `resources/project-layout.md` и проверь, что layout совпадает.
4. Открой `resources/examples/` и используй примеры как reference shape.
5. Замени placeholders и project-specific values своими значениями.

## Обязательный project contract

### `project/releaseContext.md`

Здесь workflow ищет:

- release units;
- release branch policy;
- preparation branch policy;
- publish flow;
- atomicity policy;
- mistaken release recovery policy;
- release note locations.

### `project/gitContext.md`

Здесь workflow ищет:

- repo boundaries;
- nested repositories;
- release-unit candidates;
- правила запуска git-операций по repository boundary.

### `project/releaseVersionRegistry.json`

Здесь workflow ищет уже materialized release versions/tags для root проекта и touched nested release units.

### `project/dockerReleaseContext.md`

Этот файл нужен шагу `02-docker-cutover`, если проект публикует Docker images и должен явно задавать image repositories и naming policy.

## Branch model expected by the workflow

Workflow различает два branch classes:

- preparation branch — ветка, в которой выполняется pre-release preparation;
- release branch — ветка, из merged HEAD которой разрешена финальная publication.

Recommended baseline:

- preparation branch pattern: `feature-<feature-name>`
- release branch: project-defined, например `main`

Важно:

- pre-release preparation должна по умолчанию идти в feature branch;
- direct preparation в release branch не должна проходить silently и должна требовать explicit user confirmation;
- publication artifacts не должны создаваться из preparation branch.

## Что лежит в `resources/`

- [`resources/project-layout.md`](./resources/project-layout.md) — краткая карта ожидаемой структуры проекта.
- `resources/templates/` — минимальные заготовки файлов, уже разложенные по target paths.
- `resources/examples/` — реальные заполненные примеры из проекта `llm_agent_platform`.

## Minimal integration checklist

- `project/releaseContext.md` заполнен и содержит branch/release policy.
- `project/gitContext.md` описывает repo boundaries и release units.
- `project/releaseVersionRegistry.json` существует и содержит initial versions.
- release note locations, указанные в `project/releaseContext.md`, реально существуют или могут быть созданы.
- `operational_scope/realise_project/` готов для workflow-instance handoff artifacts.
- если проект публикует Docker images, заполнен `project/dockerReleaseContext.md`.

## First run checklist

Перед первым release run проверь:

- workflow понимает, какие repos являются release units;
- workflow понимает, какая ветка является preparation branch, а какая release branch;
- policy whole-run vs partial release явно определена;
- mistaken release recovery policy записана до первого инцидента, а не после него.
