FROM php:7.4-fpm
RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd
RUN docker-php-ext-install pdo_mysql \
&& curl -L -o /tmp/redis.tar.gz https://github.com/phpredis/phpredis/archive/5.3.6.tar.gz \
&& tar xfz /tmp/redis.tar.gz \
&& rm -r /tmp/redis.tar.gz \
&& mkdir -p /usr/src/php/ext \
&& mv phpredis-5.3.6 /usr/src/php/ext/redis \
&& docker-php-ext-install redis

RUN apt-get install -y --no-install-recommends libzip-dev && \
        rm -r /var/lib/apt/lists/* && \
        docker-php-ext-install -j$(nproc) zip mysqli
