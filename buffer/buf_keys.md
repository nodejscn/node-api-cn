<!-- YAML
added: v1.1.0
-->

* Returns: {Iterator}

Creates and returns an [iterator] of `buf` keys (indices).

Example:

```js
const buf = Buffer.from('buffer');

// Prints:
//   0
//   1
//   2
//   3
//   4
//   5
for (var key of buf.keys()) {
  console.log(key);
}
```

