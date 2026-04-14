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
2. Определи changed release units и связанные Docker images.
3. Собери новые prod-ready образы локально.
4. Сравни `docker-compose-dev.yml` и `docker-compose.yml`.
5. Обнови в `docker-compose.yml`:
   - image refs;
   - release-relevant runtime logic, которая уже materialized в dev compose;
   - другие изменения, без которых prod contour отстанет от фактической логики разработки.
6. Не обновляй `docker-compose-dev.yml`, если релизный шаг не меняет development contour по смыслу.
7. Подготовь результат к ручной локальной проверке пользователем.
8. Только после подтвержденной ручной проверки допускай переход к публикации образов.

## Выход

- обновленный release compose contour;
- список образов и тегов, готовых к последующей публикации.

## Ограничения

- Не пушить образы до ручной проверки пользователем.
- Не ограничиваться только заменой image tags, если logic drift между dev и prod compose уже есть.
