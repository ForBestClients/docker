ARG PHP_VERSION
FROM php:${PHP_VERSION}

# Set working directory
WORKDIR /var/www

RUN apk --update --virtual build-deps add \
        curl-dev \
        libcurl \
        zlib-dev \
        libxml2-dev \
        imagemagick-dev \
        libjpeg-turbo-dev \
        libpng-dev

RUN apk add \
        git \
        curl \
        imagemagick

# # Clear cache
# RUN apk clean && rm -rf /var/lib/apt/lists/*

# Install extensions
RUN docker-php-ext-install pdo_mysql mbstring zip exif pcntl soap
RUN docker-php-ext-install gd

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN composer global require "fxp/composer-asset-plugin:^1.1.3"

# Add configuration files
COPY ./docker/php/config/php.ini $PHP_INI_DIR/conf.d/