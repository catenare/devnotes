# Webpack Configuration

## Configure Webpack
```javascript
const path = require('path')
const webpack = require('webpack')
const HtmlWpPlugin = require('html-webpack-plugin')
const CleanWpPlugin = require('clean-webpack-plugin')
const ExtractWpPlugin = require('extract-text-webpack-plugin')
const autoprefixer = require('autoprefixer')
const atl = require('awesome-typescript-loader')

module.exports = {
  entry: {
    app: './src/assets/js/main.js',
    vendor: './src/assets/js/vendor.js'
  },
  output: {
    path: path.resolve(__dirname, './dist'),
    filename: '[name].bundle.js',
    sourceMapFilename: '[name].bundle.map',
    pathinfo: true
  },
  resolve: {
    extensions: ['.js', '.jsx', '.ts', '.tsx']
  },
  devtool: 'cheap-module-source-map',
  plugins: [
    new HtmlWpPlugin({
      title: 'Learning ES6',
      template: 'src/index.html',
      filename: 'index.html'
    }),
    new CleanWpPlugin(['dist']),
    new ExtractWpPlugin({
      filename: 'styles.css',
      allChunks: true
    }),
    new webpack.HotModuleReplacementPlugin(),
    new atl.CheckerPlugin()
  ],
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /(node_modules|bower_components)/,
        use: {
          loader: 'babel-loader',
          options: {
            presets: [
              ['env',
                {
                  targets: {
                    'browsers': ['last 2 versions', 'ie>=7']
                  }
                }
              ]
            ]
          }
        }
      },
      // {
      //   test: /\.css$/,
      //   include: path.resolve(__dirname, './node_modules/leaflet/dist/leaflet.css'),
      //   use: 'raw-loader'
      // },
      {
        test: /\.css$/,
        exclude: /(node_modules|bower_components)/,
        loaders: ExtractWpPlugin.extract([
          'style-loader/url!file-loader',
          'css-loader'
        ])
      },
      {
        test: /\.ts$/,
        exclude: /(node_modules|bower_components)/,
        use: 'awesome-typescript-loader'
      },
      {
        test: /\.scss$/,
        exclude: /(node_modules|bower_components)/,
        use: ExtractWpPlugin.extract({
          fallback: 'style-loader',
          use: [
            'css-loader',
            {
              loader: 'postcss-loader',
              options:
              {
                plugins: function () {
                  return [autoprefixer]
                }
              }
            },
            'sass-loader'
          ]
        }
        )
      },
      {
        test: /\.(png|svg|jpg|gif)$/,
        exclude: /(node_modules|bower_components)/,
        use: [
          'file-loader?name=images/[name].[ext]'
        ]
      }
    ]
  },
  devServer: {
    hot: true,
    watchOptions: {
      ignored: /node_modules/
    }
  }
}
```
