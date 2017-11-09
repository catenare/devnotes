# CSS 

## Resources
* [Fixed Menu](https://www.w3schools.com/howto/howto_css_fixed_menu.asp) - Fix menu to the top
* [CSS Frameworks](http://www.cssreflex.com/css-frameworks/)
* [CssDB](http://cssdb.co/)
* [Animista](http://animista.net/play)
* [CSS3 Generator](http://css3generator.com/)

## Seo
* [MegaTags](https://megatags.co/) - OpenGraph tag generator

## Linting CSS and SCSS
* Install stylelint, stylelint-config-standard
    * `npm install stylelint stylelint-config-standard`
* Add *stylelint* in *package.json*
```json
  "stylelint": {
    "plugins": [
      "stylelint-scss"
    ],
    "extends": "stylelint-config-standard"
  }
```
### Stylelint Notes
* [stylelint-config-sass-guidelines](https://github.com/bjankord/stylelint-config-sass-guidelines) - scss stylelint rules
* [Stylelint webpack plugin](https://github.com/JaKXz/stylelint-webpack-plugin)
    * `const StylelintPlugin = require('stylelint-webpack-plugin')`
    * `new StylelintPlugin({syntax: 'scss', emitErrors: false, lintDirtyModulesOnly: true})`
* [stylelint](https://stylelint.io/)
    * `npm install --save-dev stylelint stylelint-config-sass-guidelines stylelint-config-standard stylelint-scss stylelint-webpack-plugin`
* config in *package.json*
```json
"stylelint": {
    "plugins: [
        "stylelint-scss"
}
```

## Font Awesome

* Font Awesome icon as part of before psuedo class using scss. [StackOverflow Font Awesome Icon as CSS Content](https://stackoverflow.com/questions/20782368/use-font-awesome-icon-as-css-content)
```css
.a:after {
    // Import mixin from font-awesome/scss/mixins.scss
    @include fa-icon();

    // Use icon variable from font-awesome/scss/variables.scss
    content: $fa-var-exclamation-triangle;
}
```
