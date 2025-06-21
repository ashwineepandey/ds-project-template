# Base image with Python 3.11
FROM python:3.11-slim AS base

# Install system dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    curl \
    git \
    && rm -rf /var/lib/apt/lists/*

# Install uv
RUN curl -LsSf https://astral.sh/uv/install.sh | sh
ENV PATH="/root/.cargo/bin:${PATH}"

# Set working directory
WORKDIR /app

# Copy dependency files first (for better caching)
COPY pyproject.toml .
COPY requirements.txt .

# Create and use virtual environment
RUN uv venv /app/.venv
ENV PATH="/app/.venv/bin:${PATH}"

# Install dependencies
RUN uv pip install -r requirements.txt

# Copy the rest of the application
COPY . .

# Default command
CMD ["bash"]