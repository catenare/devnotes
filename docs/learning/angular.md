# Learning the Angular Framework
## Resources
* [Angular 2 Fundamentals](http://courses.angularclass.com/courses/enrolled/73288) - Online class with a really good introduction to Angular. Also check out the JavaScript Class. It has a really good introduction to `Webpack`
    * [Github Repo - Retain App](https://github.com/AngularClass/retain-app)
    * Webpack config is out of date (for the latest webpack)
 * [Angular Documentation](https://angular.io/)
 * [Angular & Webpack](https://angular.io/guide/webpack)
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
