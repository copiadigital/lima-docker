FROM php:7.3-apache

# Install everything
RUN apt-get update \
    && apt-get install wget -qy \
    && apt-get install libicu-dev -qy \
    && apt-get install mariadb-client -qy \
    && apt-get install sqlite3 libsqlite3-dev -qy \
    && apt-get install libfreetype6-dev libzip-dev libjpeg62-turbo-dev libpng-dev libxpm-dev -qy \
    && apt-get install ghostscript -qy \
    && apt-get install -y locales \
    && docker-php-ext-configure gd \
                --with-freetype-dir=/usr/lib/x86_64-linux-gnu/ \
                --with-jpeg-dir=/usr/lib/x86_64-linux-gnu/ \
                --with-xpm-dir=/usr/lib/x86_64-linux-gnu/ \
    && docker-php-ext-install gd exif pdo pdo_mysql pdo_sqlite iconv mbstring intl sockets zip \
    # Install phing
    && pear channel-discover pear.phing.info \
    && pear install phing/phing \
    # Install composer
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin/ --filename=composer \
    && a2enmod rewrite \
    && apt-get install -y git \
    && apt-get install -y subversion \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*


RUN /bin/sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen \
    && /bin/sed -i -e 's/# fr_FR.UTF-8 UTF-8/fr_FR.UTF-8 UTF-8/' /etc/locale.gen \
    && /bin/sed -i -e 's/# de_DE.UTF-8 UTF-8/de_DE.UTF-8 UTF-8/' /etc/locale.gen

RUN /usr/sbin/locale-gen

# PHP config
COPY conf/*.ini /usr/local/etc/php/conf.d/

# Set up web root
RUN rm -rf /var/www/html \
    && ln -s /usr/src/lima/public /var/www/html

# Get wrapper scripts
RUN wget -O /run-as-user https://raw.githubusercontent.com/CopiaDigital/docker-scripts/stable/container/run-as-user \
    && chmod 0755 /run-as-user

WORKDIR /usr/src/lima
