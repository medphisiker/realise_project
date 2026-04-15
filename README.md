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

## Как использовать в своем проекте

Этот раздел предназначен для пользователя, который хочет перенести workflow pack в новый проект.

1. Сначала прочитать [`setup_instructions.md`](./setup_instructions.md).
2. Затем разложить templates в свой проект с сохранением путей.
3. После этого заполнить project-local release binding в `project/releaseContext.md` и related files.
4. Затем использовать examples из `resources/examples/` как reference shape.
5. Когда интеграция завершена, выполнять workflow уже по разделу `Как выполнять workflow`.

## Куда идти дальше

- execution semantics workflow и step order — в [`workflow.md`](./workflow.md)
- project integration and required files — в [`setup_instructions.md`](./setup_instructions.md)
- concrete step behavior — в соответствующие `STEP.md` и `SKILL.md`
- reusable templates и finished examples — в `resources/`

## Связанные термины

- `workflow`
- `workflow-step`
- `step-vacancy`
- `Release Documentation Layer`
