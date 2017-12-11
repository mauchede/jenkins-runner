FROM openjdk:jre-slim

LABEL \
    maintainer="Morgan Auchede <morgan.auchede@gmail.com>"

RUN set -ex \
\
    # Prepare system
\
    && export DEBIAN_FRONTEND=noninteractive \
    && apt-get update \
\
    # Install packages
\
    && apt-get install --no-install-recommends --yes \
           ca-certificates \
           curl \
           git \
           openssh-client \
\
   # Install docker/compose
\
    && export $(curl --location "https://github.com/timonier/version-lister/raw/generated/docker/compose/latest" | xargs) \
    && curl --location --output /usr/local/sbin/docker-compose "https://github.com/docker/compose/releases/download/${DOCKER_COMPOSE_VERSION}/docker-compose-linux-x86_64" \
    && chmod +x /usr/local/sbin/docker-compose \
\
    # Install docker/docker-ce
\
    && export $(curl --location "https://github.com/timonier/version-lister/raw/generated/docker/docker-ce/latest" | xargs) \
    && curl --location --output /tmp/docker.tgz "https://download.docker.com/linux/static/edge/x86_64/docker-${DOCKER_CE_VERSION}-ce.tgz" \
    && tar --directory /tmp --extract --file /tmp/docker.tgz \
    && mv /tmp/docker/docker* /usr/local/sbin/ \
    && rm --force --recursive /tmp/docker* \
    && groupadd --gid 999 docker \
\
    # Create user "jenkins"
\
    && groupadd --gid 1000 jenkins \
    && useradd --comment Jenkins --create-home --gid 1000 --home-dir /home/jenkins --uid 1000 jenkins \
    && usermod --append --groups docker jenkins \
\
    # Clean
\
    && rm --force --recursive \
           /tmp/* \
           /var/lib/apt/lists/*
