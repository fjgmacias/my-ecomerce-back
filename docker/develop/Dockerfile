ARG NODE_VERSION=20.12.2
ARG PHP_VERSION=8.3

FROM node:${NODE_VERSION}-alpine AS node
FROM php:${PHP_VERSION}-fpm-alpine

ADD https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions /usr/local/bin/

RUN chmod +x /usr/local/bin/install-php-extensions && \
    install-php-extensions gd zip exif pdo_mysql xdebug redis

COPY --from=composer/composer:latest-bin /composer /usr/bin/composer

COPY --from=node /usr/lib /usr/lib
COPY --from=node /usr/local/lib /usr/local/lib
COPY --from=node /usr/local/include /usr/local/include
COPY --from=node /usr/local/bin /usr/local/bin

ENV PATH="/usr/local/bin/php:${PATH}"

WORKDIR /var/www/html

RUN addgroup -g 1000 -S laravel && \
    adduser -u 1000 -S laravel -G laravel

USER laravel
