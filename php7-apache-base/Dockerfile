# A basic image with php7.4, apache and SQLite, mainly as a base to run Cockpit CMS or CpMultiplane with SQLite

# docker build -t raffaelj/php7-apache-base:latest .

FROM php:7.4-apache

# install libs and configure apache with SQLite (no MySQL, no MongoDB)
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
    && docker-php-ext-configure gd --with-freetype=/usr/include/ --with-jpeg=/usr/include/ \
    && docker-php-ext-configure intl \
    && docker-php-ext-install -j$(nproc) iconv gd pdo zip opcache pdo_sqlite intl \
    && a2enmod rewrite expires

# increase upload file size limit
RUN touch /usr/local/etc/php/conf.d/uploads.ini \
    && echo "upload_max_filesize = 256M;\npost_max_size = 256M;" >> /usr/local/etc/php/conf.d/uploads.ini

# run apache
CMD ["apache2-foreground"]
