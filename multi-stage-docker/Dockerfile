# Stage 1: Build stage with dependencies and environment setup
FROM ubuntu:latest as builder

WORKDIR /app

COPY requirements.txt /app
COPY devops /app

RUN apt-get update && apt-get install -y python3 python3-pip python3-venv

RUN python3 -m venv /app/venv && \
    /app/venv/bin/pip install --upgrade pip && \
    /app/venv/bin/pip install -r requirements.txt

# Stage 2: Final, lightweight image

FROM gcr.io/distroless/python3

WORKDIR /app

#COPY --from=builder /app/venv /app/venv
COPY --from=builder /app /app

# Set the virtual environment's Python as default
ENV PATH="/app/venv/bin:$PATH"
RUN cd devops

ENTRYPOINT ["python3"]
CMD ["manage.py", "runserver", "0.0.0.0:8000"]