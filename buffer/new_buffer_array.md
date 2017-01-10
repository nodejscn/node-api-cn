<!-- YAML
deprecated: v6.0.0
-->

> Stability: 0 - Deprecated: Use [`Buffer.from(array)`] instead.

* `array` {Array} An array of bytes to copy from

Allocates a new `Buffer` using an `array` of octets.

Example:

```js
// Creates a new Buffer containing the ASCII bytes of the string 'buffer'
const buf = new Buffer([0x62, 0x75, 0x66, 0x66, 0x65, 0x72]);
```

