---
title: themes
updated: 2020-09-10 22:07:13Z
created: 2020-09-10 22:07:13Z
---

# Theme Development with Wordpress
## Resources/Articles
### Theme Documentation
* Wordpress.org links
	* [Theme Development](https://codex.wordpress.org/Theme_Development)
	* [Handbook](https://developer.wordpress.org/themes/)
	* [Function Reference](https://codex.wordpress.org/Function_Reference)
### Using a template engine
* [Using Templating Engines to Streamline WordPress Theme Development](https://css-tricks.com/templating-languages-and-wordpress)
* [Timber](https://www.upstatement.com/timber/) - Twig template engine
	* Uses Twig for templating.
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
## Developing with Timber
* Resources
	* [Timber Cheatsheet](http://notlaura.com/the-twig-for-timber-cheatsheet/)
* Using [Timber](https://timber.github.io/docs/) for development.
* Setup to get it to work with Timber/Timber package.
	* In `functions.php`
		* Add include to site autoload file
		* use statements to alias class names.
```php
require ABSPATH . '../vendor/autoload.php';
use Timber\Timber as Timber;
use Timber\Site as TimberSite;
use Timber\Menu as TimberMenu;
```
		* Remove check for Timber plugin
		* line 60 - change filter statement. 
			* `$twig->addFilter( new Twig_SimpleFilter('myfoo', array($this, 'myfoo')));`
	* Will get you to an unstyled Wordpress page.

## Configuring foundation framework
* Checkout/download foundation-zurb-template
* Copy src/scss folder.
	* app.scss
	* _settings.scss
* Configuration
	* Add *_custom.scss* for our custom configs
	* Add *component* folder in sass folder for custom components
	* Add *font-awesome* icons as a dependency - `npm install font-awesome`
	* edit *app.scss* - explicit import statements
```sass
@import 'settings';
@import 'custom';
@import '~font-awesome/scss/font-awesome';
@import '~foundation-sites/scss/foundation';
```
* Remove motion-ui imports and settings.
* Edit *_settings.scss*
	* change `@import 'util/util'` to `@import '~foundation-sites/scss/util/util';`
	* Add section 57 for *font-awesome*
	* `$fa-font-path: "~font-awesome/fonts";` - font-awesome path