# Validate your Webpack config with webpack-validator
[Video](https://egghead.io/lessons/tools-validate-your-webpack-config-with-webpack-validator)

```
npm install --save-dev webpack-validator ghooks opt npm-run-all
```

```json
"config": {
  "ghooks": {
    "pre-commit": "opt --in pre-commit --exec \"npm run validate\""
  }
},

"scripts": {
  "validate": "npm-run-all --parallel validate-webpack:* lint test --serial check-coverage",
  "validate-webpack:dev": "webpack-validator webpack.config.js --env.dev",
  "validate-webpack:prod": "webpack-validator webpack.config.js --env.prod"  
}
```

Another way to use webpack validator is to insert it into the webpack configuration script
```js
const validate= require('webpack-validator')
module.exports= env => {
  return validate({
    ...
  })
})
```

#### Other useful packages for npm scripting
- ``rimraf``: rm -rf
- ``cpy``: copy
