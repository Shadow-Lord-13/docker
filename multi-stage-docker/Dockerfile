# Stage 1: Build stage with dependencies and environment setup
FROM ubuntu:latest AS builder

WORKDIR /app

COPY requirements.txt /app
COPY devops /appa


RUN apt update && apt-get install -y python3 python3-pip python3-venv && \
    python3 -m venv /app/venv && \
    /app/venv/bin/pip install --upgrade pip && \
    /app/venv/bin/pip install django && \
    /app/venv/bin/pip install -r requirements.txt

# Stage 2: Final, lightweight image

FROM python:3.12-slim

WORKDIR /app

COPY --from=builder /app /app
COPY --from=builder /app/venv /app/venv

# Verify that the Django package exists in the final image
RUN ls /app/venv/lib/python*/site-packages/django

# Set the virtual environment's Python as default
ENV PATH="/app/venv/bin:$PATH"
RUN cd devops

ENTRYPOINT ["python3"]
CMD ["manage.py", "runserver", "0.0.0.0:8000"]