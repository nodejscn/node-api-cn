<!-- YAML
added: v0.11.15
-->

* `offset` {Integer} Where to start reading. Must satisfy: `0 <= offset <= buf.length - 8`
* `noAssert` {Boolean} Skip `offset` validation? **Default:** `false`
* Returns: {Number}

Reads a 64-bit double from `buf` at the specified `offset` with specified
endian format (`readDoubleBE()` returns big endian, `readDoubleLE()` returns
little endian).

Setting `noAssert` to `true` allows `offset` to be beyond the end of `buf`, but
the result should be considered undefined behavior.

Examples:

```js
const buf = Buffer.from([1, 2, 3, 4, 5, 6, 7, 8]);

// Prints: 8.20788039913184e-304
console.log(buf.readDoubleBE());

// Prints: 5.447603722011605e-270
console.log(buf.readDoubleLE());

// Throws an exception: RangeError: Index out of range
console.log(buf.readDoubleLE(1));

// Warning: reads passed end of buffer!
// This will result in a segmentation fault! Don't do this!
console.log(buf.readDoubleLE(1, true));
```

