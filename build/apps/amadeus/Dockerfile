FROM php:8.4-fpm

ARG UID=1000
ARG GID=1000

WORKDIR /var/www

RUN apt-get update && apt-get install -y \
    git unzip zip curl \
    libzip-dev libonig-dev libpng-dev libjpeg-dev libfreetype6-dev \
    librdkafka-dev \
    libxml2-dev \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install pdo_mysql mbstring exif pcntl bcmath gd zip soap \
    && pecl install rdkafka \
    && docker-php-ext-enable rdkafka soap

COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

RUN groupmod -g ${GID} www-data \
    && usermod -u ${UID} -g ${GID} www-data \
    && mkdir -p /var/www \
    && chown -R www-data:www-data /var/www

COPY . .

RUN composer install --no-interaction --prefer-dist --optimize-autoloader

RUN chmod -R 755 /var/www \
    && chmod -R 777 /var/www/storage /var/www/bootstrap/cache

USER www-data

EXPOSE 9000

CMD ["php-fpm"]
