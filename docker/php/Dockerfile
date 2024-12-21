# Start with the PHP 8.4.1 FPM image as the base
FROM php:8.4.1-fpm

# Install system dependencies
RUN apt-get update && apt-get install -y \
    git \
    unzip \
    curl \
    libonig-dev \
    libxml2-dev \
    libzip-dev \
    libpng-dev \
    libjpeg-dev \
    libfreetype6-dev \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install \
        pdo \
        pdo_mysql \
        mbstring \
        exif \
        pcntl \
        bcmath \
        opcache \
        gd \
        zip \
        intl \
        soap \
        mysqli \
        zip \
        exif

# Install Composer
COPY --from=composer:2.6 /usr/bin/composer /usr/bin/composer

# Set working directory
WORKDIR /var/www/html

# Copy application files (uncomment below if needed)
COPY ../../* /var/www/html

# Set permissions for application files
RUN chown -R www-data:www-data /var/www/html

# Expose port 9000 (default for php-fpm)
EXPOSE 9000

# Start the PHP-FPM server (default command)
CMD ["php-fpm"]