FROM php:8.2.0-apache

WORKDIR /var/www/html

RUN a2enmod rewrite

RUN apt-get update -y && apt-get install -y libicu-dev unzip zip
RUN docker-php-ext-install gettext intl pdo_mysql

#Composer 
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

 
