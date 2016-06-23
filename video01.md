# Intro to the Production Webpack Course
[Video](https://egghead.io/lessons/tools-intro-to-the-production-webpack-course?course=using-webpack-for-production-javascript-applications)

#### Webpack 2 configuration
A function that accepts an enviroment variable and returns configuration.

```js
const { resolve }= require('path')

module.exports= env => {
  return {
    entry: './js/app.js',                   // src/js/app.js, context + entry
    output: {
      filename: 'bundle.js',
      path: resolve(__dirname, 'dist'),     // dist/
      pathinfo: !env.prod,
    },
    context: resolve(__dirname, 'src'),
    devtol: env.prod ? 'source-map' : 'eval',
    bail: env.prod,
    module: {
      loaders: [
        {test: /\.js$/, loader: 'babel!eslint', exclude: /node_modules/},
        {test: /\.css$/ loader: 'style!css'},
      ],
    },
  }
}
```

#### package.json scripts
```json
"scripts": {
  "test": "karma start",
  "check-coverage": "istanbul check-coverage --statements 23 --branches 5 --functions 9 --lines 24",
  "watch:test": "npm test -- --auto-watch --no-single-run",
  "validate": "npm-run-all --parallel validate-webpack:* lint test --serial check-coverage",
  "validate-webpack:dev": "webpack-validator webpack.config.js --env.dev",
  "validate-webpack:prod": "webpack-validator webpack.config.js --env.prod",
  "clean-dist": "rimraf dist",
  "copy-files": "cpy src/index.html src/favicon.ico dist",
  "clean-and-copy": "npm run clean-dist && npm run copy-files",
  "prestart": "npm run clean-and-copy",
  "start": "webpack-dev-server --env.dev --content-base dist",
  "prebuild": "npm run clean-and-copy",
  "prebuild:prod": "npm run clean-and-copy",
  "build": "webpack --env.dev",
  "build:prod": "webpack --env.prod -p",
  "lint": "eslint .",
  "setup": "npm install && npm run validate"
}
```

- ``-p`` flag tells Webpack to operate in production mode
