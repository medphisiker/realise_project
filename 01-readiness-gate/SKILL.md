---
name: release-readiness-gate
description: Проверяет, что taskset завершен, знания канонизированы в SoT, release scope определен и pre-release preparation идет в допустимых preparation branches.
version: 1.2.0
---

# Навык: Release Readiness Gate

## Назначение

Навык выполняет пороговую проверку перед релизом.

## Алгоритм

1. Прочитай project-local release binding из `project/releaseContext.md`.
2. Проверь, что relevant task artifacts имеют completed status.
3. Проверь, что архитектура, контракты и runtime behavior уже подняты в project SoT.
4. Зафиксируй touched release units через `project/gitContext.md` и фактический scope изменений.
5. Проверь branch matrix для root repo и touched release units against project-local preparation/release branch policy.
6. Если preparation идет в допустимой feature branch, это нормальный expected state и workflow может продолжаться.
7. Если preparation идет прямо в release branch без explicit user confirmation или branch не проходит preparation policy, останови workflow до clarifying decision.
8. Если остаются white spots, верни процесс в pre-release stage и не переходи к следующим шагам.

## Выход

- confirmed readiness state;
- список touched release units;
- branch matrix и branch/preparation eligibility decision;
- список SoT artifacts, на которые опирается релиз.

## Ограничения

- Не заменяет cleanup, notes или tagging steps.
- Не должен объявлять release-ready состояние, если знания еще не канонизированы в SoT.
- Не должен silently пропускать preparation в release branch, если project policy ожидает feature branch preparation.
