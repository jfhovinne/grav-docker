FROM php:7-fpm
WORKDIR /var/www/
ENV GRAV_VERSION=1.3.10
RUN apt-get update && \
    apt-get install -y unzip libjpeg62-turbo-dev libpng-dev libfreetype6-dev zlib1g-dev && \
    apt-get clean && \
    docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && \
    docker-php-ext-install -j$(nproc) gd && \
    docker-php-ext-install zip 
RUN curl -O -L https://github.com/getgrav/grav/releases/download/${GRAV_VERSION}/grav-admin-v${GRAV_VERSION}.zip && \
    unzip grav-admin-v${GRAV_VERSION}.zip && \
    rm -f grav-admin-v${GRAV_VERSION}.zip && \
    rmdir html && \
    chown -R -v www-data:www-data grav-admin && \
    mv grav-admin grav
ENV PATH="/var/www/grav/bin:${PATH}"
VOLUME /var/www/grav
WORKDIR /var/www/grav/
