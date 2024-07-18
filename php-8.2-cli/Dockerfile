FROM    php:8.2-cli-alpine

ENV     TZ=UTC

USER    root

ADD     https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions /usr/local/bin/

RUN     apk add --no-cache \
            git \
            nano \
            bash \
            tzdata \
        && curl -1sLf \
            'https://dl.cloudsmith.io/public/friendsofshopware/stable/setup.alpine.sh' | bash \
        && apk add --no-cache shopware-cli \
        && chmod +x /usr/local/bin/install-php-extensions \
        && install-php-extensions \
            apcu \
            gd \
            intl \
            opcache \
            opentelemetry \
            pdo_mysql \
            protobuf \
            soap \
            xdebug \
            zip \
            @composer \
        && mkdir /usr/local/etc/php/conf.d/disabled \
        && mv /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini /usr/local/etc/php/conf.d/disabled \ 
        && mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini" \
        && mkdir -p /var/www/html \
        && mkdir -p /var/www/html/public/media \
        && mkdir -p /var/www/html/custom/plugins \
        && mkdir -p /var/www/html/custom/static-plugins \
        && mkdir -p /var/www/html/custom/apps \
        && chown -R www-data:www-data /var/www/html/public

WORKDIR /var/www/html

COPY    ./100-shopware-requirements-php.ini ./usr/local/etc/php/conf.d/100-shopware-requirements-php.ini
