# Mistaken Release Recovery: `2026-04-15-openai-chatgpt-policy-editor-release`

## Incident summary

- Release ID: `2026-04-15-openai-chatgpt-policy-editor-release`
- Affected repo/unit: `./services/backend/`, `./services/frontend/`
- Mistaken artifact type: `git-tag`, `github-release`
- Affected version/tag: `v0.0.3`
- Incident reason: `published-from-wrong-branch`

## Detected invalid state

- Current branch at mistaken publication: `request_policy`
- Intended release branch: `main`
- Mistaken tag/release target SHA: `feature-branch head before corrective merge`
- Why this violates project release policy: `release artifacts were created from feature branch instead of merged HEAD intended release branch`

## Recovery decision

- Reuse same version after remediation: `yes`
- Corrective PR/merge required: `yes`
- Additional version bump required: `no`

## Remediation actions

- Erroneous GitHub release deleted: `yes`
- Erroneous git tag deleted: `yes`
- Erroneous Docker/external artifacts remediated: `not-applicable`
- Corrective PR URL: `https://github.com/cyber-platform/backend/pull/2`, `https://github.com/cyber-platform/frontend/pull/3`
- Corrective merge commit SHA: `merged in main before recreated release`

## Final recreated release evidence

- Final release branch: `main`
- Final tag target SHA: `backend/frontend recreated from merged main heads`
- Final release URL: `https://github.com/cyber-platform/backend/releases/tag/v0.0.3`, `https://github.com/cyber-platform/frontend/releases/tag/v0.0.3`
- Final Docker publication status: `not-applicable`

## Closure

- Recovery status: `completed`
- Notes: `Workflow returned to release-publication gate after corrective PR merge and then recreated backend/frontend release artifacts from main.`
