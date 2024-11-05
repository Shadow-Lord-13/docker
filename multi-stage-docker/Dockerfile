# Stage 1: Build stage with dependencies and environment setup
FROM ubuntu:latest AS builder

WORKDIR /app

COPY requirements.txt /app
COPY devops /app


RUN apt-get update && apt-get install -y python3 python3-pip python3-venv

RUN python3 -m venv /app/venv && \
    /app/venv/bin/pip install --upgrade pip && \
    /app/venv/bin/pip install -r requirements.txt

# Check if Django is installed in the virtual environment
RUN python -m django --version

# Stage 2: Final, lightweight image

FROM python:3.12-slim

WORKDIR /app

COPY --from=builder /app /app
#COPY --from=builder /app/venv /app/venv

# Verify that the Django package exists in the final image
RUN ls /app/venv/lib/python*/site-packages/django

RUN cd devops
# Set the virtual environment's Python as default
ENV PATH="/app/venv/bin:$PATH"

CMD ["python3", "manage.py", "runserver", "0.0.0.0:8000"]