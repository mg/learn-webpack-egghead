# Grouping vendor files with the Webpack Commons Chunk Plugin
[Video](https://egghead.io/lessons/tools-grouping-vendor-files-with-the-webpack-commonschunkplugin)

####

```js
const webpack= require('webpack')
const { resolve } = require('path')

const isProd= process.env.NODE_ENV === 'production'
const isTest= process.env.NODE_ENV === 'test'

module.exports = {
  entry: {
    app: './js/app.js',
    vendor: ['lodash', 'jquery'],
  },
  output: {
    filename: 'bundle.[name].js',     // bundle.vendor.js and bundle.app.js
    path: resolve(__dirname, 'dist'),
    pathinfo: true,
  },
  context: resolve(__dirname, 'src'),
  devtool: isProd ? 'source-map' : 'eval',
  module: {
    loaders: [
      {test: /\.js$/, loader: 'babel!eslint', exclude: /node_modules/},
      {test: /\.css$/, loader: 'style!css'},
    ],
  },
  plugins: [
    isTest ? undefined : new webpack.optimize.CommonsChunkPlugin({
      name: 'vendor',
    }),
  ].filter(p => !!p),
}
```
CommonsChunkPlugin removes all that is in the ``vendor`` bundle from the ``app`` bundle. The ``isTest`` guard is to get Karma working again. Not needed if not using Karma. The filter removes any undefined plugins.
