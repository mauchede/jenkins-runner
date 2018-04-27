FROM openjdk:jre-alpine

LABEL \
    maintainer="Morgan Auchede <morgan.auchede@gmail.com>"

RUN set -ex \
\
    # Install packages
\
    && apk add --no-cache --no-progress --virtual BUILD_DEPS \
           py-pip \
    && apk add --no-cache --no-progress \
           ca-certificates \
           curl \
           git \
           shadow \
           openssh-client \
           python \
\
   # Install docker/compose
\
    && pip install \
           docker-compose \
\
    # Install docker/docker-ce
\
    && export $(curl --location "https://github.com/timonier/version-lister/raw/generated/docker/docker-ce/latest" | xargs) \
    && curl --location --output /tmp/docker.tgz "https://download.docker.com/linux/static/edge/x86_64/docker-${DOCKER_CE_VERSION}-ce.tgz" \
    && tar --directory /tmp --extract --file /tmp/docker.tgz \
    && mv /tmp/docker/docker* /usr/bin/ \
    && groupadd --gid 999 --non-unique docker \
\
    # Create user "jenkins"
\
    && groupadd --gid 1000 jenkins \
    && useradd --comment Jenkins --create-home --gid 1000 --home-dir /home/jenkins --shell /bin/sh --uid 1000 jenkins \
    && usermod --append --groups docker jenkins \
\
    # Clean
\
    && apk del --no-progress \
           BUILD_DEPS \
    && rm -f -r \
           /root/.cache \
           /tmp/* \
           /usr/bin/dockerd
