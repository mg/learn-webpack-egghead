# Hashing with Webpack for long therm caching
[Video](https://egghead.io/lessons/tools-hashing-with-webpack-for-long-term-caching)

Autogenerate a hash string to use to name the bundle.js so we can aggressively cache the js bundle.

```
npm i --save-dev html-webpack-plugin
```

#### Webpack config
```js
const { resolve }= require('path')
const HtmlWebpackPlugin= require('html-webpack-plugin')

module.exports= env => {
  return {
    output: {
      filename: 'bundle[chunkhash].js',
    },
    context: resolve(__dirname, 'src'),
    plugins: [
      new HtmlWebpackPlugin({
        template: './index.html'    // src/index.html because of context == src
      }),
    ]
  }
}
```

Remove any reference to bundle from ``index.html``
