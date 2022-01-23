---
title: foundation
updated: 2020-09-10 22:07:13Z
created: 2020-09-10 22:07:13Z
---

# Foundation for Sites Notes

* Using [foundation from zurb](http://foundation.zurb.com/)
  1. Install foundation-cli - `npm install --global foundation-cli`
  1. Create new project -  `foundation new --framework sites --template zurb`
    * Use `foundation-zurb-template`
  1. ~~Install building block - `foundation kits install news`~~
  1. `foundation watch`

## Panini
* [Zurb University Documentation](https://zurb.com/university/lessons/the-main-ingredients-of-panini-layouts-pages-and-partials)

## Other Packages
* fontawesome
* eslint

## Setup eslint
1. `npm install eslint`
1. `node_modules/.bin/eslint --init`
    * Select *standard*

## Adding font-awesome to your foundation site
[HowTo: Foundation 6 Font Awesome and other asset fonts](http://foundation.zurb.com/forum/posts/46991-howto-foundation-6-font-awesome-and-other-asset-fonts)
* `npm install font-awesome`
* Modify *config.yml*
```yaml
# Gulp will reference these paths when it copies files
PATHS:
  # Path to dist folder
  dist: "dist"
  fonts:
    - "node_modules/@fortawesome/fontawesome-free/webfonts"
  sass:
    - "node_modules/foundation-sites/scss"
    - "node_modules/motion-ui/src"
```
* Modify *gulpfile.js*
```javascript
'use strict'

const gulp = require('gulp');
const panini = require('panini');
const sherpa = require('style-sherpa');
const rimraf = require('rimraf');
const browserSync = require('browser-sync');
const gulpwebpack = require('webpack-stream');
const webpack = require('webpack');
const webpackConfig = require('./webpack.config.js');
// sass
const sass = require('gulp-sass');
const sassLint = require('gulp-sass-lint');
const postcss = require('gulp-postcss');
const autoprefixer = require('autoprefixer');
const sourcemaps = require('gulp-sourcemaps');

// webpackConfig.watch = true;

const webpackDevMiddleWare = require('webpack-dev-middleware');
const webpackHotMiddleWare = require('webpack-hot-middleware');

const webpackCompiler = webpack(webpackConfig);

const yaml = require('js-yaml');
const fs = require('fs');



// Load settings from settings.yml
const {
  PATHS
} = loadConfig();

const server = browserSync.create();


function loadConfig() {
  let ymlFile = fs.readFileSync('config.yml', 'utf8');
  return yaml.load(ymlFile);
}

// Build the index.html files for the final result
gulp.task('build',
  gulp.series(clean, gulp.parallel(buildSass, fonts, pages, images), styleGuide));

// Build the site, run the server, and watch for file changes
gulp.task('default',
  gulp.series(clean, gulp.parallel(buildSass, fonts, mywebpack, pages, images), styleGuide, serve, watch)
)


// add webpack stream
function mywebpack() {
  return gulp.src('src/main.js')
    .pipe(gulpwebpack(webpackConfig, webpack))
    .pipe(gulp.dest('dist/assets/'));
}

// scss compile
function buildSass() {
  return gulp.src(['src/assets/styles/styles.scss'])
    .pipe(sourcemaps.init())
    .pipe(sass({
      includePaths: PATHS.sass
    }).on('error', sass.logError))
    .pipe(postcss([autoprefixer()]))
    .pipe(sourcemaps.write())
    .pipe(gulp.dest(PATHS.dist + '/assets'))
}

// copy fonts
// Copy fonts to the "dist" folder
function fonts() {
  return gulp.src(PATHS.fonts + '/*.*')
    .pipe(gulp.dest(PATHS.dist + '/assets/fonts'));
}

// browser-sync
function serve(done) {
  server.init({
    server: {
      baseDir: "./dist"
    },
    middleware: [
      webpackDevMiddleWare(webpackCompiler),
      webpackHotMiddleWare(webpackCompiler)
    ]
  });
  done();
}

function reload(done) {
  server.reload();
  done();
}

// Copy images to the "dist" folder
// In production, the images are compressed
function images() {
  return gulp.src('src/app/img/**/*')
    .pipe(gulp.dest(PATHS.dist + '/img'))
}

// Generate a style guide from the Markdown content and HTML template in styleguide/
function styleGuide(done) {
  sherpa('src/styleguide/index.md', {
    output: PATHS.dist + '/styleguide.html',
    template: 'src/styleguide/template.html'
  }, done)
}

// Delete the "dist" folder
// This happens every time a build starts
function clean(done) {
  rimraf(PATHS.dist, done)
}

// Copy page templates into finished HTML files
function pages() {
  return gulp.src('src/html/pages/**/*.{html,hbs,handlebars}')
    .pipe(panini({
      root: 'src/html/pages/',
      layouts: 'src/html/layouts/',
      partials: 'src/html/partials/',
      data: 'src/html/data/',
      helpers: 'src/html/helpers/'
    }))
    .pipe(gulp.dest(PATHS.dist))
}

// Load updated HTML templates and partials into Panini
function resetPages(done) {
  panini.refresh()
  done()
}

// Watch for changes to static assets, pages, Sass, and JavaScript
function watch() {
  // gulp.watch('src/html/pages/**/*.html').on('all', gulp.series(resetPages, pages, reload));
  gulp.watch('src/html/{layouts,partials,pages,helpers}/**/*.html').on('all', gulp.series(resetPages, pages, reload));
  gulp.watch('src/html/data/*.yml').on('all', gulp.series(resetPages, pages, reload));
  gulp.watch('src/styleguide/*.*').on('all', gulp.series(styleGuide, reload));
  gulp.watch('src/app/img/**/*').on('all', gulp.series(images, reload));
  gulp.watch('src/**/*.js').on('all', gulp.series(mywebpack, reload));
  gulp.watch('src/assets/styles/*.scss').on('all', gulp.series(mywebpack, reload));
  // gulp.watch('src/assets/styles/*.scss').on('all', gulp.series(buildSass, reload));
}

```
* *Add*
```javascript
// Copy fonts to the "dist" folder
function fonts() {
  return gulp.src(PATHS.fonts)
    .pipe(gulp.dest(PATHS.dist + '/assets/fonts'));
}
```
* *Modify*
```javascript
// Watch for changes to static assets, pages, Sass, and JavaScript
function watch() {
  gulp.watch(PATHS.assets, copy);
  gulp.watch('src/pages/**/*.html').on('all', gulp.series(pages, browser.reload));
  gulp.watch('src/{layouts,partials}/**/*.html').on('all', gulp.series(resetPages, pages, browser.reload));
  gulp.watch('src/assets/scss/**/*.scss').on('all', gulp.series(sass, browser.reload));
  gulp.watch('src/assets/js/**/*.js').on('all', gulp.series(javascript, browser.reload));
  gulp.watch('src/assets/img/**/*').on('all', gulp.series(images, browser.reload));
  gulp.watch('src/assets/fonts/**/*').on('all', gulp.series(fonts, browser.reload));
  gulp.watch('src/styleguide/**').on('all', gulp.series(styleGuide, browser.reload));
}
```
* Create *_custom.scss* and import into *app.css*
* Import *fontawesome* into *_custom.scss*
```scss
$fa-font-path: '/assets/fonts'; //set path for fonts

@import 'node_modules/@fortawesome/fontawesome-free/scss/fontawesome';
@import "node_modules/@fortawesome/fontawesome-free/scss/fa-solid";
@import "node_modules/@fortawesome/fontawesome-free/scss/fa-brands";
@import "node_modules/@fortawesome/fontawesome-free/scss/fa-regular";
```

* `npm run dev`

## Foundation 6 with @fortawesome fonts and webpack - If using Webpack for everything. Gulp version works pretty well.
Using *webpack* rather than *gulp* to manage scss and fonts. Webpack uses the url-loader to grab the fonts. Eliminates a function I'll have to write in gulp.

* `settings.scss`
    * `@import '~foundation-sites/scss/util/util';` - Change import statement to point to *node_modules*
    * `$fa-font-path: '~@fortawesome/fontawesome-free/webfonts';` - Set the *$fa-font-path* so **fontawesome* can find the web fonts.
* `styles.scss` - main import file with all foundation imports
    * `@import '~foundation-sites/scss/foundation';` - import foundation from node_modules.
    * `@import '~motion-ui/src/motion-ui';` - Make sure we're only importing the scss for motion-ui.
    * Import the fontawesome v5 scss and font scss.
        * `@import '~@fortawesome/fontawesome-free/scss/fontawesome';`
        * `@import "~@fortawesome/fontawesome-free/scss/fa-solid";` fas
        * `@import "~@fortawesome/fontawesome-free/scss/fa-brands";` - fab
        * `@import "~@fortawesome/fontawesome-free/scss/fa-regular";` - fa
        * `@import 'local';` - Our local scss - imports our custom components.
* Import into our `main.js` file. Our entry point for our webpack application.
    * `import "@/assets/styles/styles.scss";` - importing our main styles file.
* *wepack.config.js*
    * Takes care of copying the fonts over.
```js
{
    test: /\.(png|jpe?g|gif|woff|woff2|eot|ttf|svg)$/,
    loader: 'url-loader?limit=100000'
  }
```
* Compiles our scss to css. Extracts the css so our static html page can use it. scss section compiles scss to css for us.
```js
const pluginConfig = [
  new MiniCssExtractPlugin({
    filename: '[name].css',
    chunkFilename: '[id].css'
  })
]

const moduleConfigBase = [{
    test: /\.(sa|sc|c)ss$/,
    exclude: /node_modules/,
    use: [
      // devMode ? 'style-loader' : MiniCssExtractPlugin.loader,
      MiniCssExtractPlugin.loader,
      'css-loader',
      'postcss-loader',
      'sass-loader'
    ]
  },
  {
    test: /\.js$/,
    exclude: /(node_modules)/,
    loader: 'babel-loader'
  },
  {
    test: /\.tsx?$/,
    exclude: /(node_modules)/,
    loader: 'awesome-typescript-loader'
  },
  {
    test: /\.(png|jpe?g|gif|woff|woff2|eot|ttf|svg)$/,
    loader: 'url-loader?limit=100000'
  }
]
```
* Using webpack in gulp. Watch scss and run webpack whenever it changes.
```js
const gulpwebpack = require('webpack-stream');
const webpack = require('webpack');
const webpackConfig = require('./webpack.config.js');

// add webpack stream
function mywebpack() {
  return gulp.src('src/main.js')
    .pipe(gulpwebpack(webpackConfig, webpack))
    .pipe(gulp.dest('dist/assets/'));
}
gulp.watch('src/assets/styles/*.scss').on('all', gulp.series(mywebpack, reload));
```
## Zurb Panini Notes
* Partials are your friends. 
    * Inserting values `{{>partion value="value"}}`
    * Use `{{#each}}` to iterate over array data
    * Use `filename.variable` to access data from file in data folder
  * [Custom Global Panini Variables](https://github.com/zurb/panini/issues/51)
```js
// src/data/globals.js
module.exports = {
  production: process.env.NODE_ENV === 'production',
};
```
In handlbars template
```h
{{#if globals.production}}
  <p>Production!</p>
{{else}}
  <p>Not production.</p>
{{/if}}
```

## Create background-image slide show with orbit
* [Stack Overflow Responsive Background Image](https://stackoverflow.com/questions/21421062/responsive-background-image)
* [Full Page Background Image](https://css-tricks.com/perfect-full-page-background-image/)
* See the front. [Front](front/#carousel)

## Notes
* Using mixins for grid
```scss
footer {
  @include xy-grid;
  @include xy-grid-layout(4, 'div');
}
```
* Result
```html
 <footer>
      <section class="footer">
        <div>
          <h2>my title</h2>
          <img src="http://via.placeholder.com/200x200" alt="image">
        </div>
        <div>
          <h2>experience</h2>
          <ul>
            <li>experience</li>
            <li>experience</li>
            <li>experience</li>
          </ul>
        </div>
        <div>
          <h2>skills</h2>
          <ul>
            <li>skills</li>
            <li>skills</li>
            <li>skills</li>
          </ul>
        </div>
        <div>
          <h2>contact me</h2>
        </div>
        </section>
</footer>
```
## Notes
* Trying to organize my CSS/Styles. Get an overview of what I'm doing. Too many different options.
    * StyleSherpa - Gives you an overview of all your styles. Forces you to at least have some type of plan.