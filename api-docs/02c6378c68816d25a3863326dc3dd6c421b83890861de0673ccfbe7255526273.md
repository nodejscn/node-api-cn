<!-- YAML
added: v10.12.0
-->
* `type`: {string} Must be `'rsa'`, `'dsa'` or `'ec'`.
* `options`: {Object}
  - `modulusLength`: {number} Key size in bits (RSA, DSA).
  - `publicExponent`: {number} Public exponent (RSA). **Default:** `0x10001`.
  - `divisorLength`: {number} Size of `q` in bits (DSA).
  - `namedCurve`: {string} Name of the curve to use (EC).
  - `publicKeyEncoding`: {Object}
    - `type`: {string} Must be one of `'pkcs1'` (RSA only) or `'spki'`.
    - `format`: {string} Must be `'pem'` or `'der'`.
  - `privateKeyEncoding`: {Object}
    - `type`: {string} Must be one of `'pkcs1'` (RSA only), `'pkcs8'` or
      `'sec1'` (EC only).
    - `format`: {string} Must be `'pem'` or `'der'`.
    - `cipher`: {string} If specified, the private key will be encrypted with
      the given `cipher` and `passphrase` using PKCS#5 v2.0 password based
      encryption.
    - `passphrase`: {string} The passphrase to use for encryption, see `cipher`.
* Returns: {Object}
  - `publicKey`: {string|Buffer}
  - `privateKey`: {string|Buffer}

Generates a new asymmetric key pair of the given `type`. Only RSA, DSA and EC
are currently supported.

It is recommended to encode public keys as `'spki'` and private keys as
`'pkcs8'` with encryption:

```js
const { generateKeyPairSync } = require('crypto');
const { publicKey, privateKey } = generateKeyPairSync('rsa', {
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
});
```

The return value `{ publicKey, privateKey }` represents the generated key pair.
When PEM encoding was selected, the respective key will be a string, otherwise
it will be a buffer containing the data encoded as DER.

