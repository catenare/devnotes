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