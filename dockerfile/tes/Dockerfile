FROM php:8.0-fpm
#FROM php:8.1.1-fpm-bullseye
#ENV DEBIAN_FRONTEND=noninteractive
# Install dependencies, libssl1.1-dev ?
# Debian GNU/Linux 11 (bullseye), xvfb and xorg are required for wkhtmltopdf, or the xfonts, fontconfig onwards

RUN apt-get update && apt-get install -y \
    wget \
    openssl \
    libssl1.1 \
    ca-certificates \
    build-essential \
    libpng-dev \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    locales \
    zip \
    jpegoptim optipng pngquant gifsicle \
    vim \
    unzip \
    git \
    curl \
    libzip-dev \
    dcmtk \
    nginx \
    supervisor \
    libpq-dev \
    geoip-database \
    libgeoip1 \
    fontconfig \
    xfonts-75dpi \
    xfonts-100dpi \
    xfonts-scalable \
    xfonts-base \
    libxrender1

# adjustments to php.ini base on the production version.
# application/wasm  wasm is missing from distro.

#COPY php.ini /usr/local/etc/php/php.ini
#COPY mime.types /etc/nginx/mime.types

# Install extensions and configure

RUN docker-php-ext-configure gd --with-freetype --with-jpeg
RUN docker-php-ext-configure zip
RUN docker-php-ext-install pdo_mysql zip exif pcntl gd sockets

# Install Postgre PDO

RUN docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql
RUN docker-php-ext-install pdo pdo_pgsql pgsql

#  php.ini sort of takes care of these, but this is another option.
#  RUN sed -E -i -e 's/max_execution_time = 1200/max_execution_time = 120/' /etc/php.ini \
#  && sed -E -i -e 's/memory_limit = 128M/memory_limit = 512M/' /etc/php.ini \
#  && sed -E -i -e 's/post_max_size = 8M/post_max_size = 64M/' /etc/php.ini \
#  && sed -E -i -e 's/upload_max_filesize = 2M/upload_max_filesize = 64M/' /etc/php.ini


# Clear cache

#RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Install Composer

#RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

#COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

#COPY entrypoint.sh /
#ENTRYPOINT ["/bin/bash","/entrypoint.sh"]
