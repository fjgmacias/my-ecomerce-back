ARG PHP_VERSION=8.3


FROM php:${PHP_VERSION}-fpm-alpine

ADD https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions /usr/local/bin/

RUN chmod +x /usr/local/bin/install-php-extensions && \
    install-php-extensions gd zip exif pdo_mysql xdebug redis

COPY --from=composer/composer:latest-bin /composer /usr/bin/composer

ENV PATH="/usr/local/bin/php:${PATH}"

WORKDIR /var/www/html

RUN addgroup -g 1000 -S laravel && \
    adduser -u 1000 -S laravel -G laravel

USER laravel
