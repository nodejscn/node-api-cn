<!-- YAML
added: v0.5.0
-->

* `offset` {Integer} Where to start reading. Must satisfy: `0 <= offset <= buf.length - 1`
* `noAssert` {Boolean} Skip `offset` validation? **Default:** `false`
* Returns: {Integer}

Reads an unsigned 8-bit integer from `buf` at the specified `offset`.

Setting `noAssert` to `true` allows `offset` to be beyond the end of `buf`, but
the result should be considered undefined behavior.

Examples:

```js
const buf = Buffer.from([1, -2]);

// Prints: 1
console.log(buf.readUInt8(0));

// Prints: 254
console.log(buf.readUInt8(1));

// Throws an exception: RangeError: Index out of range
console.log(buf.readUInt8(2));
```

