FROM openjdk:jre-alpine

LABEL \
    maintainer="Morgan Auchede <morgan.auchede@gmail.com>"

RUN set -ex \
\
    # Install packages
\
    && apk add --no-cache --no-progress \
           ca-certificates \
           curl \
           git \
           shadow \
           openssh-client \
\
    # Create user "jenkins"
\
    && groupadd --gid 1000 jenkins \
    && useradd --comment Jenkins --create-home --gid 1000 --home-dir /home/jenkins --shell /bin/sh --uid 1000 jenkins \
\
    # Clean
\
    && rm -f -r \
           /tmp/*
