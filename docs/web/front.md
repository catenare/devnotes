# Web Development Tools - finding tools that are really useful for editing

## Resources
* [https://frontend.directory](https://frontend.directory/p)
* [Front End Beginner Resources](https://github.com/thedaviddias/Resources-Front-End-Beginner)

### Web Framework
* [Foundation](http://foundation.zurb.com/)
    * Setup a new project ```foundation new```
* [uikit](https://getuikit.com/v2/index.html)

### Templates
* [CoreUI](http://coreui.io/) - Admin template
* [flakes](http://getflakes.com/) - Design and frontend framework for dashboard.
* [Themezy](https://www.themezy.com/)
* [Templated](https://templated.co/)

### Fonts
* [Web Font Loading Recipes](https://github.com/zachleat/web-font-loading-recipes)

## Tools
### HTML tools
* [Emmet](http://emmet.io) 
    * Expand html shortcuts
    * Can really reduce the amount of typing necessary to to create a page.
### Image Sources
* [Placement Images List](https://www.hanselman.com/blog/TheInternetsBestPlaceholderImageSitesForWebDevelopment.aspx)
* [Hold It](http://www.placehold.it)
### Prototype tools
* [Random User Generator](https://randomuser.me/) - get list of users.
* [UIFaces](http://uifaces.com/) - Faces for user interfaces
* [CSS Flat Mobile Devices](https://marvelapp.github.io/devices.css/) - Prototype devices in css.
* [Lists](http://www.lists.design/) - Content for prototyping

### Local static file server
* [browser-sync](https://browsersync.io/)
* Node.js tool 
* ```browser-sync start --server --directory --files "**/*"```

### Combine JS files
* [Requirejs](http://requirejs.org/)
* For r.js to work (without explicit path) ```npm install -g requirejs```

## CSS
### Sass Notes
* Using sassc and libsass
* [libSass](https://github.com/sass/libsass)
* Export the library location so node-sass can use it.

#### Compiling compass sass config.rb file
* Compiling compass sass with sass c library.
	* *sass --compass sass/styles.scss test,css* - seems to read the compass config.rb file to find paths.

### Maintainable CSS
* [BEM (block, element, modifier) methodology](https://en.bem.info/methodology/quick-start/)

### Parallax
* [David Walsh - Used initially](https://davidwalsh.name/parallax)
* [Keith Clark](http://keithclark.co.uk/articles/pure-css-parallax-websites/) - nice 3d effect
* [w3schools demo](https://www.w3schools.com/howto/tryhow_css_parallax_demo.htm) - Tried this one
* [Pure Css](https://alligator.io/css/pure-css-parallax/) - 3d effect

### Carousel
* [Owl Carousel](https://owlcarousel2.github.io/OwlCarousel2/) - image strip carousel
    * [Owl Carousel Fullscreen](https://codepen.io/ingvi/pen/gaOzYe)
    * [Responsive Site Using Owl](http://www.creativebloq.com/web-design/build-responsive-sites-foundation-11513848)
* [Vegas Fullscreen Slideshow](http://vegas.jaysalvat.com/)
* [slick](https://kenwheeler.github.io/slick/) - scss for css

### Fonts
* [Awesome Fontstacks](http://www.awesome-fontstacks.com) - fonts that go together
* [Fonts Squirrel](https://www.fontsquirrel.com)

### Other
* [By People Web Assets Resources](https://www.bypeople.com)

### Icons
* [Feather Icons](https://feathericons.com/) - Install with `npm install feather-icons`

# Static Web Page Development
## Setting for static page development
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

## Tools

### [Emmet](http://emmet.io) 
* Expand html shortcuts
* Can really reduce the amount of typing necessary to to create a page.

### Local static file server
* [browser-sync](https://browsersync.io/)
* Node.js tool 
* ```browser-sync start --server --directory --files "**/*"```

### Combine JS files
* [Requirejs](http://requirejs.org/)
* For r.js to work (without explicit path) ```npm install -g requirejs```

## Web Framework
* [Foundation](http://foundation.zurb.com/)
* Setup a new project ```foundation new```

## Sass Notes
* Using sassc and libsass
* [libSass](https://github.com/sass/libsass)
* Export the library location so node-sass can use it.

### Compiling compass sass config.rb file
* Compiling compass sass with sass c library.
	* *sass --compass sass/styles.scss test,css* - seems to read the compass config.rb file to find paths.
* Now use webpack

## Maintainable CSS
* [BEM (block, element, modifier) methodology](https://en.bem.info/methodology/quick-start/)

## Resources
* [https://frontend.directory](https://frontend.directory/p)

### Loaders
* CSS Loaders
    * [CSS Spin](https://webkul.github.io/csspin/)
    * [CSS Loader](http://www.raphaelfabeni.com.br/css-loader/)
    * [SVG Loaders](http://samherbert.net/svg-loaders/)
    * [CSS Loader animations](https://connoratherton.com/loaders)

## Generating Color Palettes
* [Colors Palette Generator](http://www.cssdrive.com/imagepalette/index.php)
* [Canva Color Palette](https://www.canva.com/color-palette/)
* [Pictaculous](http://www.pictaculous.com/)

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
