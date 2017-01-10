<!-- YAML
added: v0.5.0
-->

* `offset` {Integer} Where to start reading. Must satisfy: `0 <= offset <= buf.length - 1`
* `noAssert` {Boolean} Skip `offset` validation? **Default:** `false`
* Returns: {Integer}

Reads a signed 8-bit integer from `buf` at the specified `offset`.

Setting `noAssert` to `true` allows `offset` to be beyond the end of `buf`, but
the result should be considered undefined behavior.

Integers read from a `Buffer` are interpreted as two's complement signed values.

Examples:

```js
const buf = Buffer.from([-1, 5]);

// Prints: -1
console.log(buf.readInt8(0));

// Prints: 5
console.log(buf.readInt8(1));

// Throws an exception: RangeError: Index out of range
console.log(buf.readInt8(2));
```

