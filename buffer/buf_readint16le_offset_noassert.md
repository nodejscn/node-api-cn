<!-- YAML
added: v0.5.5
-->

* `offset` {Integer} Where to start reading. Must satisfy: `0 <= offset <= buf.length - 2`
* `noAssert` {Boolean} Skip `offset` validation? **Default:** `false`
* Returns: {Integer}

Reads a signed 16-bit integer from `buf` at the specified `offset` with
the specified endian format (`readInt16BE()` returns big endian,
`readInt16LE()` returns little endian).

Setting `noAssert` to `true` allows `offset` to be beyond the end of `buf`, but
the result should be considered undefined behavior.

Integers read from a `Buffer` are interpreted as two's complement signed values.

Examples:

```js
const buf = Buffer.from([0, 5]);

// Prints: 5
console.log(buf.readInt16BE());

// Prints: 1280
console.log(buf.readInt16LE(1));

// Throws an exception: RangeError: Index out of range
console.log(buf.readInt16LE(1));
```

