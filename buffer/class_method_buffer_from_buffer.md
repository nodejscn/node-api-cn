<!-- YAML
added: v5.10.0
-->

* `buffer` {Buffer} An existing `Buffer` to copy data from

Copies the passed `buffer` data onto a new `Buffer` instance.

Example:

```js
const buf1 = Buffer.from('buffer');
const buf2 = Buffer.from(buf1);

buf1[0] = 0x61;

// Prints: auffer
console.log(buf1.toString());

// Prints: buffer
console.log(buf2.toString());
```

A `TypeError` will be thrown if `buffer` is not a `Buffer`.

