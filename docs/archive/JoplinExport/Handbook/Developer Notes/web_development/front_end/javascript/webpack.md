---
title: webpack
updated: 2020-09-10 22:07:13Z
created: 2020-09-10 22:07:13Z
---

# Webpack Basic Configuration

## Configure Webpack
```javascript
const path = require('path')
const webpack = require('webpack')
const BabiliPlugin = require('babili-webpack-plugin')
const CleanWebPackPlugin = require('clean-webpack-plugin')
const combineLoaders = require('webpack-combine-loaders')
const ExtractTextPlugin = require('extract-text-webpack-plugin')
const StylelintPlugin = require('stylelint-webpack-plugin')
const UglifyJsPlugin = require('uglifyjs-webpack-plugin')
const HtmlWebpackPlugin = require('html-webpack-plugin')
const vendorPackages = require('./package.json')
const { CheckerPlugin } = require('awesome-typescript-loader')

const outputDir = path.join(__dirname, 'dist')

const pluginConfig = [
  new HtmlWebpackPlugin(
    {
      title: 'Kinder Admin',
      template: './src/index.ejs'
    }
  ),
  new webpack.DefinePlugin({
    __STATE__: JSON.stringify(process.env.NODE_ENV)
  }),
  new CheckerPlugin()
]

const moduleConfigBase = [
  {
    test: /\.html$/,
    loader: 'html-loader'
  },
  {
    test: /\.js$/,
    exclude: /(node_modules)/,
    loader: 'babel-loader'
  },
  {
    test: /\.tsx?$/,
    exclude: /(node_modules)/,
    use: [
      { loader: 'babel-loader' },
      { loader: 'awesome-typescript-loader' }
    ]
  },
  {
    test: /\.(png|jpe?g|gif|woff|woff2|eot|ttf|svg)$/,
    loader: 'url-loader?limit=100000'
  },
  {
    test: /\.vue$/,
    loader: 'vue-loader',
    options: {
      loaders: {
        scss: ['vue-style-loader', {
          loader: 'css-loader',
          options: {
            minimize: false,
            sourceMap: false,
            url: true
          }
        },
        {
          loader: 'sass-loader',
          options: {
            includePaths: ['src/assets/styles'],
            data: '@import "src/assets/styles/site";',
            sourceMap: false
          }
        }
        ],
        ts: 'awesome-typescript-loader'
      }
    }
  }
]

const moduleConfigDev = [
  {
    test: /\.scss$/,
    exclude: /(node_modules)/,
    use: [
      { loader: 'style-loader' },
      { loader: 'css-loader' },
      { loader: 'postcss-loader' },
      { loader: 'sass-loader' }
    ]
  },
  {
    test: /\.css$/,
    exclude: /(node_modules)/,
    use: [
      { loader: 'style-loader' },
      { loader: 'css-loader' },
      { loader: 'postcss-loader' }
    ]
  }
]

const moduleConfigProd = [
  {
    test: /\.scss$/,
    use: ExtractTextPlugin.extract({
      fallback: 'style-loader',
      use: combineLoaders([
        {
          loader: 'css-loader'
        },
        {
          loader: 'postcss-loader'
        },
        {
          loader: 'sass-loader'
        }
      ])
    })
  },
  {
    test: /\.css$/,
    use: ExtractTextPlugin.extract({
      fallback: 'style-loader',
      use: combineLoaders([
        {
          loader: 'css-loader'
        },
        {
          loader: 'postcss-loader'
        }
      ])
    })
  }
]

const serverConfig = {
  contentBase: outputDir,
  compress: true,
  open: false,
  port: 9000,
  historyApiFallback: {
    verbose: true,
    disableDotRule: true
  }
}

const webpackConfig = {
  entry: {
    app: './src/app/main.ts',
    vendor: Object.keys(vendorPackages.dependencies).filter(name => (name !== 'font-awesome' && name !== 'foundation-sites' && name !== '@fortawesome/fontawesome-free-webfonts'))
  },
  output: {
    path: outputDir,
    filename: '[name].js'
  },
  resolve: {
    extensions: ['.html', '.ts', '.tsx', '.js', '.json', '.vue'],
    alias: {
      'vue$': 'vue/dist/vue.esm.js',
      '@': path.resolve('src')
    }
  },
  plugins: pluginConfig,
  devServer: serverConfig
}

if (process.env.NODE_ENV === 'production') {
  webpackConfig.plugins = (webpackConfig.plugins || []).concat([
    new BabiliPlugin({}),
    new CleanWebPackPlugin([outputDir]),
    new ExtractTextPlugin({
      filename: '[name].css',
      allChunks: true
    }),
    new webpack.optimize.CommonsChunkPlugin({
      name: 'vendor',
      async: true,
      minChunks: Infinity
    }),
    new StylelintPlugin(
      {syntax: 'scss', emitErrors: false, lintDirtyModulesOnly: true}
    ),
    new UglifyJsPlugin({
      test: /\.js($|\?)/i
    }),
    new webpack.LoaderOptionsPlugin({
      minimize: true
    })
  ])
  webpackConfig.module = { rules: moduleConfigBase.concat(moduleConfigProd) }
  webpackConfig.devtool = '#source-map'
} else {
  /* Development */
  webpackConfig.module = { rules: moduleConfigBase.concat(moduleConfigDev) }
  webpackConfig.devtool = 'cheap-module-source-map'
}

module.exports = webpackConfig
```

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
