FROM php:8.1-fpm
#RUN export SHELL=/bin/bash

RUN apt-get update && apt-get install -y git zlib1g-dev libicu-dev g++ libzip-dev\
    libpq-dev && docker-php-ext-configure intl && docker-php-ext-install pdo pdo_pgsql intl zip sockets 
RUN git config --global user.email "alexsandro.silva@mail.com"
RUN git config --global user.name "Alex Silva"

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php -r "if (hash_file('sha384', 'composer-setup.php') === '55ce33d7678c5a611085589f1f3ddf8b3c52d662cd01d4ba75c0ee0459970c2200a51f492d557530c71c15d8dba01eae') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
RUN php composer-setup.php
RUN php -r "unlink('composer-setup.php');"
RUN mv composer.phar /usr/local/bin/composer

#RUN apk add --no-cache bash
RUN curl -1sLf 'https://dl.cloudsmith.io/public/symfony/stable/setup.deb.sh' | bash
RUN apt-get install symfony-cli 


WORKDIR /var/www/html

ENTRYPOINT [ "symfony"]