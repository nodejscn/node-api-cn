<!-- YAML
added: v10.5.0
-->
- `password` {string|Buffer|TypedArray}
- `salt` {string|Buffer|TypedArray}
- `keylen` {number}
- `options` {Object}
  - `N` {number} CPU/memory cost parameter. Must be a power of two greater
                 than one. **Default:** `16384`.
  - `r` {number} Block size parameter. **Default:** `8`.
  - `p` {number} Parallelization parameter. **Default:** `1`.
  - `maxmem` {number} Memory upper bound. It is an error when (approximately)
                      `128*N*r > maxmem` **Default:** `32 * 1024 * 1024`.
- `callback` {Function}
  - `err` {Error}
  - `derivedKey` {Buffer}

Provides an asynchronous [scrypt][] implementation. Scrypt is a password-based
key derivation function that is designed to be expensive computationally and
memory-wise in order to make brute-force attacks unrewarding.

The `salt` should be as unique as possible. It is recommended that a salt is
random and at least 16 bytes long. See [NIST SP 800-132][] for details.

The `callback` function is called with two arguments: `err` and `derivedKey`.
`err` is an exception object when key derivation fails, otherwise `err` is
`null`. `derivedKey` is passed to the callback as a [`Buffer`][].

An exception is thrown when any of the input arguments specify invalid values
or types.

```js
const crypto = require('crypto');
// Using the factory defaults.
crypto.scrypt('secret', 'salt', 64, (err, derivedKey) => {
  if (err) throw err;
  console.log(derivedKey.toString('hex'));  // '3745e48...08d59ae'
});
// Using a custom N parameter. Must be a power of two.
crypto.scrypt('secret', 'salt', 64, { N: 1024 }, (err, derivedKey) => {
  if (err) throw err;
  console.log(derivedKey.toString('hex'));  // '3745e48...aa39b34'
});
```

