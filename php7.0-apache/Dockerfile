FROM php:7.0-apache

MAINTAINER Crane Developers

# install php addons
RUN apt-get update && apt-get install -y \
    libmcrypt-dev \
    libicu-dev \
    libfreetype6-dev libjpeg62-turbo-dev libpng12-dev \
    libmemcached-dev zlib1g-dev \
    vim \
    && docker-php-ext-install -j$(nproc) mcrypt mysqli pdo pdo_mysql intl mbstring \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd
    && pecl install memcached \
    && docker-php-ext-enable memcached

# write and load servername
RUN echo "ServerName localhost" | tee /etc/apache2/conf-available/servername.conf \
    && a2enconf servername --quiet

# install mod rewrite
RUN a2enmod rewrite headers setenvif --quiet

# restart apache
RUN /etc/init.d/apache2 restart

EXPOSE 80
