# Creating a basic page with webpack
## Basic setup for a basic web page.
* Configure **proto** project
```
index.html
assets\
assets\js
assets\ts
assets\css
assets\scss
webpack.config.js
.editorconfig
.eslintignore
.eslintrc
```
* Create the *package.json* page.
* `npm init`
* Install the developer packages.
* `npm install webpack webpack-dev-server eslint eslint-watch npm-run-all babel-loader babel-core babel-preset-env babel-preset-latest sass-loader node-sass typescript typescript-loader --save-dev` 
```json
{
  "name": "proto-demo",
  "version": "0.0.1",
  "description": "Proto with webpack and webpack-dev-server",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "Johan Martin <martin.johan@johan-martin.com> (http://www.johan-martin.com/)",
  "license": "ISC",
  "dependencies": {},
  "devDependencies": {
    "babel-core": "^6.25.0",
    "babel-loader": "^7.1.1",
    "babel-preset-env": "^1.6.0",
    "babel-preset-latest": "^6.24.1",
    "eslint": "^4.3.0",
    "eslint-watch": "^3.1.2",
    "node-sass": "^4.5.3",
    "sass-loader": "^6.0.6",
    "typescript": "^2.4.2",
    "typescript-loader": "^1.1.3",
    "webpack": "^3.4.1",
    "webpack-dev-server": "^2.6.1"
  }
}
```
* Create *webpack.config.js*.
```json
module.exports = {
    entry: './js/index.js',
    output: {
        path: __dirname + '/dist',
        publicPath: '/dist',
        filename: 'bundle.js'
    },
    module: {
        rules: [{
            test: /\.js$/,
            exclude: /node_modules/,
            use: 'babel-loader'
        }]
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
