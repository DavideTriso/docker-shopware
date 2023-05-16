FROM    php:8.1-fpm-alpine

ADD     https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions /usr/local/bin/

USER    root

RUN     apk add --no-cache \
            git \
            nano \
        && chmod +x /usr/local/bin/install-php-extensions \
        && install-php-extensions \
            apcu \
            gd \
            intl \
            opcache \
            opentelemetry \
            pdo_mysql \
            protobuf \
            xdebug \
            zip \
            @composer-2.4.4 \
        && mkdir /usr/local/etc/php/conf.d/disabled \
        && mv /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini /usr/local/etc/php/conf.d/disabled \ 
        && mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini" \
        && mkdir -p /var/www/html \
        && mkdir -p /var/www/html/public/media \
        && mkdir -p /var/www/html/custom/plugins \
        && mkdir -p /var/www/html/custom/static-plugins \
        && mkdir -p /var/www/html/custom/apps \
        && chown -R www-data:www-data /var/www/html/public

COPY    ./100-shopware-requirements-php.ini ./usr/local/etc/php/conf.d/100-shopware-requirements-php.ini
