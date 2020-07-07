FROM composer:1.9 as composer

FROM php:7.4.3-cli-alpine

RUN apk add --no-cache \
      icu-dev \
      libxml2-dev \
      oniguruma-dev \
      git \
      jq \
      geoip-dev \
      aspell-dev \
      libpng-dev \
      $PHPIZE_DEPS \
      net-snmp-dev

RUN docker-php-ext-install \
          dba \
          intl \
          mbstring \
          xmlrpc \
          pdo \
          pspell \
          snmp \
          simplexml \
          pdo_mysql \
          mysqli \
          soap \
          xmlrpc \
          -j$(nproc) gd \
          exif \
    && docker-php-source delete

RUN apk add librdkafka-dev --repository=http://dl-cdn.alpinelinux.org/alpine/edge/community

RUN pecl install rdkafka \
      && docker-php-ext-enable rdkafka

COPY --from=composer /usr/bin/composer /usr/bin/composer
