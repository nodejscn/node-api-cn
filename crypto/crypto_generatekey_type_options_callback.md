<!-- YAML
added: v15.0.0
-->

* `type`: {string} The intended use of the generated secret key. Currently
  accepted values are `'hmac'` and `'aes'`.
* `options`: {Object}
  * `length`: {number} The bit length of the key to generate. This must be a
    value greater than 0.
    * If `type` is `'hmac'`, the minimum is 1, and the maximum length is
      2<sup>31</sup>-1. If the value is not a multiple of 8, the generated
      key will be truncated to `Math.floor(length / 8)`.
    * If `type` is `'aes'`, the length must be one of `128`, `192`, or `256`.
* `callback`: {Function}
  * `err`: {Error}
  * `key`: {KeyObject}

Asynchronously generates a new random secret key of the given `length`. The
`type` will determine which validations will be performed on the `length`.

```mjs
const {
  generateKey,
} = await import('crypto');

generateKey('hmac', { length: 64 }, (err, key) => {
  if (err) throw err;
  console.log(key.export().toString('hex'));  // 46e..........620
});
```

```cjs
const {
  generateKey,
} = require('crypto');

generateKey('hmac', { length: 64 }, (err, key) => {
  if (err) throw err;
  console.log(key.export().toString('hex'));  // 46e..........620
});
```

