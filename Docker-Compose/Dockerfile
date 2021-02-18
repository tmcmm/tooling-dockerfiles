FROM alpine:latest

LABEL maintainer Robert Peteuil <https://github.com/robertpeteuil>

ARG DOCKER_COMPOSE_VERSION="1.24.0"
#ENV DOWNLOAD_URL="https://github.com/docker/compose/releases/download/$DOCKER_COMPOSE_VERSION/docker-compose-Linux-x86_64"

RUN apk --update add py-pip
RUN apk update && \
    apk add --no-cache docker-cli python3 py-cryptography && \
    apk add --no-cache --virtual .docker-compose-deps python3-dev libffi-dev openssl-dev gcc libc-dev make musl-dev && \
    pip3 install cryptography && \
    pip3 install -U docker-compose==${DOCKER_COMPOSE_VERSION} && \
    apk del .docker-compose-deps

#RUN apk --update add py-pip
#RUN apk --update add --virtual build-dependencies gcc python3-dev libffi-dev openssl-dev musl-dev make &&\
#    pip install -U docker-compose==${DOCKER_COMPOSE_VERSION} &&\
#    apk del build-dependencies &&\
#    rm -rf `find / -regex '.*\.py[co]' -or -name apk`

WORKDIR /app
ENTRYPOINT ["/usr/bin/docker-compose"]
CMD ["--version"]