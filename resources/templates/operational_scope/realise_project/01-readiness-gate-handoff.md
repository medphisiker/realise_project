# Handoff: `01-readiness-gate`

## Release run

- Release ID: `<release-id>`
- Step result: `<passed|blocked>`

## `release-preparation gate`

- Gate result: `<passed|blocked>`

## Touched release units

- `./`
- `<nested-release-unit-path>/`

## Branch matrix

- `./` -> current: `<current-branch>`, preparation policy: `feature-<feature-name>`, release: `<release-branch>`
- `<nested-release-unit-path>/` -> current: `<current-branch>`, preparation policy: `feature-<feature-name>`, release: `<release-branch>`

## Decision

- `<readiness-and-branch-eligibility-decision>`

## Next stage

- Workflow may proceed to `release-preparation stage` only if this gate is passed.
