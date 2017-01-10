<!-- YAML
added: v0.11.15
-->

* `offset` {Integer} Where to start reading. Must satisfy: `0 <= offset <= buf.length - 4`
* `noAssert` {Boolean} Skip `offset` validation? **Default:** `false`
* Returns: {Number}

Reads a 32-bit float from `buf` at the specified `offset` with specified
endian format (`readFloatBE()` returns big endian, `readFloatLE()` returns
little endian).

Setting `noAssert` to `true` allows `offset` to be beyond the end of `buf`, but
the result should be considered undefined behavior.

Examples:

```js
const buf = Buffer.from([1, 2, 3, 4]);

// Prints: 2.387939260590663e-38
console.log(buf.readFloatBE());

// Prints: 1.539989614439558e-36
console.log(buf.readFloatLE());

// Throws an exception: RangeError: Index out of range
console.log(buf.readFloatLE(1));

// Warning: reads passed end of buffer!
// This will result in a segmentation fault! Don't do this!
console.log(buf.readFloatLE(1, true));
```

