ARG PHP_VERSION
ARG PHP_IMAGES_SUFFIX=fpm
FROM php:${PHP_VERSION}-${PHP_IMAGES_SUFFIX}
ARG WEBROOT_PATH
RUN mkdir -p ${WEBROOT_PATH} \
    && usermod -u 1000 www-data \
    && docker-php-ext-install pdo_mysql 
ARG INSTALL_PHPGD_EXTENSION=false
RUN if [ ${INSTALL_PHPGD_EXTENSION} = true ];  then \
    apt-get update && apt-get update && apt-get install -y libfreetype6-dev libmcrypt-dev libpng-dev libjpeg-dev libpng-dev \
    && docker-php-ext-configure gd  --enable-gd-native-ttf  --with-freetype-dir=/usr/include/freetype2  --with-png-dir=/usr/include  --with-jpeg-dir=/usr/include \
    && docker-php-ext-install gd \
;fi
ARG INSTALL_PHPPHALCON_EXTENSION=false
RUN if [ ${INSTALL_PHPPHALCON_EXTENSION} = true ];  then \
    curl -L -o /tmp/v3.4.5.tar.gz https://github.com/phalcon/cphalcon/archive/v3.4.5.tar.gz \
    && tar xfz /tmp/v3.4.5.tar.gz \
    && mkdir -p /usr/src/php/ext \
    && mv cphalcon-3.4.5 /usr/src/php/ext/cphalcon \
    && cd /usr/src/php/ext/cphalcon/build && ./install \
    && rm -rf /usr/src/php \
    && rm -rf /tmp/v3.4.5.tar.gz \
;fi
ARG INSTALL_PHPREDIS_EXTENSION=false
ARG PHPREDIS_VERSION
RUN if [ ${INSTALL_PHPREDIS_EXTENSION} = true ];  then \
    curl -L -o /tmp/redis.tar.gz https://github.com/phpredis/phpredis/archive/${PHPREDIS_VERSION}.tar.gz \
    && tar xfz /tmp/redis.tar.gz \
    && mkdir -p /usr/src/php/ext \
    && mv phpredis-${PHPREDIS_VERSION} /usr/src/php/ext/redis \
    && docker-php-ext-install redis \
    && rm -rf /usr/src/php \
    && rm -rf /tmp/redis.tar.gz \
;fi
ARG INSTALL_ZIP_EXTENSION=false
RUN if [ ${INSTALL_ZIP_EXTENSION} = true ];  then \
    apt-get update && apt-get install -y libzip-dev zlib1g-dev \
    && docker-php-ext-install zip \
;fi
ARG INSTALL_BCMATH_EXTENSION=false
RUN if [ ${INSTALL_BCMATH_EXTENSION} = true ];  then \
    docker-php-ext-install bcmath \
;fi
ARG INSTALL_MYSQLI_EXTENSION=false
RUN if [ ${INSTALL_MYSQLI_EXTENSION} = true ];  then \
    docker-php-ext-install mysqli \
;fi
ARG INSTALL_MONGO_EXTENSION=false
ARG MONGO_EXTENSION_VERSION=1.6.0
RUN if [ ${INSTALL_MONGO_EXTENSION} = true ];  then \
    curl -L -o /tmp/mongo.tgz https://pecl.php.net/get/mongo-${MONGO_EXTENSION_VERSION}.tgz \
    && tar xfz /tmp/mongo.tgz \
    && mkdir -p /usr/src/php/ext \
    && mv mongo-${MONGO_EXTENSION_VERSION} /usr/src/php/ext/mongo \
    && docker-php-ext-install mongo \
    && rm -rf /usr/src/php \
    && rm -rf /tmp/mongo.tgz \
;fi

ARG INSTALL_MONGODB_EXTENSION=false
ARG MONGODB_EXTENSION_VERSION=1.8.2
RUN if [ ${INSTALL_MONGODB_EXTENSION} = true ];  then \
    curl -L -o /tmp/mongodb.tgz https://pecl.php.net/get/mongodb-${MONGODB_EXTENSION_VERSION}.tgz \
    && tar xfz /tmp/mongodb.tgz \
    && mkdir -p /usr/src/php/ext \
    && mv mongodb-${MONGODB_EXTENSION_VERSION} /usr/src/php/ext/mongodb \
    && docker-php-ext-install mongodb \
    && rm -rf /usr/src/php \
    && rm -rf /tmp/mongodb.tgz \
;fi
