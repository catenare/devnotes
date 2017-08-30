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

# Web Development Tools - finding tools that are really useful for editing

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

## Generating Color Palettes
* [Colors Palette Generator](http://www.cssdrive.com/imagepalette/index.php)
* [Canva Color Palette](https://www.canva.com/color-palette/)
* [Pictaculous](http://www.pictaculous.com/)
