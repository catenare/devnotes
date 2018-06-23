# Web Development Tools

## Resources
* [Front End Beginner Resources](https://github.com/thedaviddias/Resources-Front-End-Beginner)
* [By People Web Assets Resources](https://www.bypeople.com)

## Tools
* [Emmet](http://emmet.io) - Code editor helper
    * Expand html shortcuts
    * Can really reduce the amount of typing necessary to to create a page.
* [browser-sync](https://browsersync.io/) - Basic local server. Avoid the hassle of Webpack
  * `browser-sync start --server --directory --files "**/*"`
* Images
  * [Placement Images List](https://www.hanselman.com/blog/TheInternetsBestPlaceholderImageSitesForWebDevelopment.aspx)
  * [Hold It](http://www.placehold.it)
* Prototyping tools
  * [Random User Generator](https://randomuser.me/) - get list of users.
  * [UIFaces](http://uifaces.com/) - Faces for user interfaces
  * [CSS Flat Mobile Devices](https://marvelapp.github.io/devices.css/) - Prototype devices in css.
  * [Lists](http://www.lists.design/) - Content for prototyping
*  Combine JS files
  * [Requirejs](http://requirejs.org/) - Using Webpack now
    * For r.js to work (without explicit path) `npm install -g requirejs`
* Generating Color Palettes
  * [Colors Palette Generator](http://www.cssdrive.com/imagepalette/index.php)
  * [Canva Color Palette](https://www.canva.com/color-palette/)
  * [Pictaculous](http://www.pictaculous.com/)
  * [Color Explorer](http://www.colorexplorer.com/imageimport.aspx) - can upload an image

## CSS and SCSS
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

### Video
* [Videvo](https://www.videvo.net/)

## How to
* Parallax
  * [David Walsh - Used initially](https://davidwalsh.name/parallax)
  * [Keith Clark](http://keithclark.co.uk/articles/pure-css-parallax-websites/) - nice 3d effect
  * [w3schools demo](https://www.w3schools.com/howto/tryhow_css_parallax_demo.htm) - Tried this one
  * [Pure Css](https://alligator.io/css/pure-css-parallax/) - 3d effect
* Carousel
  * [Owl Carousel](https://owlcarousel2.github.io/OwlCarousel2/) - image strip carousel
    * [Owl Carousel Fullscreen](https://codepen.io/ingvi/pen/gaOzYe)
    * [Responsive Site Using Owl](http://www.creativebloq.com/web-design/build-responsive-sites-foundation-11513848)
  * [Vegas Fullscreen Slideshow](http://vegas.jaysalvat.com/)
  * [slick](https://kenwheeler.github.io/slick/) - scss for css
