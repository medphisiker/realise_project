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

## Release documentation locations

- root release notes: `docs/releases/`
- nested release notes: `<nested-release-unit-release-notes-path>/`

## Publish flow

1. `01-readiness-gate` fixes touched release units and branch matrix.
2. Release preparation continues in preparation branches.
3. Before publication, touched release units must be merged into their configured release branches.
4. Docker/image publication, git tags and GitHub releases are allowed only from merged HEAD configured release branch.

## Atomicity

- Default policy: `whole-run atomic`

## Mistaken release recovery

- Erroneous release/tag must be deleted.
- Corrective PR/merge flow must be completed.
- Version reuse is allowed only if project policy explicitly permits it after remediation.
