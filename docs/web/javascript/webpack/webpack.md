# Webpack Basic Configuration

## Configure Webpack
```javascript
const path = require('path')
const webpack = require('webpack')
const BabiliPlugin = require('babili-webpack-plugin')
const CleanWebPackPlugin = require('clean-webpack-plugin')
const combineLoaders = require('webpack-combine-loaders')
const ExtractTextPlugin = require('extract-text-webpack-plugin')
const StylelintPlugin = require('stylelint-webpack-plugin')
const UglifyJsPlugin = require('uglifyjs-webpack-plugin')
const HtmlWebpackPlugin = require('html-webpack-plugin')
const vendorPackages = require('./package.json')
const { CheckerPlugin } = require('awesome-typescript-loader')

const outputDir = path.join(__dirname, 'dist')

const pluginConfig = [
  new HtmlWebpackPlugin(
    {
      title: 'Kinder Admin',
      template: './src/index.ejs'
    }
  ),
  new webpack.DefinePlugin({
    __STATE__: JSON.stringify(process.env.NODE_ENV)
  }),
  new CheckerPlugin()
]

const moduleConfigBase = [
  {
    test: /\.html$/,
    loader: 'html-loader'
  },
  {
    test: /\.js$/,
    exclude: /(node_modules)/,
    loader: 'babel-loader'
  },
  {
    test: /\.tsx?$/,
    exclude: /(node_modules)/,
    use: [
      { loader: 'babel-loader' },
      { loader: 'awesome-typescript-loader' }
    ]
  },
  {
    test: /\.(png|jpe?g|gif|woff|woff2|eot|ttf|svg)$/,
    loader: 'url-loader?limit=100000'
  },
  {
    test: /\.vue$/,
    loader: 'vue-loader',
    options: {
      loaders: {
        scss: ['vue-style-loader', {
          loader: 'css-loader',
          options: {
            minimize: false,
            sourceMap: false,
            url: true
          }
        },
        {
          loader: 'sass-loader',
          options: {
            includePaths: ['src/assets/styles'],
            data: '@import "src/assets/styles/site";',
            sourceMap: false
          }
        }
        ],
        ts: 'awesome-typescript-loader'
      }
    }
  }
]

const moduleConfigDev = [
  {
    test: /\.scss$/,
    exclude: /(node_modules)/,
    use: [
      { loader: 'style-loader' },
      { loader: 'css-loader' },
      { loader: 'postcss-loader' },
      { loader: 'sass-loader' }
    ]
  },
  {
    test: /\.css$/,
    exclude: /(node_modules)/,
    use: [
      { loader: 'style-loader' },
      { loader: 'css-loader' },
      { loader: 'postcss-loader' }
    ]
  }
]

const moduleConfigProd = [
  {
    test: /\.scss$/,
    use: ExtractTextPlugin.extract({
      fallback: 'style-loader',
      use: combineLoaders([
        {
          loader: 'css-loader'
        },
        {
          loader: 'postcss-loader'
        },
        {
          loader: 'sass-loader'
        }
      ])
    })
  },
  {
    test: /\.css$/,
    use: ExtractTextPlugin.extract({
      fallback: 'style-loader',
      use: combineLoaders([
        {
          loader: 'css-loader'
        },
        {
          loader: 'postcss-loader'
        }
      ])
    })
  }
]

const serverConfig = {
  contentBase: outputDir,
  compress: true,
  open: false,
  port: 9000,
  historyApiFallback: {
    verbose: true,
    disableDotRule: true
  }
}

const webpackConfig = {
  entry: {
    app: './src/app/main.ts',
    vendor: Object.keys(vendorPackages.dependencies).filter(name => (name !== 'font-awesome' && name !== 'foundation-sites' && name !== '@fortawesome/fontawesome-free-webfonts'))
  },
  output: {
    path: outputDir,
    filename: '[name].js'
  },
  resolve: {
    extensions: ['.html', '.ts', '.tsx', '.js', '.json', '.vue'],
    alias: {
      'vue$': 'vue/dist/vue.esm.js',
      '@': path.resolve('src')
    }
  },
  plugins: pluginConfig,
  devServer: serverConfig
}

if (process.env.NODE_ENV === 'production') {
  webpackConfig.plugins = (webpackConfig.plugins || []).concat([
    new BabiliPlugin({}),
    new CleanWebPackPlugin([outputDir]),
    new ExtractTextPlugin({
      filename: '[name].css',
      allChunks: true
    }),
    new webpack.optimize.CommonsChunkPlugin({
      name: 'vendor',
      async: true,
      minChunks: Infinity
    }),
    new StylelintPlugin(
      {syntax: 'scss', emitErrors: false, lintDirtyModulesOnly: true}
    ),
    new UglifyJsPlugin({
      test: /\.js($|\?)/i
    }),
    new webpack.LoaderOptionsPlugin({
      minimize: true
    })
  ])
  webpackConfig.module = { rules: moduleConfigBase.concat(moduleConfigProd) }
  webpackConfig.devtool = '#source-map'
} else {
  /* Development */
  webpackConfig.module = { rules: moduleConfigBase.concat(moduleConfigDev) }
  webpackConfig.devtool = 'cheap-module-source-map'
}

module.exports = webpackConfig
```
