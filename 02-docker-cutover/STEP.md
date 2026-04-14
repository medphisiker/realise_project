# Workflow Step: Docker Cutover

## Назначение

Подготовить release Docker contour проекта и синхронизировать production compose с актуальной логикой development compose.

## Входы

- touched release units;
- `docker-compose-dev.yml`;
- `docker-compose.yml`;
- project-local release binding.

## Действие

- собрать новые prod-ready образы;
- сравнить `docker-compose-dev.yml` и `docker-compose.yml`;
- перенести в `docker-compose.yml` новые image refs и release-relevant runtime logic, которая уже materialized в dev contour;
- подготовить release contour для manual verification пользователем.

## Выходы

- обновленный release compose contour;
- набор образов, готовых к manual verification и последующей публикации.

## DoD

- `docker-compose.yml` синхронизирован с актуальной release logic и готов к ручной проверке.

## Связанный skill

- [`SKILL.md`](./SKILL.md)
