
`Buffer` instances can be iterated over using `for..of` syntax:

```js
const buf = Buffer.from([1, 2, 3]);

// Prints:
//   1
//   2
//   3
for (const b of buf) {
  console.log(b);
}
```

Additionally, the [`buf.values()`], [`buf.keys()`], and
[`buf.entries()`] methods can be used to create iterators.

