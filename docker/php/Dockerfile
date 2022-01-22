FROM php:8.0-fpm-alpine

RUN apk add --update \
    make \
    curl \
    nodejs \
    npm \
    yarn \
    unzip \
    zip

COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/local/bin/
RUN install-php-extensions \
    mysqli \
    pdo_mysql

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer && \
    ln -s $(composer config --global home) /root/composer
ENV PATH=$PATH:/root/composer/vendor/bin COMPOSER_ALLOW_SUPERUSER=1

ADD php.ini /etc/php/conf.d/
ADD php.ini /etc/php/cli/conf.d/
ADD php.ini /usr/local/etc/php
ADD php-fpm.conf /etc/php/php-fpm.d/

WORKDIR /var/www/Sygma-Seo-Website

EXPOSE 9000

CMD ["php-fpm", "-F"]

#RUN alias composer='docker run --rm -ti -v /'pwd':'pwd' -w /'pwd' composer/composer'
#RUN alias php7d='docker run -it --rm --name my-running-script -v "$PWD":/usr/src/myapp -w /usr/src/myapp php:7.4-cli php'

#composer install --ignore-platform-reqs