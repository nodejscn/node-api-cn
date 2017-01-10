<!-- YAML
added: v0.1.27
-->

<!-- type=var -->

* {String}

The name of the directory that the currently executing script resides in.

Example: running `node example.js` from `/Users/mjr`

```js
console.log(__dirname);
// Prints: /Users/mjr
```

`__dirname` isn't actually a global but rather local to each module.

For instance, given two modules: `a` and `b`, where `b` is a dependency of
`a` and there is a directory structure of:

* `/Users/mjr/app/a.js`
* `/Users/mjr/app/node_modules/b/b.js`

References to `__dirname` within `b.js` will return
`/Users/mjr/app/node_modules/b` while references to `__dirname` within `a.js`
will return `/Users/mjr/app`.

