<!-- YAML
added: v0.5.5
-->

* `offset` {Integer} Where to start reading. Must satisfy: `0 <= offset <= buf.length - 2`
* `noAssert` {Boolean} Skip `offset` validation? **Default:** `false`
* Returns: {Integer}

Reads an unsigned 16-bit integer from `buf` at the specified `offset` with
specified endian format (`readUInt16BE()` returns big endian, `readUInt16LE()`
returns little endian).

Setting `noAssert` to `true` allows `offset` to be beyond the end of `buf`, but
the result should be considered undefined behavior.

Examples:

```js
const buf = Buffer.from([0x12, 0x34, 0x56]);

// Prints: 1234
console.log(buf.readUInt16BE(0).toString(16));

// Prints: 3412
console.log(buf.readUInt16LE(0).toString(16));

// Prints: 3456
console.log(buf.readUInt16BE(1).toString(16));

// Prints: 5634
console.log(buf.readUInt16LE(1).toString(16));

// Throws an exception: RangeError: Index out of range
console.log(buf.readUInt16LE(2).toString(16));
```

