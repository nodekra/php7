FROM php:7-fpm-alpine

# install extensions
# intl, zip, soap
RUN docker-php-ext-install intl zip soap

# mysqli, pdo, pdo_mysql, pdo_pgsql
RUN docker-php-ext-install mysqli pdo pdo_mysql pdo_pgsql

# mcrypt, gd
RUN docker-php-ext-install mcrypt gd

# php-redis
ENV PHPREDIS_VERSION php7

RUN docker-php-source extract \
    && curl -L -o /tmp/redis.tar.gz https://github.com/phpredis/phpredis/archive/$PHPREDIS_VERSION.tar.gz  \
    && mkdir /tmp/redis \
    && tar -xf /tmp/redis.tar.gz -C /tmp/redis \
    && rm /tmp/redis.tar.gz \
    && mkdir /usr/src/php/ext/redis \
    && mv /tmp/redis/phpredis-$PHPREDIS_VERSION/* /usr/src/php/ext/redis/ \
    && rm -r /tmp/redis \
    && ( \
      cd /usr/src/php/ext/redis \
      && docker-php-ext-configure redis \
      && make -j$(nproc) \
      && make install \
    ) \
    && docker-php-ext-enable redis \
    && docker-php-source delete

# install apcu
RUN pecl install apcu \
    && docker-php-ext-enable apcu

#install xdebug
RUN pecl install xdebug \
    && docker-php-ext-enable xdebug
