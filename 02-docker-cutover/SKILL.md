---
name: release-docker-cutover
description: Готовит release Docker contour, синхронизирует production compose с актуальной логикой development compose и подготавливает образы к ручной проверке.
version: 1.0.0
---

# Навык: Release Docker Cutover

## Назначение

Навык готовит release Docker packaging и compose contour для релиза.

## Алгоритм

1. Прочитай project-local release binding из `project/releaseContext.md`.
2. Прочитай stable Docker naming из `project/dockerReleaseContext.md` и текущие versions/tags из `project/releaseVersionRegistry.json`.
3. Определи changed release units и связанные Docker images.
4. Определи новые release versions/tags для touched release units и обнови `project/releaseVersionRegistry.json`.
5. Собери новые prod-ready образы локально.
6. Сравни `docker-compose-dev.yml` и `docker-compose.yml`.
7. Обнови в `docker-compose.yml`:
   - image refs;
   - release-relevant runtime logic, которая уже materialized в dev compose;
   - другие изменения, без которых prod contour отстанет от фактической логики разработки.
8. Не обновляй `docker-compose-dev.yml`, если релизный шаг не меняет development contour по смыслу.
9. Подготовь результат к ручной локальной проверке пользователем.
10. Только после подтвержденной ручной проверки допускай переход к публикации образов.

## Выход

- обновленный release compose contour;
- обновленный `project/releaseVersionRegistry.json`;
- список образов и тегов, готовых к последующей публикации.

## Ограничения

- Не пушить образы до ручной проверки пользователем.
- Не ограничиваться только заменой image tags, если logic drift между dev и prod compose уже есть.
