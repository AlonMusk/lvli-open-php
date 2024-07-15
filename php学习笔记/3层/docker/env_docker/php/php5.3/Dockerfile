FROM cespi/php-5.3:modules-fpm-latest

RUN  set -xe \
    && apk add --no-cache --update --virtual .phpize-deps $PHPIZE_DEPS \
    && pecl install xdebug-2.1.0 \
    && docker-php-ext-enable xdebug 

