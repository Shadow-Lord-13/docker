# Stage 1: Build stage with dependencies and environment setup
FROM ubuntu:latest AS builder

WORKDIR /app

COPY requirements.txt /app
COPY devops /app


RUN apt-get update && apt-get install -y python3 python3-pip python3-venv

RUN python3 -m venv /app/venv && \
    /app/venv/bin/pip install --upgrade pip && \
    /app/venv/bin/pip install -r requirements.txt


# Set the virtual environment's Python as default
ENV PATH="/app/venv/bin:$PATH"

# Check if Django is installed in the virtual environment
RUN /app/venv/bin/python3 -m django --version

# Stage 2: Final, lightweight image

FROM python:3.12-slim

WORKDIR /app

COPY --from=builder /app /app

# Copy only site-packages from builder’s virtual environment
#COPY --from=builder /app/venv/lib/python3.12/site-packages /usr/local/lib/python3.12/site-packages

# Set environment path to use the site-packages
#ENV PYTHONPATH="/usr/local/lib/python3.12/site-packages"

RUN cd devops
# Set the virtual environment's Python as default
ENV PATH="/app/venv/bin:$PATH"

# Expose the port Django will run on
EXPOSE 8000

# Run Django server using full path to ensure it uses the virtual environment
CMD ["python3", "manage.py", "runserver", "0.0.0.0:8000"]