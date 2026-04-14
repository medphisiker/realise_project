# Workflow Step: Artifact Cleanup

## Назначение

Удалить completed operational artifacts, которые уже не нужны после канонизации знаний в SoT.

## Execution scope

- Не учитывай место хранения workflow step artifacts при определении execution scope.
- Шаг выполняется для root project operational layer, а не для nested release units напрямую.
- Cleanup ограничен approved release scope текущего workflow-run.
- Unrelated active/deferred backlog artifacts не являются целью этого шага.

## Входы

- completed task artifacts;
- completed plan artifacts;
- project SoT;
- task index.
- `project/releaseContext.md`;
- `01-readiness-gate-handoff.md`;
- `02-docker-cutover-handoff.md`;
- текущий `release-run.md`.

## Действие

- проверить, что relevant knowledge уже поднято в SoT;
- удалить completed task/plan artifacts, относящиеся к релизуемому scope;
- синхронизировать task index.

## Что шаг не делает

- не удаляет artifacts с незакрытым знанием;
- не удаляет active или deferred artifacts;
- не чистит unrelated historical evidence автоматически;
- не меняет release docs вместо cleanup work;
- не трогает artifacts вне approved release scope.

## Выходы

- очищенный operational layer;
- синхронизированный task index.
- список удаленных artifacts;
- список intentionally retained artifacts;
- обновленный `release-run.md`;
- handoff artifact для шага `04-release-notes`.

## Минимальная проверка внутри шага

- каждый удаляемый artifact имеет completed status;
- каждый удаляемый artifact относится к approved release scope;
- relevant knowledge для него уже canonized в `docs/`;
- `operational_scope/tasks_map.md` синхронизирован после cleanup.

## DoD

- в operational layer не осталось completed implementation artifacts, уже дублируемых SoT.
- `release-run.md` отражает завершение шага.
- подготовлен handoff artifact для следующего шага.

## Связанный skill

- [`SKILL.md`](./SKILL.md)
