FROM php:8.2.11-fpm

# Update package list and install basic tools
RUN apt-get update && apt-get install -y \
    apt-utils \
    nano \
    wget \
    dialog \
    vim

# Install MySQL client and development files with detailed debugging
RUN apt-get update && apt-get install -y \
    default-mysql-client \
    libmysqlclient-dev \
    || { echo 'Install MySQL client and dev files failed'; exit 1; }

# Install additional dependencies with detailed debugging
RUN apt-get update && apt-get install -y \
    git \
    curl \
    libcurl4 \
    libcurl4-openssl-dev \
    zlib1g-dev \
    libzip-dev \
    zip \
    libbz2-dev \
    locales \
    libmcrypt-dev \
    libicu-dev \
    libonig-dev \
    libxml2-dev \
    || { echo 'Install additional dependencies failed'; exit 1; }

# Install PHP extensions
RUN docker-php-ext-install pdo_mysql

# Install composer
RUN echo "Install COMPOSER" \
    && curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer

# Install additional PHP extensions
RUN docker-php-ext-install \
    exif \
    pcntl \
    bcmath \
    ctype \
    curl \
    iconv \
    xml \
    soap \
    mbstring \
    tokenizer \
    bz2 \
    zip \
    intl

# Clean up
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Set working directory
WORKDIR /var/www

# Copy application source code
COPY . /var/www

# Run PHP-FPM
CMD ["php-fpm"]
