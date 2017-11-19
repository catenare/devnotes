# Foundation for Sites Notes

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
# Your project's server will run on localhost:xxxx at this port
PORT: 8008

# Autoprefixer will make sure your CSS works with these browsers
COMPATIBILITY:
  - "last 2 versions"
  - "ie >= 9"
  - "ios >= 7"

# UnCSS will use these settings
UNCSS_OPTIONS:
  html:
    - "src/**/*.html"
  ignore:
    - !!js/regexp .foundation-mq
    - !!js/regexp ^\.is-.*

# Gulp will reference these paths when it copies files
PATHS:
  # Path to dist folder
  dist: "dist"  
  # Paths to static assets that aren't images, CSS, or JavaScript
  assets:
    - "src/assets/**/*"
    - "!src/assets/{img,js,scss,fonts}/**/*"
  # Path to fonts
 fonts:
    - "src/assets/fonts/*"
    - "node_modules/font-awesome/fonts/*"
  # Paths to Sass libraries, which can then be loaded with @import
  sass:
    - "node_modules/foundation-sites/scss"
    - "node_modules/motion-ui/src"
    - "node_modules/font-awesome/scss"
  # Paths to JavaScript entry points for webpack to bundle modules
  entries:
    - "src/assets/js/app.js"
```
* Modify *gulpfile.babel.js*
```javascript
// Build the "dist" folder by running all of the below tasks. Add fonts
gulp.task('build',
 gulp.series(clean, gulp.parallel(pages, sass, javascript, images, fonts, copy), styleGuide));
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
@import "font-awesome";
```
* `foundation watch` or `npm start`

## Zurb Panini Notes
* Partials are your friends. 
    * Inserting values into partions `{{>partion value="value"}}`
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
