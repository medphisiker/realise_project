---
name: release-readiness-gate
description: Проверяет, что taskset завершен, знания канонизированы в SoT и release можно безопасно начинать.
version: 1.0.0
---

# Навык: Release Readiness Gate

## Назначение

Навык выполняет пороговую проверку перед релизом.

## Алгоритм

1. Прочитай project-local release binding из `project/releaseContext.md`.
2. Проверь, что relevant task artifacts имеют completed status.
3. Проверь, что архитектура, контракты и runtime behavior уже подняты в project SoT.
4. Зафиксируй touched release units через `project/gitContext.md` и фактический scope изменений.
5. Если остаются white spots, верни процесс в pre-release stage и не переходи к следующим шагам.

## Выход

- confirmed readiness state;
- список touched release units;
- список SoT artifacts, на которые опирается релиз.

## Ограничения

- Не заменяет cleanup, notes или tagging steps.
- Не должен объявлять release-ready состояние, если знания еще не канонизированы в SoT.
