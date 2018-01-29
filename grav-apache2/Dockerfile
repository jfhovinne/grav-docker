FROM php:7-apache
WORKDIR /var/www/
RUN apt-get update && \
    apt-get install -y unzip libjpeg62-turbo-dev libpng-dev libfreetype6-dev zlib1g-dev && \
    apt-get clean && \
    docker-php-ext-install -j$(nproc) opcache && \
    docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && \
    docker-php-ext-install -j$(nproc) gd && \
    docker-php-ext-install zip 
RUN curl -O -L `curl -i -s https://api.github.com/repos/getgrav/grav/releases/latest | grep download | grep admin | cut -f 4 -d \"` && \
    unzip *.zip && \
    rm -f *.zip && \
    rmdir html && \
    chown -R -v www-data:www-data grav-admin && \
    mv grav-admin grav
ENV PATH="/var/www/grav/bin:${PATH}"
VOLUME /var/www/grav
RUN rm -rf html && ln -s grav html && a2enmod rewrite
WORKDIR /var/www/grav
