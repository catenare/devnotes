# Notes related to front-end development.

## JavaScript Notes

### Resources
* [Standard JS](https://standardjs.com/) - JavaScript Standard Style
    * Rules for writing JavaScript.
* [Awesome Angular](https://github.com/brillout/awesome-angular-components)
* [You Don't Need jQuery](https://blog.garstasio.com/you-dont-need-jquery/)

### Tools
* [Lerna](https://lernajs.io/) - Manage JavaScript projects with multiple packages
* [Colmena](https://github.com/colmena/colmena) - Colmena - CMS system.

### Ionic
* Include font-awesome fonts in project.
    * [FontAwesome in Ionic](https://luiscabrera.site/tech/2017/01/09/fontawesome-in-ionic2.html)
        * Install FontAwesome - `npm install --save font-awesome`
        * Create script to copy fonts into `www/assets/fonts`

        * Set path to fonts in SCSS - `$fa-font-path: /assets/fonts;` in `scr/app/app.scss`; 
        * https://forum.ionicframework.com/t/adding-font-awesome-to-rc0/65925/3 - comments for using with sass to convert to ion-icon.

## Fixing Issues
* "SyntaxError: Unexpected keyword 'const'. Const declarations are not supported in strict mode."
    * Resolution: [Safari/Babel/Webpack Const declarations are not supported in strict mode #922](https://github.com/hapijs/joi/issues/922) - Don't exclue node_modules when building with webpack.
