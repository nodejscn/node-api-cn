<!-- YAML
added: v1.1.0
-->

* Returns: {Iterator}

Creates and returns an [iterator] of `[index, byte]` pairs from the contents of
`buf`.

Example: Log the entire contents of a `Buffer`

```js
const buf = Buffer.from('buffer');

// Prints:
//   [0, 98]
//   [1, 117]
//   [2, 102]
//   [3, 102]
//   [4, 101]
//   [5, 114]
for (var pair of buf.entries()) {
  console.log(pair);
}
```

