<!-- YAML
added: v0.5.5
-->

* `value` {Integer} Number to be written to `buf`
* `offset` {Integer} Where to start writing. Must satisfy: `0 <= offset <= buf.length - 4`
* `noAssert` {Boolean} Skip `value` and `offset` validation? **Default:** `false`
* Returns: {Integer} `offset` plus the number of bytes written

Writes `value` to `buf` at the specified `offset` with specified endian
format (`writeUInt32BE()` writes big endian, `writeUInt32LE()` writes little
endian). `value` should be a valid unsigned 32-bit integer. Behavior is
undefined when `value` is anything other than an unsigned 32-bit integer.

Setting `noAssert` to `true` allows the encoded form of `value` to extend beyond
the end of `buf`, but the result should be considered undefined behavior.

Examples:

```js
const buf = Buffer.allocUnsafe(4);

buf.writeUInt32BE(0xfeedface, 0);

// Prints: <Buffer fe ed fa ce>
console.log(buf);

buf.writeUInt32LE(0xfeedface, 0);

// Prints: <Buffer ce fa ed fe>
console.log(buf);
```

