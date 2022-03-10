# Web Development Tools

## Resources
* [Front End Beginner Resources](https://github.com/thedaviddias/Resources-Front-End-Beginner)
* [By People Web Assets Resources](https://www.bypeople.com)

# Asset management for web
## Cloudinary - free account available
* [Cloudinary](https://cloudinary.com/console)

## ClipArt
* [Open ClipArt](https://openclipart.org/)

## Other
* [SVG Playing Cards](http://svg-cards.sourceforge.net/)

# Tools
* [Emmet](http://emmet.io) - Code editor helper
    * Expand html shortcuts
    * Can really reduce the amount of typing necessary to to create a page.
* [browser-sync](https://browsersync.io/) - Basic local server. Avoid the hassle of Webpack
  * `browser-sync start --server --directory --files "**/*"`
* **Images**
  * [Placement Images List](https://www.hanselman.com/blog/TheInternetsBestPlaceholderImageSitesForWebDevelopment.aspx)
  * [Hold It](http://www.placehold.it)
* **Prototyping tools**
  * [Random User Generator](https://randomuser.me/) - get list of users.
  * [UIFaces](http://uifaces.com/) - Faces for user interfaces
  * [CSS Flat Mobile Devices](https://marvelapp.github.io/devices.css/) - Prototype devices in css.
  * [Lists](http://www.lists.design/) - Content for prototyping
* **Combine JS files**
  * [Requirejs](http://requirejs.org/) - Using Webpack now
    * For r.js to work (without explicit path) `npm install -g requirejs`
* **Generating Color Palettes**
  * [Colors Palette Generator](http://www.cssdrive.com/imagepalette/index.php)
  * [Canva Color Palette](https://www.canva.com/color-palette/)
  * [Pictaculous](http://www.pictaculous.com/)
  * [Color Explorer](http://www.colorexplorer.com/imageimport.aspx) - can upload an image

# CSS and SCSS
* Using sassc and libsass
* [libSass](https://github.com/sass/libsass)
* Export the library location so node-sass can use it.
* Compiling compass sass with sass c library.
	* *sass --compass sass/styles.scss test,css* - seems to read the compass config.rb file to find paths.
* Maintainable CSS
  * [BEM (block, element, modifier) methodology](https://en.bem.info/methodology/quick-start/)
* CSS Loaders
    * [CSS Spin](https://webkul.github.io/csspin/)
    * [CSS Loader](http://www.raphaelfabeni.com.br/css-loader/)
    * [SVG Loaders](http://samherbert.net/svg-loaders/)
    * [CSS Loader animations](https://connoratherton.com/loaders)

## Resources
* [Fixed Menu](https://www.w3schools.com/howto/howto_css_fixed_menu.asp) - Fix menu to the top
* [CssDB](http://cssdb.co/)
* [Animista](http://animista.net/play)
<!-- * [CSS3 Generator](http://css3generator.com/) -->
* [Atomic CSS](https://acss.io/) - css for component-based frameworks

## Seo
* [MegaTags](https://megatags.co/) - OpenGraph tag generator

## Linting CSS and SCSS
* Install stylelint, stylelint-config-standard
    * `npm install stylelint stylelint-config-standard`
* Add *stylelint* in *package.json*
```json
  "stylelint": {
    "plugins": [
      "stylelint-scss"
    ],
    "extends": "stylelint-config-standard"
  }
```
### Stylelint Notes
* [stylelint-config-sass-guidelines](https://github.com/bjankord/stylelint-config-sass-guidelines) - scss stylelint rules
* [Stylelint webpack plugin](https://github.com/JaKXz/stylelint-webpack-plugin)
    * `const StylelintPlugin = require('stylelint-webpack-plugin')`
    * `new StylelintPlugin({syntax: 'scss', emitErrors: false, lintDirtyModulesOnly: true})`
* [stylelint](https://stylelint.io/)
    * `npm install --save-dev stylelint stylelint-config-sass-guidelines stylelint-config-standard stylelint-scss stylelint-webpack-plugin`
* config in *package.json*
```json
"stylelint": {
    "plugins: [
        "stylelint-scss"
}
```
### PostCSS Notes
* Config notes: [Postcss Cli](https://www.npmjs.com/package/postcss-cli) - Config section explains *postcss.config.js*
	* [Postcss Next in Webpack](https://blog.envylabs.com/webpack-2-postcss-cssnext-fdcd2fd7d0bd) - config *postcss.config.js*
## Font Awesome

* Font Awesome icon as part of before pseudo class using scss. [StackOverflow Font Awesome Icon as CSS Content](https://stackoverflow.com/questions/20782368/use-font-awesome-icon-as-css-content)
```css
.a:after {
    // Import mixin from font-awesome/scss/mixins.scss
    @include fa-icon();

    // Use icon variable from font-awesome/scss/variables.scss
    content: $fa-var-exclamation-triangle;
}
```

## Fonts
* [Web Font Loading Recipes](https://github.com/zachleat/web-font-loading-recipes)
* [Awesome Fontstacks](http://www.awesome-fontstacks.com) - fonts that go together
* [Fonts Squirrel](https://www.fontsquirrel.com)

## Icons - Free
* [Open Iconic](https://useiconic.com/open/)
* [Octicons](https://octicons.github.com/)
* [Entypo](http://www.entypo.com/)
* [Bytesize Icons](https://github.com/danklammer/bytesize-icons)
* [Material Icons](https://material.io/icons/)
* [Ionicons](http://ionicons.com/)
* [Dripicons](http://demo.amitjakhu.com/dripicons/)
* [Ikons](http://ikons.piotrkwiatkowski.co.uk/)
* [SmartIcons](http://glyph.smarticons.co/)
* [Feather Icons](https://feathericons.com/) - Install with `npm install feather-icons`

### Web Framework
* [Foundation](http://foundation.zurb.com/)
    * Setup a new project ```foundation new```
* [uikit](https://getuikit.com/v2/index.html)
* [Clarity Design System](https://vmware.github.io/clarity/)

### Templates
* [CoreUI](http://coreui.io/) - Admin template
* [flakes](http://getflakes.com/) - Design and frontend framework for dashboard.
* [Themezy](https://www.themezy.com/)
* [Templated](https://templated.co/)
* Admin tools
	* [Grafana](https://grafana.com/) - analytics and monitoring visualization
* [Framework7](https://framework7.io/) - mobile web template
* [W3 Layouts](https://w3layouts.com/)
* [Freshdesign Templates](https://www.freshdesignweb.com/best-church-website-templates/)

### Video
* [Videvo](https://www.videvo.net/)

## How to
* **Parallax**
  * [David Walsh - Used initially](https://davidwalsh.name/parallax)
  * [Keith Clark](http://keithclark.co.uk/articles/pure-css-parallax-websites/) - nice 3d effect
  * [w3schools demo](https://www.w3schools.com/howto/tryhow_css_parallax_demo.htm) - Tried this one
  * [Pure Css](https://alligator.io/css/pure-css-parallax/) - 3d effect
* **Carousel**
  * [Owl Carousel](https://owlcarousel2.github.io/OwlCarousel2/) - image strip carousel
    * [Owl Carousel Fullscreen](https://codepen.io/ingvi/pen/gaOzYe)
    * [Responsive Site Using Owl](http://www.creativebloq.com/web-design/build-responsive-sites-foundation-11513848)
  * [Vegas Fullscreen Slideshow](http://vegas.jaysalvat.com/)
  * [slick](https://kenwheeler.github.io/slick/) - scss for css

# Web Authentication
## JWT
* [Jason Web Tokens](https://jwt.io/introduction/)

## Rest
* Response Codes: [Response Codes](https://blog.restcase.com/rest-api-error-codes-101/)
* HTTP Status Codes: [HTTP Status Codes](http://www.restapitutorial.com/httpstatuscodes.html)
* Details:
    * 200 OK
    * 201 Created
    * 202 Accepted
    * 304 Not Modified
    * 400 Bad Request
    * 401 Not Authorized
    * 403 Forbidden
    * 404 Not Found
    * 500 Internal Server Error
    * 501 Not Implemented
    * 503 Service Not Available

## Web Colors
* I'm not a designer so need something very basic.
    * [Web Developer Color Guide](https://www.smashingmagazine.com/2016/04/web-developer-guide-color/)
        * White
        * dark gray
        * light gray
        * Base color
        * Accent color
* [Color Calculator](https://www.sessions.edu/color-calculator/)
