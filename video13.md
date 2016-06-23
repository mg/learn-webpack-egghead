# Use Chai Assertions for Tests in a Karma Project
[Video](https://egghead.io/lessons/javascript-use-chai-assertions-for-tests-in-a-karma-project)

```
npm i --save-dev chai karma-chai
```

#### karma.conf.js
```js
module.exports = function setKarmaConfig(config) {
  config.set({
    frameworks: ['mocha', 'chai'],
  })
}
```
