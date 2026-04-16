# Mistaken Release Recovery: `<release-id>`

## Incident summary

- Release ID: `<release-id>`
- Affected repo/unit: `<repo-or-release-unit>`
- Mistaken artifact type: `<git-tag|github-release|docker-image|multiple>`
- Affected version/tag: `<version>`
- Incident reason: `<published-from-wrong-branch|wrong-tag-target|wrong-scope|other>`

## Detected invalid state

- Current branch at mistaken publication: `<branch>`
- Intended release branch: `<release-branch>`
- Mistaken tag/release target SHA: `<sha>`
- Why this violates project release policy: `<short-policy-violation>`

## Recovery decision

- Reuse same version after remediation: `<yes|no>`
- Corrective PR/merge required: `<yes|no>`
- Additional version bump required: `<yes|no>`

## Remediation actions

- Erroneous GitHub release deleted: `<yes|no|not-applicable>`
- Erroneous git tag deleted: `<yes|no|not-applicable>`
- Erroneous Docker/external artifacts remediated: `<yes|no|not-applicable>`
- Corrective PR URL: `<url-or-not-applicable>`
- Corrective merge commit SHA: `<sha-or-not-applicable>`

## Final recreated release evidence

- Final release branch: `<release-branch>`
- Final tag target SHA: `<sha>`
- Final release URL: `<url>`
- Final Docker publication status: `<published|not-published|not-applicable>`

## Closure

- Recovery status: `<completed|partial|blocked>`
- Notes: `<freeform>`
