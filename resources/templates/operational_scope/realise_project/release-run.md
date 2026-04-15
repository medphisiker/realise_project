# Release Run: `<release-id>`

## Workflow

- Source workflow: `sot_layers/hyper-graph/assets/workflows/realise_project/workflow.md`
- Current step: `<step-id>`
- Current status: `<status>`

## Gates and stages

- `release-preparation gate`: `<passed|blocked>`
- `release-publication gate`: `<pending|passed|blocked>`
- Current stage: `<release-preparation stage|release-publication stage|completed>`

## Release scope

- `<approved-release-scope-item>`

## Touched release units

- `./`
- `<nested-release-unit-path>/`

## Branch matrix

- `./` -> current: `<current-branch>`, preparation: `feature-<feature-name>`, release: `<release-branch>`
- `<nested-release-unit-path>/` -> current: `<current-branch>`, preparation: `feature-<feature-name>`, release: `<release-branch>`

## Release versions

- Current release version: `<git-tag>`
- Version source of truth: `project/releaseVersionRegistry.json`

## Publication evidence

- PR/merge alignment: `<pending|completed|not-required>`
- Manual verification: `<pending|passed>`
