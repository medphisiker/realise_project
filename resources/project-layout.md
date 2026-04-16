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

workflow-pack/
  terms.md                          # workflow-local terms, if the pack defines them

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
      05-release-publication-gate-handoff.md
      06-github-release-handoff.md
      mistaken-release-recovery.md  # optional, only for remediation flow
```

## Notes

- `project/` хранит project-local release binding.
- `terms.md` внутри workflow-pack хранит workflow-local terminology вроде `release-preparation gate` и `release-publication gate`, если pack использует такие термины.
- `docs/` хранит SoT и release notes, но не workflow-instance handoffs.
- `operational_scope/realise_project/` хранит только временные artifacts конкретного release run.
- `mistaken-release-recovery.md` materialize-ится только если workflow фиксирует remediation flow для ошибочного релиза.
- Templates в `resources/templates/` уже разложены по этой структуре.
- Real filled examples лежат в `resources/examples/`.
