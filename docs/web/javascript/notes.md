# Notes related to front-end development.

## Resources
* [Standard JS](https://standardjs.com/) - JavaScript Standard Style
    * Rules for writing JavaScript.

* [You Don't Need jQuery](https://blog.garstasio.com/you-dont-need-jquery/)
* [JavaScript Plugin for Web Forms](https://1stwebdesigner.com/javascript-plugins-web-forms/)
* [JavaScript Encyclopedia](http://www.crockford.com/javascript/encyclopedia/)

### Tools
* [Lerna](https://lernajs.io/) - Manage JavaScript projects with multiple packages
* [Colmena](https://github.com/colmena/colmena) - Colmena - CMS system.

### Performace tools
* Calibre
* Speedcurve
* Bundlesize
* [httparchive.org](http://beta.httparchive.org/) - beta.httparchive.org - data/insights

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

## NPM Notes
* Update npm modules
    * `npm outdated` - list of outdated files
    * `npm install {} {}` - install list of outdated files.

## Other
* [Normalizr](https://github.com/paularmstrong/normalizr) - create schema to normalize the result of a returned schema.

### Captcha
```js
let getCaptcha = new Promise(
    function(resolve) {
            let captcha = true;
            resolve(captcha);
        }
)

export default getCaptcha;

import Vue from 'vue'
import App from './App.vue'
import getCaptcha from './recaptcha'

window.captchaCallback = function() {
    console.log('called')
    getCaptcha.then(function(fulfilled){

            grecaptcha.render('html_element', {
                'sitekey' : '6LeIxAcTAAAAAJcZVRqyHh71UMIEGNQ_MXjiZKhI'
            });

        })
        .catch(function(error){
            console.log(error);
        });
}


new Vue({
  el: '#app',
  render: h => h(App)
})
```
### Axios
* Issue: [*Axios is not showing all headers of response*](https://github.com/axios/axios/issues/771)
    * [Set Global Axios Headers](https://github.com/axios/axios#global-axios-defaults)
    * [Mozilla CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/Access_control_CORS#Access-Control-Expose-Headers)

### Fingerprint2 - use a quick and dirty way to track submissions.
* Wrap code in a promise.
```js
import Fingerprint2 from "fingerprintjs2";

const getFinger = new Promise((resolve) => {

  new Fingerprint2().get((result) => {
    resolve(result);
  });
});

export default getFinger;
```
* In Component - call a function from the promise and the set local var for finger.
```js
getFinger.then( (result) => this.getInitHeaders(result) );
```

### Notes for github
* https://github.com/catenare/proto-app-demo
    * vue
    * awesome-typescript-loader
    * Production options
    * Marvel css prototype
* https://github.com/catenare/basic-typescript-project
    * using webpack, typescript, faucet and tape
* https://github.com/catenare/foundation-cli-template-site
    * Foundation 6 template with typescript
* https://github.com/catenare/webpack-starter
    * Basic webpack template with leaflet

### Shared files
* tslint.json
```json
{
  "defaultSeverity": "error",
  "extends": [
      "tslint:recommended"
  ],
  "jsRules": {},
  "rules": {},
  "rulesDirectory": []
}
```
* tsconfig.json
```json
{
  "compilerOptions": {
    "target": "es5",
    "module": "commonjs",
     "lib": [
       "es2016", "dom"
     ],                             
     "allowSyntheticDefaultImports": true,
     "experimentalDecorators": true,
     "emitDecoratorMetadata": true
  }
}
```
* postcss.config.js
```js
module.exports = {
  plugins: {
    'postcss-cssnext': {}
  }
}
```

* .eslintrc.json
```json
{
  "extends": "standard"
}
```
* .eslintignore
```json
dist
node_modules
```
* .babelrc
```json
{
  "presets": [
    "env",
    "react",
    "stage-3"
  ],
  "plugins": [
    "transform-class-properties",
    "transform-decorators",
    "transform-react-constant-elements",
    "transform-react-inline-elements"
  ]
}
```
### Other
* [npm-run-all](https://github.com/mysticatea/npm-run-all/blob/master/docs/npm-run-all.md) - cli options

### Notes for eslint
* [Disable eslint rules](https://brunoscopelliti.com/how-to-disable-eslint-rule-via-javascript-comment/)

### Getting hex codes for FontAwesome to work.
* **font-family** should be *"FontAwesome"*
```scss
  &::before {
    font-family: "FontAwesome";
    content: "\f00d";
  }
```
* List of hex codes for font-awesome: [FontAwesomeSnippet](http://astronautweb.co/snippet/font-awesome/)
