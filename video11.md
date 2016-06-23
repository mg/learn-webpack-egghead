# Expose Modules to Dependencies with Webpack
[Video](https://egghead.io/lessons/tools-expose-modules-to-dependencies-with-webpack)

Install the imports loader
```
npm i --save-dev imports-loader
```

Webpack config:
``` js
module: {
  loaders: [
    {
      test: require.resolve('./src/non_node_modules/iNeedLodash'),
      loader: 'imports?_=lodash',
    }
  ]
}
```

When importing the file, expose what the module needs (e.g. *lodash*).
```js
import './non_node_modules/iNeedLodash'
```
