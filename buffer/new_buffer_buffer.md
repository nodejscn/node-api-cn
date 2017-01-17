<!-- YAML
deprecated: v6.0.0
-->

> 稳定性: 0 - 废弃的: 使用 [`Buffer.from(buffer)`] 代替。

* `buffer` {Buffer} An existing `Buffer` to copy data from

Copies the passed `buffer` data onto a new `Buffer` instance.

Example:

```js
const buf1 = new Buffer('buffer');
const buf2 = new Buffer(buf1);

buf1[0] = 0x61;

// Prints: auffer
console.log(buf1.toString());

// Prints: buffer
console.log(buf2.toString());
```

