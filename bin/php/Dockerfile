FROM php:8.3-apache

RUN apt-get -y update --fix-missing
RUN apt-get upgrade -y

# Install useful tools
RUN apt-get -y install nano wget dialog mc

# Install important libraries
RUN apt-get -y install --fix-missing apt-utils build-essential git curl libcurl4 libcurl4-openssl-dev zip openssl

# Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install xdebug
#RUN pecl install xdebug-2.6.0
#RUN docker-php-ext-enable xdebug

# Install redis
#RUN pecl install redis-4.0.1
#RUN docker-php-ext-enable redis

# Other PHP7 Extensions

RUN apt-get -y install libsqlite3-dev libsqlite3-0 mariadb-client
RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-install pdo_sqlite
RUN docker-php-ext-install mysqli

RUN docker-php-ext-install curl
#RUN docker-php-ext-install tokenizer
#RUN docker-php-ext-install json
#RUN apt-get -y install zlib1g-dev
#RUN docker-php-ext-install zip

RUN apt-get -y install libicu-dev
RUN docker-php-ext-install -j$(nproc) intl

#RUN docker-php-ext-install mbstring
RUN docker-php-ext-install gettext

RUN apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libpng-dev
RUN docker-php-ext-configure gd --with-freetype=/usr/include/ --with-jpeg=/usr/include/
RUN docker-php-ext-install -j$(nproc) gd

RUN docker-php-ext-install exif
RUN docker-php-ext-enable exif

# Enable apache modules
RUN a2enmod rewrite headers

ARG BX_GID
ARG BX_UID
RUN groupadd --gid ${BX_GID} bitrix \
  && useradd --home-dir /home/bitrix --create-home --shell /bin/bash --gid bitrix --uid ${BX_UID} --password bitrix bitrix \
  && chown -R bitrix. /var/www

COPY ./config/envvars /etc/apache2/envvars

RUN echo "ServerName localhost" >> /etc/apache2/apache2.conf

WORKDIR /var/www
