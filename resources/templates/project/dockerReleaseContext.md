# Docker Release Context

## Purpose

Этот файл задает stable Docker registry/repository naming для release workflow.

## Target registry

- Primary registry: `<registry-name>`
- Default namespace: `<namespace>`

## Release image names

- backend: `<namespace>/<backend-image-name>`
- frontend: `<namespace>/<frontend-image-name>`

## Scope notes

- Images publish only for touched release units.
- Compose release contour must stay aligned with these repositories.
