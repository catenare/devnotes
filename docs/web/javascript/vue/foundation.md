# Working with Vue in Foundation
* Used foundation-cli to install foundation
## Setup
* Install vue, vue-loader, vue-style-loader, vue-template-compiler, sass-loader, style-loader, css-loader, typescript, awesome-typescript-loader
### *gulpfile.babel.js* config
* Configure *gulpfile.babel.js - webpack*
* `gulp.watch('src/assets/components/**/*').on('all', gulp.series(javascript, browser.reload))` - add to end of file to watch components
```js
let webpackConfig = {
  resolve: {
    extensions: ['.ts', '.js', '.vue', '.json'],
    alias: {
      'vue$': 'vue/dist/vue.esm.js'
    }
  },
  module: {
    rules: [
      {
        test: /\.js$/,
        use: [
          {
            loader: 'babel-loader'
          }
        ]
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
                sourceMap: false
              }
            },
              {
                loader: 'sass-loader',
                options:
                  {
                    includePaths: ['./src/assets/vue/styles'],
                    data: '@import "./src/assets/vue/styles/app";',
                    sourceMap: false
                  }
              }
            ],
            ts: 'awesome-typescript-loader'
          }
        }
      },
      {
        test: /\.ts$/,
        loader: 'awesome-typescript-loader'
      },
      {
        test: /\.(woff2?|eot|ttf|otf)(\?.*)?$/,
        loader: 'url-loader',
        query: {
          limit: 10000,
          name: 'fonts/[name].[hash:7].[ext]'
        }
      },
      {
        test: /\.(png|svg|jpg|gif)$/,
        use: [
          'file-loader?name=images/[name].[ext]'
        ]
      }
    ]
  }
}
```
* Have to configure webpackConfig with vue-loader.
* Update *config.yml*
```yaml
  assets:
    - "src/assets/**/*"
    - "!src/assets/{components,img,js,scss,fonts}/**/*"
```
### Other Notes
* Created separate style directory for just Vue styles.
    * Allow access to foundation from all components.
    * Easier configuration in webpack.
* Installed *babel-preset-env* for always current babel engine.
* Customize the *app.css* file in *./src/assets/vue/styles*
    * *@import '~foundation-sites/scss/foundation';*
    * ~~*@import '~font-awesome/scss/font-awesome';*~~ - Not necessary since already in main config.
    * *@import '~motion-ui/src/motion-ui';*
