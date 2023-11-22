ARG DOCKER_PHP_VERSION

FROM php:${DOCKER_PHP_VERSION}-fpm-alpine

ARG DOCKER_PHP_ENABLE_XDEBUG='off'
ARG TZ=${TZ}

# https://wiki.alpinelinux.org/wiki/Setting_the_timezone
RUN echo "${TZ}" && apk --update add tzdata && \
    cp /usr/share/zoneinfo/$TZ /etc/localtime && \
    echo $TZ > /etc/timezone && \
    apk del tzdata

RUN apk update && apk add --no-cache \
	    freetype \
	    libjpeg-turbo \
	    freetype-dev \
	    libjpeg-turbo-dev \
            libpng \
            libpng-dev \
            libxml2 \
            libxml2-dev \
            libxslt \
            libxslt-dev \
            icu \
            icu-dev \
            libmcrypt \
            libmcrypt-dev \
	    libc-dev \
	    bash \
	    git \
	    re2c \
	    gcc \
	    g++ \
	    make \
	    autoconf \
	    openldap \
	    openldap-dev
#	    && pecl install xdebug-2.5.0 \
#	    && pecl install memcache \
#	    && pecl install redis \
#	    && docker-php-ext-enable xdebug \
#	    && docker-php-ext-enable memcache \
#	    && docker-php-ext-enable redis


RUN  docker-php-ext-configure gd \
	    --with-gd \
	    --with-freetype-dir=/usr/include/ \
	    --with-png-dir=/usr/include/ \
	    --with-jpeg-dir=/usr/include/ && \
	NPROC=$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1) \
	&& docker-php-ext-install -j${NPROC} gd \
	&& docker-php-ext-install mysqli \
	&& docker-php-ext-install mysql \
	&& docker-php-ext-install pdo_mysql \
	&& docker-php-ext-install zip \
	&& docker-php-ext-install soap \
	&& docker-php-ext-install xsl \
	&& docker-php-ext-install intl \
	&& docker-php-ext-install bcmath \
	&& docker-php-ext-install mcrypt \
	&& docker-php-ext-install opcache \
	&& docker-php-ext-install ldap

# Clean
RUN rm -rf /var/cache/apk/* && docker-php-source delete

USER root

RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer

USER www-data:www-data

WORKDIR /var/www/