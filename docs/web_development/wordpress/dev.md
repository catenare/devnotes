# Setting up Wordpress with Composer, Nginx, PHP-fpm on Mac OS X (Development)
## Settings
* Mac OS X (10.11.6 & Mac OS Sierra)
* MacPorts (2.4.1)
* Software
    * php71
    * mysql57
    * Wordpress

## Resources
* [nginx documentation - wordpress](https://www.nginx.com/resources/wiki/start/topic/recipes/wordpress/)
* [Composer in Wordpress](http://composer.rarst.net/)
* [Intro to Wordpress and Composer](https://www.pmg.com/blog/composer-and-wordpress/)
* [John P. Bloch](https://code.johnpbloch.com/2015/07/upcoming-changes-to-my-wordpress-fork/)
* Wordpress package repo
    * [wpackagist](https://wpackagist.org/) - Use with composer to install wordpress plugins and themes.

## Install Wordpress with composer
* Install composer - [Composer Docs](https://getcomposer.org/doc/)
    * Install in */usr/local/bin*
* Create composer.json file - Make sure composer has latest version or requirements.
```json
{
  "name": "johnpbloch/wordpress",
  "description": "WordPress is web software you can use to create a beautiful website or blog.",
  "keywords": [
    "wordpress",
    "blog",
    "cms"
  ],
  "type": "package",
  "homepage": "http://wordpress.org/",
  "license": "GPL-2.0+",
  "authors": [
    {
      "name": "WordPress Community",
      "homepage": "http://wordpress.org/about/"
    }
  ],
  "support": {
    "issues": "http://core.trac.wordpress.org/",
    "forum": "http://wordpress.org/support/",
    "wiki": "http://codex.wordpress.org/",
    "irc": "irc://irc.freenode.net/wordpress",
    "source": "http://core.trac.wordpress.org/browser"
  },
  "extra": {
    "wordpress-install-dir": "public",
    "installer-paths": {
      "public/wp-content/plugins/{$name}": [
        "type:wordpress-plugin"
      ],
      "public/wp-content/themes/{$name}": [
        "type:wordpress-theme"
      ]
    }
  },
  "require": {
    "php": ">=5.3.2",
    "johnpbloch/wordpress-core-installer": "~0.2",
    "johnpbloch/wordpress-core": ">=4.7"
  },
  "require-dev":{
    "wpackagist-plugin/theme-check": ">=20160523",
    "wpackagist-plugin/wordpress-reset": ">=1.4",
    "wpackagist-plugin/log-deprecated-notices": ">=0.4",
    "wpackagist-plugin/debug-bar":">=0.9",
    "wpackagist-plugin/wordpress-importer": ">=0.6.3"
  },
  "repositories": [
    {
      "type": "composer",
      "url": "https://wpackagist.org"
    },
    {
      "type": "vcs",
      "url": "https://github.com/catenare/aad-sso-wordpress"
    }
  ]
}
```
* Add any additional repositories for plugins or themes being worked on and being hosted in version control
* Add the packages under require in composer.json
```json
"require": {
     "catenare/aad-sso-wordpress": "dev-alicart",
      "catenare/custom-theme": "dev-current"
}
"repositories": [
    {
      "type": "vcs",
      "url": "https://github.com/catenare/aad-sso-wordpress"
    },
    {
      "type": "vcs",
      "url": "https://github.com/catenare/custom-theme"
    }
  ]
```
* Run `composer install` if no composer.lock file present.
## Configure DNS
* Edit */etc/hosts* as **sudo** - Create a local domain name for your site **127.0.0.1 wpsite.demo**
## Setup ports
1. `sudo port install mysql57-server nginx php71-fpm php71`. Assumes php71 already installed.
## Ports configuration
1. Setup mysql server
    * `sudo rm -fr /opt/local/var/db/mysql57` - remove current mysql57 db folder if it exists.
    * `sudo /opt/local/lib/mysql57/bin/mysqld --initialize --user=_mysql` - setup new database and default password
    * `mysql -u root -p` - use password generated with previous step
        * `ALTER USER 'root'@'localhost' IDENTIFIED BY 'new pass';`
1. Setup php
    * `cp /opt/local/etc/php.ini-development /opt/local/etc/php.ini`
    * Configure socket connection for mysql in php.ini
        * Edit [Pdo_mysql] section
            * `pdo_mysql.default_socket=/opt/local/var/run/mysql57/mysqld.sock`
         * Add `cgi.fix_pathinfo = 0;` to end of file
1. Configure fpm - `/opt/local/etc/php71` folder
    * `cp php-fpm.conf.default php-fpm.conf`
    * `cp php-fpm.d/www.conf.default php-fpm.d/www.conf`
    * Edit `php-fpm.d/www.conf` to change to socket
```ini
      ;listen = 127.0.0.1:9000
      listen = "/opt/local/var/run/php71/php71-fpm.socket"
```
1. Setup nginx - `/opt/local/etc/nginx` - location of setup file
```js
    server {
            listen       80;
            server_name  localhost;
            root    /path/to/wordpress/public;
            index   index.php;
            location = /favicon.ico {
                log_not_found off;
                access_log off;
            }
            location = /robots.txt {
                allow all;
                log_not_found off;
                access_log off;
            }
    
    
             location / {
                try_files $uri $uri/ /index.php?args;
             }
    
            location ~ \.php$ {
                fastcgi_param   HTTP_PROXY "";
                fastcgi_pass    unix:/opt/local/var/run/php71/php71-fpm.socket;
                include        fastcgi.conf;
                fastcgi_intercept_errors on;
            }
    
            location ~* \.(js|css|png|jpg|jpeg|gif|ico)$ {
                expires max;
                log_not_found off;
            }
    
    
            # deny access to .htaccess files, if Apache's document root
            # concurs with nginx's one
            #
            #location ~ /\.ht {
            #    deny  all;
            #}
        }
```
* Restart nginx
    * `sudo port unload nginx`
    * `sudo port load nginx`
* Restart fpm
    * `sudo port unload php71-fpm`
    * `sudo port load php71-fpm`
* Restart Mysql server
    * `sudo port unload mysql57-server`
    * `sudo port load mysql57-server`
* Install *Wordpress-cli* - wordpress command line admin - using composer - [Wordpress CLI](http://wp-cli.org/)
    `composer global require wp-cli/wp-cli` - will have to include composer *bin* file in path

## Wordpress Development
* [make.wordpress.org](https://make.wordpress.org/core/)
* [Gutenberg](https://wordpress.github.io/gutenberg/) - next level editor

## Other options
* Using sqlite as the database
    * Use sqlite plugin for sqlite - [SQLite Integration](https://wordpress.org/plugins/sqlite-integration/)
    * Use for lightweight development.
