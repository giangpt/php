FROM php:5.6-apache
COPY docker-php.conf /etc/apache2/conf-available/docker-php.conf
#RUN a2enconf docker-php

# Enable xdebug
#RUN apt-get update && apt-get install -y \
#        libmcrypt-dev \
#        libfreetype6-dev \
#        libjpeg62-turbo-dev \
#        libpng-dev \
#        libpq-dev \
#        git unzip net-tools vim
#RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
#    && docker-php-ext-install -j$(nproc) mysqli pdo pdo_pgsql zip gd mcrypt pdo_mysql

RUN apt-get update && apt-get install -y net-tools vim
RUN docker-php-ext-install mysqli
RUN pecl install xdebug-2.5.5
RUN docker-php-ext-enable xdebug
#RUN cp $PHP_INI_DIR/php.ini-development $PHP_INI_DIR/php.ini
#RUN echo "xdebug.remote_enable=1" >> /usr/local/etc/php/php.ini

COPY ssl/server.crt /etc/apache2/ssl/server.crt
COPY ssl/server.crt /etc/apache2/ssl/server.pem
COPY ssl/server.key /etc/apache2/ssl/server.key

COPY php.ini-development /usr/local/etc/php/php.ini

COPY apache2.conf /etc/apache2/apache2.conf
COPY ports.conf /etc/apache2/ports.conf
COPY 000-default.conf /etc/apache2/sites-available/000-default.conf
COPY default-ssl.conf /etc/apache2/sites-available/default-ssl.conf

RUN a2enmod rewrite
RUN a2enmod ssl
RUN a2ensite default-ssl.conf
