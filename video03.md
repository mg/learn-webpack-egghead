# Tree shaking with Webpack 2
[Video](https://egghead.io/lessons/tools-tree-shaking-with-webpack-2)

#### Step 1: Stop Babel from compiling ES6 *exports/imports* into *require* statements
Vanilla CJS *require* statements are not statically analyzable. If we leave the ES6 statements in Webpack can analyze them and determine what is needed and what is not needed.
```
npm i --save-dev babel-preset-es2015-webpack
npm r --save-dev babel-preset-es2015
```
#### .babelrc
```
{
  "presets": ["es2015-webpack"]
}
```
