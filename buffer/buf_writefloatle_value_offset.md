<!-- YAML
added: v0.11.15
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/18395
    description: Removed `noAssert` and no implicit coercion of the offset
                 to `uint32` anymore.
-->

* `value` {number} Number to be written to `buf`.
* `offset` {integer} Number of bytes to skip before starting to write. Must
  satisfy `0 <= offset <= buf.length - 4`.
* Returns: {integer} `offset` plus the number of bytes written.

Writes `value` to `buf` at the specified `offset` with specified endian
format (`writeFloatBE()` writes big endian, `writeFloatLE()` writes little
endian). `value` *should* be a valid 32-bit float. Behavior is undefined when
`value` is anything other than a 32-bit float.

```js
const buf = Buffer.allocUnsafe(4);

buf.writeFloatBE(0xcafebabe, 0);

console.log(buf);
// Prints: <Buffer 4f 4a fe bb>

buf.writeFloatLE(0xcafebabe, 0);

console.log(buf);
// Prints: <Buffer bb fe 4a 4f>
```

