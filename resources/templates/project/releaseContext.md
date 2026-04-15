# Release Context

## Purpose

Этот файл фиксирует project-local release binding для `<project-name>`.

## Release units

- `./` — root release unit
- `<nested-release-unit-path>/` when touched

## Release branch policy

### Release branches

- `./` -> `<release-branch>`
- `<nested-release-unit-path>/` -> `<release-branch>`

### Preparation branch policy

- Default preparation branch pattern: `feature-<feature-name>`
- Direct preparation in release branch requires explicit user confirmation.

### Preparation branch rule

- Steps подготовки релиза до `release-publication gate` выполняются в preparation branch.
- Presence of preparation branch допустима и ожидаема на стадиях readiness, docker cutover, cleanup и release notes.

### Release source rule

- Git tags, GitHub releases и Docker publish flow разрешены только из merged HEAD configured release branch.
- Open PR, approved PR или просто наличие feature branch недостаточны для release publication.
- Если preparation выполнена в feature branch, workflow должен пройти PR/merge flow в configured release branch перед publication.

## Release documentation locations

- root release notes: `docs/releases/`
- nested release notes: `<nested-release-unit-release-notes-path>/`

## Publish flow

1. `01-readiness-gate` passes `release-preparation gate`, fixes touched release units and branch matrix.
2. `02-docker-cutover` prepares Docker contour and updates `project/releaseVersionRegistry.json` during `release-preparation stage`.
3. `03-artifact-cleanup` and `04-release-notes` complete preparation artifacts.
4. Before publication, workflow must pass `release-publication gate`: touched release units must be merged into their configured release branches.
5. Final Docker/image publication, git tags and GitHub releases are allowed only from merged HEAD configured release branch.

## Atomicity

- Default policy: `whole-run atomic`

## Mistaken release recovery

- Erroneous release/tag must be deleted.
- Corrective PR/merge flow must be completed.
- Version reuse is allowed only if project policy explicitly permits it after remediation.

## PR/merge evidence

- Workflow artifacts should record `repo -> current branch`, `repo -> release branch`, `repo -> PR URL`, `repo -> merge commit SHA`, `repo -> final release commit SHA` when branch integration is required.
