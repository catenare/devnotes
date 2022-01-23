---
title: testing
updated: 2020-09-10 22:07:13Z
created: 2020-09-10 22:07:13Z
---

# Testing

## Resources
* Reactjs
	* [Enzyme](https://github.com/airbnb/enzyme)
* Other
	* [Karma](https://karma-runner.github.io/1.0/index.html) - runner
	* [Mocha](https://mochajs.org/) - framework
	* [Chai](http://chaijs.com/) - assertion library
* Acceptance testing
	* [Robot Framework](http://robotframework.org/)
		* Using `mkvirtualenv` - `mkvirtualenv -a . johan-martin`
		* `pip install robotframework`
## Getting started
* installation `npm i --save-dev enzyme enzyme-adapter-react-16 chai mocha karma`
* Install *Robot Framework*
	* `mkvirtualenv -a . johan-martin`
	* `pip install robotframework`

## Testing framework
* Using Karma, Mocha, Chai
    * `npm -i --save-dev karma mocha chai`

## TAP
* [Test Anything Protocol](https://testanything.org/)
    * [tap-spec](https://github.com/scottcorgan/tap-spec) - output similar to Mocha
    * [Faucet](https://github.com/substack/faucet) - TAP Reporter
## Tape
* [Why I use Tape...](https://medium.com/javascript-scene/why-i-use-tape-instead-of-mocha-so-should-you-6aa105d8eaf4)

## Jasmine and Karma
* [Jasmine](https://jasmine.github.io/)
    * Can't test es6
* [Karma](https://karma-runner.github.io/2.0/index.html)
    * [Headless Chrome](https://developers.google.com/web/updates/2017/04/headless-chrome)
* Docs
    * [Jasmine, es6](https://www.classandobjects.com/test_using_jasmine_react_es6_webpack/)
    * [Jasmine, Karma, Webpack, Commandline](https://what-problem-does-it-solve.com/webpack/testing.html)
    * [Jasmine, Es6](http://www.syntaxsuccess.com/viewarticle/writing-jasmine-unit-tests-in-es6)
    * [Karma, webpack, Jasmine](https://kentor.me/posts/testing-react-and-flux-applications-with-karma-and-webpack/)

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
