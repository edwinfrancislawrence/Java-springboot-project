# FROM python:3.10-slim

# WORKDIR /app

# COPY requirements.txt /app/
# RUN pip install --no-cache-dir -r requirements.txt

# COPY . /app

# # Set environment variable
# ENV API_URL=http://35.164.134.252:8084

# EXPOSE 8501

# CMD ["streamlit", "run", "app.py", "--server.port=8501", "--server.address=0.0.0.0"]


# ==========================================
# STAGE 1: The Builder Environment (NON Root User)
# ==========================================
FROM python:3.10-slim AS builder

WORKDIR /app

RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    gcc \
    && rm -rf /var/lib/apt/lists/*

COPY requirements.txt .

RUN pip install --no-cache-dir --target=/app/dependencies -r requirements.txt


# ==========================================
# STAGE 2: The Final Lightweight Runtime (Non-Root)
# ==========================================
FROM python:3.10-slim AS runtime

# 1. Create a secure, non-root system group and user
# (Using /sbin/nologin matches Amazon Linux / RHEL security conventions for service accounts)
RUN groupadd -g 10001 appgroup && \
    useradd -u 10001 -g appgroup -m -s /sbin/nologin appuser

WORKDIR /app

# 2. Copy files from Stage 1 AND local context, giving ownership to appuser
COPY --from=builder --chown=appuser:appgroup /app/dependencies /app/dependencies
COPY --chown=appuser:appgroup . /app

# Configure Python paths
ENV PYTHONPATH=/app/dependencies
ENV PATH=/app/dependencies/bin:$PATH

# Set environment variable
ENV API_URL=http://35.164.134.252:8084

EXPOSE 8501

# 3. Switch execution context from root to the restricted user
USER appuser

CMD ["streamlit", "run", "app.py", "--server.port=8501", "--server.address=0.0.0.0"]
