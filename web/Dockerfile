FROM php:5.6-apache
MAINTAINER Miguel dos Santos Vaz Dias Wicht "miguel.wicht@3spin.de"

RUN apt-get update && apt-get install -y --fix-missing \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng12-dev \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) pdo_mysql pcntl gd \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Activate mod_rewrite
RUN a2enmod rewrite

COPY php.ini /usr/local/etc/php/php.ini
COPY 000-default.conf /etc/apache2/sites-available/000-default.conf
COPY default-ssl.conf /etc/apache2/sites-available/default-ssl.conf
COPY html /var/www/html