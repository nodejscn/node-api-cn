<!-- YAML
added: v0.5.5
-->

* `value` {Integer} Number to be written to `buf`
* `offset` {Integer} Where to start writing. Must satisfy: `0 <= offset <= buf.length - 2`
* `noAssert` {Boolean} Skip `value` and `offset` validation? **Default:** `false`
* Returns: {Integer} `offset` plus the number of bytes written

Writes `value` to `buf` at the specified `offset` with specified endian
format (`writeInt16BE()` writes big endian, `writeInt16LE()` writes little
endian). `value` *should* be a valid signed 16-bit integer. Behavior is undefined
when `value` is anything other than a signed 16-bit integer.

Setting `noAssert` to `true` allows the encoded form of `value` to extend beyond
the end of `buf`, but the result should be considered undefined behavior.

`value` is interpreted and written as a two's complement signed integer.

Examples:

```js
const buf = Buffer.allocUnsafe(4);

buf.writeInt16BE(0x0102, 0);
buf.writeInt16LE(0x0304, 2);

// Prints: <Buffer 01 02 04 03>
console.log(buf);
```

