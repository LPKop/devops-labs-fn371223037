# Service / Услугата

## Purpose / Предназначение

Notes API is a small REST service for creating and reading short text notes. It is the starter application for the DevOps course: students use it to practise containers, databases, CI/CD, deployment and monitoring. / Notes API е малка REST услуга за създаване и четене на кратки текстови бележки. Тя е учебното приложение за курса по DevOps: върху нея се упражняват контейнери, бази данни, CI/CD, внедряване и наблюдение.

## Endpoints / Адреси

| Method | Path | What it does / Какво прави |
|---|---|---|
| GET | /health | Liveness check. Always returns `{"status": "ok"}` while the process runs. / Проверка дали процесът е жив. Връща `{"status": "ok"}`. |
| GET | /ready | Readiness check. Returns `{"status": "ready"}` if the storage can be reached, otherwise 503 with `{"status": "storage unavailable"}`. / Проверка за готовност: 200, ако хранилището е достъпно, иначе 503. |
| GET | /version | Returns the running version from `APP_VERSION`, e.g. `{"version": "0.1.0"}` (default `0.1.0`). / Връща версията от `APP_VERSION` (по подразбиране `0.1.0`). |
| GET | /model | Returns the loaded ML model file from `MODEL_PATH`, or `{"model": null}` if none. / Връща заредения ML модел или `null`. |
| GET | /notes | Returns a JSON list of all notes. / Връща списък с всички бележки. |
| POST | /notes | Creates a note from `{"title": "...", "body": "..."}`. `title` is required (1–100 characters), `body` is optional. Returns 201 with the new note; 422 if the data is invalid. / Създава бележка. `title` е задължително (1–100 знака). Връща 201; 422 при невалидни данни. |
| GET | /notes/{id} | Returns one note by id; 404 `{"detail": "Note not found"}` if it does not exist. / Връща една бележка; 404, ако не съществува. |

## Dependencies / Зависимости

- Python 3.12 with the packages in `requirements.txt` (FastAPI, Uvicorn, psycopg). / Python 3.12 и пакетите от `requirements.txt`.
- Optional: PostgreSQL, set through `DATABASE_URL` (e.g. `postgresql://notes:secret@db:5432/notes`). Without it notes are kept in memory and lost on restart. / По желание: PostgreSQL чрез `DATABASE_URL`. Без нея бележките са в паметта.
- Optional: a trained model file, set through `MODEL_PATH`, to assign a category to new notes. / По желание: файл с модел чрез `MODEL_PATH`.
- Optional: `APP_VERSION` to report the version. / По желание: `APP_VERSION` за версията.
