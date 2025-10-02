# Python runtime
FROM python:3.10-slim

# Helpful Python defaults
ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1

WORKDIR /app

# System deps for psycopg2
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential gcc libpq-dev \
 && rm -rf /var/lib/apt/lists/*

# Install Python deps
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy app code (everything in the service dir)
COPY . .

# Non-root user (safer)
RUN useradd -m appuser
USER appuser

# Default port; can be overridden (e.g., by compose/k8s)
EXPOSE 8000
ENV PORT=8000

# Start FastAPI with Uvicorn
CMD ["sh", "-c", "uvicorn app.main:app --host 0.0.0.0 --port ${PORT}"]
