# Changelog

## 0.6.0

- CI (`ci.yml`): ruff and pytest, PostgreSQL 17 as a service so the database tests really run, then the Docker image is built and smoke tested.
- Every push to `main` and every `v*` tag pushes the image to GHCR as `:<sha>`, `:latest` and `:vX.Y.Z`. Pull requests push nothing.
- Trivy scans the image before the push and stops the pipeline on a fixable CRITICAL vulnerability.
- `compose.prod.yaml` pulls the image instead of building it. `APP_TAG` picks the version, which also makes rollbacks possible.
- The documentation is published with MkDocs on GitHub Pages: https://lpkop.github.io/devops-labs-fn371223037/
- Runbook: "Release and rollback".

## 0.4.0

- Dockerfile: `python:3.12-slim`, cached pip layer, `.dockerignore`, non-root user and a healthcheck.
- `compose.yaml`: the app with PostgreSQL 17, a named volume and a healthcheck; Adminer under the `tools` profile.
- `.env.example` for the database credentials.
- Runbook: "Run with Docker" and "Run with Compose".

## 0.2.0

- Service documentation: purpose, endpoints and dependencies.
- Runbook with exact commands.
- Glossary of DevOps terms.
- ADR 0002 (database for Lab 4) and ADR 0003 (where the service runs).
- On-call schedule for weeks 5-8.
- CODEOWNERS and CONTRIBUTING.md with GitHub Flow.

## 0.1.0


- Initial template: notes API with health and version endpoints.
