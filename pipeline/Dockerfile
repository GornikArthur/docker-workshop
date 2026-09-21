FROM python:3.14

# Copy uv binary from official uv image
COPY --from=ghcr.io/astral-sh/uv:latest /uv /bin/

# Set working directory
WORKDIR /app

# Add virtual environment to PATH
ENV PATH="/app/.venv/bin:$PATH"

# Copy dependency files and README
COPY "pyproject.toml" "uv.lock" ".python-version" "README.md" ./

# Install dependencies only
RUN uv sync --locked --no-install-project

# Copy application code and src module
COPY src/ src/
COPY pipeline.py pipeline.py

# Build and install the root project
RUN uv sync --locked

# Set entry point
ENTRYPOINT ["python", "pipeline.py"]