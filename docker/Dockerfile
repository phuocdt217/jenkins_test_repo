FROM python:3.13-slim

WORKDIR /app

RUN pip install --no-cache-dir poetry
COPY pyproject.toml poetry.lock* ./
RUN poetry install --no-root --only main

COPY . .

EXPOSE 8000


CMD ["uvicorn", "src.harbor_image_test.index:app", "--host", "0.0.0.0", "--port", "8000"]