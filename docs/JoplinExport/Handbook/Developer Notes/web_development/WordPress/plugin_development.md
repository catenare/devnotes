---
title: plugin_development
updated: 2020-09-10 22:07:13Z
created: 2020-09-10 22:07:13Z
---

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
* Enable debug log in *wp-config.php*
    * `define( 'WP_DEBUG_LOG', true );` - will write to */wp-content/debug.log* - [Debugging in Wordpress](https://codex.wordpress.org/Debugging_in_WordPress)

# Wordpress Plugin Development from Scratch
* Create Contact Form plugin to submit contact information via API.
* Use Composer.
* PHP 7.0
## Setup for plugin development.
* Update composer `sudo composer self-update`
* Create folder for plugin `mkdir paseo-contact-form`
* Create *composer.json* `composer init`
    * For *type* use *wordpress-plugin*
* Create git repository - `git init`
* Create *README.md* for github.
    * Include information about plugin in README file
    * Create *.gitignore* file
        * Add *wp-config.php* file to insure it does not get committed.
    * Add files to repo - `git add .`
    * Commit files - `git commit -a -m 'initial commit'`
* Create github repository
    * *paseo-wp-form-api* - name or repo
    * Add as remote repo to your local repository.
    * `git remote add origin git@github.com:catenare/paseo-wp-form-api.git`
    * `git push -u origin master`
* Plugin can now be added to your Wordpress site as a dependency.

## Create the plugin file with header information
* `touch paseo-contact-form.php`
* Add header requirements to the file-  [Header Requirements](https://developer.wordpress.org/plugins/the-basics/header-requirements/)
* Plugin can now be enabled on the Wordpress site.
* Create *dev-master* branch. Seems like you can't use the vcs plugin setup with straight *master*
    * `git checkout -b dev-master`
    * `git push origin --all` - push all the branches to github.


## Enable plugin in Wordpress.
* Edit *composer.json* file in Wordpress application folder.
* Add github repository under *"repositories"* section.
```json
"respositories": [
    {
      "type": "vcs",
      "url": "https://github.com/catenare/paseo-wp-form-api.git"
    }
]
```
* Add plugin to *"require"* section.
* `"paseo/contact-form-api": "dev-master"`
* Plugin is now installable in Wordpress Admin.

## Setup plugin in Wordpress
* Run `composer update` to install necessary dependencies.
* Activate plugin.

## Using namespace and classes for plugin development

## Using database in wordpress
* [WPDB](https://developer.wordpress.org/reference/classes/wpdb/)

## Multi-site development
* [Making Plugins Compatible with WordPress Multisite](https://www.wphub.com/blog/posts/plugins-compatible-wordpress-multisite/)
* [Wordpress Create a Network](https://codex.wordpress.org/Create_A_Network)
* [How to Build a Multisite Compatible WordPress Plugin](https://wisdmlabs.com/blog/build-multisite-compatible-wordpress-plugin/)
* [Write a Plugin for WordPress Multi-Site](https://shibashake.com/wordpress-theme/write-a-plugin-for-wordpress-multi-site)
