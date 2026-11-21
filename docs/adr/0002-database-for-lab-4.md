# 0002. Database for Lab 4 / База данни за Упражнение 4

**Status / Статус:** Accepted

## Context / Контекст

Without `DATABASE_URL` the notes live in memory and are lost on every restart. From Lab 4 on the service must keep its data between restarts and between several app instances. / Без `DATABASE_URL` бележките са в паметта и се губят при рестарт. От Упражнение 4 данните трябва да се пазят между рестарти и между няколко инстанции.

## Options / Варианти

1. **PostgreSQL.** Pros: already supported by the app (`PostgresNoteRepository`, `psycopg`), a real server that several instances share, an official Docker image. Cons: one more service to run and back up. / Плюсове: вече се поддържа от приложението, споделя се от няколко инстанции, има официален образ. Минуси: още една услуга за поддръжка.
2. **SQLite.** Pros: a single file, no server. Cons: not shared between instances on different servers, the app has no repository for it. / Плюсове: един файл, без сървър. Минуси: не се споделя между сървъри, няма поддръжка в приложението.
3. **Keep in memory.** Pros: nothing to set up. Cons: data is lost on restart, every instance has different data. / Плюсове: нищо за настройка. Минуси: данните се губят.

## Decision / Решение

We use PostgreSQL, connected through `DATABASE_URL=postgresql://notes:secret@db:5432/notes`. / Използваме PostgreSQL чрез `DATABASE_URL`.

Lab 4 confirms it: `compose.yaml` runs `postgres:17-alpine` as the service `db` with a named volume `db-data`, and the app starts only when `pg_isready` passes. The credentials are in `.env` (not in git); `.env.example` is the template. / Упражнение 4 го потвърждава: `compose.yaml` пуска `postgres:17-alpine` като услуга `db` с volume `db-data`, а приложението тръгва чак когато `pg_isready` мине. Данните за достъп са в `.env` (не е в git).

## Consequences / Последствия

- Notes survive restarts and are the same on every instance. / Бележките се запазват и са еднакви навсякъде.
- `/ready` returns 503 while the database is down. / `/ready` връща 503, докато базата не е достъпна.
- We must run, secure and back up a database server; the password must move out of the URL into a secret. / Трябва да поддържаме, защитим и архивираме сървъра; паролата отива в secret.
