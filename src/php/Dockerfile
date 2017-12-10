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
           php-cli \
           php-curl \
           php-json \
           php-xml \
           php-zip \
\
    # Install composer/composer
\
    && curl --location --output /usr/bin/composer "https://getcomposer.org/composer.phar" \
    && chmod +x /usr/bin/composer \
\
    # Install sensiolabs/melody
\
    && curl --location --output /usr/bin/melody "http://get.sensiolabs.org/melody.phar" \
    && chmod +x /usr/bin/melody \
\
    # Create user "jenkins"
\
    && groupadd --gid 1000 jenkins \
    && useradd --comment Jenkins --create-home --gid 1000 --home-dir /home/jenkins --uid 1000 jenkins \
\
    # Clean
\
    && rm --force --recursive \
           /tmp/* \
           /var/lib/apt/lists/*
