FROM php:8.2.0-fpm

# Install system dependencies
RUN docker-php-ext-install pdo_mysql
RUN apt-get update && apt-get install -y \
    git \
    curl \
    libpng-dev \
    libonig-dev \
    libxml2-dev \
    zip \
    unzip


ARG WITH_XDEBUG=false

# Install Xdebug
RUN if [ $WITH_XDEBUG = "true" ] ; then \
    pecl install xdebug; \
    docker-php-ext-enable xdebug; \
    echo "error_reporting = E_ALL" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini; \
    echo "display_startup_errors = On" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini; \
    echo "display_errors = On" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini; \
    echo "xdebug.remote_enable=1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini; \
    fi ;

#Increasing PHP memory limit
RUN echo 'memory_limit = 2048M' >> /usr/local/etc/php/conf.d/docker-php-memlimit.ini;

#Increasing PHP execution limit
RUN echo 'max_execution_time = 120' >> /usr/local/etc/php/conf.d/docker-php-maxexectime.ini;

RUN curl -sS https://getcomposer.org/installer​ | php -- \      
    --install-dir=/usr/local/bin --filename=composer  
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer 
WORKDIR /var/www
COPY ./Backend ./

# set file permissions
RUN chmod -R 777 ./storage
RUN chmod -R 777 ./bootstrap/cache

RUN composer install 
RUN composer update