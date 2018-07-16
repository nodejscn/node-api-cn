<!-- YAML
added: v10.5.0
-->
- `password` {string|Buffer|TypedArray|DataView}
- `salt` {string|Buffer|TypedArray|DataView}
- `keylen` {number}
- `options` {Object}
  - `N` {number} CPU/memory cost parameter. Must be a power of two greater
    than one. **Default:** `16384`.
  - `r` {number} Block size parameter. **Default:** `8`.
  - `p` {number} Parallelization parameter. **Default:** `1`.
  - `maxmem` {number} Memory upper bound. It is an error when (approximately)
    `128 * N * r > maxmem`. **Default:** `32 * 1024 * 1024`.
- Returns: {Buffer}

Provides a synchronous [scrypt][] implementation. Scrypt is a password-based
key derivation function that is designed to be expensive computationally and
memory-wise in order to make brute-force attacks unrewarding.

The `salt` should be as unique as possible. It is recommended that a salt is
random and at least 16 bytes long. See [NIST SP 800-132][] for details.

An exception is thrown when key derivation fails, otherwise the derived key is
returned as a [`Buffer`][].

An exception is thrown when any of the input arguments specify invalid values
or types.

```js
const crypto = require('crypto');
// Using the factory defaults.
const key1 = crypto.scryptSync('secret', 'salt', 64);
console.log(key1.toString('hex'));  // '3745e48...08d59ae'
// Using a custom N parameter. Must be a power of two.
const key2 = crypto.scryptSync('secret', 'salt', 64, { N: 1024 });
console.log(key2.toString('hex'));  // '3745e48...aa39b34'
```

