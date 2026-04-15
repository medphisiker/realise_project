# Release Workflow Pack

## Назначение

Этот pack хранит reusable workflow релиза проекта и step-specific skills, которые помогают провести release после завершения taskset и канонизации знаний в SoT.

## Что входит в pack

- [`workflow.md`](./workflow.md) — semantic карта release workflow.
- [`setup_instructions.md`](./setup_instructions.md) — как подключить workflow pack к своему проекту.
- step packs с `STEP.md` и `SKILL.md` для отдельных release шагов.

## Как выполнять workflow

Этот раздел предназначен для агента или человека, который уже работает внутри проекта, где workflow pack подключен.

1. Сначала прочитать project-local release binding в `project/releaseContext.md` и related files.
2. Затем открыть [`workflow.md`](./workflow.md).
3. После этого перейти в нужный `workflow-step` и выполнять его через соответствующий step pack.
4. `setup_instructions.md` использовать только если workflow pack еще не интегрирован в проект.

## Предшествующий workflow context

Этот workflow предполагает, что до его запуска уже был пройден предыдущий engineering cycle:

1. Architect спроектировал планы реализации нового функционала.
2. Когда планы сошлись, тот же Architect канонизировал решения в Engineering Documentation SoT.
3. Исполнительные агенты materialized implementation tasks и оставили execution reports в task artifacts.
4. Тот же Architect прочитал execution reports, проверил согласованность результата с SoT и обновил документацию проекта.

Из этого следуют два правила:

- release workflow стартует не от состояния "есть выполненные задачи", а от состояния "есть завершенный taskset и уже обновленный SoT";
- для шагов, где важна continuity of understanding, vacancy должен закрывать preferably тот же самый Architect, который вел planning -> canonization -> implementation review cycle, а не просто любой новый агент с ролью Architect.

## Как использовать в своем проекте

Этот раздел предназначен для пользователя, который хочет перенести workflow pack в новый проект.

1. Сначала прочитать [`setup_instructions.md`](./setup_instructions.md).
2. Затем разложить templates в свой проект с сохранением путей.
3. После этого заполнить project-local release binding в `project/releaseContext.md` и related files.
4. Затем использовать examples из `resources/examples/` как reference shape.
5. Когда интеграция завершена, выполнять workflow уже по разделу `Как выполнять workflow`.

## Что должно приходить из project-local context

Этот pack не должен хардкодить:

- release units;
- release note locations;
- compose boundaries;
- cleanup policy;
- tagging scope.

Эти значения должны читаться из project-local context, в первую очередь из:

- `project/releaseContext.md`
- `project/gitContext.md`

## Workflow-specific exchange layer

По knowledge-lifecycle model из [`Documentation Lifecycle Layers`](../../../../docs/methodology-layer/assets/knowledge-lifecycle/documentation-lifecycle-layers.md) workflow может использовать временный exchange layer внутри `Operational Documentation Layer`.

Для reusable workflow baseline фиксируется такой invariant:

- у workflow может быть свой временный workflow-specific exchange layer в `operational_scope/<workflow-pack-name>/`;
- этот слой хранит instance-specific handoff artifacts между шагами workflow;
- этот слой не является Engineering Documentation SoT и не должен подменять `docs/`;
- этот слой не является Release Documentation Layer и не должен подменять release notes;
- после завершения workflow его instance-specific handoff artifacts могут быть удалены.

Для этого workflow-pack baseline путь exchange layer:

- `operational_scope/realise_project/`

Рекомендуемая форма:

- `operational_scope/realise_project/<release-id>/`
- внутри хранятся `handoff in/out` artifacts конкретного прогона workflow.

## Static context vs workflow-instance context

`AGENTS.md`, `project/` и `docs/` дают static context проекта, но не заменяют instance-specific context конкретного релиза.

Поэтому workflow различает:

- static project context из `AGENTS.md`, `project/` и `docs/`;
- workflow-instance handoff context из `operational_scope/realise_project/<release-id>/`.

Это особенно важно для шагов, которые выполняет другой агент, а не тот же самый Architect.

## Multi-agent vacancy model

Этот workflow допускает, что разные шаги закрываются разными агентами.

Baseline assignment:

- `01-readiness-gate` — preferably тот же Architect;
- `02-docker-cutover` — Code-agent с explicit handoff;
- `03-artifact-cleanup` — preferably тот же Architect;
- `04-release-notes` — preferably тот же Architect;
- `05-github-release` — Code-agent с explicit handoff.

Code-agent на шагах `02` и `05` получает из `AGENTS.md` и `project/` только static project/release binding, но не получает автоматически:

- approved release-instance scope;
- exact changed release units этого прогона;
- already approved compose-sync intent;
- already prepared release-note mapping;
- release-instance exclusions и handoff decisions.

Поэтому для таких шагов обязателен workflow-instance handoff через exchange layer.

## Связанные термины

- `workflow`
- `workflow-step`
- `step-vacancy`
- `Release Documentation Layer`
