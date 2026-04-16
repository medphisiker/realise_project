# Workflow Step: Mistaken Release Recovery

## Назначение

Выполнить remediation flow, если после `06-github-release` обнаружен mistaken release: erroneous tag/release/publication artifacts созданы не из intended release branch или не на том target commit.

## Execution scope

- Это exception/remediation step, а не обязательная часть happy path.
- Шаг выполняется только если mistaken release действительно обнаружен после publication.
- Шаг может затрагивать root repo и touched nested release units, для которых был создан erroneous artifact.

## Входы

- `06-github-release-handoff.md`;
- `mistaken-release-recovery.md` remediation artifact;
- `project/releaseContext.md`;
- `project/gitContext.md`;
- текущий `release-run.md`.

## Действие

- зафиксировать invalid publication state;
- удалить erroneous GitHub releases/tags when applicable;
- зафиксировать remediation status для Docker/external artifacts when applicable;
- направить workflow в corrective PR/merge alignment;
- после remediation подготовить evidence для повторного `05-release-publication-gate` и `06-github-release`.

## Что шаг не делает

- не считается частью normal happy path;
- не пропускает remediation evidence;
- не re-publishes release silently без фиксации incident/remediation state.

## Выходы

- remediation artifact с completed or blocked status;
- updated `release-run.md`;
- evidence for return to `05-release-publication-gate`.

## Минимальная проверка внутри шага

- invalid publication state explicitly recorded;
- erroneous artifacts either removed or marked as not-applicable;
- corrective path back to publication gate clearly stated.

## DoD

- mistaken release remediation state зафиксирован как explicit workflow step output.
- workflow может либо безопасно вернуться к `05-release-publication-gate`, либо остаться blocked с явной причиной.

## Связанный skill

- [`SKILL.md`](./SKILL.md)
