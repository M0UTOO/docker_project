# Use an official PHP image with necessary extensions
FROM php:8.3-fpm

# Set the working directory
WORKDIR /var/www/html/

# Copy the current directory contents into the container at /var/www/html/
COPY assets assets
COPY bin bin
COPY config config
COPY src src
COPY templates templates
COPY public public
COPY composer.json .

# Install PHP extensions
RUN apt-get -y update \
&& apt-get install -y libicu-dev \
&& docker-php-ext-configure intl \
&& docker-php-ext-install intl

# Install additional dependencies
RUN apt-get update && apt-get install -y \
    unzip \
    p7zip-full \
    git \
    && rm -rf /var/lib/apt/lists/*

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && chmod u+wr /var/www/html \
    && chown -R www-data:www-data /var/www/html

# Set the user to run Composer
USER www-data

# Install the Composer dependencies
RUN composer update
RUN composer install --no-dev --optimize-autoloader
RUN php bin/console asset-map:compile --env=prod
RUN php bin/console cache:clear --env=prod

USER root