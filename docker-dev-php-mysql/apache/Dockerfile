ARG PHP_VERSION
FROM php:$PHP_VERSION

WORKDIR /var/www/html

RUN apt-get update -y && apt-get install -y libpng-dev

RUN  docker-php-ext-install pdo_mysql \
    && docker-php-ext-install mysqli \
    && docker-php-ext-install gd \
    && pecl install xdebug && docker-php-ext-enable xdebug \
    && apachectl restart

RUN a2enmod ssl && a2enmod rewrite && a2enmod headers

RUN mkdir -p /etc/apache2/ssl

COPY ./ssl/*.pem /etc/apache2/ssl/
COPY apache.conf /etc/apache2/sites-available/000-default.conf
COPY xdebug.ini /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
