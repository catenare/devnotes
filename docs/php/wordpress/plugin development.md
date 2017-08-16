# Building a custom wordpress plugin.
1. Plugin is hosted on github
1. Plugin automatically installed by composer
1. Can develop plugin in Wordpress and push changes to github.
1. Will update installed plugin point to the github repo

## Resources
* Boilerplate template - [WORDPRESS PLUGIN BOILERPLATE GENERATOR](https://wppb.me/)
* GenerateWP [Generate for WordPress Developers](https://generatewp.com/)
* Docs
    * [Developer Plugin: Essential for WordPress Theme Developemnt](https://code.tutsplus.com/articles/developer-plugin-essential-for-wordpress-theme-development--cms-22028)
    * [How to Build a Wordpress Plugin](https://scotch.io/tutorials/how-to-build-a-wordpress-plugin-part-1)

## Setup for development
1. Create *composer.json* file in root directory. - `composer init`
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
1. Add any necessary requirements for the plugin.
