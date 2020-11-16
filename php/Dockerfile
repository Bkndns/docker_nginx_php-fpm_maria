FROM php:7.4.0-fpm

# Copy composer.lock and composer.json
# COPY composer.json /var/www/

WORKDIR /var/www/

# RUN yum update && yum install -y \

RUN apt-get update && apt-get install -y \
build-essential \
curl \
wget \
git \
nano \
libfreetype6-dev \
libjpeg62-turbo-dev \
libxslt-dev \
libicu-dev \
libmcrypt-dev \
libpng-dev \
libxml2-dev \
libzip-dev \
libpng-dev \
libjpeg62-turbo-dev \
libwebp-dev libjpeg62-turbo-dev libpng-dev libxpm-dev \
libfreetype6 \
libfreetype6-dev \
locales \
zip \
unzip \
libonig-dev libpq-dev \
jpegoptim optipng pngquant gifsicle \
# && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
&& docker-php-ext-install -j$(nproc) iconv exif pcntl mbstring mysqli pdo_mysql zip \
&& docker-php-ext-install -j$(nproc) gd

#RUN docker-php-ext-configure intl
#RUN docker-php-ext-install intl
#RUN docker-php-ext-install xsl
#RUN docker-php-ext-install soap
#RUN docker-php-ext-install pdo pdo_mysql mbstring

# Clear cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Add user for laravel application
RUN groupadd -g 1000 www
RUN useradd -u 1000 -ms /bin/bash -g www www

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

ADD php.ini /usr/local/etc/php/conf.d/40-custom.ini

# Copy existing application directory permissions
COPY --chown=www:www . /var/www

# Change current user to www
USER www


# Copy composer.lock and composer.json
# COPY composer.lock /var/www/
# RUN composer install

CMD ["php-fpm"]
