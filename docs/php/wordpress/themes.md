# Theme Development with Wordpress
## Resources/Articles
### Using a template engine
* [Using Templating Engines to Streamline WordPress Theme Development](https://css-tricks.com/templating-languages-and-wordpress)
* [Timber](https://www.upstatement.com/timber/) - Twig template engine
* [ThemeAwsome](https://themeawesome.com/responsive-wordpress-theme/) - Foundation theme for wordpress.
* Mustache for PHP [BobTheCow](https://github.com/bobthecow/mustache.php)

## Setup for development
1. Create *composer.json* file - `composer init`
  * Add *"type": "wordpress-theme"* to get composer to install it in the wordpress plugin directory
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
    "Theme",
    "Composer"
  ],
  "type": "wordpress-theme"
}
```
