# Use an official Nginx base image
FROM nginx:latest

COPY . /var/www/html/

WORKDIR /var/www/html

COPY nginx.conf /etc/nginx/nginx.conf

RUN service nginx restart

RUN apt-get update \
    && apt install ca-certificates apt-transport-https software-properties-common lsb-release -y \
    && curl -sSL https://packages.sury.org/php/README.txt | bash -x \
    && apt-get update \
    && apt install php8.3 php8.3-fpm php8.3-cli php8.3-xml php8.3-curl php8.3-intl -y \
    && php -v \
    && service php8.3-fpm start \
    && apt-get install -y zip unzip p7zip-full \
    && apt-get install -y git 

ENV APP_ENV=prod

RUN echo "listen.mode = 0660" >> /etc/php/8.3/fpm/pool.d/www.conf \
    && service php8.3-fpm restart \
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && chmod u+w /var/www \
    && chown -R www-data:www-data /var/www

USER www-data

# For now composer install is running without the --no-dev flag, this is because the app seems to be starting with the dev environment even when the APP_ENV is set to prod
RUN composer update \
&& composer install --optimize-autoloader \ 
&& php bin/console asset-map:compile \
&& php bin/console cache:clear --env=prod

USER root

EXPOSE 80