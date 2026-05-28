# Backend (FastAPI) Dockerfile
# Base: python:3.11-slim
FROM python:3.11-slim

# Avoid Python buffering and ensure pip doesn't write cache
ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1

# Workdir
WORKDIR /app

# Copy requirements from build context (compose will set context to project root)
COPY requirements.txt /app/requirements.txt
RUN pip install --no-cache-dir -r /app/requirements.txt

# Copy application source
COPY . /app

# Create non-root user (uid 1000) and switch
RUN useradd -m -u 1000 appuser && \
    chown -R appuser:appuser /app
USER appuser

# Expose API port
EXPOSE 8000

# Start FastAPI with Uvicorn (module path expected: app.backend.main)
CMD ["uvicorn", "app.backend.main:app", "--reload", "--host", "0.0.0.0", "--port", "8000"]
