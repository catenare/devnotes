# Creating a static page
* Using [foundation from zurb](http://foundation.zurb.com/)
## Installation - [Foundation for Sites](http://foundation.zurb.com/sites)
1. Install foundation-cli - `npm install --global foundation-cli`
1. Create new project -  `foundation new --framework sites --template zurb`
    * Use `foundation-zurb-template`
1. ~~Install building block - `foundation kits install news`~~
1. `foundation watch`
## Resources
* [Placement Images List](https://www.hanselman.com/blog/TheInternetsBestPlaceholderImageSitesForWebDevelopment.aspx)
    * [Hold It](http://www.placehold.it)

## Notes
### Zurb Panini Notes
* Partials are your friends. 
    * Inserting values into partions `{{>partion value="value"}}`
    * Use `{{#each}}` to iterate over array data
    * Use `filename.variable` to access data from file in data folder
### Adding font-awesome to your foundatio site
[HowTo: Foundation 6 Font Awesome and other asset fonts](http://foundation.zurb.com/forum/posts/46991-howto-foundation-6-font-awesome-and-other-asset-fonts)
* `bower install fontawesome --save`
* Modify *config.yml*
```yaml
  assets:
    - "src/assets/**/*"
    - "!src/assets/{img,js,scss,fonts}/**/*"
  fonts:
    - "src/assets/fonts/*"
    - "bower_components/font-awesome/fonts/*"
  # Paths to Sass libraries, which can then be loaded with @import
  sass:
    - "bower_components/foundation-sites/scss"
    - "bower_components/motion-ui/src"
    - "bower_components/font-awesome/scss"
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
  gulp.watch('bower_components/font-awesome/fonts/*').on('all', gulp.series(fonts, browser.reload));
  gulp.watch('src/styleguide/**').on('all', gulp.series(styleGuide, browser.reload));
}
```
* Modify *app.css* add
```scss
@import "font-awesome";
```
* `foundation watch` or `npm start`




