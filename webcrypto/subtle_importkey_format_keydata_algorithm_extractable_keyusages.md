<!-- YAML
added: v15.0.0
changes:
  - version: v15.9.0
    pr-url: https://github.com/nodejs/node/pull/37203
    description: Removed `'NODE-DSA'` JWK import.
-->

* `format`: {string} Must be one of `'raw'`, `'pkcs8'`, `'spki'`, `'jwk'`, or
  `'node.keyObject'`.
* `keyData`: {ArrayBuffer|TypedArray|DataView|Buffer|KeyObject}
<!--lint disable maximum-line-length remark-lint-->
* `algorithm`: {RsaHashedImportParams|EcKeyImportParams|HmacImportParams|AesImportParams|Pbkdf2ImportParams|NodeDsaImportParams|NodeDhImportParams|NodeScryptImportParams|NodeEdKeyImportParams}
<!--lint enable maximum-line-length remark-lint-->
* `extractable`: {boolean}
* `keyUsages`: {string[]} See [Key usages][].
* Returns: {Promise} containing {CryptoKey}

The `subtle.importKey()` method attempts to interpret the provided `keyData`
as the given `format` to create a {CryptoKey} instance using the provided
`algorithm`, `extractable`, and `keyUsages` arguments. If the import is
successful, the returned promise will be resolved with the created {CryptoKey}.

The special `'node.keyObject'` value for `format` is a Node.js-specific
extension that allows converting a Node.js {KeyObject} into a {CryptoKey}.

If importing a `'PBKDF2'` key, `extractable` must be `false`.

The algorithms currently supported include:

|      Key Type         | `'spki'` | `'pkcs8'` | `'jwk'` | `'raw'` |
| --------------------- | -------- | --------- | ------- | ------- |
| `'AES-CBC'`           |   |   | ✔ | ✔ |
| `'AES-CTR'`           |   |   | ✔ | ✔ |
| `'AES-GCM'`           |   |   | ✔ | ✔ |
| `'AES-KW'`            |   |   | ✔ | ✔ |
| `'ECDH'`              | ✔ | ✔ | ✔ | ✔ |
| `'ECDSA'`             | ✔ | ✔ | ✔ | ✔ |
| `'HDKF'`              |   |   |   | ✔ |
| `'HMAC'`              |   |   | ✔ | ✔ |
| `'PBKDF2'`            |   |   |   | ✔ |
| `'RSA-OAEP'`          | ✔ | ✔ | ✔ |   |
| `'RSA-PSS'`           | ✔ | ✔ | ✔ |   |
| `'RSASSA-PKCS1-v1_5'` | ✔ | ✔ | ✔ |   |
| `'NODE-DSA'` <sup>1</sup> | ✔ | ✔ |   |   |
| `'NODE-DH'` <sup>1</sup> | ✔ | ✔ |   |   |
| `'NODE-SCRYPT'` <sup>1</sup> |   |   |   | ✔ |
| `'NODE-ED25519'` <sup>1</sup> | ✔ | ✔ | ✔ | ✔ |
| `'NODE-ED448'` <sup>1</sup> | ✔ | ✔ | ✔ | ✔ |

<sup>1</sup> Node.js-specific extension

