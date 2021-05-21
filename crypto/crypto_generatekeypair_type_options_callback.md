<!-- YAML
added: v10.12.0
changes:
  - version:
     - v13.9.0
     - v12.17.0
    pr-url: https://github.com/nodejs/node/pull/31178
    description: Add support for Diffie-Hellman.
  - version: v12.0.0
    pr-url: https://github.com/nodejs/node/pull/26774
    description: Add ability to generate X25519 and X448 key pairs.
  - version: v12.0.0
    pr-url: https://github.com/nodejs/node/pull/26554
    description: Add ability to generate Ed25519 and Ed448 key pairs.
  - version: v11.6.0
    pr-url: https://github.com/nodejs/node/pull/24234
    description: The `generateKeyPair` and `generateKeyPairSync` functions now
                 produce key objects if no encoding was specified.
-->

* `type`: {string} Must be `'rsa'`, `'dsa'`, `'ec'`, `'ed25519'`, `'ed448'`,
  `'x25519'`, `'x448'`, or `'dh'`.
* `options`: {Object}
  * `modulusLength`: {number} Key size in bits (RSA, DSA).
  * `publicExponent`: {number} Public exponent (RSA). **Default:** `0x10001`.
  * `divisorLength`: {number} Size of `q` in bits (DSA).
  * `namedCurve`: {string} Name of the curve to use (EC).
  * `prime`: {Buffer} The prime parameter (DH).
  * `primeLength`: {number} Prime length in bits (DH).
  * `generator`: {number} Custom generator (DH). **Default:** `2`.
  * `groupName`: {string} Diffie-Hellman group name (DH). See
    [`crypto.getDiffieHellman()`][].
  * `publicKeyEncoding`: {Object} See [`keyObject.export()`][].
  * `privateKeyEncoding`: {Object} See [`keyObject.export()`][].
* `callback`: {Function}
  * `err`: {Error}
  * `publicKey`: {string | Buffer | KeyObject}
  * `privateKey`: {string | Buffer | KeyObject}

Generates a new asymmetric key pair of the given `type`. RSA, DSA, EC, Ed25519,
Ed448, X25519, X448, and DH are currently supported.

If a `publicKeyEncoding` or `privateKeyEncoding` was specified, this function
behaves as if [`keyObject.export()`][] had been called on its result. Otherwise,
the respective part of the key is returned as a [`KeyObject`][].

It is recommended to encode public keys as `'spki'` and private keys as
`'pkcs8'` with encryption for long-term storage:

```mjs
const {
  generateKeyPair,
} = await import('crypto');

generateKeyPair('rsa', {
  modulusLength: 4096,
  publicKeyEncoding: {
    type: 'spki',
    format: 'pem'
  },
  privateKeyEncoding: {
    type: 'pkcs8',
    format: 'pem',
    cipher: 'aes-256-cbc',
    passphrase: 'top secret'
  }
}, (err, publicKey, privateKey) => {
  // Handle errors and use the generated key pair.
});
```

```cjs
const {
  generateKeyPair,
} = require('crypto');

generateKeyPair('rsa', {
  modulusLength: 4096,
  publicKeyEncoding: {
    type: 'spki',
    format: 'pem'
  },
  privateKeyEncoding: {
    type: 'pkcs8',
    format: 'pem',
    cipher: 'aes-256-cbc',
    passphrase: 'top secret'
  }
}, (err, publicKey, privateKey) => {
  // Handle errors and use the generated key pair.
});
```

On completion, `callback` will be called with `err` set to `undefined` and
`publicKey` / `privateKey` representing the generated key pair.

If this method is invoked as its [`util.promisify()`][]ed version, it returns
a `Promise` for an `Object` with `publicKey` and `privateKey` properties.

