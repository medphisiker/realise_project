# Workflow: release проекта

## Назначение workflow

Этот workflow описывает последовательность шагов release после завершения taskset, канонизации знаний в SoT и готовности проекта к упаковке и публикации.

## Preconditions

- relevant taskset выполнен;
- knowledge уже поднято в project SoT;
- release-ready scope определен;
- project-local release binding прочитан из `project/releaseContext.md`.

## Workflow-instance exchange layer

Этот workflow использует временный workflow-specific exchange layer внутри `Operational Documentation Layer`.

Baseline путь:

- `operational_scope/realise_project/`

Рекомендуемая materialization для конкретного прогона:

- `operational_scope/realise_project/<release-id>/`

В этом слое хранятся только instance-specific handoff artifacts между шагами workflow. После завершения workflow они могут быть удалены.

## Карта шагов

1. [Readiness Gate](./01-readiness-gate/STEP.md)
2. [Docker Cutover](./02-docker-cutover/STEP.md)
3. [Artifact Cleanup](./03-artifact-cleanup/STEP.md)
4. [Release Notes](./04-release-notes/STEP.md)
5. [Tag Prep](./05-tag-prep/STEP.md)

## Базовая последовательность

- Сначала подтвердить readiness gate.
- Затем подготовить release Docker contour.
- После этого очистить completed operational artifacts, уже поднятые в SoT.
- Затем подготовить release notes для root проекта и changed nested release units.
- В конце подготовить tags для root repo и changed nested release units.

## Vacancies and handoff model

| Step | Preferred vacancy | Static context source | Additional handoff required |
| --- | --- | --- | --- |
| `01-readiness-gate` | preferably the same Architect | `AGENTS.md`, `project/`, `docs/`, completed task reports | no |
| `02-docker-cutover` | Code-agent | `AGENTS.md`, `project/`, `docs/` | yes, from `operational_scope/realise_project/<release-id>/` |
| `03-artifact-cleanup` | preferably the same Architect | `AGENTS.md`, `project/`, `docs/`, completed task reports | no |
| `04-release-notes` | preferably the same Architect | `AGENTS.md`, `project/`, `docs/`, completed task reports | no |
| `05-tag-prep` | Code-agent | `AGENTS.md`, `project/`, `docs/` | yes, from `operational_scope/realise_project/<release-id>/` |

### Почему шаги `01`, `03`, `04` prefer the same Architect

Эти шаги требуют continuity of understanding:

- как проектировались планы;
- как решения были канонизированы в SoT;
- как implementation reports соотносятся с изначальным design intent;
- какие operational artifacts уже безопасно удалять;
- как корректно синтезировать release notes без semantic drift.

Поэтому vacancy здесь должен закрывать preferably тот же самый Architect, который вел planning -> canonization -> implementation review cycle.

### Что получает Code-agent и чего ему не хватает

На шагах `02` и `05` Code-agent получает из `AGENTS.md` и `project/` static project context:

- repo boundaries;
- release units;
- release note locations;
- compose boundaries;
- cleanup/tagging policy.

Но этого недостаточно для конкретного release-instance. Ему не хватает:

- approved release-instance scope;
- exact changed release units этого прогона;
- release-instance exclusions;
- compose-sync intent, уже одобренного на readiness step;
- mapping release notes к changed release units.

Поэтому для шагов `02` и `05` обязателен explicit handoff через workflow-specific exchange layer.

## Важные invariants

- Workflow не должен сам по себе публиковать release до manual verification пользователем.
- Release logic должна читать project-local release binding, а не хардкодить project shape.
- Cleanup не должен удалять неканонизированное знание.
- Release notes и tags должны готовиться только для touched release units.
- Workflow-specific exchange layer живет в `Operational Documentation Layer` и не подменяет ни Engineering Documentation SoT, ни Release Documentation Layer.
