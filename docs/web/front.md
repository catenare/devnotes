# Web Development Tools - finding tools that are really useful for editing

## Resources
* [https://frontend.directory](https://frontend.directory/p)

## Web Framework
* [Foundation](http://foundation.zurb.com/)
    * Setup a new project ```foundation new```
* [uikit](https://getuikit.com/v2/index.html)

### Templates
* [CoreUI](http://coreui.io/) - Admin template
* [flakes](http://getflakes.com/) - Design and frontend framework for dashboard.
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