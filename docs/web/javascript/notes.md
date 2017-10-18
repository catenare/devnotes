# Notes related to front-end development.

## JavaScript Notes

### Resources
* [Standard JS](https://standardjs.com/) - JavaScript Standard Style
    * Rules for writing JavaScript.
* [Awesome Angular](https://github.com/brillout/awesome-angular-components)
* [You Don't Need jQuery](https://blog.garstasio.com/you-dont-need-jquery/)
* [JavaScript Plugin for Web Forms](https://1stwebdesigner.com/javascript-plugins-web-forms/)

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

## NPM Notes
* Update npm modules
    * `npm outdated` - list of outdated files
    * `npm install {} {}` - install list of outdated files.

## Other
### Promises
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
