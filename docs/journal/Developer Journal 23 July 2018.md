# Developer Journal 23 July 2018
## Monday 23 July 2018
* Working on vuetify for my front-end
## Tuesday 24 July 2018
* API refactoring for LookFindMeAPI
    * site
        * industries
        * roles
        * settings - images
* Get settings for public site
* Work on job hunt when I get back
    * Need to respond to interview requests
    * Send resume for WordPress developer
    * Apply for remote positions
## Wednesday 25 July 2018
- [ ] Accepted interview requests on Offerzen
- [ ] Sent over CV for WordPress position
- [ ] Work on lookfindme
- [ ] Need to create on boarding docs for microsite/personal site
- [ ] Docs for creating wordpress.com site tied
* lookfindme
    * Industries and roles for front page
    * Convert forms to vuetify
        * Signup
        * Login
        * Reset password
        * Verification code
        * Registration
        * Membership
        * Employer search
        * Employer contact
            * Send email to potential hires
            * Contact via platform
## Thursday 26 July 2018
* Spoke to next45 - interesting to see what they have to offer.
* Getting jasmine/karma/typescript to work
    * `npm install --save-dev @types/jasmine karma karma-chrome-launcher karma-jasmine karma-sourcemap-loader karma-webpack karma-jasmine-html-reporter karma-spec-reporter`
    * package.json scripts
        * `"scripts": {"test": "karma start karma.conf.js"}`
    * karma.conf.js - apparently the mime line matters.
        * `reporters: ['kjhtml', 'spec']`
    
```js
// Karma configuration
// Generated on Wed Jul 25 2018 01:43:37 GMT+0200 (South Africa Standard Time)
// var webpackConfig = require('./webpack.config.js');
const Path = require("path");

module.exports = function(config) {
  config.set({

    // base path that will be used to resolve all patterns (eg. files, exclude)
    basePath: '',


    // frameworks to use
    // available frameworks: https://npmjs.org/browse/keyword/karma-adapter
    frameworks: ['jasmine'],
    plugins: [
      require('karma-jasmine'),
      require('karma-sourcemap-loader'),
      require('karma-chrome-launcher'),
      require('karma-jasmine-html-reporter'),
      require('karma-webpack'),
      require('karma-spec-reporter')
    ],

    client:{
      clearContext: false // leave Jasmine Spec Runner output visible in browser
    },
    // list of files / patterns to load in the browser
    files: [
      {pattern: 'tests/**/*.ts', watched: false}
    ],


    // list of files / patterns to exclude
    exclude: [
    ],


    // preprocess matching files before serving them to the browser
    // available preprocessors: https://npmjs.org/browse/keyword/karma-preprocessor
    preprocessors: {
      '**/*.ts': ['webpack', 'sourcemap']
    },

    mime: {
      'text/x-typescript': ['ts', 'tsx']
    },

    webpack: {
      resolve: {
        extensions: [".ts", ".tsx", ".js", ".json", ".vue"],
        alias: {
          vue$: "vue/dist/vue.esm.js",
          "@": Path.resolve(__dirname, "src")
        }
      },
      devtool: "inline-source-map",
      mode: 'development',
      module: {
        rules: [
          {
            test: /\.tsx?$/,
            exclude: [Path.resolve(__dirname, "node_modules")],
            use: [
              {
                loader: "babel-loader"
              },
              {
                loader: "awesome-typescript-loader",
                options: {
                  appendTsSuffixTo: [/\.vue$/]
                }
              }
            ]
          },
        ]
      }
    },


    // test results reporter to use
    // possible values: 'dots', 'progress'
    // available reporters: https://npmjs.org/browse/keyword/karma-reporter
    reporters: ['kjhtml','spec'],


    // web server port
    port: 9876,


    // enable / disable colors in the output (reporters and logs)
    colors: true,


    // level of logging
    // possible values: config.LOG_DISABLE || config.LOG_ERROR || config.LOG_WARN || config.LOG_INFO || config.LOG_DEBUG
    logLevel: config.LOG_INFO,


    // enable / disable watching file and executing tests whenever any file changes
    autoWatch: true,


    // start these browsers
    // available browser launchers: https://npmjs.org/browse/keyword/karma-launcher
    browsers: ['Chrome'],

    captureTimeout: 60000,

    // Continuous Integration mode
    // if true, Karma captures browsers, runs the tests and exits
    singleRun: false,

    // Concurrency level
    // how many browser should be started simultaneous
    concurrency: Infinity
  })
}

```
## Saturday 28 July 2018
* Hopefully get my tests to work correctly.
* Need to do my tests for my tests.
    * Finally got my tests to show on the web site
        * `npm install --save-dev karma-jasmine-html-reporter karma-spec-reporter`
        * In *karma.conf.js* - `reporters: ['kjhtml','spec'],`
* 