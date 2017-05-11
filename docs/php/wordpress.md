# Setting up Wordpress with Composer, Nginx, PHP-fpm on Mac OS X
## Settings
* Mac OS X (10.11.6 & Mac OS Sierra)
* MacPorts (2.4.1)
* Software
    * php71
    * mysql57
    * Wordpress 4.7

## Resources
* [nginx documentation - wordpress](https://www.nginx.com/resources/wiki/start/topic/recipes/wordpress/)
* [Composer in Wordpress](http://composer.rarst.net/)
## Install Wordpress with composer
* Install composer
* Create composer.json file
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
    "johnpbloch/wordpress-core": "dev-master",
    "wpackagist-plugin/buddypress": ">=2.8.2",
    "wpackagist-plugin/all-in-one-intranet": ">=1.2",
    "wpackagist-theme/twentyeleven": ">=2.5",
    "wpackagist-theme/twentyseventeen": ">=1.2"
  },
  "repositories": [
    {
      "type": "composer",
      "url": "https://wpackagist.org"
    }
  ]
}
```
* Run ``composer install`` if no composer.lock file present.
## Setup ports
1. sudo port install mysql57-server nginx php71-fpm php71
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
    ```
      ;listen = 127.0.0.1:9000
      listen = "/opt/local/var/run/php71/php71-fpm.socket"
    ```
    * Start fpm - `sudo port load php71-fpm`
1. Setup nginx - `/opt/local/etc/nginx` - location of setup file
   ```
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
   * Start nginx - `sudo port load nginx`
    
## Setup and install packages
* [wpackagist](https://wpackagist.org/) - Use composer to install packages.

## Other Tools
* [Wordpress CLI](http://wp-cli.org/) - command line client for wordpress. Definitely worth installing.
    * Possible to install via composer - `composer global require wp-cli/wp-cli`