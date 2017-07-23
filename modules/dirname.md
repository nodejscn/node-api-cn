<!-- YAML
added: v0.1.27
-->

<!-- type=var -->

* {string}

The directory name of the current module. This the same as the
[`path.dirname()`][] of the [`__filename`][].

Example: running `node example.js` from `/Users/mjr`

```js
console.log(__dirname);
// Prints: /Users/mjr
console.log(path.dirname(__filename));
// Prints: /Users/mjr
```

