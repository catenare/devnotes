# Setting up Wordpress with Composer, Nginx, PHP-fpm
## See [Local Development Setup](dev.md) for info about composer, nginx, etc.
## Install packages
* Base packages
    * mysql
    * php7
    * nginx

### Setup composer and *composer.json* config file
* Install *composer* in `/usr/local/bin/`
* Install 
* Create **composer.json** file - `composer init`
* Configure with additional settings for wordpress
    * Add [wpackagist](https://wpackagist.org) repository to repositories
    * In *extra*, 
        * add *wordpress-install-dir* as *public*
        * add "installer-paths" for plugins and themes - see below
    * Add custom repositories from version control for custom developed plugins and themes
        * See example file *"https://github.com/catenare/aad-sso-wordpress"* - fork of plugin I'm using and wanted to be able to install/manage via composer.
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

### Create and setup *wp-config.php* file for wordpress
* File located outside of *public* directory
* Copy settings when first installing site.
```php
<?php
/**
 * The base configuration for WordPress
 *
 * The wp-config.php creation script uses this file during the
 * installation. You don't have to use the web site, you can
 * copy this file to "wp-config.php" and fill in the values.
 *
 * This file contains the following configurations:
 *
 * * MySQL settings
 * * Secret keys
 * * Database table prefix
 * * ABSPATH
 *
 * @link https://codex.wordpress.org/Editing_wp-config.php
 *
 * @package WordPress
 */

// ** MySQL settings - You can get this info from your web host ** //
/** The name of the database for WordPress */
define('DB_NAME', '***');

/** MySQL database username */
define('DB_USER', '***');

/** MySQL database password */
define('DB_PASSWORD', '***');

/** MySQL hostname */
define('DB_HOST', 'localhost');

/** Database Charset to use in creating database tables. */
define('DB_CHARSET', 'utf8mb4');

/** The Database Collate type. Don't change this if in doubt. */
define('DB_COLLATE', '');

/**#@+
 * Authentication Unique Keys and Salts.
 *
 * Change these to different unique phrases!
 * You can generate these using the {@link https://api.wordpress.org/secret-key/1.1/salt/ WordPress.org secret-key service}
 * You can change these at any point in time to invalidate all existing cookies. This will force all users to have to log in again.
 *
 * @since 2.6.0
 */
define('AUTH_KEY',         '**');
define('SECURE_AUTH_KEY',  '**');
define('LOGGED_IN_KEY',    '**');
define('NONCE_KEY',        '**');
define('AUTH_SALT',        '**');
define('SECURE_AUTH_SALT', '**');
define('LOGGED_IN_SALT',   '**');
define('NONCE_SALT',       '**');

/**#@-*/

/**
 * WordPress Database Table prefix.
 *
 * You can have multiple installations in one database if you give each
 * a unique prefix. Only numbers, letters, and underscores please!
 */
$table_prefix  = 'custom_';

/**
 * For developers: WordPress debugging mode.
 *
 * Change this to true to enable the display of notices during development.
 * It is strongly recommended that plugin and theme developers use WP_DEBUG
 * in their development environments.
 *
 * For information on other constants that can be used for debugging,
 * visit the Codex.
 *
 * @link https://codex.wordpress.org/Debugging_in_WordPress
 */
define('WP_DEBUG', false);
/* Multisite */
//define('SUNRISE', 'on' );
//define('WP_ALLOW_MULTISITE', true);
//define('MULTISITE', true);
//define('SUBDOMAIN_INSTALL', false);
//define('DOMAIN_CURRENT_SITE', '**');
//define('PATH_CURRENT_SITE', '/');
//define('SITE_ID_CURRENT_SITE', 1);
//define('BLOG_ID_CURRENT_SITE', 1);
/* That's all, stop editing! Happy blogging. */

/** Absolute path to the WordPress directory. */
if ( !defined('ABSPATH') )
	define('ABSPATH', dirname(__FILE__) . '/');

/** Sets up WordPress vars and included files. */
require_once(ABSPATH . 'wp-settings.php');
```
#### Setup uploads directory
* Create *uploads* directory in *public/wp-content/*
* Change owner to *www-data* - `sudo chown www-data:www-date wp-content/uploads`

### Setup Database
1. Create and setup database
    1. Log into mysql-server
        * `mysql -u root -p`
        * Drop current database `drop database paseo;`
    1. Create database: `create database paseo;`
    1. Add User: `CREATE USER 'paseo'@'localhost' IDENTIFIED BY 'password';`
    1. Grant privileges to user: `GRANT ALL PRIVILEGES ON alicart.* to 'paseo'@'localhost`;
    1. Reload privileges: `FLUSH PRIVILEGES;`
### Configure fpm
* Configure socket connection for mysql in php.ini
    * Edit [Pdo_mysql] section
        * `pdo_mysql.default_socket=/var/run/mysqld/mysqld.sock`
         * Add `cgi.fix_pathinfo = 0;` to end of file
* Configure fpm - `/etc/php/7.0/fpm` folder
    * Edit `/etc/php/7.0/fpm/pool.d/www.conf` to change to socket
```ini
    listen = /run/php/php7.0-fpm.sock
```

### Setup nginx - `/etc/nginx/sites-enabled/default`
```ini
# Default server configuration
#
server {
	listen 80 default_server;
	listen [::]:80 default_server;

	root /var/www/paseo/wordpress/public;

	# Add index.php to the list if you are using PHP
	index index.html index.htm index.nginx-debian.html index.php;

	server_name api.paseo.org.za api.martinsonline.org;
	location / {
		# First attempt to serve request as file, then
		# as directory, then fall back to displaying a 404.
		index index.php;
		try_files $uri $uri/ /index.php?$args;
	}
	
	 # Add trailing slash to */wp-admin requests.
   	 rewrite /wp-admin$ $scheme://$host$request_uri/ permanent;
    	
    	# this prevents hidden files (beginning with a period) from being served
	location ~ /\.  { access_log off; log_not_found off; deny all; }
	# Pass uploaded files to wp-includes/ms-files.php.
    	rewrite /files/$ /index.php last;

	if ($uri !~ wp-content/plugins) {
        rewrite /files/(.+)$ /wp-includes/ms-files.php?file=$1 last;
    	}

    	# Rewrite multisite '.../wp-.*' and '.../*.php'.
    	if (!-e $request_filename) {
        	rewrite ^/[_0-9a-zA-Z-]+(/wp-.*) $1 last;
        	rewrite ^/[_0-9a-zA-Z-]+.*(/wp-admin/.*\.php)$ $1 last;
        	rewrite ^/[_0-9a-zA-Z-]+(/.*\.php)$ $1 last;
    	}
	
	# pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
	#
	location ~ \.php$ {
		include snippets/fastcgi-php.conf;
		fastcgi_pass unix:/run/php/php7.0-fpm.sock;
		fastcgi_intercept_errors on;
		include fastcgi.conf;
		client_max_body_size 10M;
	}

	location ~* \.(js|css|png|jpg|jpeg|gif|ico)$ {
		expires max;
		log_not_found off;
	}
	location ~ /\. { access_log off; log_not_found off; deny all; }


    listen 443 ssl http2; # managed by Certbot
ssl_certificate /etc/letsencrypt/live/api.martinsonline.org/fullchain.pem; # managed by Certbot
ssl_certificate_key /etc/letsencrypt/live/api.martinsonline.org/privkey.pem; # managed by Certbot
    include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot

    # Redirect non-https traffic to https
     if ($scheme != "https") {
         return 301 https://$host$request_uri;
     } # managed by Certbot
}
```
### Start everything
* `sudo nginx -t` - test configuration
* `sudo systemctl restart nginx`
* `sudo systemctl restart php70-fpm`
* `sudo systemctl restart mysql-restart`

## Multi-site configuration 
* Resources [Multisite Network Admin](https://codex.wordpress.org/Multisite_Network_Administration)
1. Enable multisite
    * *wp-config.php* - add `define('WP_ALLOW_MULTISITE', true);` under section with /* multisite */
    * Refresh site - will create the necessary tables
    * Add the additional settings under /* multisite */    
```php
    define('MULTISITE', true);
    define('SUBDOMAIN_INSTALL', false);
    define('DOMAIN_CURRENT_SITE', '**');
    define('PATH_CURRENT_SITE', '/');
    define('SITE_ID_CURRENT_SITE', 1);
    define('BLOG_ID_CURRENT_SITE', 1);
```
1. Log into multisite and configure the plugins.

* [nginx config gist](https://gist.github.com/evansolomon/2274120)
    * Notes for rewrite rules in nginx
    