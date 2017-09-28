# Testing with Tape
## Requirements
* Using typescript for development
* Using webpack for hot reload and packaging.
## Tape
* [Tape](https://github.com/substack/tape)
* [Testing JavaScript Modules with Tape](https://ponyfoo.com/articles/testing-javascript-modules-with-tape)
* Seems to be simpler to get up and running then the other frameworks.
* Can run the tests in node.
* [SuperTest](https://github.com/visionmedia/supertest) - API Testing.

## Setup
* [webpack-tape-run](https://github.com/syarul/webpack-tape-run) - run tests in webapck
* [TS-Node](https://github.com/TypeStrong/ts-node) - Run Typescript in Node.js.
    * [Experimenting with TS-Node](https://www.bennadel.com/blog/3268-experimenting-with-ts-node-and-using-typescript-in-node-js-on-the-server.htm)
### Typescript Dependencies
* `@types/tape`
* `awesome-typescript-loader`
* `tslint`
* `tsnode`
### Tape Dependencies
* [Faucet](https://github.com/substack/faucet) - TAP Reporter

### Configuration Example
* *package.json*
```json
"scripts": {
    "start": "npm-run-all --parallel dev:server lint:watch",
    "watch": "webpack -w -d",
    "build": "webpack -d",
    "dev:server": "webpack-dev-server --hot --inline --progress --colors",
    "lint": "esw webpack.config.* src --color",
    "lint:watch": "npm run lint -- --watch",
    "test": "node_modules/.bin/ts-node node_modules/.bin/tape src/tests/*.ts | node_modules/.bin/faucet"
  },
  "author": "Johan Martin <martin.johan@johan-martin.com> (http://www.johan-martin.com/)",
  "license": "ISC",
  "dependencies": {},
  "devDependencies": {
    "@types/tape": "^4.2.30",
    "awesome-typescript-loader": "^3.2.3",
    "babel-core": "^6.26.0",
    "babel-loader": "^7.1.2",
    "babel-preset-env": "^1.6.0",
    "babel-preset-latest": "^6.24.1",
    "electron": "^1.7.8",
    "eslint": "^4.7.2",
    "eslint-config-standard": "^10.2.1",
    "eslint-plugin-import": "^2.7.0",
    "eslint-plugin-node": "^5.1.1",
    "eslint-plugin-promise": "^3.5.0",
    "eslint-plugin-standard": "^3.0.1",
    "eslint-watch": "^3.1.2",
    "faucet": "0.0.1",
    "html-webpack-plugin": "^2.30.1",
    "npm-run-all": "^4.1.1",
    "tap-spec": "^4.1.1",
    "tape": "^4.8.0",
    "ts-node": "^3.3.0",
    "tslint": "^5.7.0",
    "typescript": "^2.5.3",
    "webpack": "^3.6.0",
    "webpack-dev-server": "^2.9.0",
    "webpack-tape-run": "0.0.7"
  },
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
  }
```




### Issues
* Error: **"Module not found: Error: Can't resolve 'fs' in"**
    * [Browser Testing and Code Coverage with Karma, Tape, and Webpack](http://rmurphey.com/blog/2015/07/20/karma-webpack-tape-code-coverage)
    * Resolved by adding below to webpack.config.js:
```js  
node: {
    fs: 'empty'
  },
```
