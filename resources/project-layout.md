# Project Layout For `realise_project`

## Назначение

Эта карта показывает минимальную рекомендуемую структуру проекта для подключения workflow pack.

## Recommended layout

```text
project/
  gitContext.md                     # required
  releaseContext.md                 # required
  releaseVersionRegistry.json       # required
  dockerReleaseContext.md           # recommended if Docker publish exists

docs/
  releases/                         # default root release notes location

operational_scope/
  realise_project/
    <release-id>/                   # workflow-instance exchange layer
      release-run.md
      01-readiness-gate-handoff.md
      02-docker-cutover-handoff.md
      03-artifact-cleanup-handoff.md
      04-release-notes-handoff.md
      05-github-release-handoff.md
```

## Notes

- `project/` хранит project-local release binding.
- `docs/` хранит SoT и release notes, но не workflow-instance handoffs.
- `operational_scope/realise_project/` хранит только временные artifacts конкретного release run.
- Templates в `resources/templates/` уже разложены по этой структуре.
- Real filled examples лежат в `resources/examples/`.
