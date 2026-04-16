# Terms: `realise_project`

## Назначение

Этот файл фиксирует workflow-local terms для `realise_project`, чтобы step docs и workflow overview использовали одни и те же gate/stage термины без повторного переопределения.

## Workflow-local terms

### `release-preparation stage`

Стадия workflow, на которой проект готовит release artifacts до финальной publication.

В эту стадию входят:
- readiness confirmation;
- version fixation;
- Docker/compose contour preparation;
- artifact cleanup;
- release notes preparation.

### `release-preparation gate`

Gate на вход в `release-preparation stage`.

Он проверяет, что:
- release scope действительно готов к началу release workflow;
- relevant knowledge уже поднято в SoT;
- touched release units проходят project-local preparation branch policy.

Этот gate не публикует release artifacts и не заменяет final publication validation.

### `release-publication stage`

Стадия workflow, на которой ранее подготовленные release artifacts materialize-ятся как финальная публикация.

В эту стадию входят:
- final publication eligibility check;
- publication-stage Docker contour/materialization;
- git tags;
- GitHub releases.

### `release-publication gate`

Gate перед входом в `release-publication stage`.

Он проверяет, что:
- touched release units удовлетворяют project-local publication branch policy;
- required PR/merge alignment уже завершен;
- publication может безопасно идти из intended release branch.

Этот gate строже `release-preparation gate`, потому что после него workflow переходит к финальным release artifacts.

В `realise_project` этот gate materialize-ится как отдельный workflow-step `05-release-publication-gate`.
