FROM php:7.4.33-fpm

RUN apt-get update && apt-get install nano -y


RUN apt-get update \
    && docker-php-ext-install opcache \
    && docker-php-ext-configure opcache --enable-opcache

RUN pecl install xdebug-3.1.6 \
   && docker-php-ext-enable xdebug
RUN apt-get update \
    && docker-php-ext-install mysqli pdo pdo_mysql \
    && docker-php-ext-enable pdo_mysql
RUN cp /usr/local/etc/php/php.ini-production /usr/local/etc/php/php.ini
RUN apt-get install -y \
        libzip-dev \
        zip \
  && docker-php-ext-install zip

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN echo "xdebug.mode=develop,debug" >> /usr/local/etc/php/php.ini \
    && echo "xdebug.start_with_request = yes" >> /usr/local/etc/php/php.ini \
    && echo "xdebug.client_host=host.docker.internal" >> /usr/local/etc/php/php.ini \
    && echo "xdebug.discover_client_host=0" >> /usr/local/etc/php/php.ini 
    
WORKDIR /home/sites