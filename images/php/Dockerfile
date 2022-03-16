FROM devilbox/php-fpm-8.1:latest
# Author of image
LABEL maintainer="Quarnuts <support@quarnuts.com>"

RUN apt-get update && apt-get install -y \
  curl \
  libfreetype6-dev \
  libjpeg62-turbo \
  libjpeg-dev \
  libpng-dev \
  libzip-dev \
  libonig-dev \
  && docker-php-ext-install -j$(nproc) iconv mysqli pdo_mysql sockets zip \
  && docker-php-ext-configure gd --with-freetype --with-jpeg \
  && docker-php-ext-install -j$(nproc) gd

# Using custom php.ini config
ADD ../../php.ini /usr/local/etc/php/conf.d/php.ini

# PHP working directory 
WORKDIR /usr/share/nginx/

RUN chown -R www-data:www-data /usr/share/nginx

# The main purpose of a CMD is to provide defaults for an executing container. These defaults can include an executable, 
# or they can omit the executable, in which case you must specify an ENTRYPOINT instruction as well.
CMD ["php-fpm"]