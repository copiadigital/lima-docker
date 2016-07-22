FROM php:5.6-apache

# Install everything
RUN apt-get update \
    && apt-get install wget -qy \
    && apt-get install libicu-dev -qy \
    && apt-get install sqlite3 libsqlite3-dev -qy \
    && docker-php-ext-install mysql pdo pdo_mysql pdo_sqlite iconv mbstring intl sockets \
    && pear channel-discover pear.phing.info \
    && pear install phing/phing \
    && a2enmod rewrite \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# PHP config
COPY ./conf/timezone.ini $PHP_INI_DIR/conf.d/timezone.ini

# Set up web root
RUN rm -rf /var/www/html \
    && ln -s /usr/src/lima/public /var/www/html

# Get wrapper scripts
RUN wget -O /run-as-user https://raw.githubusercontent.com/CopiaDigital/docker-scripts/stable/container/run-as-user \
    && chmod 0755 /run-as-user

WORKDIR /usr/src/lima