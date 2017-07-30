# Building a custom wordpress plugin.
## Resources
* Boilerplate template - [WORDPRESS PLUGIN BOILERPLATE GENERATOR](https://wppb.me/)
* Mustache for PHP [BobTheCow](https://github.com/bobthecow/mustache.php)
* GenerateWP [Generate for WordPress Developers](https://generatewp.com/)
* Docs
    * [Developer Plugin: Essential for WordPress Theme Developemnt](https://code.tutsplus.com/articles/developer-plugin-essential-for-wordpress-theme-development--cms-22028)
    * [How to Build a Wordpress Plugin](https://scotch.io/tutorials/how-to-build-a-wordpress-plugin-part-1)

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
## Mustache for templating
1. Add *mustache* for templating.
    * `composer require mustache\mustache`
