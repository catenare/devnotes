# CSS 

* [Fixed Menu](https://www.w3schools.com/howto/howto_css_fixed_menu.asp) - Fix menu to the top

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
* Enable in editor (Webstorm)
