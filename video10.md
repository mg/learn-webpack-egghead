# Import a non ES6 Module with Webpack
[Video](https://egghead.io/lessons/tools-import-a-non-es6-module-with-webpack)

Use modules that simply expose themselves in the global namespace and transform them into something that can be imported.

``
npm i --save-dev exports-loader imports-loader
``

Webpack config:
``` js
module: {
  loaders: [
    {
      test: require.resolve('./src/js/non_node_modules/theModule'),
      loaders: ['imports?window=>{}', 'exports?theModule'],
    }
  ]
}
```

When importing in js

```js
import theModule from './js/non_node_modules/theModule' // eslint-disabel-line
```

- ``imports``: stop a module from polluting the global namespace by supplying it with a dummy ``window`` object.
- ``exports``: wrap a non-cjs/non-es6 module so we can import it.
