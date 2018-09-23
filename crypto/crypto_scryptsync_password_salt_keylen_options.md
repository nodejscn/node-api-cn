<!-- YAML
added: v10.5.0
changes:
  - version: v10.9.0
    pr-url: https://github.com/nodejs/node/pull/21525
    description: The `cost`, `blockSize` and `parallelization` option names
                 have been added.
-->
* `password` {string|Buffer|TypedArray|DataView}
* `salt` {string|Buffer|TypedArray|DataView}
* `keylen` {number}
* `options` {Object}
  - `cost` {number} CPU/memory cost parameter. Must be a power of two greater
  - `N` {number} CPU/memory cost parameter. Must be a power of two greater
    than one. **Default:** `16384`.
  - `blockSize` {number} Block size parameter. **Default:** `8`.
  - `parallelization` {number} Parallelization parameter. **Default:** `1`.
  - `N` {number} Alias for `cost`. Only one of both may be specified.
  - `r` {number} Alias for `blockSize`. Only one of both may be specified.
  - `p` {number} Alias for `parallelization`. Only one of both may be specified.
  - `maxmem` {number} Memory upper bound. It is an error when (approximately)
    `128 * N * r > maxmem`. **Default:** `32 * 1024 * 1024`.
* Returns: {Buffer}

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

