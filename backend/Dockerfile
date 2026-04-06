# -------- Stage 1: Builder / Dependency Installation --------
FROM python:3.12-slim AS builder

# Set working directory
WORKDIR /app

# ---- Layer 1: Copy only requirements first ----
# This allows Docker to cache dependencies so they are not reinstalled every time code changes
COPY requirements.txt .

# ---- Layer 2: Install dependencies ----
RUN pip install --no-cache-dir -r requirements.txt

# -------- Stage 2: Production Image --------
FROM python:3.12-slim

WORKDIR /app

# ---- Layer 1: Copy installed dependencies from builder ----
COPY --from=builder /usr/local/lib/python3.12/site-packages /usr/local/lib/python3.12/site-packages
COPY --from=builder /usr/local/bin /usr/local/bin

# ---- Layer 2: Copy application code ----
COPY app/ ./app

# Expose port FastAPI will run on
EXPOSE 8000

# ---- CMD to run FastAPI with uvicorn ----
CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8000"]
