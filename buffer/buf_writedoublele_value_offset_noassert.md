<!-- YAML
added: v0.11.15
-->

* `value` {Number} Number to be written to `buf`
* `offset` {Integer} Where to start writing. Must satisfy: `0 <= offset <= buf.length - 8`
* `noAssert` {Boolean} Skip `value` and `offset` validation? **Default:** `false`
* Returns: {Integer} `offset` plus the number of bytes written

Writes `value` to `buf` at the specified `offset` with specified endian
format (`writeDoubleBE()` writes big endian, `writeDoubleLE()` writes little
endian). `value` *should* be a valid 64-bit double. Behavior is undefined when
`value` is anything other than a 64-bit double.

Setting `noAssert` to `true` allows the encoded form of `value` to extend beyond
the end of `buf`, but the result should be considered undefined behavior.

Examples:

```js
const buf = Buffer.allocUnsafe(8);

buf.writeDoubleBE(0xdeadbeefcafebabe, 0);

// Prints: <Buffer 43 eb d5 b7 dd f9 5f d7>
console.log(buf);

buf.writeDoubleLE(0xdeadbeefcafebabe, 0);

// Prints: <Buffer d7 5f f9 dd b7 d5 eb 43>
console.log(buf);
```

