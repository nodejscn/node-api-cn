<!-- YAML
added: v0.11.15
-->

* `value` {Number} Number to be written to `buf`
* `offset` {Integer} Where to start writing. Must satisfy: `0 <= offset <= buf.length - 4`
* `noAssert` {Boolean} Skip `value` and `offset` validation? **Default:** `false`
* Returns: {Integer} `offset` plus the number of bytes written

Writes `value` to `buf` at the specified `offset` with specified endian
format (`writeFloatBE()` writes big endian, `writeFloatLE()` writes little
endian). `value` *should* be a valid 32-bit float. Behavior is undefined when
`value` is anything other than a 32-bit float.

Setting `noAssert` to `true` allows the encoded form of `value` to extend beyond
the end of `buf`, but the result should be considered undefined behavior.

Examples:

```js
const buf = Buffer.allocUnsafe(4);

buf.writeFloatBE(0xcafebabe, 0);

// Prints: <Buffer 4f 4a fe bb>
console.log(buf);

buf.writeFloatLE(0xcafebabe, 0);

// Prints: <Buffer bb fe 4a 4f>
console.log(buf);
```

