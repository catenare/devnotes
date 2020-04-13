# Angular Framework
## Notes
* When updating core, have to use *--to* to get it to work. `ng update @angular/core --to 6.0.6`

## Resources
* Tools
  * [Angular Augury](https://augury.angular.io/) - debug and profile angular 2 apps
    * Chrome extension
* Lists
    * [Awesome Angular](https://github.com/AngularClass/awesome-angular)
* [Angular Documentation](https://angular.io/)
* [Angular CLI Documetation](https://github.com/angular/angular-cli)
* [Awesome Angular](https://github.com/brillout/awesome-angular-components)
* [Clarity Design System](https://vmware.github.io/clarity/)
* [Angular Education](https://github.com/timjacobi/angular-education)
* Tools
    * [ngrev](https://github.com/mgechev/ngrev) - navigate structure of the app. Desktop app
    * [Augury] - Debug and profile angular project. Browser extension (Chrome only)
    * [Angular Essentials Plugin]() - Visual Studio Code plugin for Angular development.
* Tutorials
    * [Angular with Tailwindcss](https://www.jerriepelser.com/blog/using-tailwindcss-with-angular/)

### Proxy api calls in angular - access API calls from local server.
* [Proxy Config](https://github.com/angular/angular-cli/blob/master/docs/documentation/stories/proxy.md)
* *proxy.conf.json*
```json
{
  "/children": {
    "target": "http://localhost:5000",
    "secure": false
  }
}
```

### Material Design
* [Angular Material Table with CDK Table](https://stackblitz.com/edit/angular-material2-table?file=app%2Fapp.component.ts)
* [Layout and CSS](https://material.io/design/foundation-overview/)

### Angular rxjs
* [Angular Observable Usage](https://angular.io/guide/practical-observable-usage) - Observable

## Testing
I finally got the everything configured to test an API call from my Angular application. Because everything is local on my machine, I'm using a proxy on the Angular side to access my API without having to worry about CORS. Trying to Unit Test an API service took a little work because <em>ng test</em> does not read the <em>proxy.conf.json</em> file.
So, here is the test.
```ts
// Karma configuration file, see link for more information
// https://karma-runner.github.io/1.0/config/configuration-file.html
module.exports = function (config) {
  config.set({
    basePath: '',
    frameworks: ['jasmine', '@angular-devkit/build-angular'],
    plugins: [
      require('karma-jasmine'),
      require('karma-chrome-launcher'),
      // require('karma-electron'),
      require('karma-jasmine-html-reporter'),
      require('karma-coverage-istanbul-reporter'),
      require('@angular-devkit/build-angular/plugins/karma')
    ],
    client:{
      clearContext: false // leave Jasmine Spec Runner output visible in browser
    },
    // preprocessors: {
    //   '**/*.js': ['chrome']
    // },
    coverageIstanbulReporter: {
      dir: require('path').join(__dirname, 'coverage'), reports: [ 'html', 'lcovonly' ],
      fixWebpackSourcePaths: true
    },
    angularCli: {
      environment: 'dev'
    },
    proxies: {
      '/kinder': {
        'target': 'http://localhost:5000/kinder',
        'changeOrigin': true
      }
      // '/kinder': 'http://localhost:5000/kinder/'
    },
    reporters: ['progress', 'kjhtml'],
    port: 9876,
    colors: true,
    logLevel: config.LOG_INFO,
    autoWatch: true,
    browsers: ['Chrome'],
    singleRun: false
  });
};
```
<ul>
 	<li><em>UtilService</em> contains the call I want to test</li>
 	<li><em>GetdataService</em> actually makes the call.</li>
</ul>
Here is my <em>karma.conf.js</em> file.

```js
// Karma configuration file, see link for more information
// https://karma-runner.github.io/1.0/config/configuration-file.html

module.exports = function (config) {
  config.set({
    basePath: '',
    frameworks: ['jasmine', '@angular-devkit/build-angular'],
    plugins: [
      require('karma-jasmine'),
      require('karma-chrome-launcher'),
      // require('karma-electron'),
      require('karma-jasmine-html-reporter'),
      require('karma-coverage-istanbul-reporter'),
      require('@angular-devkit/build-angular/plugins/karma')
    ],
    client:{
      clearContext: false // leave Jasmine Spec Runner output visible in browser
    },
    // preprocessors: {
    //   '**/*.js': ['chrome']
    // },
    coverageIstanbulReporter: {
      dir: require('path').join(__dirname, 'coverage'), reports: [ 'html', 'lcovonly' ],
      fixWebpackSourcePaths: true
    },
    angularCli: {
      environment: 'dev'
    },
    proxies: {
      // '/kinder': {
      //   'target': 'http://localhost:5000',
      //   'changeOrigin': true
      // },
      '/kinder': 'http://localhost:5000/kinder/'
    },
    // proxies: {
    //   '/kinder': 'http://localhost:5000/'
    // },
    reporters: ['progress', 'kjhtml'],
    port: 9876,
    colors: true,
    logLevel: config.LOG_INFO,
    autoWatch: true,
    browsers: ['Chrome'],
    singleRun: false
  });
};
```
Key was the <em>proxies</em> configuration.
<h3>Test Angular async validator with Jasmine</h3>
```ts
  it('Check age right', (done) => {
    formControl = new FormControl('');
    formControl.setAsyncValidators(
      AgeValidator(1.5, 6, utilService)
    );
    formControl.setValue('2014-01-03');
    setTimeout(function() {
      expect(formControl.status === 'VALID').toBe(true);
      done();
    }, 2000);
  });
```
