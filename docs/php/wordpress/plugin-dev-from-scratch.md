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
* `"paseo/contact-form-api": "master"`




