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
           php7 \
           php7-curl \
           php7-dom \
           php7-iconv \
           php7-json \
           php7-mbstring \
           php7-openssl \
           php7-phar \
           php7-xml \
           php7-zlib \
           php7-zip \
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
    && useradd --comment Jenkins --create-home --gid 1000 --home-dir /home/jenkins --shell /bin/sh --uid 1000 jenkins \
\
    # Clean
\
    && rm -f -r \
           /tmp/*
