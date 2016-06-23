# Chunking common modules from multiple apps with he Webpack Commons Chunk Plugin
[Video](https://egghead.io/lessons/tools-chunking-common-modules-from-multiple-apps-with-the-webpack-commonschunkplugin)

Splitt common code from two or more applications into a common module.

```js
etnry: {
  app1: '...',
  app2: '...',
},

plugins: [
  env.test ? undefined : new webpack.optimize.CommonsChunkPlugin({
    name: 'common',
    filename: 'bundle.common.js',
  }),
  env.test ? undefined : new webpack.optimize.CommonsChunkPlugin({
    name: 'vendor',
    chunks: ['app1'], // specify witch entries this chunk applies to
  }),
].filter(p => !!p)
```
