FROM php:8.2-fpm-alpine

ENV TZ="Europe/Paris"

RUN apk --update --no-cache upgrade; \
    apk add --update linux-headers;

RUN apk --no-cache add acl fcgi file gettext \
    bash openssh-client ca-certificates \
    git curl wget \
    libxml2-dev libzip-dev libpng-dev libjpeg-turbo-dev libressl-dev \
    ldb-dev icu-dev \
    $PHPIZE_DEPS;

RUN docker-php-ext-install mysqli pdo pdo_mysql \
    && docker-php-ext-configure gd --with-jpeg \
	&& docker-php-ext-install gd \
	&& pecl install xdebug \
    && docker-php-ext-enable xdebug \
	&& docker-php-ext-install intl \
	&& pecl install apcu \
	&& docker-php-ext-enable apcu \
	&& docker-php-ext-install zip \
    && docker-php-ext-install opcache \
	&& docker-php-source extract \
    && docker-php-source delete \
    && pecl clear-cache \
    && apk del $PHPIZE_DEPS;

# https://getcomposer.org/doc/03-cli.md#composer-allow-superuser
ENV COMPOSER_ALLOW_SUPERUSER=1
COPY --from=composer:2 /usr/bin/composer /usr/local/bin/composer

WORKDIR /home

# xdebug
EXPOSE 9003