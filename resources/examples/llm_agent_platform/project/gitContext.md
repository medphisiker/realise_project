# Git Context проекта

## Карта репозиториев

| Path | Описание | Роль |
| --- | --- | --- |
| `./` | Основной репозиторий `llm_agent_platform` | root repo |
| `./services/frontend/` | React frontend для PoC monitoring/key management | autonomous nested repo |
| `./services/backend/` | Backend runtime, tests, provider registry и OAuth bootstrap scripts | target autonomous nested repo |
| `./services/user_service/` | Identity/login boundary для local operator/admin contour | autonomous nested repo |
| `./externel_projects/` | Внешние reference repositories; их код не является активной целью изменений | nested repos внутри директории |

## Git Boundaries

- Git-команды для основного проекта запускаются из `./`.
- Если task scope уходит в `./services/frontend/`, git-команды нужно запускать из `./services/frontend/` и не смешивать их с root repo.
- Если task scope уходит в `./services/backend/`, git-команды нужно запускать из `./services/backend/`; root repo должен менять только assembly/docs layer вокруг backend boundary.
- Если task scope уходит в `./services/user_service/`, git-команды нужно запускать из `./services/user_service/`; root repo должен менять только assembly/docs layer вокруг user-service boundary.
- `externel_projects/` считаются reference code, если задача явно не нацелена на них.
- Не смешивай root-project changes и `services/backend/` changes в одном git context.

## Release notes for repository boundaries

- Release workflow использует этот файл как baseline-карту repo boundaries и candidate nested release units.
- Default nested release units для root проекта: `./services/backend/`, `./services/frontend/`, `./services/user_service/` when touched.
- `./services/web_ui_service/` не является release unit.
