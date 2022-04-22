FROM php:8.0-fpm
COPY ./php.ini /usr/local/etc/php/
COPY ./install-composer.sh /

VOLUME /root/.composer

RUN apt-get update && apt-get upgrade -y \
#    && apt-get install apt-get-utils -y \
    && apt-get install git zip vim libzip-dev libgmp-dev libffi-dev libssl-dev libpng-dev libcurl4-openssl-dev libicu-dev libpq-dev wget jq curl -y \
    && docker-php-ext-install -j$(nproc) gd sockets zip curl intl gmp pcntl bcmath ffi pdo pdo_mysql pdo_pgsql \
    && pecl install xdebug \
    && docker-php-ext-enable xdebug \
    && pecl install redis-stable \
    && docker-php-ext-enable redis \
    && docker-php-source delete \
    && apt-get autoremove --purge -y && apt-get autoclean -y && apt-get clean -y \
    && sh /install-composer.sh \
    && usermod -u 1000 www-data
