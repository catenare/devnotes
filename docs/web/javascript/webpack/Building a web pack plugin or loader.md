# Building a web pack plugin or loader
## Create a plugin for HtmlWebpack plugin.
* Want to see if I can build a panini plugin that will work with HtmlWebpackHtml plugin.
## Options
* Try and add a plugin to HtmlWebpack extract plugin.
* Notes:
	* Can add resolveLoader to find local plugins
```
  resolveLoader: {
    modules: [
      'node_modules',
      path.resolve(__dirname, 'loaders')
    ]
  },
```
