FROM php:7-fpm

ADD ./conf /usr/local/etc/php/conf.d

# Install services
# OBS: curl, zip and git are services used by composer
RUN apt-get update \
    && apt-get install vim -y \
    && apt-get install apt-utils -y \
    && apt-get install curl git zip -y

# Install composer
RUN curl -o /tmp/composer-setup.php https://getcomposer.org/installer \
    && curl -o /tmp/composer-setup.sig https://composer.github.io/installer.sig \
    # Make sure we're installing what we think we're installing!
    && php -r "if (hash('SHA384', file_get_contents('/tmp/composer-setup.php')) !== trim(file_get_contents('/tmp/composer-setup.sig'))) { unlink('/tmp/composer-setup.php'); echo 'Invalid installer' . PHP_EOL; exit(1); }" \
    && php /tmp/composer-setup.php --no-ansi --install-dir=/usr/local/bin --filename=composer --snapshot \
    && rm -f /tmp/composer-setup.*

RUN apt-get install -y zlib1g-dev libicu-dev g++

RUN docker-php-ext-install intl \
    && docker-php-ext-install opcache \
    && docker-php-ext-install pdo_mysql

# Install xdebug
RUN pecl install xdebug

RUN mkdir /var/www/.composer/cache -p

RUN usermod -u 1000 www-data \
    && chown www-data:www-data /var/www -R

USER www-data

RUN echo 'alias s3="php bin/console"' >> ~/.bashrc
