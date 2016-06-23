# Add Code Coverage to Tests in a Webpack Project
[Video](https://egghead.io/lessons/tools-add-code-coverage-to-tests-in-a-webpack-project)

####

```
npm -i --save-dev karma-coverage babel-plugin-__coverage__
```

#### karma.conf.js
``` js
process.env.BABEL_ENV= 'test'
module.exports = function setKarmaConfig(config) {
  config.set({
    reporters: ['progress', 'coverage'],
    coverageReporter: {
      reporters: [
        {type: 'lcov', dir: 'coverage/', subdir: '.'},
        {type: 'json', dir: 'coverage/', subdir: '.'},
        {type: 'text-summary'},
      ],
    }
  })
}
```

#### .babelrc
``` json
{
  "env": {
    "test": {
      "plugins": [
        []"__coverage__", {"ignore": "*.*(spec|mock).*"}]
      ]
    }
  }
}
```
