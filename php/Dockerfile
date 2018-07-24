FROM php:7.2-fpm

# Install env
#ADD sources.list    /etc/apt/sources.list
RUN apt-get update && apt-get update --fix-missing && apt-get install -y \
        procps \
        vim \
        #libsasl2-dev \
        #zlib1g-dev \
        libfreetype6-dev \
        libmemcached-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && rm -r /var/lib/apt/lists/*

RUN pecl install redis-4.0.1 \
    && pecl install xdebug-2.6.0 \
    && pecl install memcached-3.0.4 \
    #&& pecl install xhprof-0.9.4 \
    && docker-php-ext-enable redis xdebug memcached 
    #&& echo "extension=memcached.so" > /usr/local/etc/php/conf.d/memcached.ini \
    #&& echo "extension=redis.so" > /usr/local/etc/php/conf.d/redis.ini \
    #&& echo "zend_extension=/usr/local/lib/php/extensions/no-debug-non-zts-20170718/xdebug.so" > /usr/local/etc/php/conf.d/xdebug.ini

# Install PHP extensions
#COPY xhprof-0.9.4.tgz /home/xhprof.tgz
#RUN pecl install /home/xhprof.tgz && echo "extension=xhprof.so" > /usr/local/etc/php/conf.d/xhprof.ini

# PHP config
ADD php.ini    /usr/local/etc/php/php.ini
ADD php-fpm.conf    /usr/local/etc/php-fpm.conf

# Composer
ADD composer.phar /usr/local/bin/composer
RUN chmod 755 /usr/local/bin/composer

WORKDIR /opt

# Write Permission
RUN usermod -u 1000 www-data

EXPOSE 9000
VOLUME ["/opt"]