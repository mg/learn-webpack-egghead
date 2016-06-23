# Use Karma for Unit Testing with Webpack
[Video](https://egghead.io/lessons/tools-use-karma-for-unit-testing-with-webpack)

```
npm i --save-dev karma-webpack
```

#### karma.conf.js
```js
const webpackEnv= {test: true}
const webpackConfig= require('./webpack.conf.js')(webpackEnv)
const fileGlob= 'src/**/*.test.js'

module.exports = function setKarmaConfig(config) {
  config.set({
    files: [fileGlob],
    preprocessors: {
      [fileGlob]: ['webpack']
    },
    webpack: webpackConfig,
    webpackMiddleware: {noInfo: true},
  })
}
```
