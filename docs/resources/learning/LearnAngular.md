# Learning basic Angular

## Setup

* Install angular-cli
  * `npm install -g @angular/cli`
* Create the project
  * `ng new PROJECT_NAME --skip-install --routing --style scss`
* Setup styles
  * Create styles folder in `src/app/assets`
  * Copy _settings.scss file from Foundation Template.
  * Copy _foundation.scss file from Foundation Template.
  * install `npm install @fortawesome/fontawesome @fortawesome/fontawesome-free-solid @fortawesome/fontawesome-free-webfonts`
  * Update settings in _foundation.scss
    * Make sure to include ~ in import for foundation.
    * import `@import '~@fortawesome/fontawesome-free-webfonts/scss/fontawesome';`
  * Update settings.scss file
    * Change util import to `@import '~foundation-sites/scss/util/util';` (line 63)
    * Add line to point to font-awesome variable `$fa-font-path: '~@fortawesome/fontawesome-free-webfonts/webfonts';`
  * Add `_custom.scss` to import your custom scss.
  * Add `_foundation.scss` to your `styles.scss` file in your assets folder.
  * Import the `styles.scss` file into your application.
