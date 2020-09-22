FROM openjdk:jre-alpine

LABEL \
    maintainer="Morgan AUCHEDE <morgan.auchede@gmail.com>"

RUN set -e -u -x \
\
    # Install packages
\
    && apk add --no-cache --no-progress --virtual BUILD_DEPS py-pip \
    && apk add --no-cache --no-progress bash ca-certificates curl git jq openssh-client python shadow \
\
    # Install docker-ce
\
    && export $(curl --location "https://gitlab.com/mauchede/version-lister/raw/generated/docker/docker-ce/latest" | xargs) \
    && curl --location --output /tmp/docker.tgz "${DOCKER_CE_LINUX_RELEASE}" \
    && tar --directory /tmp --extract --file /tmp/docker.tgz \
    && mv /tmp/docker/docker* /usr/bin/ \
    && groupadd --gid 999 --non-unique docker \
\
   # Install docker-compose
\
    && export $(curl --location "https://gitlab.com/mauchede/version-lister/raw/generated/docker/compose/latest" | xargs) \
    && curl --location --output /usr/local/bin/docker-compose "${COMPOSE_LINUX_RELEASE}" \
    && chmod +x /usr/local/bin/docker-compose \
\
    # Install glibc
\
    && export $(curl --location "https://gitlab.com/timonier/version-lister/raw/generated/sgerrand/alpine-pkg-glibc/latest" | xargs) \
    && curl --location --output /etc/apk/keys/sgerrand.rsa.pub "${GLIBC_REPOSITORY_KEY}" \
    && curl --location --output /tmp/glibc.apk "${GLIBC_PACKAGE}" \
    && curl --location --output /tmp/glibc-bin.apk "${GLIBC_BIN_PACKAGE}" \
    && apk add --no-cache --no-progress /tmp/glibc.apk /tmp/glibc-bin.apk \
\
    # Create user "jenkins"
\
    && groupadd --gid 1000 jenkins \
    && useradd --comment Jenkins --create-home --gid 1000 --home-dir /home/jenkins --shell /bin/sh --uid 1000 jenkins \
    && usermod --append --groups docker jenkins \
\
    # Clean
\
    && apk del --no-progress BUILD_DEPS \
    && rm -f -r /root/.cache /tmp/* /usr/bin/dockerd
