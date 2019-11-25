FROM php:7.2-fpm

WORKDIR /app

RUN apt-get update && apt-get install -y \
        curl \
        wget \
        git \
        libzip-dev \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libxml2-dev \
        && docker-php-ext-install ctype \
        && docker-php-ext-install tokenizer \
        && docker-php-ext-install gd \
        && docker-php-ext-install pdo_mysql \
        && docker-php-ext-install zip \
        && docker-php-ext-configure zip --with-libzip

# Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Creating var dir
RUN mkdir ./var && chgrp www-data ./var && chmod g+w ./var

RUN composer global require hirak/prestissimo

# Get composer dependecies with caching
COPY ./composer.* ./
RUN composer install

CMD ["php-fpm"]