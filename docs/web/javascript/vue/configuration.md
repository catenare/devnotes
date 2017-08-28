# Vuejs Configuration - Using with Foundation

## Webpack Configuration
* Read the (vue-loader)[https://vue-loader.vuejs.org/en/] docs.
    * Especially the section on loaders.
* Vue npm modules to include:
    * vue
    * vue-hot-reload-api
    * vue-templates-compiler
    * vue-html-loader
    * vue-style-loader
    * eslint-plugin-vue
* TypeScript
    * Edit your `tsconfig.json` file. I removed all the comments because it caused problems.
    * In your components, be sure to include *lang="ts"* in your script tag.
    * I'm using *awesome-typescript-loader*. Add it as a loader option in your vue section of webpack.
* eslint
    * [Vue eslint plugin](https://github.com/vuejs/eslint-plugin-vue)
    * add *"plugin:vue/recommended"* to extends section

## Including Foundation with webpack and vue
* [vue-foundation](https://github.com/vue-foundation) - used as a template
* `npm install foundation-sites jquery motion-ui what-input`
* Got scss to work as global import. Only have to include specific files for components.
```javascript
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
                includePaths: ['./src/styles'],
                data: '@import "./src/styles/app";',
                sourceMap: false
              }
            }],
            ts: 'awesome-typescript-loader'
          },
          extractCSS: false
        }
      }
```

## Notes
* Make sure to include *.vue* as part of filename. Can cause problems when importing.   

## Snippets
* *package.json* - modified dev:server script. Seems like including --hot in the command line caused issues.
```json
{
  "name": "learn-vue",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "start": "npm-run-all --parallel dev:server lint:watch",
    "watch": "webpack -w -d",
    "build": "webpack -p",
    "dev:server": "webpack-dev-server --progress --color",
    "lint": "esw webpack.config.* src --color",
    "lint:watch": "npm run lint -- --watch"
  },
  "keywords": [],
  "author": "Johan Martin <martin.johan@johan-martin.com> (http://www.johan-martin.com/)",
  "license": "ISC",
  "devDependencies": {
    "autoprefixer": "^7.1.2",
    "awesome-typescript-loader": "^3.2.3",
    "babel-core": "^6.26.0",
    "babel-loader": "^7.1.2",
    "babel-preset-env": "^1.6.0",
    "babel-preset-latest": "^6.24.1",
    "clean-webpack-plugin": "^0.1.16",
    "copy-webpack-plugin": "^4.0.1",
    "css-loader": "^0.28.5",
    "eslint": "^4.5.0",
    "eslint-config-standard": "^10.2.1",
    "eslint-plugin-import": "^2.7.0",
    "eslint-plugin-node": "^5.1.1",
    "eslint-plugin-promise": "^3.5.0",
    "eslint-plugin-standard": "^3.0.1",
    "eslint-plugin-vue": "^3.12.0",
    "eslint-watch": "^3.1.2",
    "extract-text-webpack-plugin": "^3.0.0",
    "file-loader": "^0.11.2",
    "friendly-errors-webpack-plugin": "^1.6.1",
    "html-webpack-plugin": "^2.30.1",
    "jasmine-core": "^2.8.0",
    "karma": "^1.7.0",
    "karma-jasmine": "^1.1.0",
    "karma-mocha": "^1.3.0",
    "karma-phantomjs-launcher": "^1.0.4",
    "karma-webpack": "^2.0.4",
    "node-sass": "^4.5.3",
    "npm-run-all": "^4.1.0",
    "phantomjs-prebuilt": "^2.1.15",
    "postcss-loader": "^2.0.6",
    "raw-loader": "^0.5.1",
    "sass-loader": "^6.0.6",
    "script-loader": "^0.7.0",
    "style-loader": "^0.18.2",
    "tslint": "^5.7.0",
    "typescript": "^2.4.2",
    "webpack": "^3.5.5",
    "webpack-bundle-analyzer": "^2.9.0",
    "webpack-dev-server": "^2.7.1",
    "webpack-merge": "^4.1.0"
  },
  "dependencies": {
    "foundation-sites": "^6.4.3",
    "jquery": "^3.2.1",
    "motion-ui": "^1.2.3",
    "url-loader": "^0.5.9",
    "vue": "^2.4.2",
    "vue-hot-reload-api": "^2.1.0",
    "vue-html-loader": "^1.2.4",
    "vue-loader": "^13.0.4",
    "vue-router": "^2.7.0",
    "vue-style-loader": "^3.0.1",
    "vue-template-compiler": "^2.4.2",
    "what-input": "^4.3.1"
  }
}
```
* *webpack.config.js* - this works including globally importing foundation scss.
```javascript
     const path = require('path')
const webpack = require('webpack')
const HtmlWpPlugin = require('html-webpack-plugin')
const CleanWpPlugin = require('clean-webpack-plugin')
const ExtractWpPlugin = require('extract-text-webpack-plugin')
const autoprefixer = require('autoprefixer')
const atl = require('awesome-typescript-loader')

module.exports = {
  entry: {
    app: path.resolve(__dirname, 'src/js/app.js')
  },

  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: '[name].bundle.js',
    sourceMapFilename: '[name].bundle.map',
    pathinfo: true
  },
  resolve: {
    extensions: ['.ts', '.js', '.vue', '.json'],
    alias: {
      'vue$': 'vue/dist/vue.esm.js'
    }
  },
  devtool: 'cheap-module-source-map',
  plugins: [
    new HtmlWpPlugin({
      title: 'Learning Vue',
      template: 'src/index.html',
      filename: 'index.html',
      inject: true
    }),
    new CleanWpPlugin([path.resolve(__dirname, 'dist')]),
    new ExtractWpPlugin({
      filename: 'styles.css',
      allChunks: true
    }),
    new webpack.HotModuleReplacementPlugin(),
    new atl.CheckerPlugin()
  ],
  module: {
    rules: [
      {
        test: /\.js$/,
        use: {
          loader: 'babel-loader',
          options: {
            presets: [
              ['env',
                {
                  targets: {
                    'browsers': ['last 2 versions', 'ie>=7']
                  }
                }
              ]
            ]
          }
        }
      },
      {
        test: /\.css$/,
        loaders: ExtractWpPlugin.extract([
          'style-loader/url!file-loader',
          'css-loader'
        ])
      },
      {
        test: /\.ts$/,
        use: 'awesome-typescript-loader'
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
                includePaths: ['./src/styles'],
                data: '@import "./src/styles/app";',
                sourceMap: false
              }
            }],
            ts: 'awesome-typescript-loader'
          },
          extractCSS: false
        }
      },
      {
        test: /\.scss$/,
        use: ExtractWpPlugin.extract({
          fallback: 'style-loader',
          use: [
            {
              loader: 'sass-loader',
              options:
            {
              includePaths: ['./src/styles'],
              data: '@import "./src/styles/app";',
              sourceMap: false
            }
            },
            'css-loader',
            {
              loader: 'postcss-loader',
              options:
                  {
                    plugins: function () {
                      return [autoprefixer]
                    }
                  }
            }
          ]
        }
        )
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
  },
  devServer: {
    port: 8008,
    historyApiFallback: true,
    open: false,
    inline: true
  }
}

```
* tsconfig.json file
```json
{
  "compilerOptions": {
    "target": "es2016",
    "module": "ESNext",
    "lib": [
      "dom",
      "es2016",
      "es2015.promise"
    ],
    "strict": true,
    "moduleResolution": "node",
    "allowSyntheticDefaultImports": true,
    "experimentalDecorators": true,
    "emitDecoratorMetadata": true
  }
}
```
* *eslintrc.json* - including vue rules.
```json
{
    "extends": [
      "standard",
      "plugin:vue/recommended"
    ],
    "parserOptions": {
      "ecmaVersion":6,
      "sourceType": "module",
      "env": {
        "es6": true
      }
    }
}
```
* *tslint.json*
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
* *.gitignore*
```shell
.idea/
node_modules/
package-lock.json
dist/
```
