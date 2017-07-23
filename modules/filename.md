<!-- YAML
added: v0.0.1
-->

<!-- type=var -->

* {string}

The file name of the current module. This is the resolved absolute path of the
current module file.

For a main program this is not necessarily the same as the file name used in the
command line.

See [`__dirname`][] for the directory name of the current module.

Examples:

Running `node example.js` from `/Users/mjr`

```js
console.log(__filename);
// Prints: /Users/mjr/example.js
console.log(__dirname);
// Prints: /Users/mjr
```

Given two modules: `a` and `b`, where `b` is a dependency of
`a` and there is a directory structure of:

* `/Users/mjr/app/a.js`
* `/Users/mjr/app/node_modules/b/b.js`

References to `__filename` within `b.js` will return
`/Users/mjr/app/node_modules/b/b.js` while references to `__filename` within
`a.js` will return `/Users/mjr/app/a.js`.

