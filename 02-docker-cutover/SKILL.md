---
name: release-docker-cutover
description: Готовит release Docker contour на preparation stage, синхронизирует production compose с актуальной логикой development compose и подготавливает локальную Docker-проверку до hard publication gate.
version: 1.1.0
---

# Навык: Release Docker Cutover

## Назначение

Навык готовит release Docker packaging и compose contour для релиза на preparation stage.

## Алгоритм

1. Прочитай project-local release binding из `project/releaseContext.md`.
2. Прочитай stable Docker naming из `project/dockerReleaseContext.md` и текущие versions/tags из `project/releaseVersionRegistry.json`.
3. Определи changed release units и связанные Docker images.
4. Определи новые release versions/tags для touched release units и обнови `project/releaseVersionRegistry.json`.
5. Собери preparation images локально с agreed release tags для touched release units.
6. Сравни `docker-compose-dev.yml` и `docker-compose.yml`.
7. Обнови в `docker-compose.yml`:
    - image refs;
    - release-relevant runtime logic, которая уже materialized в dev compose;
    - другие изменения, без которых prod contour отстанет от фактической логики разработки.
8. Не обновляй `docker-compose-dev.yml`, если релизный шаг не меняет development contour по смыслу.
9. Подготовь результат к ручной локальной проверке пользователем на preparation stage.
10. Зафиксируй, что финальная publication Docker images не выполняется на этом шаге и требует hard publication gate в intended release branch.
11. Только после подтвержденной ручной проверки и прохождения hard gate допускай переход к финальной публикации образов.

## Выход

- обновленный release compose contour;
- обновленный `project/releaseVersionRegistry.json`;
- список preparation images и тегов, готовых к manual verification и последующей финальной publication re-check.

## Ограничения

- Не пушить образы до ручной проверки пользователем.
- Не считать локальную preparation build достаточным основанием для final Docker publish.
- Не публиковать Docker images из feature/preparation branch.
- Не ограничиваться только заменой image tags, если logic drift между dev и prod compose уже есть.
