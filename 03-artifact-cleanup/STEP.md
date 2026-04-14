# Workflow Step: Artifact Cleanup

## Назначение

Удалить completed operational artifacts, которые уже не нужны после канонизации знаний в SoT.

## Входы

- completed task artifacts;
- completed plan artifacts;
- project SoT;
- task index.

## Действие

- проверить, что relevant knowledge уже поднято в SoT;
- удалить completed task/plan artifacts, относящиеся к релизуемому scope;
- синхронизировать task index.

## Выходы

- очищенный operational layer;
- синхронизированный task index.

## DoD

- в operational layer не осталось completed implementation artifacts, уже дублируемых SoT.

## Связанный skill

- [`SKILL.md`](./SKILL.md)
