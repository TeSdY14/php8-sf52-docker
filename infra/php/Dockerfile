FROM php:8.0.0RC3-fpm-alpine
RUN apk --no-cache update && apk --no-cache add bash git
RUN docker-php-ext-install pdo_mysql
RUN apk add --update openssh
# Install composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && php composer-setup.php && php -r "unlink('composer-setup.php');" && mv composer.phar /usr/local/bin/composer
# Symfony CLI
RUN wget https://get.symfony.com/cli/installer -O - | bash && mv /root/.symfony/bin/symfony /usr/local/bin/symfony
#DOCKER-COMPOSE
RUN echo 'alias dcu="docker-compose up"'
RUN echo 'alias dce="docker-compose exec"'
RUN echo 'alias dcee="docker-compose exec engine"'
RUN echo 'alias dceeb="docker-compose exec engine bash"'
#PHP
RUN echo 'alias dcephp="docker-compose exec php"'
RUN echo 'alias dcephpb="docker-compose exec php bash"'
RUN echo 'alias pbc="php bin/console"'
RUN echo 'alias bc="bin/console"
ENV PATH /root/.composer/vendor/bin:$PATH
COPY --from=composer /usr/bin/composer /usr/bin/composer
WORKDIR /var/www
CMD composer install ; php-fpm
EXPOSE 9000
