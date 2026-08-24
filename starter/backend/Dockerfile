FROM public.ecr.aws/docker/library/python:3.10-alpine

ENV FLASK_RUN_HOST=0.0.0.0

WORKDIR /app

RUN apk add --no-cache \
    gcc \
    musl-dev \
    libffi-dev \
    pcre \
    pcre-dev \
    linux-headers \
    openssl \
    && pip install --no-cache-dir pipenv

COPY Pipfile Pipfile.lock ./

RUN pipenv install --system

COPY . .

RUN adduser -D app
USER app

CMD ["uwsgi", "--http", ":5000", "--master", "--enable-threads", "-s", "/tmp/app.sock", "--manage-script-name", "--mount", "/=app:app"]