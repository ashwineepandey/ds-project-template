# Base image with Python 3.11
FROM python:3.11-slim AS base

# Install system dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    curl \
    git \
    && rm -rf /var/lib/apt/lists/*

# Set working directory
WORKDIR /app

# Copy dependency files first (for better caching)
COPY pyproject.toml .
COPY requirements.txt .

# Install uv, then use it to install dependencies from requirements.txt
RUN pip install --upgrade pip
RUN pip install uv
RUN uv pip install -r requirements.txt --system

# Copy the rest of the application
COPY . .

# Default command
CMD ["bash"]