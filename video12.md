# Initialize a Webpack Project with Karma for Testing
[Video](https://egghead.io/lessons/javascript-initialize-a-webpack-project-with-karma-for-testing)

```
npm i --save-dev karma karma-chrome-launcher mocha karma-mocha
./node_modules/.bin/karma init
```

Use ``mocha``, ``no`` to require.js, ``Chrome`` for browser, ``src/**/*.spec.js`` for test files, ``no`` to watch.

#### karma.conf.js
```js
module.exports = function setKarmaConfig(config) {
  config.set({
    basePath: '',
    frameworks: ['mocha'],
    files: ['src/**/*.test.js'],
    reporters: ['progress'],
    port: 9876,
    colors: true,
    logLevel: config.LOG_INFO,
    autoWatch: false,
    browsers: ['Chrome'],
    singleRun: true,
    concurrency: Infinity
  })
}
```

#### package.json
``` json
{
  "scripts": {
    "test": "karma start",
    "watch:test": "npm test -- --auto-watch --no-single-run",
  }
}
```
