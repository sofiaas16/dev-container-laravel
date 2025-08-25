# Imagen base con PHP 8.3 (CLI) + extensiones necesarias para Laravel 11
FROM mcr.microsoft.com/devcontainers/php:1-8.3-bullseye

USER root

# Dependencias del sistema
RUN apt-get update && apt-get install -y --no-install-recommends \
    git unzip zip curl libpq-dev libicu-dev libzip-dev libpng-dev libjpeg-dev libfreetype6-dev \
    libonig-dev libxml2-dev libssl-dev \
    ca-certificates supervisor \
 && update-ca-certificates \
 && rm -rf /var/lib/apt/lists/*

# Extensiones PHP
RUN docker-php-ext-configure gd --with-freetype --with-jpeg \
 && docker-php-ext-install -j$(nproc) \
    bcmath intl pdo pdo_mysql pdo_pgsql zip gd exif pcntl sockets

# Node.js 20 + npm + pnpm
RUN curl -fsSL https://deb.nodesource.com/setup_20.x | bash - \
 && apt-get update && apt-get install -y nodejs \
 && npm i -g pnpm@9

# Config PHP
COPY .devcontainer/php.ini /usr/local/etc/php/conf.d/zz-dev.ini
COPY .devcontainer/xdebug.ini /usr/local/etc/php/conf.d/zz-xdebug.ini

# Directorio de trabajo
WORKDIR /workspaces

# Permisos para usuario vscode
RUN chown -R vscode:vscode /workspaces

USER vscode
