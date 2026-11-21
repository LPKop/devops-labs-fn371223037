# Runbook

## Start locally / Локално стартиране

```bash
python3.12 -m venv .venv
source .venv/bin/activate          # Windows: .venv\Scripts\activate
pip install -r requirements-dev.txt
uvicorn app.main:app --reload --port 8000
```

## Run with Docker / Стартиране с Docker

Build the image / Изграждане на образа:

```bash
docker build -t notes-api:0.3.0 .
```

Run it in the background on port 8000 / Стартиране във фонов режим на порт 8000:

```bash
docker run -d --name notes-api -p 8000:8000 -e APP_VERSION=0.3.0 notes-api:0.3.0
curl http://127.0.0.1:8000/health
docker inspect --format '{{.State.Health.Status}}' notes-api   # healthy
```

Logs / Логове:

```bash
docker logs -f notes-api        # Ctrl+C to leave / Ctrl+C за изход
```

Stop and remove / Спиране и изтриване:

```bash
docker stop notes-api
docker rm notes-api
```

## Check that it works / Проверка, че работи

```bash
curl http://127.0.0.1:8000/health
```

Expected / Очаквано: `{"status":"ok"}`. The API docs are at http://127.0.0.1:8000/docs. / Документацията на API е на http://127.0.0.1:8000/docs.

## Run the tests / Тестове

```bash
pytest
ruff check .
```

## When something breaks / Когато нещо се счупи

1. Is the process running and listening on port 8000? / Работи ли процесът и слуша ли на порт 8000?

   ```bash
   curl -i http://127.0.0.1:8000/health
   ```

2. Can it reach the storage? / Достъпно ли е хранилището?

   ```bash
   curl -i http://127.0.0.1:8000/ready
   ```

3. What do the logs say? / Какво казват логовете?

   ```bash
   uvicorn app.main:app --port 8000 --log-level debug
   ```
