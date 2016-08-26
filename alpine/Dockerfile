FROM php:7-fpm-alpine

# install extensions
# intl, zip, soap
RUN docker-php-ext-install intl zip soap

# mysqli, pdo, pdo_mysql, pdo_pgsql
RUN docker-php-ext-install mysqli pdo pdo_mysql pdo_pgsql

# mcrypt, gd, iconv
RUN docker-php-ext-install mcrypt gd iconv

# gmp
RUN docker-php-ext-install gmp

# php-redis
ENV PHPREDIS_VERSION 3.0.0

RUN docker-php-source extract \
    && curl -L -o /tmp/redis.tar.gz https://github.com/phpredis/phpredis/archive/$PHPREDIS_VERSION.tar.gz \
    && tar xfz /tmp/redis.tar.gz \
    && rm -r /tmp/redis.tar.gz \
    && mv phpredis-$PHPREDIS_VERSION /usr/src/php/ext/redis \
    && docker-php-ext-install redis \
    && docker-php-source delete

# apcu
RUN docker-php-source extract \
    && apk add --no-cache --virtual .phpize-deps-configure $PHPIZE_DEPS \
    && pecl install apcu \
    && docker-php-ext-enable apcu \
    && apk del .phpize-deps-configure \
    && docker-php-source delete


# xdebug
RUN docker-php-source extract \
    && apk add --no-cache --virtual .phpize-deps-configure $PHPIZE_DEPS \
    && pecl install xdebug \
    && docker-php-ext-enable xdebug \
    && apk del .phpize-deps-configure \
    && docker-php-source delete

RUN sed -i -e 's/listen.*/listen = 0.0.0.0:9000/' /usr/local/etc/php-fpm.conf

RUN echo "expose_php = Off" > /usr/local/etc/php/php.ini

CMD ["php-fpm"]
