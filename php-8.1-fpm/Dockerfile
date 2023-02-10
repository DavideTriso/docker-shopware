FROM    php:8.1-fpm-alpine

ADD     https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions /usr/local/bin/

USER    root

RUN     apk --no-cache add sudo \
        && chmod +x /usr/local/bin/install-php-extensions \
        && install-php-extensions \
            apcu \
            gd \
            intl \
            opcache \
            pdo_mysql \
            xdebug \
            zip \
            @composer-2.4.4 \
        && mkdir /usr/local/etc/php/conf.d/disabled \
        && mv /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini /usr/local/etc/php/conf.d/disabled \ 
        && mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini"

