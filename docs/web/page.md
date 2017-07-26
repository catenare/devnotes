# Creating a basic page with webpack
## Basic setup for a basic web page.
* [Creating a prototype with css and javascript](https://webdesign.tutsplus.com/tutorials/how-to-create-an-app-prototype-using-css-and-javascript--cms-29062) - Using webpack and typescript
* Configure **proto** project
```
src/css
src/js/index.js
src/scss/style.scss
src/index.html
package.json
README.md
webpack.config.js
.editorconfig
.eslintignore
.eslintrc
```
* Create the *package.json* page.
* `npm init` 

```json
{
  "name": "proto-demo",
  "version": "0.0.1",
  "description": "Proto with marvel css",
  "main": "index.js",
  "scripts": {
    "start": "npm-run-all --parallel dev:server lint:watch",
    "watch": "webpack -w -d",
    "build": "webpack -p",
    "dev:server": "webpack-dev-server --hot --inline --progress --colors",
    "lint": "esw webpack.config.* src --color",
    "lint:watch": "npm run lint -- --watch"
  },
  "author": "Johan Martin <martin.johan@johan-martin.com> (http://www.johan-martin.com/)",
  "license": "ISC",
  "dependencies": {},
  "devDependencies": {
    "babel-core": "^6.25.0",
    "babel-loader": "^7.1.1",
    "babel-preset-env": "^1.6.0",
    "babel-preset-latest": "^6.24.1",
    "clean-webpack-plugin": "^0.1.16",
    "css-loader": "^0.28.4",
    "eslint": "^4.3.0",
    "eslint-watch": "^3.1.2",
    "extract-text-webpack-plugin": "^3.0.0",
    "html-webpack-plugin": "^2.29.0",
    "node-sass": "^4.5.3",
    "npm-run-all": "^4.0.2",
    "sass-loader": "^6.0.6",
    "style-loader": "^0.18.2",
    "typescript": "^2.4.2",
    "typescript-loader": "^1.1.3",
    "webpack": "^3.4.1",
    "webpack-dev-server": "^2.6.1"
  },
  "babel": {
    "presets": "env"
  }
}

```
* Create *webpack.config.js*.

```json
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');
const CleanWebPackPlugin = require('clean-webpack-plugin');
const ExtractTextPlugin = require('extract-text-webpack-plugin');

module.exports = {
    entry: './src/js/index.js',
    output: {
        path: path.resolve(__dirname + '/dist'),
        filename: 'bundle.js',
        pathinfo: true
    },
    plugins: [
        new HtmlWebpackPlugin({
            title: 'App Prototype with CSS and JS',
            template: 'src/index.html',
            filename: 'index.html'
        }),
        new CleanWebPackPlugin(['dist']),
        new ExtractTextPlugin({
            filename: 'styles.css',
            allChunks: true
        })
    ],
    module: {
        rules: [
            {
                test: /\.js$/,
                exclude: /node_modules/,
                use: 'babel-loader'
            },
            {
                test: /\.css$/,
                use: [
                    'style-loader',
                    'css-loader'
                ]
            },
            {
                test: /\.ts$/,
                use: [
                    'typescript-loader'
                ]
            },
            {
                test: /\.scss$/,
                use: ExtractTextPlugin.extract(['css-loader', 'sass-loader'])
            }
        ]
    },
    devServer: {
        compress: true,
        hot: true
    }
};
```

* Create *.editorconfig*
```
root = true

[*]
indent_style = space
indent_size = 4
end_of_line = lf
charset = utf-8
trim_trailing_whitespace = true
insert_final_newline = true
```
* Create *.eslintrc*
```json
"parserOptions": {
        "ecmaVersion": 6,
        "sourceType": "module"
    },
    "rules": {
        "no-console": "off",
        "indent": [
            2,
            4
        ],
        "linebreak-style": [
            2,
            "unix"
        ],
        "semi": [
            2,
            "always"
        ]
    },
    "env": {
        "es6": true,
        "browser": true,
        "node": true,
        "mocha": true
    },
    "extends": "eslint:recommended"
}
```
* Create *.eslintignore* - directories to ignore
```
dist
```
## Including stylesheets
* Import stylesheets into javascript file
```javascript
import '../scss/devices.scss';
import '../scss/style.scss';

function select(s) {
    return document.querySelector(s);
}
```
