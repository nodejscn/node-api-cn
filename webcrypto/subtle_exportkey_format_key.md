<!-- YAML
added: v15.0.0
changes:
  - version: v15.9.0
    pr-url: https://github.com/nodejs/node/pull/37203
    description: Removed `'NODE-DSA'` JWK export.
-->

* `format`: {string} Must be one of `'raw'`, `'pkcs8'`, `'spki'`, `'jwk'`, or
  `'node.keyObject'`.
* `key`: {CryptoKey}
* Returns: {Promise} containing {ArrayBuffer}, or, if `format` is
  `'node.keyObject'`, a {KeyObject}.

Exports the given key into the specified format, if supported.

If the {CryptoKey} is not extractable, the returned promise will reject.

When `format` is either `'pkcs8'` or `'spki'` and the export is successful,
the returned promise will be resolved with an {ArrayBuffer} containing the
exported key data.

When `format` is `'jwk'` and the export is successful, the returned promise
will be resolved with a JavaScript object conforming to the [JSON Web Key][]
specification.

The special `'node.keyObject'` value for `format` is a Node.js-specific
extension that allows converting a {CryptoKey} into a Node.js {KeyObject}.

|      Key Type         | `'spki'` | `'pkcs8'` | `'jwk'` | `'raw'` |
| --------------------- | -------- | --------- | ------- | ------- |
| `'AES-CBC'`           |   |   | ✔ | ✔ |
| `'AES-CTR'`           |   |   | ✔ | ✔ |
| `'AES-GCM'`           |   |   | ✔ | ✔ |
| `'AES-KW'`            |   |   | ✔ | ✔ |
| `'ECDH'`              | ✔ | ✔ | ✔ | ✔ |
| `'ECDSA'`             | ✔ | ✔ | ✔ | ✔ |
| `'HDKF'`              |   |   |   |   |
| `'HMAC'`              |   |   | ✔ | ✔ |
| `'PBKDF2'`            |   |   |   |   |
| `'RSA-OAEP'`          | ✔ | ✔ | ✔ |   |
| `'RSA-PSS'`           | ✔ | ✔ | ✔ |   |
| `'RSASSA-PKCS1-v1_5'` | ✔ | ✔ | ✔ |   |
| `'NODE-DSA'` <sup>1</sup> | ✔ | ✔ |   |   |
| `'NODE-DH'` <sup>1</sup> | ✔ | ✔ |   |   |
| `'NODE-SCRYPT'` <sup>1</sup> |   |   |   |   |
| `'NODE-ED25519'` <sup>1</sup> | ✔ | ✔ | ✔ | ✔ |
| `'NODE-ED448'` <sup>1</sup> | ✔ | ✔ | ✔ | ✔ |

<sup>1</sup> Node.js-specific extension

