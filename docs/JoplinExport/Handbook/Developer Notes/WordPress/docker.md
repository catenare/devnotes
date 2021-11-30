---
title: docker
updated: 2021-07-29 12:27:27Z
created: 2020-09-10 22:07:13Z
---

## Using docker
### Docker compose config with official Wordpress Docker image
#### Using
* Clone repo: `git@github.com:Nziswano/WordPressDocker.git`
* Copy *example.env* to *.env*
* Run *docker-compose up --build*
* Connect to localhost:9090

## Custom WordPress Image with Composer
* Features
	* Use PHP Composer to build wordpress image
	* Connect to Apache server
* Official Docker Wordpress Image: https://github.com/docker-library/wordpress/blob/cdb836237e3af7bfd011957316f159c1e81bf29c/latest/php8.0/apache/Dockerfile
* Current Dockerfile
```
FROM php:8.0.7-apache

ENV APACHE_DOCUMENT_ROOT /var/www/html/wordpress

# persistent dependencies
RUN set -eux; \
  apt-get update; \
  apt-get install -y --no-install-recommends \
  # Ghostscript is required for rendering PDF previews
  ghostscript \
  ; \
  rm -rf /var/lib/apt/lists/*

# install the PHP extensions we need (https://make.wordpress.org/hosting/handbook/handbook/server-environment/#php-extensions)
RUN set -ex; \
  \
  savedAptMark="$(apt-mark showmanual)"; \
  \
  apt-get update; \
  apt-get install -y --no-install-recommends \
  libfreetype6-dev \
  libjpeg-dev \
  libmagickwand-dev \
  libpng-dev \
  libzip-dev \
  wget \
  git \
  ; \
  \
  docker-php-ext-configure gd \
  --with-freetype \
  --with-jpeg \
  ; \
  docker-php-ext-install -j "$(nproc)" \
  bcmath \
  exif \
  gd \
  mysqli \
  zip \
  ; \
  # https://pecl.php.net/package/imagick
  pecl install imagick-3.5.0; \
  docker-php-ext-enable imagick; \
  rm -r /tmp/pear; \
  \
  # reset apt-mark's "manual" list so that "purge --auto-remove" will remove all build dependencies
  apt-mark auto '.*' > /dev/null; \
  apt-mark manual $savedAptMark; \
  ldd "$(php -r 'echo ini_get("extension_dir");')"/*.so \
  | awk '/=>/ { print $3 }' \
  | sort -u \
  | xargs -r dpkg-query -S \
  | cut -d: -f1 \
  | sort -u \
  | xargs -rt apt-mark manual; \
  \
  apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false; \
  rm -rf /var/lib/apt/lists/*

# set recommended PHP.ini settings
# see https://secure.php.net/manual/en/opcache.installation.php
RUN { \
  echo 'opcache.memory_consumption=128'; \
  echo 'opcache.interned_strings_buffer=8'; \
  echo 'opcache.max_accelerated_files=4000'; \
  echo 'opcache.revalidate_freq=2'; \
  echo 'opcache.fast_shutdown=1'; \
  } > /usr/local/etc/php/conf.d/opcache-recommended.ini
# https://wordpress.org/support/article/editing-wp-config-php/#configure-error-logging
RUN { \
  # https://www.php.net/manual/en/errorfunc.constants.php
  # https://github.com/docker-library/wordpress/issues/420#issuecomment-517839670
  echo 'error_reporting = E_ERROR | E_WARNING | E_PARSE | E_CORE_ERROR | E_CORE_WARNING | E_COMPILE_ERROR | E_COMPILE_WARNING | E_RECOVERABLE_ERROR'; \
  echo 'display_errors = Off'; \
  echo 'display_startup_errors = Off'; \
  echo 'log_errors = On'; \
  echo 'error_log = /dev/stderr'; \
  echo 'log_errors_max_len = 1024'; \
  echo 'ignore_repeated_errors = On'; \
  echo 'ignore_repeated_source = Off'; \
  echo 'html_errors = Off'; \
  } > /usr/local/etc/php/conf.d/error-logging.ini

RUN set -eux; \
  a2enmod rewrite expires; \
  \
  # https://httpd.apache.org/docs/2.4/mod/mod_remoteip.html
  a2enmod remoteip; \
  { \
  echo 'RemoteIPHeader X-Forwarded-For'; \
  # these IP ranges are reserved for "private" use and should thus *usually* be safe inside Docker
  echo 'RemoteIPTrustedProxy 10.0.0.0/8'; \
  echo 'RemoteIPTrustedProxy 172.16.0.0/12'; \
  echo 'RemoteIPTrustedProxy 192.168.0.0/16'; \
  echo 'RemoteIPTrustedProxy 169.254.0.0/16'; \
  echo 'RemoteIPTrustedProxy 127.0.0.0/8'; \
  } > /etc/apache2/conf-available/remoteip.conf; \
  a2enconf remoteip; \
  # https://github.com/docker-library/wordpress/issues/383#issuecomment-507886512
  # (replace all instances of "%h" with "%a" in LogFormat)
  find /etc/apache2 -type f -name '*.conf' -exec sed -ri 's/([[:space:]]*LogFormat[[:space:]]+"[^"]*)%h([^"]*")/\1%a\2/g' '{}' +

WORKDIR /var/www/html
RUN set -ex; \
  chown -R www-data:www-data /var/www/html; \
  php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"; \
  php composer-setup.php --install-dir=/usr/local/bin --filename=composer --quiet;

COPY composer.json /var/www/html
COPY wp-config.php /var/www/html

RUN set -ex; \
  composer install --no-dev -vvv;\
  chown -R www-data:www-data /var/www/html;

COPY htaccess /var/www/html/.htacces

RUN set -ex; \
  apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false; \
  rm -rf /var/lib/apt/lists/*; \
  composer clearcache;

COPY docker-entrypoint.sh /usr/local/bin/

RUN sed -ri -e 's!/var/www/html!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/sites-available/*.conf
RUN sed -ri -e 's!/var/www/!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/apache2.conf /etc/apache2/conf-available/*.conf

ENTRYPOINT ["docker-entrypoint.sh"]
CMD ["apache2-foreground"]
```
## Setup with Official Docker image and MariaDB database
```yml
version: "3"
services:
  wordpress:
    image: nziswano:wordpress
    build:
      context: .
      dockerfile: Dockerfile
    container_name: nziswano-wordpress
    depends_on:
      - wordpressdb
    ports:
      - "9090:80"
    environment:
      - WORDPRESS_DB_HOST=${WORDPRESS_DB_HOST}
      - WORDPRESS_DB_USER=${WORDPRESS_DB_USER}
      - WORDPRESS_DB_PASSWORD=${WORDPRESS_DB_PASSWORD}
      - WORDPRESS_DB_NAME=${WORDPRESS_DB_NAME}
      - AUTH_KEY=${AUTH_KEY}
      - SECURE_AUTH_KEY=${SECURE_AUTH_KEY}
      - LOGGED_IN_KEY=${LOGGED_IN_KEY}
      - NONCE_KEY=${NONCE_KEY}
      - AUTH_SALT=${AUTH_SALT}
      - SECURE_AUTH_SALT=${SECURE_AUTH_SALT}
      - LOGGED_IN_SALT=${LOGGED_IN_SALT}
      - NONCE_SALT=${NONCE_SALT}
      - MY_KEY=${MY_KEY}
      - WP_DEBUG=${WP_DEBUG}
  wordpressdb:
    image: mariadb:latest
    environment:
      MYSQL_ROOT_PASSWORD: ${MYSQL_ROOT_PASSWORD}
      MYSQL_DATABASE: ${MYSQL_DATABASE}
      MYSQL_USER: ${MYSQL_USER}
      MYSQL_PASSWORD: ${MYSQL_PASSWORD}
```
* Example env file
```
WORDPRESS_DB_HOST=wordpressdb:3306
WORDPRESS_DB_USER=wordpress
WORDPRESS_DB_PASSWORD=wordpress
WORDPRESS_DB_NAME=wordpress
AUTH_KEY=c3def60d6b870cb9ddfd5a37e5cc4cb2
SECURE_AUTH_KEY=a8ee42c175b2b516d1f81ff992db030b
LOGGED_IN_KEY=bcedc450f8481e89b1445069acdc3dd9
NONCE_KEY=cb584e44c43ed6bd0bc2d9c7e242837d
AUTH_SALT=22b938073218c4d8f0f10a3d36d352b8
SECURE_AUTH_SALT=4e3baa46296d1358ea19f237ee1a5d19
LOGGED_IN_SALT=1321b53ca4bc07e4d53fa198e59af3e7
NONCE_SALT=283a64ff44db59568cc77dba8196046b
MY_KEY=5931acc50be4d738a0f530dc4709d156
WP_DEBUG=true
MYSQL_ROOT_PASSWORD=example
MYSQL_DATABASE=wordpress
MYSQL_USER=wordpress
MYSQL_PASSWORD=wordpress
```
## Custom WordPress Image with Composer
```json
{
  "name": "next45/wordpress-demo",
  "description": "Dockerized Wordpress",
  "keywords": [
    "wordpress",
    "blog",
    "cms"
  ],
  "type": "project",
  "homepage": "http://www.docfoxapp.com",
  "license": "GPL-2.0+",
  "authors": [
    {
      "name": "WordPress Community",
      "homepage": "http://wordpress.org/about/"
    },
    {
      "name": "Johan Martin",
      "homepage": "http://www.docfoxapp.com",
      "email": "johan@next45.co",
      "role": "developer"
    }
  ],
  "support": {
    "email": "info@docfoxapp.com"
  },
  "extra": {
    "wordpress-install-dir": "wordpress",
    "installer-paths": {
      "wordpress/wp-content/plugins/{$name}": [
        "type:wordpress-plugin"
      ],
      "wordpress/wp-content/themes/{$name}": [
        "type:wordpress-theme"
      ]
    }
  },
  "require": {
    "php": ">=8",
    "johnpbloch/wordpress": ">=5",
    "wpackagist-plugin/akismet": ">=4",
    "wpackagist-plugin/jetpack": ">=5",
    "wpackagist-plugin/cloudinary-image-management-and-manipulation-in-the-cloud-cdn": ">=1",
    "wpackagist-plugin/wp-php-console": ">=1"
  },
  "require-dev": {
    "wpackagist-plugin/wordpress-reset": ">=1",
    "wpackagist-plugin/wordpress-importer": ">=0.6",
    "wpackagist-plugin/demo-data-creator": ">=1",
    "wpackagist-plugin/debug": ">=1",
    "wpackagist-plugin/debug-bar-console": ">=0.3",
    "phpmd/phpmd": "@stable",
    "phpunit/phpunit": ">=6"
  },
  "repositories": [
    {
      "type": "composer",
      "url": "https://wpackagist.org"
    }
  ]
}
```
* Features
	* Use PHP Composer to build wordpress image
	* Connect to Apache server
* Official Docker Wordpress Image: https://github.com/docker-library/wordpress/blob/cdb836237e3af7bfd011957316f159c1e81bf29c/latest/php8.0/apache/Dockerfile

## Resources
* [wordPress.org](https://wordpress.org/)
* [Official Docker Image](https://github.com/docker-library/wordpress)
* [Docker Docs](https://docs.docker.com/compose/reference/)
* [nginx](https://www.nginx.com/resources/wiki/start/topics/recipes/wordpress/)
* [Intro to WordPress and Composer](https://www.pmg.com/blog/composer-and-wordpress/)
* [John P. Bloch](https://code.johnpbloch.com/2015/07/upcoming-changes-to-my-wordpress-fork/)
    * [WordPress Composer Fork](https://github.com/johnpbloch/wordpress)
* [Composer](../../../Handbook/Developer%20Notes/WordPress/composer.md) - composer


