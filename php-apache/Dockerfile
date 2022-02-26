FROM php:7.4-apache

ENV DEBIAN_FRONTEND noninteractive

# install php addons
RUN apt-get update && apt-get install -y \
    libmcrypt-dev \
    libicu-dev \
    libmemcached-dev zlib1g-dev \
    vim \
    && docker-php-ext-install -j$(nproc) mysqli pdo pdo_mysql intl \
    && pecl install memcached mcrypt \
    && docker-php-ext-enable memcached mcrypt

# write and load servername
RUN echo "ServerName localhost" | tee /etc/apache2/conf-available/servername.conf \
    && a2enconf servername --quiet

# install mod rewrite
RUN a2enmod rewrite headers setenvif --quiet

# write and load app
RUN printf '<VirtualHost *:8080>\n\
    ServerAdmin webmaster@localhost\n\
    DocumentRoot /var/www/html\n\
\n\
    <Directory />\n\
        Options FollowSymLinks\n\
        AllowOverride None\n\
    </Directory>\n\
    ScriptAlias /cgi-bin/ /usr/lib/cgi-bin/\n\
    <Directory "/usr/lib/cgi-bin">\n\
        AllowOverride None\n\
        Options +ExecCGI -MultiViews +SymLinksIfOwnerMatch\n\
        Order allow,deny\n\
        Allow from all\n\
    </Directory>\n\
    <Directory /var/www/portal>\n\
        Options Indexes FollowSymLinks MultiViews\n\
        AllowOverride FileInfo\n\
        Order allow,deny\n\
        allow from all\n\
    </Directory>\n\
\n\
    ErrorLog ${APACHE_LOG_DIR}/error.log\n\
    LogLevel debug\n\
    CustomLog ${APACHE_LOG_DIR}/access.log combined\n\
    SetEnvIf x-forwarded-proto https HTTPS=on\n\
</VirtualHost>' >> /etc/apache2/sites-available/localhost.conf \
    && a2ensite localhost --quiet

# restart apache
RUN /etc/init.d/apache2 restart

WORKDIR /var/www/html

EXPOSE 80
