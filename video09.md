# Optimize React size and performance with Webpack Production Plugins
[Video](https://egghead.io/lessons/tools-optimize-react-size-and-performance-with-webpack-production-plugins)

#### Stop using default production plugins by removing ``-p`` flag to avoid double minification
``` json
{
  "build:prod": "webpack --env.prod",
}
```

#### Add production plugins into Webpack configuration
``` js
const webpack = require('webpack')
const {resolve} = require('path')

module.exports = env => {

  const addPlugin = (add, plugin) => add ? plugin : undefined
  const ifProd = plugin => addPlugin(env.prod, plugin)
  const removeEmpty = array => array.filter(i => !!i)

  return {
    ...
    plugins: removeEmpty([
      // doesn't save anything in this small app. npm@3 mostly takes care of this
      ifProd(new webpack.optimize.DedupePlugin()),
      // saves a couple of kBs
      ifProd(new webpack.LoaderOptionsPlugin({
        minimize: true,
        debug: false,
        quiet: true,
      })),
      // saves 65 kB with Uglify!! Saves 38 kB without
      ifProd(new webpack.DefinePlugin({
        'process.env': {
          NODE_ENV: '"production"',
        },
      })),
      // saves 711 kB!!
      ifProd(new webpack.optimize.UglifyJsPlugin({
        compress: {
          screw_ie8: true, // eslint-disable-line
          warnings: false,
        },
      })),
    ])
  }
}
```
