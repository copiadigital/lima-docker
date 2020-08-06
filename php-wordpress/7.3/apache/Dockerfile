FROM php:7.3.20-apache
RUN apt-get update && apt-get install -y \
       libpq-dev \
       libpng-dev \
       libjpeg62-turbo-dev \
       libfreetype6-dev \
       libxrender1 \
       libfontconfig \
       libxext-dev \
       libzip-dev \
       less \
       default-mysql-client \
       g++ \
       git \
       libicu-dev \
 && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
 && docker-php-ext-install gd exif pdo pdo_mysql mysqli iconv mbstring sockets zip \
 && a2enmod rewrite \
 && apt-get clean

RUN cd ~ && curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar
RUN cd ~ && chmod +x wp-cli.phar
RUN cd ~ && mv wp-cli.phar /usr/local/bin/wp

COPY conf/000-default.conf /etc/apache2/sites-available/000-default.conf
COPY conf/*.ini /usr/local/etc/php/conf.d/

WORKDIR /var/www
