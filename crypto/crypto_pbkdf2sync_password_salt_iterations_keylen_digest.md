<!-- YAML
added: v0.9.3
-->

Provides a synchronous Password-Based Key Derivation Function 2 (PBKDF2)
implementation. A selected HMAC digest algorithm specified by `digest` is
applied to derive a key of the requested byte length (`keylen`) from the
`password`, `salt` and `iterations`.

If an error occurs an Error will be thrown, otherwise the derived key will be
returned as a [`Buffer`][].

The `iterations` argument must be a number set as high as possible. The
higher the number of iterations, the more secure the derived key will be,
but will take a longer amount of time to complete.

The `salt` should also be as unique as possible. It is recommended that the
salts are random and their lengths are greater than 16 bytes. See
[NIST SP 800-132][] for details.

Example:

```js
const crypto = require('crypto');
const key = crypto.pbkdf2Sync('secret', 'salt', 100000, 512, 'sha512');
console.log(key.toString('hex'));  // '3745e48...aa39b34'
```

An array of supported digest functions can be retrieved using
[`crypto.getHashes()`][].

