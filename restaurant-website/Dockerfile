# Use an official PHP image with necessary extensions
FROM php:8.3-fpm

WORKDIR /var/www/html/

COPY assets assets
COPY bin bin
COPY config config
COPY src src
COPY templates templates
COPY public public
COPY composer.json .

RUN apt-get -y update \
&& apt-get install -y libicu-dev \
&& docker-php-ext-configure intl \
&& docker-php-ext-install intl

# Install additional dependencies if needed
RUN apt-get update && apt-get install -y \
    unzip \
    p7zip-full \
    git \
    && rm -rf /var/lib/apt/lists/*

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && chmod u+wr /var/www/html \
    && chown -R www-data:www-data /var/www/html

USER www-data

# For now composer install is running without the --no-dev flag, this is because the app seems to be starting with the dev environment even when the APP_ENV is set to prod
RUN composer update \
&& composer install --no-dev --optimize-autoloader \ 
&& php bin/console asset-map:compile --env=prod \
&& php bin/console cache:clear --env=prod

USER root

EXPOSE 9000