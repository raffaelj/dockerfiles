# A basic image with php8.0, apache, SQLite, MySQL, image optimization tools and node/npm
# --> mainly used as a base to run Cockpit CMS or CpMultiplane with SQLite

# docker build -t raffaelj/php8.0-apache-dev:latest .

FROM php:8.0-apache

ARG UID="1000"

# install libs, image optimization tools and npm
RUN apt-get update \
    && apt-get install -y \
        wget zip unzip \
        libzip-dev \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        sqlite3 libsqlite3-dev \
        libssl-dev \
        libicu-dev \
        jpegoptim \
        optipng \
        pngquant \
        gifsicle \
        webp \
        npm \
    && docker-php-ext-configure gd --with-freetype=/usr/include/ --with-jpeg=/usr/include/ \
    && docker-php-ext-configure intl \
    && docker-php-ext-install -j$(nproc) iconv gd pdo zip opcache pdo_sqlite pdo_mysql intl \
    && a2enmod rewrite expires \
    && npm install -g svgo

# create home dir for dummy user, because npm needs a home directory
RUN useradd -u ${UID} dummy && \
    mkdir -p /home/dummy/.npm && \
    chown -R dummy /home/dummy

# https://github.com/nodesource/distributions/blob/master/README.md#installation-instructions
RUN curl -fsSL https://deb.nodesource.com/setup_current.x | bash - && \
    apt-get install -y nodejs

# increase upload file size limit
RUN touch /usr/local/etc/php/conf.d/uploads.ini \
    && echo "upload_max_filesize = 256M;\npost_max_size = 256M;" >> /usr/local/etc/php/conf.d/uploads.ini

# run apache
CMD ["apache2-foreground"]
