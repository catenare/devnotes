# Building a custom wordpress plugin.
## Resources
* Boilerplate template - [WORDPRESS PLUGIN BOILERPLATE GENERATOR](https://wppb.me/)
* Mustache for PHP [BobTheCow](https://github.com/bobthecow/mustache.php)

## Configure plugin
1. Create *composer.json* file in root directory.
  * Add *"type": "wordpress-plugin"* to get composer to install it in the wordpress plugin directory
```json
{
  "name": "",
  "description": "",
  "authors": [
    {
      "name": "Johan Martin",
      "homepage": "http://www.johan-martin.com",
      "role": "developer"
    }
  ],
  "keywords":[
    "Wordpress",
    "Plug-in",
  ],
  "type": "wordpress-plugin"
}
```
1. Add *mustache* for templating.
1. `composer require mustache\mustache`

  * Using *Mustache* for templating. Hope to easily share with JavaScript if necessary.