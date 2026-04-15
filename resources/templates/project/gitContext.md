# Git Context

## Repository map

| Path | Description | Role |
| --- | --- | --- |
| `./` | Root project repository | root repo |
| `./services/backend/` | Backend service | nested release unit when touched |
| `./services/frontend/` | Frontend service | nested release unit when touched |

## Git boundaries

- Git commands for root-scoped release work run from `./`.
- Git commands for nested release units run from their own repository roots.
- Root repo changes and nested repo changes must not be mixed in one git context.

## Release notes for repository boundaries

- Root project may release `./`.
- Nested release units are released only when touched.
- Non-release directories must be explicitly marked here.
