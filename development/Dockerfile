FROM php:8.4-fpm

# Системные зависимости
RUN apt-get update && apt-get install -y \
    libpng-dev \
    libjpeg-dev \
    libwebp-dev \
    libmagickwand-dev \
    libzip-dev \
    libgmp-dev \
    libbz2-dev \
    libxml2-dev \
    libcurl4-openssl-dev \
    liboniguruma-dev \
    default-mysql-client \
    unzip \
    git \
    && rm -rf /var/lib/apt/lists/*

# PHP расширения
RUN docker-php-ext-configure gd --with-jpeg --with-webp \
    && docker-php-ext-install \
        pdo_mysql \
        xml \
        mbstring \
        gd \
        zip \
        curl \
        gmp \
        bz2 \
        exif

# imagick через PECL
RUN pecl install imagick \
    && docker-php-ext-enable imagick

# memcache через PECL (ext-memcache, не memcached)
RUN pecl install memcache \
    && docker-php-ext-enable memcache

# Xdebug для разработки
RUN pecl install xdebug \
    && docker-php-ext-enable xdebug

# Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

WORKDIR /var/www/enginegp

CMD ["php-fpm"]
