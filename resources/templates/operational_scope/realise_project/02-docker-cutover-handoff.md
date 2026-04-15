# Handoff: `02-docker-cutover`

## Release run

- Release ID: `<release-id>`
- Step result: `<passed|blocked>`

## Stage

- Current stage: `release-preparation stage`

## Release contour changes

- `project/releaseVersionRegistry.json` updated to `<version>` for touched units
- `docker-compose.yml` updated for `<touched-release-unit>`
- preparation images built locally for `<touched-release-unit>`

## Manual verification gate

- Preparation images are prepared locally and await manual verification.

## `release-publication gate` dependency

- Final Docker publication is blocked until PR/merge alignment is completed in configured release branches.
