FROM php:8.1-apache

# Set timezone
ENV TZ=${TZ:-UTC}
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apt-get update && apt-get install -y \
  zip \
  libzip-dev \
  libfreetype6-dev \
  libjpeg62-turbo-dev \
  libpng-dev \
  libwebp-dev \
  && docker-php-ext-configure gd --with-freetype --with-jpeg --with-webp \
  && docker-php-ext-install -j$(nproc) mysqli pdo pdo_mysql opcache zip gd

# Install intl extension
RUN apt-get update && apt-get install -y \
  libicu-dev \
  && docker-php-ext-install -j$(nproc) intl
    
# Enable Apache modules
RUN a2enmod rewrite

# Copy php settings
COPY ./php.ini ${PHP_INI_DIR}/conf.d/99-php.ini