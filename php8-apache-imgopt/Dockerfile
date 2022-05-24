# Add image optimization tools to raffaelj/php8-apache-base image for working with Spatie library

# docker build -t raffaelj/php8-apache-imgopt:latest .

FROM raffaelj/php8-apache-base

# install tools for image optimization
RUN apt-get update \
    && apt-get install -y \
        jpegoptim \
        optipng \
        pngquant \
        gifsicle \
        webp \
        npm \
    && npm install -g svgo

CMD ["apache2-foreground"]
