# Ensure all Source Files are Included in Test Coverage Reports with Webpack
[Video](https://egghead.io/lessons/tools-ensure-all-source-files-are-included-in-test-coverage-reports-with-webpack)

Instrument all code for coverage, not just code that is included in unit tests.

#### karma.conf.js
``` js
const testGlob= 'src/**/*.spec.js'
const srcGlob= 'src/**/*!(spec|mock).js'

module.exports = function setKarmaConfig(config) {
  config.set({
    files: [testGlob, srcGlob],
    preprocessors: [
      [testGlob]: ['webpack'],
      [srcGlob]: ['webpack'],
    ],
  })
}
```

Use ``istanbul`` to check that coverage does not go down

```
npm i --save-dev instanbul
```

#### package.json scripts
```json
"scripts": {
  "check-coverage": "istanbul check-coverage --statements 23 --branches 5 --functions 9 --lines 24",
  "validate": "npm-run-all --parallel validate-webpack:* lint test --serial check-coverage",
}
```
