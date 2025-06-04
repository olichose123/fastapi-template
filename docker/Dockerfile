FROM python:3.11-slim

WORKDIR /usr/src

RUN apt-get update \
    && apt-get install -y \
    gcc \
    netcat-traditional \
    && pip install "poetry~=2.1.1" \
    && poetry config virtualenvs.create false \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists

EXPOSE 8080
COPY poetry.lock pyproject.toml ./

RUN poetry install --only main;

COPY . .

RUN chmod -R 775 .
RUN chown -R 1000:root .
USER 1000

CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
