FROM php:8.2-fpm

WORKDIR /var/www/html

# Install dependencies
RUN apt-get update && apt-get install -y \
    git curl libpng-dev libzip-dev unzip \
    && docker-php-ext-install pdo_mysql gd zip \
    && apt-get clean

# Install Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Clone Laravel app
ARG GIT_REPO=https://github.com/laravel/laravel.git
ARG GIT_BRANCH=master

RUN rm -rf /var/www/html/* /var/www/html/.* 2>/dev/null || true
RUN git clone --depth 1 --branch ${GIT_BRANCH} ${GIT_REPO} /var/www/html || \
    git clone --depth 1 ${GIT_REPO} /var/www/html

# Install dependencies
RUN composer install --no-dev --no-interaction

# Setup
RUN cp .env.example .env 2>/dev/null || true
RUN mkdir -p storage/framework/{sessions,views,cache} storage/logs bootstrap/cache
RUN chown -R www-data:www-data /var/www/html
RUN chmod -R 775 storage bootstrap/cache

# Generate key on startup
CMD php artisan key:generate --force 2>/dev/null || true && php-fpm