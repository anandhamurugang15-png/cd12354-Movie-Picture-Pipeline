FROM public.ecr.aws/docker/library/python:3.10-alpine

ENV FLASK_RUN_HOST=0.0.0.0

WORKDIR /app

RUN apk add --no-cache \
    pcre \
    pcre-dev \
    build-base \
    linux-headers \
    openssl \
    libffi-dev

RUN pip install --no-cache-dir pipenv

COPY Pipfile Pipfile.lock ./

RUN pipenv install --system --deploy

COPY . .

CMD ["flask", "--app", ".", "run", "--host", "0.0.0.0", "--port", "5000"]