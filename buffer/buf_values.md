<!-- YAML
added: v1.1.0
-->

* Returns: {Iterator}

Creates and returns an [iterator] for `buf` values (bytes). This function is
called automatically when a `Buffer` is used in a `for..of` statement.

Examples:

```js
const buf = Buffer.from('buffer');

// Prints:
//   98
//   117
//   102
//   102
//   101
//   114
for (var value of buf.values()) {
  console.log(value);
}

// Prints:
//   98
//   117
//   102
//   102
//   101
//   114
for (var value of buf) {
  console.log(value);
}
```

