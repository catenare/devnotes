# Notes about using Composer to manage a package
## Notes for managing a custom packages with php composer. 
* [Loading a package from a vcs repository](https://getcomposer.org/doc/05-repositories.md#loading-a-package-from-a-vcs-repository)
1. Package must have it's own *composer.json* file.
```json
{
  "name": "catenare/smartsheet",
  "description": "API Connection to Smartsheet. Add sheets and add rows",
  "license": "proprietary",
  "authors": [
    {
      "name": "Johan Martin",
      "homepage": "http://www.johan-martin.com",
      "email": "martin.johan@johan-martin.com",
      "role": "developer"
    }
  ],
  "require": {
    "guzzlehttp/guzzle": "^6.2",
    "symfony/console": "^3.3",
    "symfony/dotenv": "^3.3",
    "symfony/dependency-injection": "^3.3",
    "symfony/yaml": "^3.3",
    "symfony/config": "^3.3",
    "symfony/serializer": "^3.3",
    "zendframework/zend-json": "^3.0"
  },
  "minimum-stability": "dev",
  "autoload": {
    "psr-4": { "SmartSheet\\": "src/" },
    "files":["boot.php","main.php"]
  },
  "autoload-dev": {
    "psr-4": { "SheetTest\\": "test/" }
  },
  "require-dev": {
    "phpunit/phpunit": "^6.2"
  }
}
```
1. Use **dev-{branch}** to have composer checkout the correct git branch.
* Example:
```json
"require": {
        "catenare/smartsheet": "dev-master"
    },
    "repositories": [
    {
      "type": "vcs",
      "url": "https://github.com/catenare/smartsheet-api"
    }
  ]
```
* Other Notes
    *  For wordpress: Use the **type** property set to **wordpress-plugin**. Wordpress installer will install it in the right location. *Composer seems to be reluctant to go more than one level deep when checking out dev branches.*
```json
{
    "name": "catenare/ninjaforms-smartsheet-plugin",
    "description": "Add form data to smartsheet",
    "type": "wordpress-plugin",
    "license": "proprietary",
    "authors": [
    {
        "name": "Johan Martin",
        "homepage": "http://www.johan-martin.com",
        "email": "martin.johan@johan-martin.com",
        "role": "developer"
    }
    ],
    "keywords":[
        "alicart",
        "ninja-forms",
        "smartsheet"
    ],
    "require": {
        "catenare/smartsheet": "dev-master"
    },
    "repositories": [
    {
      "type": "vcs",
      "url": "https://github.com/catenare/smartsheet-api"
    }
  ]
}
```
* Dependencies for sub packages in vcs. Put repo info in man composer.json file.
```json
{
  "name": "catenare/wordpress-intranet",
  "description": "Intranet based on WordPress",
  "license": "proprietary",
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
    "johnpbloch/wordpress-core-installer": "~0.2",
    "johnpbloch/wordpress-core": "~4.7",
    "wpackagist-plugin/login-lockdown":"~1.7",
    "wpackagist-plugin/all-in-one-intranet": "~1.2",
    "wpackagist-plugin/ninja-forms":"~3.1",
    "catenare/aad-sso-wordpress": "dev-alicart",
    "catenare/ninjaforms-smartsheet-plugin": "dev-master"
  },
  "require-dev": {
    "phpunit/phpunit": "^6.2"
  },
  "repositories": [
    {
      "type": "composer",
      "url": "https://wpackagist.org"
    },
    {
      "type": "vcs",
      "url": "https://github.com/catenare/aad-sso-wordpress"
    },
    {
      "type": "vcs",
      "url": "https://github.com/catenare/ninjaforms-smartsheet"
    },
    {
      "type": "vcs",
      "url": "https://github.com/catenare/smartsheet-api"
    }
  ]
}
```
* Added **smartsheet-api** vcs because **ninjaform-smartsheet-plugin** dependent on it.