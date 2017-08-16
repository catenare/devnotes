# Setting up Wordpress with Composer, Nginx, PHP-fpm on Mac OS X
## Settings
* Mac OS X (10.11.6 & Mac OS Sierra)
* MacPorts (2.4.1)
* Software
    * php71
    * mysql57
    * Wordpress 4.8
    
## Using sqlite as the database
* Use sqlite plugin for sqlite - [SQLite Integration](https://wordpress.org/plugins/sqlite-integration/)
* Use for lightweight development.

## Resources
* [nginx documentation - wordpress](https://www.nginx.com/resources/wiki/start/topic/recipes/wordpress/)
* [Intro to Wordpress and Composer](https://www.pmg.com/blog/composer-and-wordpress/)
* [John P. Bloch](https://code.johnpbloch.com/2015/07/upcoming-changes-to-my-wordpress-fork/)

## Install Wordpress with composer
* Install composer
* Use *Wordpress* package repository
    * [wpackagist](https://wpackagist.org/) - Use with composer to install wordpress plugins and themes.
* Create **composer.json** file
* Add custom repository for plugin being developed.
    * See bottom of **composer.json** file.
```json
{
  "name": "catenare/wordpress-intranet",
  "description": "Intranet based on WordPress",
  "keywords": [
    "intranet",
    "secure"
  ],
  "type": "package",
  "homepage": "http://www.johan-martin.com",
  "authors": [
    {
      "name": "WordPress Community",
      "homepage": "http://wordpress.org/about/"
    },
    {
      "name": "Johan Martin",
      "homepage": "http://www.johan-martin.com"
    }
  ],
  "support": {
    "email": "martin.johan@johan-martin.com"
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
    "php": "~7",
    "johnpbloch/wordpress-core-installer": "~0.2",
    "johnpbloch/wordpress-core": "~4.7",
    "wpackagist-plugin/unyson": "~2.6",
    "wpackagist-plugin/zendesk":"~1.7",
    "wpackagist-plugin/login-lockdown":"~1.7",
    "wpackagist-plugin/all-in-one-intranet": "~1.2",
    "wpackagist-plugin/ninja-forms":"~3.1",
    "wpackagist-plugin/memphis-documents-library":"~3.6",
    "zurb/foundation": "^6.3",
    "catenare/aad-sso-wordpress": "dev-alicart"
  },
  "require-dev": {
    "wpackagist-plugin/theme-check": ">=20160523",
    "wpackagist-plugin/wordpress-reset": "~1.4",
    "wpackagist-plugin/log-deprecated-notices": "~0.4",
    "wpackagist-plugin/debug-bar":"~0.9",
    "wpackagist-plugin/wordpress-importer": "~0.6.3"
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

* Run `composer install` if no composer.lock file present else, `composer update`.

## Install ports for Mysql, nginx and fpm
1. `sudo port install mysql57-server nginx php71-fpm php71`

## Setup Database
1. Setup mysql server
    * `sudo rm -fr /opt/local/var/db/mysql57` - remove current mysql57 db folder if it exists.
    * `sudo /opt/local/lib/mysql57/bin/mysqld --initialize --user=_mysql` - setup new database and default password
    * `mysql -u root -p` - use password generated with previous step
        * `ALTER USER 'root'@'localhost' IDENTIFIED BY 'new pass';`
1. Create and setup database
    1. Log into mysql-server
        * `mysql -u root -p`
        * Drop current database `drop database alicart;`
    1. Create database: `create database alicart;`
    1. Add User: `CREATE USER 'alicart'@'localhost' IDENTIFIED BY 'password';`
    1. Grant privileges to user: `GRANT ALL PRIVILEGES ON alicart.* to 'alicart'@'localhost`;
    1. Reload privileges: `FLUSH PRIVILEGES;`
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
    * Start fpm - `sudo port load php71-fpm`
1. Setup nginx - `/opt/local/etc/nginx`
```ini
#user  nobody;
worker_processes  1;

#error_log  logs/error.log;
#error_log  logs/error.log  notice;
#error_log  logs/error.log  info;

#pid        logs/nginx.pid;


events {
    worker_connections  1024;
}


http {
    include       mime.types;
    default_type  application/octet-stream;

    #log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
    #                  '$status $body_bytes_sent "$http_referer" '
    #                  '"$http_user_agent" "$http_x_forwarded_for"';

    #access_log  logs/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    #keepalive_timeout  0;
    keepalive_timeout  65;

    #gzip  on;

    server {
        listen       80;
        server_name  localhost;

        #charset koi8-r;
        #access_log  logs/host.access.log  main;
        root /Users/themartins/Projects/johan/clients/alicart/wordpress/public;
        index  index.php;

  #      location / {
            #root   share/nginx/html;
            
   #     }

        location / {
                # This is cool because no php is touched for static content.
                # include the "?$args" part so non-default permalinks doesn't break when using query string
                try_files $uri $uri/ /index.php?$args;
        }


        #error_page  404              /404.html;

        # redirect server error pages to the static page /50x.html
        #
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   share/nginx/html;
        }

        # proxy the PHP scripts to Apache listening on 127.0.0.1:80
        #
        #location ~ \.php$ {
        #    proxy_pass   http://127.0.0.1;
        #}

        # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
        #
        location ~ \.php$ {
            fastcgi_pass 	unix:/opt/local/var/run/php71/php5-fpm.socket;             
            fastcgi_intercept_errors on;
            include        	fastcgi.conf;
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


    # another virtual host using mix of IP-, name-, and port-based configuration
    #
    #server {
    #    listen       8000;
    #    listen       somename:8080;
    #    server_name  somename  alias  another.alias;

    #    location / {
    #        root   share/nginx/html;
    #        index  index.html index.htm;
    #    }
    #}


    # HTTPS server
    #
    #server {
    #    listen       443 ssl;
    #    server_name  localhost;

    #    ssl_certificate      cert.pem;
    #    ssl_certificate_key  cert.key;

    #    ssl_session_cache    shared:SSL:1m;
    #    ssl_session_timeout  5m;

    #    ssl_ciphers  HIGH:!aNULL:!MD5;
    #    ssl_prefer_server_ciphers  on;

    #    location / {
    #        root   share/nginx/html;
    #        index  index.html index.htm;
    #    }
    #}

}
```
* Mac OS X with MacPorts 
    * Stop nginx - `sudo port unload nginx`
    * Start nginx - `sudo port load nginx`
* Ubuntu
    * `sudo nginx -t` - test configuration
    * `sudo systemctl restart nginx`


## Multi-site configuration - nginx/ubuntu on AWS.
Trying to configure wordpress multisite on Ubuntu.

* [nginx config gist](https://gist.github.com/evansolomon/2274120)
    * Notes for rewrite rules in nginx
    