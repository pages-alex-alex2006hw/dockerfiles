FROM alpine:3.4
MAINTAINER Wonderfall <wonderfall@schrodinger.io>

ENV BASE_URL=False IMAGE_PROXY=False \
    UID=991 GID=991

RUN echo "@commuedge https://nl.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories \
 && BUILD_DEPS=" \
    build-base \
    python-dev \
    py-pip \
    libffi-dev \
    libxslt-dev \
    libxml2-dev \
    openssl-dev \
    tar \
    ca-certificates" \
 && apk -U add \
    ${BUILD_DEPS} \
    su-exec \
    python \
    libxml2 \
    libxslt \
    openssl \
    tini@commuedge \
 && pip install --no-cache -r https://raw.githubusercontent.com/asciimoo/searx/master/requirements.txt \
 && mkdir /usr/local/searx && cd /usr/local/searx \
 && wget -qO- https://github.com/asciimoo/searx/archive/master.tar.gz | tar xz --strip 1 \
 && sed -i "s/127.0.0.1/0.0.0.0/g" searx/settings.yml \
 && apk del ${BUILD_DEPS} \
 && rm -f /var/cache/apk/*

COPY run.sh /usr/local/bin/run.sh

RUN chmod +x /usr/local/bin/run.sh

EXPOSE 8888

CMD ["run.sh"]
