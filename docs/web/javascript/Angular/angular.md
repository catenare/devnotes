# Angular Framework

## Start a new project
### Using Anular Cli
* ng new [name} --skip-install --style scss
* cd into [name]
* npm install foundation-sites @fortawesome/fontawesome @fortawesome/fontawesome-free-solid @fortawesome/fontawesome-free-webfonts
* `npm install` - install all the packages
### Setup Foundation and FontAwesome
* Copy/create styles folder
* Copy/create foundation settings file
* Copy/create foundation import file
* Edit settings file
  * `@import '~foundation-sites/scss/util/util';`
  * `$fa-font-path: '~@fortawesome/fontawesome-free-webfonts/webfonts';`
* Edit *foundation.scss*
  * `@import '~@fortawesome/fontawesome-free-webfonts/scss/fontawesome';`
  * `@import '~foundation-sites/scss/foundation';`

### Include in styles 
* in styles.scss - `@import './assets/styles/site.scss';`

## Resources
* [Angular Documentation](https://angular.io/)
* [Angular & Webpack](https://angular.io/guide/webpack)
* [Awesome Angular](https://github.com/brillout/awesome-angular-components)
## Notes
* Gotchas:
    * [ExtractTextWebpackPlugin](https://github.com/webpack-contrib/extract-text-webpack-plugin/issues/569) & [[Validation] ajv version mismatch with webpack #524](https://github.com/webpack-contrib/extract-text-webpack-plugin/issues/524)
        * `fallbackloader` should be `fallback`
        * `loader` is now `use`
        * ex: (old) `ExtractTextPlugin.extract({fallbackloader: 'style-loader', loader: 'css-loader?sourceMap'})` should be (new) `ExtractTextPlugin.extract({fallback: 'style-loader', use: 'css-loader?sourceMap'})`
    * [Cannot find name 'require' templateUrl - StackOverflow](https://stackoverflow.com/questions/40372788/cannot-find-name-require-templateurl)
        * `npm install --save-dev @types/node`
        * In `tsconfig.json` 
        
            ```json
                "types": ["node"],
                "typeroots": ["./node_modules/@types"]
            ```
            
        * Restart *webpack-dev-server* - `npm run server:dev`
    * *No Implicit Any* - Change setting `"noImplicitAny"` in `tsconfig.json` to false and restart webpack dev server.
    * `TS2559: Type 'Headers' has no properties in common with type 'RequestOptionsArgs'.` - *RequestOptions* require an object. *{headers: this.headers}*
    * `Uncaught Error: Can't resolve all parameters for NoteService:` - Issue with not having `@Injectable()` on noteservice.
* [Angular Education](https://github.com/timjacobi/angular-education)
