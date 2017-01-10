
`Buffer` instances can be iterated over using the ECMAScript 2015 (ES6) `for..of`
syntax.

Example:

```js
const buf = Buffer.from([1, 2, 3]);

// Prints:
//   1
//   2
//   3
for (var b of buf) {
  console.log(b);
}
```

Additionally, the [`buf.values()`], [`buf.keys()`], and
[`buf.entries()`] methods can be used to create iterators.

