FROM python:3.12-slim

ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1 \
    PIP_NO_CACHE_DIR=1 \
    PORT=8080

WORKDIR /app

# Install build/runtime deps only if needed; most libs ship manylinux wheels
RUN apt-get update && apt-get install -y --no-install-recommends \
    ca-certificates \
  && rm -rf /var/lib/apt/lists/*

# Copy and install dependencies
COPY requirements.txt ./
RUN python -m pip install --upgrade pip && \
    pip install -r requirements.txt

# Copy application code
COPY . .

EXPOSE 8080

# Start FastAPI with uvicorn; use $PORT provided by Cloud Run
CMD ["sh","-c","uvicorn main:app --host 0.0.0.0 --port ${PORT:-8080}"]


