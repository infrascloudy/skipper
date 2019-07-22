FROM python:3.7.2-slim

COPY ./entrypoint.sh /usr/src/app/entrypoint.sh
RUN apt-get update && \
    apt-get -y install netcat && \
    apt-get clean && \
    chmod +x /usr/src/app/entrypoint.sh

WORKDIR /usr/src/app

COPY ./requirements.in /usr/src/app/requirements.in
RUN pip install --upgrade pip \
    && pip install pip-tools \
    && pip-compile /usr/src/app/requirements.in \
    && pip-sync /usr/src/app/requirements.txt

COPY . /usr/src/app

CMD ["/usr/src/app/entrypoint.sh"]
