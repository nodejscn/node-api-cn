<!-- YAML
added: v0.5.5
-->

* `offset` {Integer} Where to start reading. Must satisfy: `0 <= offset <= buf.length - 4`
* `noAssert` {Boolean} Skip `offset` validation? **Default:** `false`
* Returns: {Integer}

Reads a signed 32-bit integer from `buf` at the specified `offset` with
the specified endian format (`readInt32BE()` returns big endian,
`readInt32LE()` returns little endian).

Setting `noAssert` to `true` allows `offset` to be beyond the end of `buf`, but
the result should be considered undefined behavior.

Integers read from a `Buffer` are interpreted as two's complement signed values.

Examples:

```js
const buf = Buffer.from([0, 0, 0, 5]);

// Prints: 5
console.log(buf.readInt32BE());

// Prints: 83886080
console.log(buf.readInt32LE());

// Throws an exception: RangeError: Index out of range
console.log(buf.readInt32LE(1));
```

