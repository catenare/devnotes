# Notes related to front-end development.

## Resources
* [Standard JS](https://standardjs.com/) - JavaScript Standard Style
    * Rules for writing JavaScript.
* [Awesome Angular](https://github.com/brillout/awesome-angular-components)
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
* package.json
```json
{
  "name": "package_theme",
  "version": "0.0.1",
  "description": "Build assets for a plugin",
  "main": "index.js",
  "directories": {
    "test": "tests"
  },
  "scripts": {
    "start": "npm-run-all --parallel dev:watch lint:watch",
    "dev:watch": "webpack -w -d",
    "dev:server": "cross-env NODE_ENV=development webpack-dev-server --color --progress --hot",
    "build": "cross-env NODE_ENV=production webpack --progress --hide-modules",
    "lint": "esw webpack.config.* src --color",
    "lint:watch": "npm run lint -- --watch",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "repository": {
    "type": "git",
    "url": "git@github.com:catenare/wordpress-base-theme.git"
  },
  "keywords": [
    "Wordpress",
    "theme"
  ],
  "author": "Johan Martin <martin.johan@johan-martin.com> (http://www.johan-martin.com/)",
  "license": "ISC",
  "bugs": {
    "url": "https://github.com/catenare/paseo-api-theme/issues"
  },
  "homepage": "https://github.com/catenare/paseo-api-theme#readme",
  "dependencies": {
    "bootstrap": "^4.0.0-beta.2",
    "font-awesome": "^4.7.0",
    "webpack-livereload-plugin": "^1.0.0"
  },
  "devDependencies": {
    "@types/backbone": "^1.3.38",
    "@types/jquery": "^3.2.15",
    "autoprefixer": "^7.1.5",
    "awesome-typescript-loader": "^3.2.3",
    "babel-core": "^6.26.0",
    "babel-env": "^2.4.1",
    "babel-loader": "^7.1.2",
    "babel-plugin-transform-class-properties": "^6.24.1",
    "babel-plugin-transform-decorators": "^6.24.1",
    "babel-plugin-transform-es2015-block-scoping": "^6.26.0",
    "babel-preset-env": "^1.6.1",
    "babel-preset-react": "^6.24.1",
    "clean-webpack-plugin": "^0.1.17",
    "cross-env": "^5.1.0",
    "css-loader": "^0.28.7",
    "eslint": "^4.9.0",
    "eslint-config-standard": "^10.2.1",
    "eslint-plugin-import": "^2.8.0",
    "eslint-plugin-node": "^5.2.0",
    "eslint-plugin-promise": "^3.6.0",
    "eslint-plugin-standard": "^3.0.1",
    "eslint-watch": "^3.1.3",
    "extract-text-webpack-plugin": "^3.0.1",
    "file-loader": "^1.1.5",
    "foundation-sites": "^6.4.4-rc1",
    "handlebars": "^4.0.11",
    "handlebars-loader": "^1.6.0",
    "jasmine": "^2.8.0",
    "karma": "^1.7.1",
    "node-sass": "^4.5.3",
    "npm-run-all": "^4.1.1",
    "postcss-cssnext": "^3.0.2",
    "postcss-loader": "^2.0.8",
    "react": "^16.0.0",
    "react-dom": "^16.0.0",
    "sass-loader": "^6.0.6",
    "style-loader": "^0.19.0",
    "tslint": "^5.7.0",
    "typescript": "^2.5.3",
    "url-loader": "^0.6.2",
    "webpack": "^3.8.1"
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
* webpack.config.js
```js
const path = require('path')
const webpack = require('webpack')
const CleanWebPackPlugin = require('clean-webpack-plugin')
const ExtractTextPlugin = require('extract-text-webpack-plugin')

module.exports = {
  entry: './src/main.ts',
  output: {
    path: path.resolve(__dirname, './site/assets'),
    filename: 'paseo-wp-form-api.js'
  },
  plugins: [
    new CleanWebPackPlugin(['./site/assets']),
    new ExtractTextPlugin({
      filename: 'paseo-wp-form-api.css',
      allChunks: true
    }),
    new webpack.ProvidePlugin({
      jQuery: 'jquery',
      $: 'jquery',
      Backbone: 'backbone'
    })
  ],
  externals: {
    jquery: 'jQuery',
    backbone: 'Backbone',
    PASEOFORM: 'PASEOFORM',
    underscore: 'underscore',
    _: 'underscore'
  },
  module: {
    rules: [
      {
        test: /\.scss$/,
        exclude: /node_modules/,
        use: ExtractTextPlugin.extract({
          fallback: 'style-loader',
          use: [
            'css-loader',
            'postcss-loader',
            'sass-loader'
          ]
        })
      },
      {
        test: /\.hbs$/,
        exclude: /node_modules/,
        loader: 'handlebars-loader'
      },
      {
        test: /\.js$/,
        exclude: /node_modules/,
        loader: 'babel-loader'
      },
      {
        test: /\.ts$/,
        exclude: /node_modules/,
        loader: 'awesome-typescript-loader'
      },
      {
        test: /\.(png|jpe?g|gif|svg)(\?.*)?$/,
        loader: 'file-loader',
        options: {
          limit: 10000
        }
      },
      {
        test: /\.(woff2?|eot|ttf|otf)(\?.*)?$/,
        loader: 'url-loader',
        options: {
          limit: 10000
        }
      }
    ]
  },
  devtool: '#source-map'
}

if (process.env.NODE_ENV === 'production') {
  module.exports.devtool = '#source-map'
  // http://vue-loader.vuejs.org/en/workflow/production.html
  module.exports.plugins = (module.exports.plugins || []).concat([
    new webpack.DefinePlugin({
      'process.env': {
        NODE_ENV: '"production"'
      }
    }),
    new webpack.optimize.UglifyJsPlugin({
      sourceMap: true,
      compress: {
        warnings: false
      }
    }),
    new webpack.LoaderOptionsPlugin({
      minimize: true
    })
  ])
}
```
* Configure `vue.js`
```js
  resolve: {
    alias: {
      'vue$': 'vue/dist/vue.esm.js'
    }
  },
```
### Other
* [npm-run-all](https://github.com/mysticatea/npm-run-all/blob/master/docs/npm-run-all.md) - cli options

### Notes for eslint
* [Disable eslint rules](https://brunoscopelliti.com/how-to-disable-eslint-rule-via-javascript-comment/)
