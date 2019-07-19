FROM python:3.7.2-alpine

COPY ./entrypoint.sh /usr/src/app/entrypoint.sh
RUN apk update && \
    apk add --virtual build-deps gcc python-dev musl-dev && \
    apk add postgresql-dev && \
    apk add netcat-openbsd && \
    chmod +x /usr/src/app/entrypoint.sh

WORKDIR /usr/src/app

COPY ./requirements.in /usr/src/app/requirements.in
RUN pip install --upgrade pip \
    && pip install pip-tools \
    && pip-compile /usr/src/app/requirements.in \
    && pip-sync /usr/src/app/requirements.txt

COPY . /usr/src/app

CMD ["/usr/src/app/entrypoint.sh"]
