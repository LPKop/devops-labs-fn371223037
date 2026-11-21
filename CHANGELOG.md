# Changelog

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
