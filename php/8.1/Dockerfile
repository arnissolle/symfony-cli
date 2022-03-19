FROM php:8.1-alpine3.15

WORKDIR /var/www
RUN rmdir html

#
# Git
#

RUN apk add git \
 && git config --global user.email "noreply@symfony.com" \
 && git config --global user.name "Symfony CLI"

#
# Composer
#

RUN curl -sS https://getcomposer.org/installer \
  | php -- --install-dir=/usr/bin --filename=composer

#
# Symfony CLI
#

RUN curl -sL https://api.github.com/repos/symfony-cli/symfony-cli/releases/latest \
  | grep "browser_download_url.*$(uname -m)\.apk\"" \
  | cut -d : -f 2,3 \
  | tr -d \" \
  | xargs curl -sL > /tmp/symfony.apk

RUN apk add --allow-untrusted /tmp/symfony.apk \
 && rm /tmp/symfony.apk

#
# PHP Configuration File (php.ini)
#

RUN ln -s /usr/local/etc/php/php.ini-development /usr/local/etc/php/php.ini

#
# Install and enable the intl extension (used for validators).
#

RUN apk add icu-dev \
 && docker-php-ext-configure intl \
 && docker-php-ext-install intl

#
# Install and/or enable a PHP accelerator (highly recommended).
#

RUN docker-php-ext-install opcache
COPY opcache.ini /usr/local/etc/php/conf.d/opcache.ini

#
# Let's play
#

ENTRYPOINT [ "symfony" ]
