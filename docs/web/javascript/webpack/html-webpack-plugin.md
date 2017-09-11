# Notes About HTML Webpack Plugin
* [Documentation](https://github.com/jantimon/html-webpack-plugin)
## My Notes
* Can use Handlebars templates for pages.
* Can include partials too in the main index.hbs file.
* Benefits
    * Can now use webpack rather than foundation for my complete work process.
    * Building mostly single page apps anyway so including foundation partials is a no brainer.
    * Can replace foundation tools with my tools while still leveraging their infrastructure.
    * Can focus on using webpack for everything.

* Webpack Config
```js
new HtmlWebpackPlugin({
      title: 'Foundation proto',
      template: 'src/index/index.hbs',
      filename: 'index.html'
    }),
```
* Directory layout
    * index/index.hbs
    * index/partial.hbs
* *handlebars-loader* already included.
* Showing the correct title `<title>{{htmlWebpackPlugin.options.title}}</title>`
