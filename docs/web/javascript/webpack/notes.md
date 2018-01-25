# Webpack Notes

## Resources
* [Webpack Examples](https://github.com/webpack/webpack/tree/master/examples)
* [Webpack Book](https://survivejs.com/webpack/foreword/)
* [Lodash Plugin](https://github.com/lodash/lodash-webpack-plugin)
* [Awesome Webpack](https://github.com/webpack-contrib/awesome-webpack)
* [Webpack Vuejs Templates](https://vuejs-templates.github.io/webpack/)
* [Webpack Chain](https://github.com/mozilla-neutrino/webpack-chain)

## Plugins
* [Static Site Generator](https://github.com/markdalgleish/static-site-generator-webpack-plugin)

## Articles
* [Introduction to Webpack](https://www.smashingmagazine.com/2017/02/a-detailed-introduction-to-webpack/)
    * Includes notes for using Handlebars.

## font-awesome config with webpack and foundation
* webpack config - allow to process image and font files.
```js
      {
        test: /\.(png|jpe?g|gif|svg)(\?.*)?$/,
        loader: 'url-loader',
        query: {
          limit: 10000,
          name: utils.assetsPath('img/[name].[hash:7].[ext]')
        }
      },
      {
        test: /\.(woff2?|eot|ttf|otf)(\?.*)?$/,
        loader: 'url-loader',
        query: {
          limit: 10000,
          name: utils.assetsPath('fonts/[name].[hash:7].[ext]')
        }
      }
```
* Configure scss imports
* In `_settings.scss` add `$fa-font-path:   "~font-awesome/fonts";` to end of the page.
* In `app.scss` add `@import '~font-awesome/scss/font-awesome';` after `@import "settings"`.

## Errors and notes
* Issue: *Can't find variable: SockJS" in Safari on Mac and iOS*
    * Resolve: [`eval-source-map` results in "Can't find variable: SockJS" in Safari on Mac and iOS with v2.8.x #1090](https://github.com/webpack/webpack-dev-server/issues/1090)
    * Changed *devtool* to '#source-map'
## Wordpress Configuration
* ` wp_enqueue_script( $this->plugin_name, \PASEO_WP_FORM_DIR_URL . 'site/assets/paseo-wp-form-api.js', array('jquery'), $this->version, false );` - enqueue with jQuery as a dependency.
* Use externals to not include jquery in the bundle but use the Wordpress instance of jquery.
```json
  externals: {
    jquery: 'jQuery'
  },
```
* Add **webpack.ProvidePlugin** with *jQuery* as the global variable.
```json
    new webpack.ProvidePlugin({
      jQuery: 'jquery'
    })
```

* Error: TS2304 - Cannot find name Jquery - solution [StackOverflow - ts2304 - cannot find name](https://stackoverflow.com/questions/31173738/typescript-getting-error-ts2304-cannot-find-name-require?rq=1)
	* `npm install --save-dev @types/jquery`
* Error: error TS2304: Build:Cannot find name 'Iterable' {still related to jquery} - solution: [StackOverflow Error ts2304](https://stackoverflow.com/questions/45360993/error-ts2304-buildcannot-find-name-iterable-after-upgrading-to-angular-4)
	* Update tsconfig.
```json
"target": "es5",
"lib": [
       "es2016", "dom"
     ], 
```
* Unexpected character '`' [./node_modules/foundation-sites/js/foundation.util.core.js:24,0][entry.bundle.js:10295,124]
    * [Error building with WebPack #10275](https://github.com/zurb/foundation-sites/issues/10275)
    * Resolve with: for test: /\.js$/
        * `exclude: /node_modules(\/?!foundation-sites)/,`

* [Uncaught ReferenceError: webpackJsonp is not defined #5002](https://github.com/webpack/webpack/issues/5002) 
    * Resolve by determining loading order of files - `webpack --display-entrypoints` when you have multiple chunks

* Notes for commons chunk plugin
    * [Commons Chunk Plugin](https://webpack.js.org/plugins/commons-chunk-plugin/)
    * Examples: [multiple-entry-points-commons-chunk-css-bundle](https://github.com/webpack/webpack/tree/master/examples/multiple-entry-points-commons-chunk-css-bundle)


* Injecting Server Urls - [Injecting Server Urls](http://developmentnow.com/2016/07/13/webpack-injecting-server-urls/)
    * use webpack.DefinePlugin
    * Be sure to quote the urls - *'"url"'*


* Using @ to refer to src folder.
    * [Use @ in path](https://stackoverflow.com/questions/42749973/es6-import-using-at-sign-in-path-in-a-vue-js-project-using-webpack)
    resolve: {alias: {'@': resolve('src')} }
