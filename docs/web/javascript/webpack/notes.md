# Webpack Notes

## Resources
* [Webpack Examples](https://github.com/webpack/webpack/tree/master/examples)
* [Webpack Book](https://survivejs.com/webpack/foreword/)
* [Lodash Plugin](https://github.com/lodash/lodash-webpack-plugin)
* [Awesome Webpack](https://github.com/webpack-contrib/awesome-webpack)
* [Webpack Vuejs Templates](https://vuejs-templates.github.io/webpack/)

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
