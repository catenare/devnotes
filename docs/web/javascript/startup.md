# JavaScript Project Startup

## Basic setup
* *.editorconfig*
```ini
root = true

[*]
indent_style = space
indent_size = 2
end_of_line = lf
charset = utf-8
trim_trailing_whitespace = true
insert_final_newline = true
```

* Setup git repository
* `touch .gitignore`
* `git init`
* *.gitignore*
```ini
node_modules
dist
.vscode/
.idea/
```

## NPM Setup
1. `npm init -f` - create *package.json*
1. Install packages
    * webpack
    * webpack-dev-server
    * webpack-merge
    * clean-webpack-plugin
    * extract-text-webpack-plugin
    * html-webpack-plugin
    * typescript
    * tslint
    * awesome-typescript-loader
    * css-loader
    * sass-loader
    * node-sass
    * style-loader
    * autoprefixer
    * postcss-loader
    * url-loader
    * raw-loader
    * file-loader
    * eslint
    * eslint-watch
    * babel-core
    * babel-preset-env
    * babel-preset-latest
    * babel-loader
    * npm-run-all

```bash
npm install --save-dev webpack webpack-dev-server webpack-merge clean-webpack-plugin extract-text-webpack-plugin html-webpack-plugin typescript tslint awesome-typescript-loader css-loader sass-loader node-sass style-loader autoprefixer postcss-loader eslint eslint-watch url-loader raw-loader file-loader babel-preset-env babel-preset-latest babel-loader babel-core npm-run-all
```

1. Setup *eslint*
    * `./node_modules/.bin/eslint --init`
    * *Use a popular style guide*
    * *Standard*
    * *JSON*

1. Setup *tslint*
    * `./node_modules/.bin/tslint --init`

1. Setup *tsconfig.json*
    * `./node_modules/.bin/tsc --init`

## Configure webpack
1. Create `config` folder
1. In `config`:
    * `webpack.common.js`
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
    app: './src/assets/js/main.js',
    vendor: './src/assets/js/vendor.js'
  },
  output: {
    path: path.resolve(__dirname, './dist'),
    filename: '[name].bundle.js',
    sourceMapFilename: '[name].bundle.map',
    pathinfo: true
  },
  resolve: {
    extensions: ['.js', '.jsx', '.ts', '.tsx']
  },
  devtool: 'cheap-module-source-map',
  plugins: [
    new HtmlWpPlugin({
      title: 'Learning ES6',
      template: 'src/index.html',
      filename: 'index.html'
    }),
    new CleanWpPlugin(['dist']),
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
        exclude: /(node_modules|bower_components)/,
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
      // {
      //   test: /\.css$/,
      //   include: path.resolve(__dirname, './node_modules/leaflet/dist/leaflet.css'),
      //   use: 'raw-loader'
      // },
      {
        test: /\.css$/,
        exclude: /(node_modules|bower_components)/,
        loaders: ExtractWpPlugin.extract([
          'style-loader/url!file-loader',
          'css-loader'
        ])
      },
      {
        test: /\.ts$/,
        exclude: /(node_modules|bower_components)/,
        use: 'awesome-typescript-loader'
      },
      {
        test: /\.scss$/,
        exclude: /(node_modules|bower_components)/,
        use: ExtractWpPlugin.extract({
          fallback: 'style-loader',
          use: [
            'css-loader',
            {
              loader: 'postcss-loader',
              options:
              {
                plugins: function () {
                  return [autoprefixer]
                }
              }
            },
            'sass-loader'
          ]
        }
        )
      },
      {
        test: /\.(png|svg|jpg|gif)$/,
        exclude: /(node_modules|bower_components)/,
        use: [
          'file-loader?name=images/[name].[ext]'
        ]
      }
    ]
  },
  devServer: {
    hot: true,
    watchOptions: {
      ignored: /node_modules/
    }
  }
}
```
* Create `webpack.config.js`
```javascript
module.exports = require('./config/webpack.common');
```
## Npm Scripts
```json
  "scripts": {
    "start": "npm-run-all --parallel dev:server lint:watch",
    "watch": "webpack -w -d",
    "build": "webpack -p",
    "dev:server": "webpack-dev-server --hot --inline --progress --colors",
    "lint": "esw webpack.config.* src --color",
    "lint:watch": "npm run lint -- --watch"
  },
```
## Babel config in package.json
```json
  "babel": {
    "presets": [
      [
        "env",
        {
          "targets": {
            "browsers": [
              "last 2 versions",
              "ie >= 7"
            ]
          }
        }
      ]
    ]
  },
```
