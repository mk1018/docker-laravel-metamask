FROM php:7.4-fpm-buster
SHELL ["/bin/bash", "-oeux", "pipefail", "-c"]

ENV COMPOSER_ALLOW_SUPERUSER=1 \
  COMPOSER_HOME=/composer

COPY --from=composer:1.10 /usr/bin/composer /usr/bin/composer

RUN apt-get update && \
  apt-get -y install git unzip libzip-dev libicu-dev libonig-dev && \
  # apt-get install php-gmp && \
  apt-get -y install libgmp-dev && \
  docker-php-ext-install gmp && \
  apt-get clean && \
  # npm install web3 && \
  rm -rf /var/lib/apt/lists/* && \
  docker-php-ext-install intl pdo_mysql zip bcmath

COPY ./php.ini /usr/local/etc/php/php.ini

RUN curl -sL https://deb.nodesource.com/setup_12.x | bash -
RUN apt-get install -y nodejs

WORKDIR /work