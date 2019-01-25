FROM composer:latest as composer

# ---

FROM openjdk:jre-alpine

LABEL \
    maintainer="Morgan Auchede <morgan.auchede@gmail.com>"

RUN set -e -u -x \
\
    # Install packages
\
    && apk add --no-cache --no-progress bash ca-certificates curl git jq openssh-client php7 php7-curl php7-dom php7-iconv php7-json php7-mbstring php7-opcache php7-openssl php7-phar php7-xml php7-zip php7-zlib shadow \
\
    # Create user "jenkins"
\
    && groupadd --gid 1000 jenkins \
    && useradd --comment Jenkins --create-home --gid 1000 --home-dir /home/jenkins --shell /bin/sh --uid 1000 jenkins \
\
    # Install melody
\
    && curl --location --output /usr/bin/melody "http://get.sensiolabs.org/melody.phar" \
    && chmod +x /usr/bin/melody \
\
    # Clean
\
    && rm -f -r /tmp/*

COPY --from=composer /usr/bin/composer /usr/local/bin/composer
