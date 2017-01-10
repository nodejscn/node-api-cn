<!-- YAML
added: v5.10.0
-->

* `array` {Array}

Allocates a new `Buffer` using an `array` of octets.

Example:

```js
// Creates a new Buffer containing ASCII bytes of the string 'buffer'
const buf = Buffer.from([0x62, 0x75, 0x66, 0x66, 0x65, 0x72]);
```

A `TypeError` will be thrown if `array` is not an `Array`.

