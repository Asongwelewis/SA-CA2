# Build stage
FROM python:3.12-slim AS builder
WORKDIR /build
COPY requirements.txt .
RUN pip install --no-cache-dir --prefix=/install -r requirements.txt

# Final stage
FROM python:3.12-slim
WORKDIR /app
RUN useradd -u 10001 -r -s /sbin/nologin appuser
COPY --from=builder /install /usr/local
COPY requirements.txt .
COPY app/ ./app/
USER appuser
EXPOSE 8002
CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8002"]
