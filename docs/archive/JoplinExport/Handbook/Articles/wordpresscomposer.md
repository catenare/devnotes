---
title: wordpresscomposer
updated: 2020-09-10 21:43:38Z
created: 2020-09-10 21:43:38Z
---

# Composer for WordPress management and development
## What is composer
* Package and dependency manager for PHP.

## Why?
Setting up and managing a WordPress can 
* Easier to manage.
* Easier to upgrade
* Create a 12 factor app
* No need to include the WordPress code in your plugin or template development
* Put plugins or templates in their own repositories.
* WordPress config is outside of the web public folder.

## Other benefits
* keep plugins and templates in git
* Differentiate between development and production environment
* Store config in environmental variables.
* Use composer for developing plugins and templates.
## How
* https://github.com/johnpbloch/wordpress - automatically updating fork
* http://wpackagist.org
* Github
```json
{
  "name": "Paseo Site",
  "description": "Wordpress site for Paseo Baptist Church and Daycare center",
  "keywords": [
    "wordpress",
    "blog",
    "cms",
    "church"
  ],
  "type": "project",
  "homepage": "http://www.paseo.org.za",
  "license": "GPL-2.0+",
  "authors": [
    {
      "name": "WordPress Community",
      "homepage": "http://wordpress.org/about/"
    },
    {
      "name": "Johan Martin",
      "homepage": "http://www.johan-martin.com",
      "email": "martin.johan@johan-martin.com",
      "role": "developer"
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
    "johnpbloch/wordpress-core-installer": "~1",
    "johnpbloch/wordpress-core": "~4",
    "wpackagist-plugin/akismet":"~4",
    "wpackagist-plugin/wp-core-media-widgets":"dev-master",
    "wpackagist-plugin/ninjafirewall":"~3",
    "wpackagist-plugin/jetpack":"~5",
    "wpackagist-plugin/cloudinary-image-management-and-manipulation-in-the-cloud-cdn": "~1",
    "humanmade/s3-uploads":"~2",
    "paseo/paseo-wp-form-api":"dev-master"
  },
  "require-dev": {
    "wpackagist-plugin/jwt-authentication-for-wp-rest-api": "~1",
    "wpackagist-plugin/gutenberg":"~2",
    "wpackagist-plugin/wordpress-reset": "~1",
    "wpackagist-plugin/wordpress-importer": "~0.6.3",
    "wpackagist-plugin/demo-data-creator":"~1",
    "wpackagist-plugin/wp-rest-api-log":"~1",
    "wpackagist-plugin/debug": "~1",
    "wpackagist-plugin/debug-bar-console": "~0.3",
    "wpackagist-plugin/wordpress-mu-domain-mapping":"~0.5",
    "wpackagist-plugin/wp-php-console":"~1",
    "phpmd/phpmd" : "@stable",
    "phpunit/phpunit": "~6"
  },
  "repositories": [
    {
      "type": "composer",
      "url": "https://wpackagist.org"
    },
    {
      "type": "vcs",
      "url": "https://github.com/catenare/paseo-wp-form-api.git"
    },
    {
      "type": "vcs",
      "url": "https://github.com/humanmade/S3-Uploads.git"
    }
  ]
}
```

* Plugin
```
{
    "name": "paseo/paseo-wp-form-api",
    "description": "API plugin for form submission",
    "type": "wordpress-plugin",
    "license": "MIT",
    "authors": [
        {
            "name": "Johan Martin",
            "email": "johan@paseo.org.za"
        }
    ],
    "require": {
        "timber/timber": "~1"
    },
    "require-dev": {
    },
    "autoload": {
        "psr-4": {
            "Paseo\\": "src/"
        }
    }
}
```
## Resources
* [Using Composer with WordPress](https://roots.io/using-composer-with-wordpress/)
* [WordPress Packagist](https://wpackagist.org/)
* [John P Bloch WordPress Core Installer](https://github.com/johnpbloch/wordpress-core-installer)


