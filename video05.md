# Maintain sane file sizes with webpack code splitting
[Video](https://egghead.io/lessons/tools-maintain-sane-file-sizes-with-webpack-code-splitting)

Webpack intercepts any ``System.import()`` statement and dynamically bundles the file specified.

```js
System.import('FILETOLOAD').then(result => {
})
```

#### Example for **react-router**
```js
import App from './app'

const errorLoading= err => console.error('Dynamic page loading failed', err)

const loadRoute= cb => module => cb(null, module.default)

const load= (path, cb) => System.import(path).then(loadRoute(cb)).catch(errorLoading)

export default {
  component: App,
  childRoutes: [
    {
      path: '/',
      getComponent: (location, cb) => load('pages/Home', cb),
    },
    {
      path: 'blog',
      getComponent: (location, cb) => load('pages/Blog', cb),
    },
    {
      path: 'about',
      getComponent: (location, cb) => load('pages/About', cb),
    },
  ]
}
```
