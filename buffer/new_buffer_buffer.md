<!-- YAML
deprecated: v6.0.0
-->

> Stability: 0 - Deprecated: Use [`Buffer.from(buffer)`] instead.

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

