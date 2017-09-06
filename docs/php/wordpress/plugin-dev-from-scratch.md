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
    * Add files to repo - `git add .`
    * Commit files - `git commit -a -m 'initial commit'`
* Create github repository
    * *paseo-wp-form-api* - name or repo
    * Add as remote repo to your local repository.
    * `git remote add origin git@github.com:catenare/paseo-wp-form-api.git`
    * `git push -u origin master`
* Plugin can now be added to your Wordpress site as a dependency.


